---
title: "aaaClusterize MySQL avec équilibrage de la charge des jeux | Documents Microsoft"
description: "Configurer une équilibrage de la charge, la haute disponibilité que Linux MySQL cluster créé avec le modèle de déploiement classique hello sur Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Utiliser des jeux d’équilibrage tooclusterize MySQL sur Linux
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. A [modèle Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) n’est disponible que si vous avez besoin de toodeploy un cluster MySQL.

Cet article explore et illustre hello différentes approches disponibles toodeploy services hautement disponibles basés sur Linux sur Microsoft Azure, en explorant MySQL Server haute disponibilité comme une introduction. Une vidéo illustrant cette approche est disponible sur [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Nous allons présenter une solution haute disponibilité MySQL à maître unique, deux nœuds et sans partage basée sur DRBD, Corosync et Pacemaker. Seul un nœud à la fois exécute MySQL. Lecture et en écriture à partir de hello les ressources DRBD sont également limité tooonly un seul nœud à la fois.

Il n’est pas nécessaire pour une solution d’adresse IP virtuelle, comme les VL, car vous allez utiliser des jeux dans la détection de fonctionnalité et de point de terminaison de tourniquet tooprovide Microsoft Azure, la suppression et récupération ordonnée de hello VIP d’équilibrage. Hello VIP est une adresse IPv4 routable globalement attribuée par Microsoft Azure lorsque vous créez le service cloud hello.

Plusieurs architectures sont possibles pour MySQL, comme NBD Cluster, Percona et Galera, ainsi que plusieurs solutions intermédiaires, notamment au moins une disponible sous forme de machine virtuelle sur [VM Depot](http://vmdepot.msopentech.com). Tant que ces solutions peuvent répliquer sur monodiffusion ou la multidiffusion ou la diffusion et ne s’appuient sur un stockage partagé ou de plusieurs interfaces réseau, les scénarios hello doivent être facile toodeploy sur Microsoft Azure.

Architectures de cluster peuvent être étendues produits tooother comme PostgreSQL et OpenLDAP de façon similaire. Cette procédure d’équilibrage de charge sans partage peut notamment être testée correctement avec OpenLDAP à multiples maîtres. Vous pouvez regarder la vidéo sur le blog Channel 9.

## <a name="get-ready"></a>Se préparer
Vous devez suivant de hello ressources et des capacités :

  - Compte d’un Microsoft Azure avec un abonnement valide, en mesure de toocreate au moins deux machines virtuelles (XS a été utilisé dans cet exemple)
  - Un réseau et un sous-réseau
  - Un groupe d’affinités
  - Un groupe à haute disponibilité
  - capacité toocreate disques durs virtuels de Hello en hello même région que le service de cloud computing hello et les joindre les machines virtuelles Linux toohello

### <a name="tested-environment"></a>Environnement testé
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync et Pacemaker

### <a name="affinity-group"></a>Groupe d'affinités
Créer un groupe d’affinités pour la solution de hello en vous connectant toohello portail Azure classic, en sélectionnant **paramètres**et la création d’un groupe d’affinités. Groupe d’affinités de toothis seront attribuées les ressources allouées créés ultérieurement.

### <a name="networks"></a>Réseaux
Un nouveau réseau est créé, et un sous-réseau est créé à l’intérieur du réseau de hello. Cet exemple utilise un réseau 10.10.10.0/24 avec un seul sous-réseau /24.

### <a name="virtual-machines"></a>Machines virtuelles
Hello premier ordinateur virtuel de 13.10 Ubuntu est créé à l’aide d’une image de galerie d’Ubuntu Endorsed et est appelée `hadb01`. Un nouveau service cloud est créé dans le processus de hello, appelé hadb. Ce nom illustre hello partagé, nature équilibrée, service de hello aura lors de l’ajout de davantage de ressources. Hello la création de `hadb01` est se déroule normalement et terminées à l’aide du portail de hello. Un point de terminaison pour SSH est automatiquement créé et réseau hello est sélectionné. Vous pouvez maintenant créer un groupe à haute disponibilité pour les machines virtuelles de hello.

Après la première machine virtuelle est créée (techniquement, lors de la création de service de cloud computing hello) de hello, créer hello deuxième machine virtuelle, `hadb02`. Pourquoi deuxième machine virtuelle, utilisez Ubuntu 13.10 VM à partir de la galerie de hello à l’aide du portail de hello, mais utiliser un service cloud existant, `hadb.cloudapp.net`, au lieu de créer un nouveau. ensemble de réseau et la disponibilité de Hello doit être sélectionné automatiquement. Un point de terminaison SSH est également créé.

Une fois que les deux ordinateurs virtuels ont été créés, prenez note du port SSH hello `hadb01` (TCP 22) et `hadb02` (affectée automatiquement par Azure).

### <a name="attached-storage"></a>Stockage associé
Attacher un tooboth disque nouvelles machines virtuelles et créer des disques de 5 Go dans les processus hello. les disques Hello sont hébergés dans le conteneur de disque dur virtuel hello en cours d’utilisation pour vos disques de système d’exploitation principal. Une fois que les disques sont créés et attachés, n’est pas toorestart besoin Linux car noyau de hello verront la nouvelle unité de hello. Cet appareil est généralement `/dev/sdc`. Vérifiez `dmesg` pour la sortie de hello.

Sur chaque machine virtuelle, créez une partition à l’aide de `cfdisk` (partition principale, de Linux) et d’écriture hello nouvelle table. Ne créez pas de système de fichiers sur cette partition.

## <a name="set-up-hello-cluster"></a>Configurer le cluster de hello
Utilisez APT tooinstall Corosync STIMULATEUR et DRBD sur les deux ordinateurs virtuels Ubuntu. toodo avec `apt-get`, exécutez hello code suivant :

    sudo apt-get install corosync pacemaker drbd8-utils.

N’installez pas MySQL pour l’instant. Debian et Ubuntu des scripts d’installation initialisera un répertoire de données MySQL sur `/var/lib/mysql`, mais étant donné que le répertoire de hello sera remplacé par un système de fichiers DRBD, vous devez tooinstall MySQL ultérieurement.

Vérifier (à l’aide de `/sbin/ifconfig`) que les deux ordinateurs virtuels utilisent les adresses de sous-réseau de 10.10.10.0/24 hello et que qu’ils peuvent exécuter un ping sur eux par nom. Vous pouvez également utiliser `ssh-keygen` et `ssh-copy-id` toomake que les deux ordinateurs virtuels peuvent communiquer via le protocole SSH sans mot de passe.

### <a name="set-up-drbd"></a>Configurer DRBD
Créer une ressource DRBD qui utilise hello sous-jacent `/dev/sdc1` tooproduce de partitionner un `/dev/drbd1` ressources qui peuvent être mis en forme à l’aide d’ext3 et utilisés dans les nœuds principaux et secondaires.

1. Ouvrez `/etc/drbd.d/r0.res` et hello de la copie après la définition de ressource sur les deux ordinateurs virtuels :

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Initialiser les ressources hello à l’aide de `drbdadm` sur les deux ordinateurs virtuels :

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Sur hello d’ordinateur virtuel principal (`hadb01`), forcer la propriété (principal) de ressource DRBD hello :

        sudo drbdadm primary --force r0

Si vous examinez le contenu de hello de/proc/drbd (`sudo cat /proc/drbd`) sur les deux ordinateurs virtuels, vous devez voir `Primary/Secondary` sur `hadb01` et `Secondary/Primary` sur `hadb02`, il est cohérent avec la solution hello à ce stade. disque de 5 Go Hello est synchronisé sur réseau 10.10.10.0/24 hello aucun toocustomers frais.

Après la synchronisation de disque de hello, vous pouvez créer le système de fichiers hello sur `hadb01`. À des fins de test, nous avons utilisé ext2, mais hello suivante de code crée un système de fichiers ext3 :

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Monter hello DRBD ressource
Vous êtes maintenant prêt toomount ressources DRBD hello `hadb01`. Le système Debian et ses dérivés utilisent `/var/lib/mysql` en tant que répertoire de données MySQL. Étant donné que vous n’avez pas installé MySQL, créer le répertoire de hello et monter hello DRBD ressource. tooperform cette option, exécutez hello suivant le code de `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Configurez MySQL
Vous êtes maintenant prêt tooinstall MySQL sur `hadb01`:

    sudo apt-get install mysql-server

Pour `hadb02`, vous avez deux options. Vous pouvez installer mysql server, ce qui /var/lib/mysql de créer, remplir avec un nouveau répertoire de données, puis supprimez le contenu de hello. tooperform cette option, exécutez hello suivant le code de `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

deuxième option de Hello est toofailover trop`hadb02` , puis installez le serveur mysql il. Scripts d’installation remarquerez une installation existante de hello et ne modifie pas.

Exécution hello code sur Suivant `hadb01`:

    sudo drbdadm secondary –force r0

Exécution hello code sur Suivant `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Si vous ne prévoyez pas toofailover DRBD maintenant, hello première option est plus facile, bien que sans doute moins élégante. Une fois la configuration terminée, vous pouvez commencer à travailler sur votre base de données MySQL. Exécution hello code sur Suivant `hadb02` (ou de serveurs de hello est actif, selon tooDRBD) :

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Cette dernière instruction désactive l’authentification pour l’utilisateur racine de hello dans cette table. Elle doit être remplacée par vos instructions GRANT de production et n'est incluse qu'à titre d'exemple.

Si vous souhaitez remplacer les requêtes toomake à partir d’ordinateurs virtuels en dehors de hello (qui est l’objectif de hello de ce guide), vous devez également tooenable mise en réseau pour MySQL. Sur les deux ordinateurs virtuels, ouvrez `/etc/mysql/my.cnf` et accédez trop`bind-address`. Modifier l’adresse de hello provenant de 127.0.0.1 too0.0.0.0. Après avoir enregistré le fichier de hello, émettre une `sudo service mysql restart` sur votre serveur principal actuel.

### <a name="create-hello-mysql-load-balanced-set"></a>Créer le jeu d’équilibrage de charge MySQL hello
Revenir en arrière toohello portail, accédez trop`hadb01`, puis choisissez **points de terminaison**. toocreate un point de terminaison, choisissez MySQL (le port TCP 3306) à partir de la liste déroulante de hello et sélectionnez **créer nouveau jeu d’équilibrage**. Point de terminaison nom hello équilibrés en charge `lb-mysql`. Définissez **temps** too5 secondes minimum.

Après avoir créé le point de terminaison hello, accédez trop`hadb02`, choisissez **points de terminaison**et créer un point de terminaison. Choisissez `lb-mysql`, puis sélectionnez MySQL à partir de la liste déroulante de hello. Vous pouvez également utiliser hello CLI d’Azure pour cette étape.

Vous avez maintenant tout ce dont vous avez besoin pour une opération manuelle du cluster de hello.

### <a name="test-hello-load-balanced-set"></a>Test d’un jeu d’équilibrage de la charge hello
Il est possible d’exécuter des tests à partir d’une machine externe à l’aide d’un client MySQL, ou à l’aide de certaines applications, telles que phpMyAdmin exécutée en tant que site web Azure. Dans ce cas, vous avez utilisé l’outil de ligne de commande de MySQL sur une autre boîte Linux :

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Basculement manuel
Vous pouvez simuler des basculements en arrêtant MySQL, en commutant la machine virtuelle principale de DRBD et en redémarrant MySQL.

tooperform cette tâche, exécutez hello suivant de code de hadb01 :

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Puis, sur hadb02 :

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Après un basculement manuel, vous pouvez répéter votre requête à distance. Elle devrait fonctionner parfaitement.

## <a name="set-up-corosync"></a>Configurer Corosync
Corosync est requis pour STIMULATEUR toowork l’infrastructure cluster sous-jacent hello. Pour les pulsations (et autres méthodes comme Ultramonkey), Corosync est un fractionnement des fonctionnalités CRM hello, tandis que STIMULATEUR reste tooHeartbeat ressemble davantage de fonctionnalités.

Hello principale contrainte pour Corosync sur Azure est que Corosync préfère multidiffusion diffusion sur les communications de monodiffusion, mais mise en réseau de Microsoft Azure prend uniquement en charge la monodiffusion.

Heureusement, Corosync dispose d’un mode de monodiffusion fonctionnel. Hello seule véritable contrainte est comme tous les nœuds ne sont pas communiquer entre eux, vous devez les nœuds de hello toodefine dans vos fichiers de configuration, y compris leurs adresses IP. Nous pouvons utiliser des fichiers d’exemple hello Corosync pour la monodiffusion et la modification de lier l’adresse, les listes de nœud et les répertoires de journalisation (Ubuntu utilise `/var/log/corosync` tandis que hello exemple fichiers utilisent `/var/log/cluster`) et activer les outils de quorum.

> [!NOTE]
> Utilisez hello suit `transport: udpu` directive et hello définies manuellement les adresses IP pour les deux nœuds.

Exécution hello code sur Suivant `/etc/corosync/corosync.conf` pour les deux nœuds :

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Copiez ce fichier de configuration sur les deux machines virtuelles et démarrez Corosync dans les deux nœuds :

    sudo service start corosync

Peu après le démarrage du service de hello, cluster de hello doit être établie dans l’anneau d’actuel hello et quorum doit être constitué. Nous pouvons vérifier cette fonctionnalité en consultant des journaux ou en hello suivant le code en cours d’exécution :

    sudo corosync-quorumtool –l

Vous verrez toohello similaire de sortie suivant image :

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Configurer Pacemaker
STIMULATEUR utilise hello toomonitor de cluster pour les ressources, définir quand les couleurs primaires sont défaillants et passer ces toosecondaries de ressources. Les ressources peuvent notamment être définies à partir d'un ensemble de scripts disponibles ou à partir de script LSB (de type init).

Nous souhaitons STIMULATEUR ressource DRBD hello trop « propre », point de montage hello et le service de MySQL hello. Si STIMULATEUR peut activer et désactiver DRBD, monter et démonter et puis démarrer ou arrêter MySQL Bonjour bon de commande lorsque quelque chose se produit avec hello principal, le programme d’installation est terminée.

Lors de la première installation de Pacemaker, votre configuration doit être simple. Exemple :

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Vérifier la configuration de hello en exécutant `sudo crm configure show`.
2. Puis créez un fichier (comme `/tmp/cluster.conf`) avec hello suivant des ressources :

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Charger le fichier hello dans la configuration de hello. Vous ne devez toodo cela dans un seul nœud.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Vérifiez que Pacemaker se lance au démarrage dans les deux nœuds :

        sudo update-rc.d pacemaker defaults

5. À l’aide de `sudo crm_mon –L`, vérifiez qu’un de vos nœuds est devenue master hello pour le cluster de hello et toutes les ressources hello est en cours d’exécution. Vous pouvez utiliser toocheck de montage et ps des ressources de hello sont en cours d’exécution.

Hello ci-dessous capture d’écran illustre `crm_mon` avec un seul nœud est arrêté (sortie en sélectionnant Ctrl + C) :

![crm_mon node stopped](./media/mysql-cluster/image002.png)

Cette capture d'écran montre les deux nœuds, avec un maître et un esclave :

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Test
Vous êtes prêts pour une simulation de basculement automatique. Il existe deux façons toodo cela : conditionnelle et inconditionnelle.

fonction d’arrêt du cluster hello utilise Hello moyen souple : ``crm_standby -U `uname -n` -v on``. Si vous utilisez ce paramètre sur le contrôleur de hello, esclave de hello adopte. N’oubliez pas de tooset cette toooff précédent. Dans le cas contraire, crm_mon affichera un nœud en veille.

Hello dépens est en cours d’arrêt vers le bas hello ordinateur virtuel principal (hadb01) via le portail de hello ou en modifiant hello le niveau d’exécution sur hello VM (autrement dit, arrêt, arrêt). Ainsi, Corosync et STIMULATEUR en échangeant les cours de ce masque hello vers le bas. Vous pouvez tester cela (utile pour les fenêtres de maintenance), mais vous pouvez également forcer le scénario de hello en figeant hello machine virtuelle.

## <a name="stonith"></a>STONITH
Il doit être possible de tooissue un arrêt de la machine virtuelle via hello CLI d’Azure à la place d’un script STONITH qui contrôle un périphérique physique. Vous pouvez utiliser `/usr/lib/stonith/plugins/external/ssh` en tant que base et activer STONITH dans la configuration du cluster hello. CLI Azure doit être installé globalement et paramètres de publication hello et profil doit être chargée pour les utilisateurs du cluster hello.

Exemple de code pour la ressource de hello est disponible sur [GitHub](https://github.com/bureado/aztonith). Modifier la configuration du cluster hello en ajoutant hello suivant trop`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> script de Hello n’effectue pas contrôles vers le haut/bas. ressource SSH Hello d’origine avait 15 chèques ping, mais des temps de récupération pour une machine virtuelle Azure peuvent être plus variable.

## <a name="limitations"></a>Limites
Hello limites suivantes s’appliquent :

* Hello linbit DRBD ressource script qui gère DRBD en tant que ressource dans les utilisations STIMULATEUR `drbdadm down` lors de l’arrêt d’un nœud, même si le nœud de hello est simplement se mettre en veille. Ce n’est pas idéale, car les esclave hello ne va pas synchroniser ressource DRBD de hello alors que le maître de hello Obtient des écritures. Si le maître de hello n’échoue pas gracieusement, esclave de hello peut prendre sur un état de système de fichiers plus anciens. Cela peut être résolu de deux façons :
  * En appliquant un `drbdadm up r0` dans tous les nœuds du cluster grâce à une surveillance locale (non groupée)
  * En modifiant le script DRBD linbit hello et en faisant en sorte que `down` n’est pas appelée`/usr/lib/ocf/resource.d/linbit/drbd`
* équilibrage de charge Hello nécessitant au moins cinq secondes toorespond, applications doivent être adaptée aux clusters et être plus tolérant vis-à-vis du délai d’attente. D’autres architectures peuvent également aider, par exemple les files d’attente intégrées et les intergiciels de requête.
* MySQL de paramétrage est tooensure nécessaire que l’écriture est effectuée à un rythme gérable et les caches sont vidé toodisk aussi souvent que possible toominimize une perte de la mémoire.
* Écrire des performances dépend de la machine virtuelle, car le mécanisme de hello utilisé par le périphérique de hello DRBD tooreplicate d’interconnexion dans un commutateur virtuel hello.
