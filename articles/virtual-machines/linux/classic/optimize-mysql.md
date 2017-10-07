---
title: aaaOptimize des performances de MySQL sur Linux | Documents Microsoft
description: "Découvrez comment toooptimize MySQL en cours d’exécution sur une machine virtuelle Azure (VM) Linux en cours d’exécution."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Optimiser les performances de MySQL sur les machines virtuelles Linux Azure
De nombreux facteurs, en matière de choix de matériel virtuel et de configuration logicielle, ont une incidence sur les performances de MySQL sur Azure. Cet article se concentre sur l’optimisation des performances grâce aux configurations de stockage, système et de base de données.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur les optimisations de Linux VM avec modèle de gestionnaire de ressources hello, consultez [optimiser votre VM Linux sur Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Utiliser RAID sur une machine virtuelle Azure
Le stockage est un facteur clé hello qui affecte les performances de base de données dans les environnements de cloud. Disque unique tooa comparés RAID peut fournir un accès plus rapide via la concurrence. Pour plus d’informations, consultez [Niveaux RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

Le débit d’E/S disque et le temps de réponse d’E/S dans Azure peuvent être améliorés grâce à RAID. Nos tests de laboratoire montrent que débit d’e/s disque peut être doublé et temps de réponse d’e/s peut être réduit de moitié en moyenne lorsque le nombre de hello de disques RAID est doublé (à partir de deux toofour, quatre tooeight, etc.). Voir l’ [annexe A](#AppendixA) pour plus d’informations.  

En outre e/s toodisk MySQL performances sont améliorées lorsque vous augmentez le niveau RAID de hello.  Voir l’ [annexe B](#AppendixB) pour plus d’informations.  

Vous pourriez également la taille de segment tooconsider hello. En règle générale, lorsque vous disposez d’une plus grande taille de segment, vous obtenez une surcharge inférieure, en particulier pour les écritures de grande taille. Toutefois, lorsque la taille de segment hello est trop volumineux, il peut ajouter une charge supplémentaire qui vous empêche de tirer parti de RAID. taille par défaut actuel de Hello est de 512 Ko, ce qui s’avère idéal pour les environnements de production plus générales toobe. Voir l’ [annexe C](#AppendixC) pour plus d’informations.   

Il existe des limites sur le nombre de disques que vous pouvez ajouter, selon le type de machine virtuelle. Ces limites sont présentées en détail sur la page [Tailles de machines virtuelles et services cloud pour Microsoft Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Vous aurez besoin dans les données attachées disques toofollow hello RAID par exemple dans cet article, mais vous pouvez choisir tooset RAID avec moins de disques.  

Cet article suppose que vous avez déjà créé une machine virtuelle Linux et que MYSQL est installé et configuré. Pour plus d’informations sur la prise en main, consultez Comment tooinstall MySQL sur Azure.  

### <a name="set-up-raid-on-azure"></a>Configurer RAID sur Azure
Hello étapes suivantes montrent comment toocreate RAID sur Azure à l’aide de hello portail Azure. Vous pouvez également configurer RAID à l’aide de scripts Windows PowerShell.
Dans cet exemple, nous allons configurer RAID 0 avec quatre disques.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Ajouter un ordinateur virtuel de données disque tooyour
Bonjour portail Azure, accédez toohello le tableau de bord et sélectionnez hello toowhich de machine virtuelle souhaité tooadd un disque de données. Dans cet exemple, la machine virtuelle de hello est mysqlnode1.  

<!--![Virtual machines][1]-->

Cliquez sur **Disques**, puis cliquez sur **Attach New** (Attacher nouveau).

![Les machines virtuelles ajoutent des disques.](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Créez un nouveau disque de 500 Go. Assurez-vous que **préférences de Cache hôte** est défini trop**aucun**.  Lorsque vous avez terminé, cliquez sur **OK**.

![Attacher un disque vide](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Cela ajoute un disque vide à votre machine virtuelle. Répétez cette étape trois fois afin de disposer de quatre disques de données pour RAID.  

Vous pouvez voir hello ajouté les lecteurs dans la machine virtuelle de hello en examinant le journal des messages hello du noyau. Par exemple, toosee cela sur Ubuntu, hello utilisez commande suivante :  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Créer RAID avec hello des disques supplémentaires
Hello étapes suivantes décrivent comment trop[configurer le logiciel RAID sur Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Si vous utilisez un système de fichiers XFS hello, exécutez hello comme suit après avoir créé RAID.
>
>

tooinstall XFS sur Debian et Ubuntu Linux Mint, hello utilisez commande suivante :  

    apt-get -y install xfsprogs  

tooinstall XFS sur Fedora, CentOS ou RHEL, hello utilisez commande suivante :  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Configuration d’un nouveau chemin d’accès de stockage
Utilisez hello suivant tooset de commande d’un nouveau chemin d’accès de stockage :  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Copie hello d’origine toohello nouveau stockage chemin de données
Utilisez hello suivant commande toocopy données toohello nouveau stockage chemin d’accès :  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Modifier les autorisations pour MySQL puisse accéder aux (lecture et écriture) disque de données hello
Utilisez hello commande toomodify autorisations suivantes :  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Ajuster les e/s de disque hello algorithme de planification
Linux implémente quatre types d’algorithmes de planification d’E/S :  

* Algorithme NOOP (aucune opération)
* Algorithme d’échéance (échéance)
* Algorithme de file d’attente complètement juste (CFQ)
* Algorithme de période de budget (anticipatif)  

Vous pouvez sélectionner différents planificateurs d’e/s sous performances toooptimize de différents scénarios. Dans un environnement d’accès complètement aléatoire, il n'est pas une différence significative entre hello CFQ et les algorithmes d’échéance pour les performances. Nous vous recommandons de définir tooDeadline d’environnement hello MySQL de base de données pour la stabilité. En cas de nombreuses E/S séquentielles, CFQ peut réduire les performances d’E/S de disque.   

Pour les disques SSD et d’autres équipements, NOOP ou échéance permettre obtenir de meilleures performances que le planificateur par défaut hello.   

Toohello préalable noyau 2.5, e/s de la valeur par défaut hello planification algorithme est échéance. CFQ à partir du noyau de hello 2.6.18, est devenu l’algorithme de planification d’e/s par défaut hello.  Vous pouvez spécifier ce paramètre au moment du démarrage du noyau ou modifier ce paramètre de manière dynamique lorsque le système de hello est en cours d’exécution.  

Bonjour à l’exemple suivant montre comment toocheck et ensemble hello algorithme NOOP toohello du planificateur par défaut dans la famille de distribution Debian hello.  

### <a name="view-hello-current-io-scheduler"></a>Planificateur de vue hello actuel d’e/s
Planificateur de hello tooview exécutez hello de commande suivante :  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Après la sortie, ce qui indique le planificateur actuel de hello s’affiche :  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Changer de périphérique en cours hello (/ dev/sda) de l’algorithme de planification hello d’e/s
Exécutez hello suivant de commandes toochange hello appareil :  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Définir cette propriété pour /dev/sda uniquement n’est pas utile. Elle doit être définie sur tous les disques de données où se trouve la base de données hello.  
>
>

Vous devez voir hello suivant de sortie, indiquant que grub.cfg a été reconstruite avec succès et que le planificateur par défaut hello a été mis à jour tooNOOP :  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Pourquoi la famille de distribution Red Hat, vous devez uniquement hello de commande suivante :

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Configuration des paramètres d’opérations de fichier système
Une meilleure pratique est toodisable hello *atime* fonctionnalité de journalisation sur le système de fichiers hello. Atime est le dernier temps d’accès fichier hello. Chaque fois qu’un fichier est accédé, les enregistrements de système de fichier hello hello horodatage dans le journal de hello. Toutefois, cette information est rarement utilisée. Vous pouvez la désactiver si vous n’en avez pas besoin, ce qui réduit le temps global d’accès au disque.  

toodisable atime journalisation, vous devez toomodify hello fichier system configuration fichier trouve fstab et ajouter hello **noatime** option.  

Par exemple, modifiez hello vim/etc/fstab fichier en ajoutant hello noatime comme indiqué dans hello suivant l’exemple :  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Ensuite, remontez le système de fichiers hello avec hello commande suivante :  

    mount -o remount /RAID0

Hello de test modifié le résultat. Lorsque vous modifiez le fichier de test hello, temps d’accès hello n’est pas mis à jour. Bonjour suivant illustrent les exemples ressemble le code hello avant et après modification.

Avant :        

![Code avant la modification de l’accès][5]

Après :

![Code après la modification de l’accès][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Augmenter le nombre maximal de hello de handles du système d’accès concurrentiel élevé
MySQL est une base de données à forte concurrence. nombre de handles simultanées par défaut de Hello est 1024 pour Linux, ce qui n’est pas toujours suffisant. Les étapes suivantes de hello utilisation tooincrease hello maximale simultanées poignées de hello système toosupport élevé d’accès concurrentiel de MySQL.

### <a name="modify-hello-limitsconf-file"></a>Modifier le fichier de limits.conf hello
hello tooincrease maximale autorisée de descripteurs simultanées, ajouter hello quatre lignes dans le fichier de /etc/security/limits.conf hello suivantes. Notez que 65536 est le nombre maximal de hello système de hello pouvant prendre en charge.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Mettre à jour système hello pour les nouvelles limites de hello
système de hello tooupdate, exécutez hello suivant de commandes :  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Assurez-vous que les limites de hello sont mis à jour au moment du démarrage
Placez hello suivant les commandes de démarrage dans le fichier de /etc/rc.local hello afin qu’il prendra effet au moment du démarrage.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Optimisation de base de données MySQL
tooconfigure MySQL sur Azure, vous pouvez utiliser hello même stratégie réglage des performances que vous utilisez sur un ordinateur local.  

règles d’optimisation Hello principales d’e/s sont :   

* Augmenter la taille du cache hello.
* Réduisez le délai de réponse E/S.  

paramètres du serveur MySQL toooptimize, vous pouvez mettre à jour fichier my.cnf hello, qui est le fichier de configuration par défaut hello pour des ordinateurs clients et serveur.  

Hello des éléments de configuration suivants sont hello principaux facteurs qui affectent les performances de MySQL :  

* **innodb_buffer_pool_size**: pool de mémoires tampons hello contient les données mises en mémoire tampon et l’index de hello. Cela a généralement la valeur % too70 de mémoire physique.
* **innodb_log_file_size**: taille de journal de restauration par progression hello. Vous utilisez tooensure de journaux de restauration par progression que les opérations d’écriture sont récupérables, fiable et rapide après un incident. A la valeur too512 Mo, ce qui vous donne suffisamment d’espace disque pour la journalisation des opérations d’écriture.
* **max_connections** : parfois, les applications ne ferment pas les connexions correctement. Une valeur supérieure, vous accordez hello serveur toorecycle désactivé des connexions plus de temps. Hello le nombre maximal de connexions est 10 000, mais hello recommandé maximale est de 5 000.
* **Innodb_file_per_table**: ce paramètre Active ou désactive la possibilité de hello des tables de toostore InnoDB dans des fichiers distincts. Activez tooensure d’option hello que plusieurs opérations d’administration avancées peuvent être appliquées efficacement. À partir d’un point de vue des performances, il peut accélérer la transmission d’espace table hello et optimiser les performances de gestion de débris hello. Hello recommandé pour cette option est activé.</br></br>
À partir de MySQL 5.6, hello par défaut est ON, par conséquent, aucune action n’est requise. Pour les versions antérieures, hello par défaut est OFF. paramètre de Hello doit être modifié avant le chargement de données, car seules les tables nouvellement créés sont affectées.
* **innodb_flush_log_at_trx_commit**: valeur par défaut de hello est 1, avec hello étendue too0 ~ 2. valeur par défaut de Hello est l’option la plus appropriée pour la base de données MySQL autonome hello. Hello de 2 permet hello plus l’intégrité des données et est adapté aux maître dans un MySQL Cluster. le paramètre Hello 0 permet de perte de données, ce qui peut affecter la fiabilité, dans certains cas avec de meilleures performances et convient aux subordonné dans un MySQL Cluster.
* **Innodb_log_buffer_size**: tampon de journal hello permet des transactions toorun sans avoir tooflush hello journal toodisk avant la validation des transactions hello. Toutefois, s’il existe des objets binaires volumineux ou un champ de texte, le cache de hello est consommé rapidement et e/s disque fréquentes sera déclenché. Il est mieux augmenter la taille de mémoire tampon hello si la variable d’état Innodb_log_waits n’est pas 0.
* **query_cache_size**: hello meilleure option est toodisable à partir du début de hello. Too0 query_cache_size (il s’agit de paramètre par défaut de hello dans MySQL 5.6) et utiliser d’autres toospeed méthodes des requêtes.  

Consultez [annexe D](#AppendixD) pour une comparaison des performances avant et après l’optimisation de hello.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Activer le journal des requêtes lentes hello MySQL pour l’analyse hello goulot d’étranglement
journal des requêtes lentes Hello MySQL peut vous aider à identifier les requêtes lentes hello pour MySQL. Après avoir activé le journal des requêtes lentes hello MySQL, vous pouvez utiliser les outils MySQL comme **mysqldumpslow** goulot d’étranglement de performances tooidentify hello.  

Par défaut, cette option n’est pas activée. Journal des requêtes lentes hello sous tension peut consommer des ressources du processeur. Nous vous recommandons d’activer ce dernier temporairement, pour résoudre les goulots d’étranglement de performances. tooturn sur le journal des requêtes lentes hello :

1. Modifier le fichier my.cnf de hello en ajoutant hello suivant lignes toohello fin :

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Redémarrez le serveur MySQL de hello.

        service  mysql  restart

3. Vérifiez si le paramètre de hello prend effet à l’aide de hello **afficher** commande.

![Journal des requêtes lentes ON][7]   

![Résultats du journal des requêtes lentes][8]

Dans cet exemple, vous pouvez voir que cette fonctionnalité de requête lentes hello a été activée. Vous pouvez ensuite utiliser hello **mysqldumpslow** outil toodetermine les goulots d’étranglement et optimiser les performances, telles que l’ajout d’index.

## <a name="appendices"></a>Annexes
Hello Voici des exemples de données test de performances produits dans un environnement lab ciblé. Ils fournissent des informations générales sur les tendances de données de performances hello avec des performances différentes approches de paramétrage. résultats de Hello peuvent varier sous différentes versions de produit ou d’environnement.

### <a name="AppendixA"></a>Annexe A  
**Performances du disque (IOPS) avec des niveaux RAID différents**

![E/S par seconde du disque avec des niveaux RAID différents][9]

**Commandes de test**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> la charge de travail Hello de ce test utilise 64 threads, la tentative de limite supérieure de hello tooreach de RAID.
>
>

### <a name="AppendixB"></a>Annexe B  
**Comparaison des performances (débit) MySQL avec des niveaux RAID différents**   
(système de fichiers XFS)

![Comparaison des performances MySQL avec des niveaux RAID différents][10]  
![Comparaison des performances MySQL avec des niveaux RAID différents][11]

**Commandes de test**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents**  
![Comparaison des performances (OLTP) MySQL avec des niveaux RAID différents][12]

**Commandes de test**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Annexe C   
**Comparaison des performances (IOPS) de disque avec différentes tailles de segment**  
(système de fichiers XFS)

![][13]

**Commandes de test**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

tailles des fichiers Hello utilisés pour ce test sont 30 Go et 1 Go, respectivement, avec RAID 0 (4 disques) XFS système de fichiers.

### <a name="AppendixD"></a>Annexe D  
**Comparaison des performances (débit) MySQL avant et après l’optimisation**  
(système de fichiers XFS)

![Comparaison des performances (débit) MySQL avant et après l’optimisation][14]

**Commandes de test**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Hello de configuration par défaut et l’optimisation est comme suit :**

| Paramètres | Default | Optimisation |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Aucune |7 Go |
| **innodb_log_file_size** |5 Mo |512 Mo |
| **max_connections** |100 |5 000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 Mo |128 Mo |
| **query_cache_size** |16 Mo |0 |

Pour plus [les paramètres de configuration de l’optimisation](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consultez toohello [instructions officielles de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Environnement de test**  

| Matériel | Détails |
| --- | --- |
| UC |AMD Opteron(tm) Processeur 4171 HE/4 cœurs |
| Mémoire |14 Go |
| Disque |10 Go/disque |
| SE |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

