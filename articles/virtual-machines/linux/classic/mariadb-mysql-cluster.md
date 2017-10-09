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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="9f795-103">Cluster MariaDB (MySQL) : didacticiel Azure</span><span class="sxs-lookup"><span data-stu-id="9f795-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f795-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="9f795-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="9f795-105">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="9f795-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="9f795-107">Cluster MariaDB entreprise est désormais disponible dans hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9f795-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="9f795-108">nouvelle offre de Hello déploient automatiquement un cluster MariaDB Galera sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9f795-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="9f795-109">Vous devez utiliser la nouvelle offre à partir de hello [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="9f795-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="9f795-110">Cet article vous explique comment toocreate un multimaître [Galera](http://galeracluster.com/products/) cluster de [MariaDBs](https://mariadb.org/en/about/) (un remplacement dans le désordre solide, évolutive et fiable pour MySQL) toowork dans un environnement hautement disponible sur Azure machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9f795-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="9f795-111">Présentation de l'architecture</span><span class="sxs-lookup"><span data-stu-id="9f795-111">Architecture overview</span></span>
<span data-ttu-id="9f795-112">Cet article décrit comment les étapes hello toocomplete suivant :</span><span class="sxs-lookup"><span data-stu-id="9f795-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="9f795-113">Créer un cluster à trois nœuds.</span><span class="sxs-lookup"><span data-stu-id="9f795-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="9f795-114">Disques de données hello distinct à partir du disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="9f795-115">Créer des disques de données hello dans le paramètre de RAID 0/agrégé par bande tooincrease IOPS.</span><span class="sxs-lookup"><span data-stu-id="9f795-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="9f795-116">Utiliser l’équilibrage de charge Azure toobalance hello de charge pour les nœuds de hello trois.</span><span class="sxs-lookup"><span data-stu-id="9f795-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="9f795-117">toominimize répétitive fonctionne, créez une image de machine virtuelle contient MariaDB + Galera et l’utiliser toocreate hello autres machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="9f795-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Architecture du système](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="9f795-119">Cette rubrique utilise hello [CLI d’Azure](../../../cli-install-nodejs.md) outils, vous devez donc vous assurer toodownload les et les connecter des instructions toohello conséquente tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9f795-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="9f795-120">Si vous avez besoin d’une commande de toohello de référence disponibles dans hello CLI d’Azure, consultez hello [référence des commandes CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9f795-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="9f795-121">Vous devez également trop[créer une clé SSH pour l’authentification] et prenez note de l’emplacement du fichier .pem hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="9f795-122">Créer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="9f795-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="9f795-123">Infrastructure</span><span class="sxs-lookup"><span data-stu-id="9f795-123">Infrastructure</span></span>
1. <span data-ttu-id="9f795-124">Créer un groupe d’affinités de toohold hello ressources ensemble.</span><span class="sxs-lookup"><span data-stu-id="9f795-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="9f795-125">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9f795-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="9f795-126">Créer un toohost de compte de stockage de tous les disques de notre.</span><span class="sxs-lookup"><span data-stu-id="9f795-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="9f795-127">Vous ne doivent pas placer plus de 40 disques très sollicités sur hello même tooavoid de compte de stockage atteint la limite du compte de stockage hello 20 000 e/s.</span><span class="sxs-lookup"><span data-stu-id="9f795-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="9f795-128">Dans ce cas, vous êtes bien inférieur à cette limite, donc vous devez stocker toutes les informations sur le même compte pour plus de simplicité de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="9f795-129">Rechercher le nom hello d’image de machine virtuelle hello CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="9f795-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="9f795-130">sortie de Hello sera quelque chose comme `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="9f795-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="9f795-131">Utilisez ce nom dans hello suivant l’étape.</span><span class="sxs-lookup"><span data-stu-id="9f795-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="9f795-132">Créer le modèle d’ordinateur virtuel hello et remplacez /path/to/key.pem avec chemin d’accès hello où vous avez stocké la clé SSH .pem hello généré.</span><span class="sxs-lookup"><span data-stu-id="9f795-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="9f795-133">Joindre des données de 500 Go quatre disques toohello machine virtuelle pour une utilisation dans une configuration RAID de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="9f795-134">Utiliser SSH toosign toohello modèle machine virtuelle que vous avez créé au mariadbhatemplate.cloudapp.net:22 et connectez-vous à l’aide de votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="9f795-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="9f795-135">Logiciel</span><span class="sxs-lookup"><span data-stu-id="9f795-135">Software</span></span>
1. <span data-ttu-id="9f795-136">Obtenir la racine de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="9f795-137">Installez la prise en charge RAID :</span><span class="sxs-lookup"><span data-stu-id="9f795-137">Install RAID support:</span></span>

    <span data-ttu-id="9f795-138">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-138">a.</span></span> <span data-ttu-id="9f795-139">Installez mdadm.</span><span class="sxs-lookup"><span data-stu-id="9f795-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="9f795-140">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-140">b.</span></span> <span data-ttu-id="9f795-141">Créer la configuration de RAID 0/stripe hello avec un système de fichiers EXT4.</span><span class="sxs-lookup"><span data-stu-id="9f795-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="9f795-142">c.</span><span class="sxs-lookup"><span data-stu-id="9f795-142">c.</span></span> <span data-ttu-id="9f795-143">Créer le répertoire de point de montage hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="9f795-144">d.</span><span class="sxs-lookup"><span data-stu-id="9f795-144">d.</span></span> <span data-ttu-id="9f795-145">Récupérer hello UUID d’un périphérique RAID hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="9f795-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="9f795-146">e.</span><span class="sxs-lookup"><span data-stu-id="9f795-146">e.</span></span> <span data-ttu-id="9f795-147">Modifiez /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="9f795-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="9f795-148">f.</span><span class="sxs-lookup"><span data-stu-id="9f795-148">f.</span></span> <span data-ttu-id="9f795-149">Ajout automatique de tooenable périphérique hello le montage de redémarrage, en remplaçant hello UUID avec la valeur de hello obtenu à partir de hello précédente **blkid de** commande.</span><span class="sxs-lookup"><span data-stu-id="9f795-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="9f795-150">g.</span><span class="sxs-lookup"><span data-stu-id="9f795-150">g.</span></span> <span data-ttu-id="9f795-151">Montez la nouvelle partition de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="9f795-152">Installez MariaDB.</span><span class="sxs-lookup"><span data-stu-id="9f795-152">Install MariaDB.</span></span>

    <span data-ttu-id="9f795-153">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-153">a.</span></span> <span data-ttu-id="9f795-154">Créer un fichier de MariaDB.repo hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="9f795-155">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-155">b.</span></span> <span data-ttu-id="9f795-156">Renseignez les fichiers de référentiel hello avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="9f795-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="9f795-157">c.</span><span class="sxs-lookup"><span data-stu-id="9f795-157">c.</span></span> <span data-ttu-id="9f795-158">conflits de tooavoid, supprimer postfix existant et mariadb-libs.</span><span class="sxs-lookup"><span data-stu-id="9f795-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="9f795-159">d.</span><span class="sxs-lookup"><span data-stu-id="9f795-159">d.</span></span> <span data-ttu-id="9f795-160">Installez MariaDB avec Galera.</span><span class="sxs-lookup"><span data-stu-id="9f795-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="9f795-161">Déplacer hello MySQL Active toohello RAID de niveau bloc l’unité de données.</span><span class="sxs-lookup"><span data-stu-id="9f795-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="9f795-162">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-162">a.</span></span> <span data-ttu-id="9f795-163">Copier le répertoire MySQL en cours de hello dans son nouvel emplacement et supprimer l’ancien répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="9f795-164">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-164">b.</span></span> <span data-ttu-id="9f795-165">Définir des autorisations pour le nouveau répertoire de hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="9f795-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="9f795-166">c.</span><span class="sxs-lookup"><span data-stu-id="9f795-166">c.</span></span> <span data-ttu-id="9f795-167">Créer un lien symbolique qui pointe hello ancien répertoire toohello nouvel emplacement sur hello partition RAID.</span><span class="sxs-lookup"><span data-stu-id="9f795-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="9f795-168">Étant donné que [SELinux interfère avec les opérations de cluster hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), il est nécessaire toodisable pour hello session active.</span><span class="sxs-lookup"><span data-stu-id="9f795-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="9f795-169">Modifier `/etc/selinux/config` toodisable pour des redémarrages ultérieurs.</span><span class="sxs-lookup"><span data-stu-id="9f795-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="9f795-170">Validez l’exécution de MySQL.</span><span class="sxs-lookup"><span data-stu-id="9f795-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="9f795-171">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-171">a.</span></span> <span data-ttu-id="9f795-172">Démarrez MySQL.</span><span class="sxs-lookup"><span data-stu-id="9f795-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="9f795-173">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-173">b.</span></span> <span data-ttu-id="9f795-174">Sécuriser l’installation de MySQL hello, définir le mot de passe racine hello, supprimer les utilisateurs anonymes toodisable racine distant connexion et supprimer la base de données de test hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="9f795-175">c.</span><span class="sxs-lookup"><span data-stu-id="9f795-175">c.</span></span> <span data-ttu-id="9f795-176">Créez un utilisateur de base de données hello pour les opérations de cluster et éventuellement pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="9f795-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="9f795-177">d.</span><span class="sxs-lookup"><span data-stu-id="9f795-177">d.</span></span> <span data-ttu-id="9f795-178">Arrêtez MySQL.</span><span class="sxs-lookup"><span data-stu-id="9f795-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="9f795-179">Créez un espace réservé de configuration.</span><span class="sxs-lookup"><span data-stu-id="9f795-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="9f795-180">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-180">a.</span></span> <span data-ttu-id="9f795-181">Modifier hello MySQL configuration toocreate un espace réservé pour les paramètres de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="9f795-182">Ne remplacez pas hello  **`<Variables>`**  ou supprimez les commentaires maintenant.</span><span class="sxs-lookup"><span data-stu-id="9f795-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="9f795-183">Ces opérations auront lieu une fois que vous aurez créé une machine virtuelle à partir de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="9f795-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="9f795-184">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-184">b.</span></span> <span data-ttu-id="9f795-185">Modifier hello  **[galera]**  section et il effacer.</span><span class="sxs-lookup"><span data-stu-id="9f795-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="9f795-186">c.</span><span class="sxs-lookup"><span data-stu-id="9f795-186">c.</span></span> <span data-ttu-id="9f795-187">Modifier hello **[mariadb]** section.</span><span class="sxs-lookup"><span data-stu-id="9f795-187">Edit hello **[mariadb]** section.</span></span>

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
8. <span data-ttu-id="9f795-188">Ouvrir les ports requis sur le pare-feu à l’aide de FirewallD sur CentOS 7 hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="9f795-189">MySQL : `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="9f795-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="9f795-190">GALERA : `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="9f795-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="9f795-191">GALERA IST : `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="9f795-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="9f795-192">RSYNC : `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="9f795-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="9f795-193">Recharger hello pare-feu :`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="9f795-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="9f795-194">Optimiser le système hello pour les performances.</span><span class="sxs-lookup"><span data-stu-id="9f795-194">Optimize hello system for performance.</span></span> <span data-ttu-id="9f795-195">Pour plus d’informations, consultez la section [Stratégie d’optimisation des performances](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="9f795-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="9f795-196">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-196">a.</span></span> <span data-ttu-id="9f795-197">Modifiez le fichier de configuration MySQL hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9f795-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="9f795-198">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-198">b.</span></span> <span data-ttu-id="9f795-199">Modifier hello **[mariadb]** section et ajouter hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="9f795-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f795-200">Nous recommandons que innodb\_buffer\_pool_size soit égal à 70 % de la mémoire de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9f795-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="9f795-201">Dans cet exemple, il a été défini à 2,45 Go pour le support hello machine virtuelle Azure avec 3,5 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="9f795-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="9f795-202">Arrêter MySQL, désactiver le service MySQL de s’exécuter sur tooavoid démarrage interrompre le cluster de hello lors de l’ajout d’un nœud et annuler le déploiement d’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="9f795-203">Capturer hello machine virtuelle via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="9f795-204">(Actuellement, [émettre &#1268; dans les outils de CLI d’Azure hello](https://github.com/Azure/azure-xplat-cli/issues/1268) décrit les faits hello que les images capturées par les outils CLI d’Azure hello ne capturent pas de disques de données hello attaché.)</span><span class="sxs-lookup"><span data-stu-id="9f795-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="9f795-205">a.</span><span class="sxs-lookup"><span data-stu-id="9f795-205">a.</span></span> <span data-ttu-id="9f795-206">Arrêt de la machine de hello via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="9f795-207">b.</span><span class="sxs-lookup"><span data-stu-id="9f795-207">b.</span></span> <span data-ttu-id="9f795-208">Cliquez sur **Capture** et spécifiez le nom de l’image en tant que hello **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="9f795-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="9f795-209">Fournissez une description et cochez « J’ai exécuté waagent. »</span><span class="sxs-lookup"><span data-stu-id="9f795-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Capture de machine virtuelle de hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="9f795-211">Créer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="9f795-211">Create hello cluster</span></span>
<span data-ttu-id="9f795-212">Créez trois machines virtuelles avec modèle hello créé, puis configurez et démarrez hello cluster.</span><span class="sxs-lookup"><span data-stu-id="9f795-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="9f795-213">Créer hello première machine virtuelle CentOS 7 VM de hello mariadb-galera-image de l’image vous avez créé, en fournissant hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9f795-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="9f795-214">Nom du réseau virtuel : mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="9f795-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="9f795-215">Sous-réseau : mariadb</span><span class="sxs-lookup"><span data-stu-id="9f795-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="9f795-216">Taille de la machine : moyenne</span><span class="sxs-lookup"><span data-stu-id="9f795-216">Machine size: medium</span></span>
 - <span data-ttu-id="9f795-217">Nom du service cloud : mariadbha (ou le nom que vous souhaitez toobe accessible via mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="9f795-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="9f795-218">Nom de la machine : mariadb1</span><span class="sxs-lookup"><span data-stu-id="9f795-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="9f795-219">Nom d’utilisateur : azureuser</span><span class="sxs-lookup"><span data-stu-id="9f795-219">Username: azureuser</span></span>
 - <span data-ttu-id="9f795-220">Accès SSH : activé</span><span class="sxs-lookup"><span data-stu-id="9f795-220">SSH access: enabled</span></span>
 - <span data-ttu-id="9f795-221">En fichier .pem de hello SSH certificat et en remplaçant /path/to/key.pem avec chemin d’accès hello où vous avez stocké la clé SSH .pem hello généré.</span><span class="sxs-lookup"><span data-stu-id="9f795-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f795-222">Hello commandes suivantes sont répartis sur plusieurs lignes par souci de clarté, mais vous devez entrer chacun une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="9f795-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="9f795-223">Créez deux machines virtuelles en les connectant un service de cloud toohello mariadbha.</span><span class="sxs-lookup"><span data-stu-id="9f795-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="9f795-224">Modifier le nom de machine virtuelle hello et hello port tooa unique port SSH pas en conflit avec d’autres machines virtuelles dans hello même service cloud.</span><span class="sxs-lookup"><span data-stu-id="9f795-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

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
  <span data-ttu-id="9f795-225">Pour MariaDB3 :</span><span class="sxs-lookup"><span data-stu-id="9f795-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="9f795-226">Vous devez tooget hello adresse IP interne de chacune des machines virtuelles de hello trois pour l’étape suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="9f795-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Obtention d’une adresse IP virtuelle](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="9f795-228">Utiliser SSH toosign toohello trois sur des machines virtuelles et de modifier le fichier de configuration hello sur chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="9f795-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="9f795-229">Supprimez les commentaires  **`wsrep_cluster_name`**  et  **`wsrep_cluster_address`**  en supprimant hello  **#**  au début de hello de ligne de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="9f795-230">En outre, remplacez  **`<ServerIP>`**  dans  **`wsrep_node_address`**  et  **`<NodeName>`**  dans  **`wsrep_node_name`**  avec hello IP de la machine virtuelle d’adresses et de nom, respectivement, et de ne pas commenter les lignes ainsi.</span><span class="sxs-lookup"><span data-stu-id="9f795-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="9f795-231">Démarrer le cluster de hello sur MariaDB1 et laissez-le s’exécutent au démarrage.</span><span class="sxs-lookup"><span data-stu-id="9f795-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="9f795-232">Démarrez MySQL sur MariaDB2 et MariaDB3 et laissez-le s’exécuter au démarrage.</span><span class="sxs-lookup"><span data-stu-id="9f795-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="9f795-233">Cluster d’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="9f795-233">Load balance hello cluster</span></span>
<span data-ttu-id="9f795-234">Lorsque vous avez créé des machines virtuelles de hello en cluster, vous avez ajouté les dans un ensemble de disponibilité appelé clusteravset tooensure qu’ils ont été placées sur différents domaines d’erreur et de mise à jour et que Azure jamais effectue une maintenance sur toutes les machines à la fois.</span><span class="sxs-lookup"><span data-stu-id="9f795-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="9f795-235">Cette configuration requise hello toobe pris en charge par hello contrat de niveau de service Azure (SLA).</span><span class="sxs-lookup"><span data-stu-id="9f795-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="9f795-236">Maintenant utiliser des demandes de toobalance d’équilibrage de charge Azure entre trois nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="9f795-237">Exécutez hello suivant de commandes sur votre ordinateur à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9f795-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="9f795-238">structure de paramètres de commande Hello est :`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="9f795-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="9f795-239">Hello CLI définit hello charge équilibrage sonde intervalle too15 secondes, ce qui peuvent être un peu trop longues.</span><span class="sxs-lookup"><span data-stu-id="9f795-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="9f795-240">Modifier dans le portail hello sous **points de terminaison** pour une des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="9f795-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Ajouter un point de terminaison](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="9f795-242">Sélectionnez **hello Reconfigure Balanced définir**.</span><span class="sxs-lookup"><span data-stu-id="9f795-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Reconfigurer hello-jeu d’équilibrage](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="9f795-244">Modification **intervalle de sondage** too5 secondes et enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="9f795-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Modifier l’intervalle de sondage](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="9f795-246">Validez le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="9f795-246">Validate hello cluster</span></span>
<span data-ttu-id="9f795-247">travail Hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="9f795-247">hello hard work is done.</span></span> <span data-ttu-id="9f795-248">cluster de Hello doit maintenant être accessible à `mariadbha.cloudapp.net:3306`, qui atteint l’équilibrage de charge hello et acheminer les demandes entre hello trois machines virtuelles sans heurts et efficacement.</span><span class="sxs-lookup"><span data-stu-id="9f795-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="9f795-249">Utiliser votre tooconnect de client favori MySQL, ou vous connecter à partir d’un des tooverify de machines virtuelles de hello l’utilisation de ce cluster.</span><span class="sxs-lookup"><span data-stu-id="9f795-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="9f795-250">Ensuite, créez une base de données et insérez-y des données.</span><span class="sxs-lookup"><span data-stu-id="9f795-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="9f795-251">vous avez créé de la base de données Hello renvoie hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="9f795-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9f795-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f795-252">Next steps</span></span>
<span data-ttu-id="9f795-253">Dans cet article, vous avez créé un cluster MariaDB + Galera hautement disponible à trois nœuds sur des machines virtuelles Azure exécutant CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="9f795-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="9f795-254">machines virtuelles de Hello sont à charge équilibrée avec équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="9f795-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="9f795-255">Vous souhaiterez peut-être toolook à [une autre façon toocluster MySQL sur Linux](mysql-cluster.md) ainsi que les méthodes trop[optimiser et de tester les performances de MySQL sur les machines virtuelles Azure Linux](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="9f795-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

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
