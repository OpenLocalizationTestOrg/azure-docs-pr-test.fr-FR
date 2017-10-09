---
title: aaaRun un MariaDB (MySQL) de cluster sur Azure | Documents Microsoft
description: "Création d’un cluster MySQL MariaDB + Galera sur des machines virtuelles Azure"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Cluster MariaDB (MySQL) : didacticiel Azure
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique. Cet article décrit le modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources Azure hello.

> [!NOTE]
> Cluster MariaDB entreprise est désormais disponible dans hello Azure Marketplace. nouvelle offre de Hello déploient automatiquement un cluster MariaDB Galera sur Azure Resource Manager. Vous devez utiliser la nouvelle offre à partir de hello [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

Cet article vous explique comment toocreate un multimaître [Galera](http://galeracluster.com/products/) cluster de [MariaDBs](https://mariadb.org/en/about/) (un remplacement dans le désordre solide, évolutive et fiable pour MySQL) toowork dans un environnement hautement disponible sur Azure machines virtuelles.

## <a name="architecture-overview"></a>Présentation de l'architecture
Cet article décrit comment les étapes hello toocomplete suivant :

- Créer un cluster à trois nœuds.
- Disques de données hello distinct à partir du disque du système d’exploitation hello.
- Créer des disques de données hello dans le paramètre de RAID 0/agrégé par bande tooincrease IOPS.
- Utiliser l’équilibrage de charge Azure toobalance hello de charge pour les nœuds de hello trois.
- toominimize répétitive fonctionne, créez une image de machine virtuelle contient MariaDB + Galera et l’utiliser toocreate hello autres machines virtuelles du cluster.

![Architecture du système](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> Cette rubrique utilise hello [CLI d’Azure](../../../cli-install-nodejs.md) outils, vous devez donc vous assurer toodownload les et les connecter des instructions toohello conséquente tooyour abonnement Azure. Si vous avez besoin d’une commande de toohello de référence disponibles dans hello CLI d’Azure, consultez hello [référence des commandes CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Vous devez également trop[créer une clé SSH pour l’authentification] et prenez note de l’emplacement du fichier .pem hello.
>
>

## <a name="create-hello-template"></a>Créer le modèle de hello
### <a name="infrastructure"></a>Infrastructure
1. Créer un groupe d’affinités de toohold hello ressources ensemble.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Créez un réseau virtuel.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Créer un toohost de compte de stockage de tous les disques de notre. Vous ne doivent pas placer plus de 40 disques très sollicités sur hello même tooavoid de compte de stockage atteint la limite du compte de stockage hello 20 000 e/s. Dans ce cas, vous êtes bien inférieur à cette limite, donc vous devez stocker toutes les informations sur le même compte pour plus de simplicité de hello.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Rechercher le nom hello d’image de machine virtuelle hello CentOS 7.

        azure vm image list | findstr CentOS
   sortie de Hello sera quelque chose comme `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Utilisez ce nom dans hello suivant l’étape.
5. Créer le modèle d’ordinateur virtuel hello et remplacez /path/to/key.pem avec chemin d’accès hello où vous avez stocké la clé SSH .pem hello généré.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Joindre des données de 500 Go quatre disques toohello machine virtuelle pour une utilisation dans une configuration RAID de hello.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Utiliser SSH toosign toohello modèle machine virtuelle que vous avez créé au mariadbhatemplate.cloudapp.net:22 et connectez-vous à l’aide de votre clé privée.

### <a name="software"></a>Logiciel
1. Obtenir la racine de hello.

        sudo su

2. Installez la prise en charge RAID :

    a. Installez mdadm.

              yum install mdadm

    b. Créer la configuration de RAID 0/stripe hello avec un système de fichiers EXT4.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Créer le répertoire de point de montage hello.

              mkdir /mnt/data
    d. Récupérer hello UUID d’un périphérique RAID hello nouvellement créé.

              blkid | grep /dev/md0
    e. Modifiez /etc/fstab.

              vi /etc/fstab
    f. Ajout automatique de tooenable périphérique hello le montage de redémarrage, en remplaçant hello UUID avec la valeur de hello obtenu à partir de hello précédente **blkid de** commande.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Montez la nouvelle partition de hello.

              mount /mnt/data

3. Installez MariaDB.

    a. Créer un fichier de MariaDB.repo hello.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Renseignez les fichiers de référentiel hello avec hello suivant le contenu :

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. conflits de tooavoid, supprimer postfix existant et mariadb-libs.

           yum remove postfix mariadb-libs-*
    d. Installez MariaDB avec Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Déplacer hello MySQL Active toohello RAID de niveau bloc l’unité de données.

    a. Copier le répertoire MySQL en cours de hello dans son nouvel emplacement et supprimer l’ancien répertoire de hello.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Définir des autorisations pour le nouveau répertoire de hello en conséquence.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Créer un lien symbolique qui pointe hello ancien répertoire toohello nouvel emplacement sur hello partition RAID.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Étant donné que [SELinux interfère avec les opérations de cluster hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), il est nécessaire toodisable pour hello session active. Modifier `/etc/selinux/config` toodisable pour des redémarrages ultérieurs.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Validez l’exécution de MySQL.

   a. Démarrez MySQL.

           service mysql start
   b. Sécuriser l’installation de MySQL hello, définir le mot de passe racine hello, supprimer les utilisateurs anonymes toodisable racine distant connexion et supprimer la base de données de test hello.

           mysql_secure_installation
   c. Créez un utilisateur de base de données hello pour les opérations de cluster et éventuellement pour vos applications.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Arrêtez MySQL.

            service mysql stop
7. Créez un espace réservé de configuration.

   a. Modifier hello MySQL configuration toocreate un espace réservé pour les paramètres de cluster hello. Ne remplacez pas hello  **`<Variables>`**  ou supprimez les commentaires maintenant. Ces opérations auront lieu une fois que vous aurez créé une machine virtuelle à partir de ce modèle.

            vi /etc/my.cnf.d/server.cnf
   b. Modifier hello  **[galera]**  section et il effacer.

   c. Modifier hello **[mariadb]** section.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Ouvrir les ports requis sur le pare-feu à l’aide de FirewallD sur CentOS 7 hello.

   * MySQL : `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA : `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST : `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC : `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Recharger hello pare-feu :`firewall-cmd --reload`

9. Optimiser le système hello pour les performances. Pour plus d’informations, consultez la section [Stratégie d’optimisation des performances](optimize-mysql.md).

   a. Modifiez le fichier de configuration MySQL hello à nouveau.

            vi /etc/my.cnf.d/server.cnf
   b. Modifier hello **[mariadb]** section et ajouter hello suivant le contenu :

   > [!NOTE]
   > Nous recommandons que innodb\_buffer\_pool_size soit égal à 70 % de la mémoire de votre machine virtuelle. Dans cet exemple, il a été défini à 2,45 Go pour le support hello machine virtuelle Azure avec 3,5 Go de RAM.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Arrêter MySQL, désactiver le service MySQL de s’exécuter sur tooavoid démarrage interrompre le cluster de hello lors de l’ajout d’un nœud et annuler le déploiement d’ordinateur de hello.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Capturer hello machine virtuelle via le portail de hello. (Actuellement, [émettre &#1268; dans les outils de CLI d’Azure hello](https://github.com/Azure/azure-xplat-cli/issues/1268) décrit les faits hello que les images capturées par les outils CLI d’Azure hello ne capturent pas de disques de données hello attaché.)

    a. Arrêt de la machine de hello via le portail de hello.

    b. Cliquez sur **Capture** et spécifiez le nom de l’image en tant que hello **mariadb-galera-image**. Fournissez une description et cochez « J’ai exécuté waagent. »
      
      ![Capture de machine virtuelle de hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Créer le cluster de hello
Créez trois machines virtuelles avec modèle hello créé, puis configurez et démarrez hello cluster.

1. Créer hello première machine virtuelle CentOS 7 VM de hello mariadb-galera-image de l’image vous avez créé, en fournissant hello informations suivantes :

 - Nom du réseau virtuel : mariadbvnet
 - Sous-réseau : mariadb
 - Taille de la machine : moyenne
 - Nom du service cloud : mariadbha (ou le nom que vous souhaitez toobe accessible via mariadbha.cloudapp.net)
 - Nom de la machine : mariadb1
 - Nom d’utilisateur : azureuser
 - Accès SSH : activé
 - En fichier .pem de hello SSH certificat et en remplaçant /path/to/key.pem avec chemin d’accès hello où vous avez stocké la clé SSH .pem hello généré.

   > [!NOTE]
   > Hello commandes suivantes sont répartis sur plusieurs lignes par souci de clarté, mais vous devez entrer chacun une seule ligne.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Créez deux machines virtuelles en les connectant un service de cloud toohello mariadbha. Modifier le nom de machine virtuelle hello et hello port tooa unique port SSH pas en conflit avec d’autres machines virtuelles dans hello même service cloud.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  Pour MariaDB3 :

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. Vous devez tooget hello adresse IP interne de chacune des machines virtuelles de hello trois pour l’étape suivante de hello :

    ![Obtention d’une adresse IP virtuelle](./media/mariadb-mysql-cluster/IP.png)
4. Utiliser SSH toosign toohello trois sur des machines virtuelles et de modifier le fichier de configuration hello sur chacun d’eux.

        sudo vi /etc/my.cnf.d/server.cnf

    Supprimez les commentaires  **`wsrep_cluster_name`**  et  **`wsrep_cluster_address`**  en supprimant hello  **#**  au début de hello de ligne de hello.
    En outre, remplacez  **`<ServerIP>`**  dans  **`wsrep_node_address`**  et  **`<NodeName>`**  dans  **`wsrep_node_name`**  avec hello IP de la machine virtuelle d’adresses et de nom, respectivement, et de ne pas commenter les lignes ainsi.
5. Démarrer le cluster de hello sur MariaDB1 et laissez-le s’exécutent au démarrage.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Démarrez MySQL sur MariaDB2 et MariaDB3 et laissez-le s’exécuter au démarrage.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Cluster d’équilibrage de charge hello
Lorsque vous avez créé des machines virtuelles de hello en cluster, vous avez ajouté les dans un ensemble de disponibilité appelé clusteravset tooensure qu’ils ont été placées sur différents domaines d’erreur et de mise à jour et que Azure jamais effectue une maintenance sur toutes les machines à la fois. Cette configuration requise hello toobe pris en charge par hello contrat de niveau de service Azure (SLA).

Maintenant utiliser des demandes de toobalance d’équilibrage de charge Azure entre trois nœuds de hello.

Exécutez hello suivant de commandes sur votre ordinateur à l’aide de hello CLI d’Azure.

structure de paramètres de commande Hello est :`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Hello CLI définit hello charge équilibrage sonde intervalle too15 secondes, ce qui peuvent être un peu trop longues. Modifier dans le portail hello sous **points de terminaison** pour une des machines virtuelles de hello.

![Ajouter un point de terminaison](./media/mariadb-mysql-cluster/Endpoint.PNG)

Sélectionnez **hello Reconfigure Balanced définir**.

![Reconfigurer hello-jeu d’équilibrage](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Modification **intervalle de sondage** too5 secondes et enregistrer vos modifications.

![Modifier l’intervalle de sondage](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Validez le cluster de hello
travail Hello est effectuée. cluster de Hello doit maintenant être accessible à `mariadbha.cloudapp.net:3306`, qui atteint l’équilibrage de charge hello et acheminer les demandes entre hello trois machines virtuelles sans heurts et efficacement.

Utiliser votre tooconnect de client favori MySQL, ou vous connecter à partir d’un des tooverify de machines virtuelles de hello l’utilisation de ce cluster.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Ensuite, créez une base de données et insérez-y des données.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

vous avez créé de la base de données Hello renvoie hello tableau suivant :

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez créé un cluster MariaDB + Galera hautement disponible à trois nœuds sur des machines virtuelles Azure exécutant CentOS 7. machines virtuelles de Hello sont à charge équilibrée avec équilibrage de charge Azure.

Vous souhaiterez peut-être toolook à [une autre façon toocluster MySQL sur Linux](mysql-cluster.md) ainsi que les méthodes trop[optimiser et de tester les performances de MySQL sur les machines virtuelles Azure Linux](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[créer une clé SSH pour l’authentification]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
