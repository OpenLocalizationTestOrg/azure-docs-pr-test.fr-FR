---
title: "Optimiser les performances de MySQL sur Linux | Microsoft Docs"
description: "Apprenez à optimiser MySQL sur une machine virtuelle Azure exécutant Linux."
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
ms.openlocfilehash: 7e7582a31cb3e74fd8c3cd0dd54961392d9c53bb
ms.sourcegitcommit: 6a6e14fdd9388333d3ededc02b1fb2fb3f8d56e5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Optimiser les performances de MySQL sur les machines virtuelles Linux Azure
De nombreux facteurs, en matière de choix de matériel virtuel et de configuration logicielle, ont une incidence sur les performances de MySQL sur Azure. Cet article se concentre sur l’optimisation des performances grâce aux configurations de stockage, système et de base de données.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique. Cet article traite du modèle de déploiement classique. Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager. Pour plus d’informations sur les optimisations de machines virtuelles Linux avec le modèle Resource Manager, consultez [Optimiser votre machine virtuelle Linux sur Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Utiliser RAID sur une machine virtuelle Azure
Le stockage est le facteur clé en matière d’incidence sur les performances de base de données dans les environnements de cloud. Grâce à la concurrence, RAID peut fournir un accès plus rapide qu’un seul disque. Pour plus d’informations, consultez [Niveaux RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

Le débit d’E/S disque et le temps de réponse d’E/S dans Azure peuvent être améliorés grâce à RAID. Nos tests de laboratoire montrent que le débit d’E/S disque peut être multiplié par deux et le temps de réponse d’E/S réduit de moitié en moyenne lorsque le nombre de disques RAID est doublé (de deux à quatre, quatre à huit, etc.). Voir l’ [annexe A](#AppendixA) pour plus d’informations.  

En plus des E/S disque, augmenter le niveau RAID améliore également les performances MySQL.  Voir l’ [annexe B](#AppendixB) pour plus d’informations.  

Il peut être intéressant de prendre en compte la taille de segment. En règle générale, lorsque vous disposez d’une plus grande taille de segment, vous obtenez une surcharge inférieure, en particulier pour les écritures de grande taille. Toutefois, lorsque la taille de segment est trop élevée, cela peut renforcer la surcharge et vous empêcher de tirer parti de RAID. La taille actuelle de la valeur par défaut est de 512 Ko, ce qui est le plus approprié pour les environnements de production standard. Voir l’ [annexe C](#AppendixC) pour plus d’informations.   

Il existe des limites sur le nombre de disques que vous pouvez ajouter, selon le type de machine virtuelle. Ces limites sont présentées en détail sur la page [Tailles de machines virtuelles et services cloud pour Microsoft Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Vous aurez besoin de quatre disques de données attachés pour suivre l’exemple RAID de cet article, même si vous pouvez choisir de configurer RAID avec moins de disques.  

Cet article suppose que vous avez déjà créé une machine virtuelle Linux et que MYSQL est installé et configuré. Pour plus d’informations sur la prise en main, consultez la page Installation de MySQL sur Azure.  

### <a name="set-up-raid-on-azure"></a>Configurer RAID sur Azure
Les étapes suivantes montrent comment créer RAID dans Azure à l’aide du portail Azure. Vous pouvez également configurer RAID à l’aide de scripts Windows PowerShell.
Dans cet exemple, nous allons configurer RAID 0 avec quatre disques.  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a>Ajouter un disque de données à votre machine virtuelle
Dans le portail Azure, accédez au tableau de bord et sélectionnez la machine virtuelle à laquelle vous souhaitez ajouter un disque de données. Dans cet exemple, la machine virtuelle est mysqlnode1.  

<!--![Virtual machines][1]-->

Cliquez sur **Disques**, puis cliquez sur **Attach New** (Attacher nouveau).

![Les machines virtuelles ajoutent des disques.](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Créez un nouveau disque de 500 Go. Assurez-vous que **Host Cache Preference** (Préférence de cache hôte) a la valeur **Aucun**.  Lorsque vous avez terminé, cliquez sur **OK**.

![Attacher un disque vide](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Cela ajoute un disque vide à votre machine virtuelle. Répétez cette étape trois fois afin de disposer de quatre disques de données pour RAID.  

Vous pouvez voir les disques ajoutés à la machine virtuelle en examinant le journal des messages du noyau. Par exemple, pour voir cela avec Ubuntu, utilisez la commande suivante :  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a>Création de RAID avec les disques supplémentaires
Les étapes suivantes décrivent la [configuration logicielle de RAID sur Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Si vous utilisez le système de fichiers XFS, exécutez les étapes ci-dessous après avoir créé le RAID.
>
>

Pour installer XFS sur Debian, Ubuntu ou Linux Mint, utilisez la commande suivante :  

    apt-get -y install xfsprogs  

Pour installer XFS sur Fedora, CentOS ou RHEL, utilisez la commande suivante :  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Configuration d’un nouveau chemin d’accès de stockage
Utilisez la commande suivante pour configurer un nouveau chemin d’accès de stockage :  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a>Copie des données d’origine vers le nouveau chemin d’accès de stockage
Utilisez la commande suivante pour copier des données dans le nouveau chemin d’accès de stockage :  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a>Modification des autorisations pour que MySQL puisse accéder (en lecture et écriture) au disque de données
Utilisez la commande suivante pour modifier les autorisations :  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a>Ajustement de l’algorithme de planification d’E/S disque
Linux implémente quatre types d’algorithmes de planification d’E/S :  

* Algorithme NOOP (aucune opération)
* Algorithme d’échéance (échéance)
* Algorithme de file d’attente complètement juste (CFQ)
* Algorithme de période de budget (anticipatif)  

Vous pouvez sélectionner différents planificateurs d’E/S sous différents scénarios pour optimiser les performances. Dans un environnement à accès complètement aléatoire, il n’existe pas de grande différence entre les algorithmes CFQ et d’échéance du point de vue des performances. Nous vous recommandons de définir l’environnement de base de données MySQL sur échéance pour la stabilité. En cas de nombreuses E/S séquentielles, CFQ peut réduire les performances d’E/S de disque.   

Pour les disques SSD et autres équipements, NOOP ou échéance peuvent fournir de meilleures performances que le planificateur par défaut.   

Avant le noyau 2.5, l’algorithme de planification d’E/S par défaut est échéance. À partir du noyau 2.6.18, CFQ est devenu l’algorithme de planification d’E/S par défaut.  Vous pouvez spécifier ce paramètre au moment du démarrage du noyau ou le modifier dynamiquement lorsque le système est en cours d’exécution.  

L’exemple suivant montre comment vérifier et définir le planificateur par défaut sur l’algorithme NOOP dans la famille de distribution Debian.  

### <a name="view-the-current-io-scheduler"></a>Visualiser le planificateur d’E/S actuel
Pour afficher le planificateur, exécutez la commande suivante :  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Vous verrez la sortie suivante, indiquant le planificateur actuel :  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a>Changer le dispositif actuel (/dev/sda) de l’algorithme de planification d’E/S
Exécutez les commandes suivantes pour modifier le dispositif actuel :  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Définir cette propriété pour /dev/sda uniquement n’est pas utile. Elle doit être définie sur tous les disques de données où réside la base de données.  
>
>

Vous devriez voir la sortie suivante, qui indique que grub.cfg a été régénéré avec succès et que le planificateur par défaut a été mis à jour vers NOOP :  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Pour la famille de distribution Red Hat, la commande suivante suffit :

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Configuration des paramètres d’opérations de fichier système
Une meilleure pratique consiste à désactiver la fonctionnalité de journalisation *atime* sur le système de fichiers. Atime est le dernier temps d’accès au fichier. Chaque fois qu’un fichier est accessible, le système de fichiers enregistre l’horodatage dans le journal. Toutefois, cette information est rarement utilisée. Vous pouvez la désactiver si vous n’en avez pas besoin, ce qui réduit le temps global d’accès au disque.  

Pour désactiver la journalisation atime, vous devez modifier le fichier de configuration système /etc/ fstab et ajouter l’option **noatime** .  

Par exemple, modifiez le fichier vim /etc/fstab, en ajoutant noatime comme indiqué dans l’exemple ci-dessous :  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Puis, remontez le système de fichiers avec la commande suivante :  

    mount -o remount /RAID0

Testez le résultat modifié. Lorsque vous modifiez le fichier de test, le temps d’accès n’est pas actualisé. Les exemples suivants montrent à quoi ressemble le code avant et après la modification.

Avant :        

![Code avant la modification de l’accès][5]

Après :

![Code après la modification de l’accès][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a>Augmentation du nombre maximal de handles du système pour la concurrence élevée
MySQL est une base de données à forte concurrence. Le nombre de handles concurrents est de 1024 pour Linux, ce qui n’est pas toujours suffisant. Utilisez les étapes suivantes pour augmenter les handles simultanés maximaux du système pour prendre en charge la haute concurrence de MySQL.

### <a name="modify-the-limitsconf-file"></a>Modification du fichier limits.conf
Ajoutez les quatre lignes suivantes dans le fichier /etc/security/limits.conf pour augmenter le nombre maximal de handles simultanés autorisés. Notez que 65536 est le nombre maximal que le système peut prendre en charge.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-the-system-for-the-new-limits"></a>Mise à jour du système pour les nouvelles limites
Pour mettre à jour le système, exécutez les commandes suivantes :  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a>Assurez-vous que les limites sont mises à jour au moment du démarrage
Placez les commandes de démarrage suivantes dans le fichier /etc/rc.local afin qu’elles prennent effet lors du démarrage.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Optimisation de base de données MySQL
Vous pouvez utiliser la même stratégie de réglage de performances pour configurer MySQL sur Azure que sur un ordinateur local.  

Les règles d’optimisation d’E/S principales sont :   

* Augmentez la taille du cache.
* Réduisez le délai de réponse E/S.  

Pour optimiser les paramètres du serveur MySQL, vous pouvez mettre à jour le fichier my.cnf, qui est le fichier de configuration par défaut du serveur et des ordinateurs clients.  

Les éléments de configuration suivants sont les principaux facteurs qui ont une incidence sur les performances de MySQL :  

* **innodb_buffer_pool_size** : le pool de mémoires tampons contient les données mises en mémoire tampon et l’index. Il est généralement défini sur 70 % de la mémoire physique.
* **innodb_log_file_size** : il s’agit de la taille du journal de rétablissement. Vous utilisez des journaux de rétablissement pour vous assurer que les opérations d’écriture sont rapides, fiables et récupérables après une panne. Il est défini sur 512 Mo, afin de vous donner suffisamment d’espace disque pour la journalisation des opérations d’écriture.
* **max_connections** : parfois, les applications ne ferment pas les connexions correctement. Une valeur supérieure accordera au serveur davantage de temps pour recycler les connexions inactives. Le nombre maximal de connexions est de 10 000, mais le maximum recommandé est de 5 000.
* **Innodb_file_per_table** : ce paramètre active ou désactive la capacité de InnoDB de stocker des tables dans des fichiers distincts. Activer l’option garantit que plusieurs opérations d’administration avancées peuvent être appliquées efficacement. Du point de vue des performances, elle peut accélérer la transmission d’espace de table et optimiser les performances de gestion de débris. Le paramètre recommandé pour cette option est ON.</br></br>
À partir de MySQL 5.6, le paramètre par défaut est ON, donc aucune action n’est nécessaire. Pour les versions antérieures, le paramètre par défaut est OFF. Le paramètre doit être modifié avant le chargement des données, étant donné que seules les tables nouvellement créées sont affectées.
* **innodb_flush_log_at_trx_commit** : la valeur par défaut est 1 et l’étendue 0~2. La valeur par défaut est l’option la plus adaptée pour une base de données MySQL autonome. Choisir 2 offre la meilleure intégrité des données et convient à Master dans le cluster MySQL. Choisir 0 autorise la perte de données, ce qui peut avoir une incidence sur la fiabilité (dans certains cas avec de meilleures performances) et convient à Slave dans le cluster MySQL.
* **Innodb_log_buffer_size** : le tampon journal autorise les transactions à s’exécuter, sans avoir à vider le journal sur le disque avant la validation des transactions. Toutefois, s’il existe des objets binaires ou un champ de texte volumineux, le cache est consommé rapidement et des E/S disque fréquentes seront déclenchées. Il est préférable d’augmenter la taille de la mémoire tampon si la variable d’état Innodb_log_waits n’est pas 0.
* **query_cache_size** : le meilleur choix consiste à la désactiver dès le départ. Définissez query_cache_size sur 0 (ce qui est le paramètre par défaut dans MySQL 5.6) et utilisez d’autres méthodes pour accélérer les requêtes.  

Consultez [l’Annexe D](#AppendixD) pour obtenir une comparaison des performances avant et après l’optimisation.

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a>Activation du journal des requêtes lentes MySQL pour analyser le goulot d’étranglement de performances
Le journal des requêtes lentes MySQL peut vous aider à identifier les requêtes lentes pour MySQL. Après avoir activé le journal des requêtes lentes MySQL, vous pouvez utiliser les outils MySQL comme **mysqldumpslow** pour identifier le goulot d’étranglement de performances.  

Par défaut, cette option n’est pas activée. Activer le journal des requêtes lentes peut consommer des ressources du processeur. Nous vous recommandons d’activer ce dernier temporairement, pour résoudre les goulots d’étranglement de performances. Pour activer le journal des requêtes lentes :

1. Modifiez le fichier my.cnf en ajoutant les lignes suivantes à la fin :

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Redémarrez le serveur MySQL.

        service  mysql  restart

3. Vérifiez si le paramètre prend effet à l’aide de la commande **show**.

![Journal des requêtes lentes ON][7]   

![Résultats du journal des requêtes lentes][8]

Dans cet exemple, vous pouvez voir que la fonctionnalité de requête lente a été activée. Vous pouvez ensuite utiliser l’outil **mysqldumpslow** pour déterminer les goulots d’étranglement et optimiser les performances, comme l’ajout d’index.

## <a name="appendices"></a>Annexes
Vous trouverez ci-dessous des exemples de données de test de performances obtenues sur un environnement lab ciblé. Ils fournissent des informations générales sur la tendance des données de performances, avec différentes approches de réglage des performances. Les résultats peuvent varier selon les versions de produit ou l’environnement.

### <a name="AppendixA"></a>Annexe A  
**Performances du disque (IOPS) avec des niveaux RAID différents**

![E/S par seconde du disque avec des niveaux RAID différents][9]

**Commandes de test**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> La charge de travail de ce test utilise 64 threads, pour tenter d’atteindre la limite supérieure de RAID.
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

La taille des fichiers utilisés pour ce test est de 30 Go et 1 Go respectivement, avec le système de fichiers XFS RAID 0 (4 disques).

### <a name="AppendixD"></a>Annexe D  
**Comparaison des performances (débit) MySQL avant et après l’optimisation**  
(système de fichiers XFS)

![Comparaison des performances (débit) MySQL avant et après l’optimisation][14]

**Commandes de test**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Le paramètre de configuration pour la valeur par défaut et l’optimisation est le suivant :**

| parameters | Default | Optimisation |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Aucune |7 Go |
| **innodb_log_file_size** |5 Mo |512 Mo |
| **max_connections** |100 |5 000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 Mo |128 Mo |
| **query_cache_size** |16 Mo |0 |

Pour obtenir plus de détails sur les [paramètres de configuration d’optimisation](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consultez les [instructions officielles de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

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

