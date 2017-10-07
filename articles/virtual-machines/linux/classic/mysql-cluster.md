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
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="f0936-103">Utiliser des jeux d’équilibrage tooclusterize MySQL sur Linux</span><span class="sxs-lookup"><span data-stu-id="f0936-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0936-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="f0936-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="f0936-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f0936-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f0936-107">A [modèle Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) n’est disponible que si vous avez besoin de toodeploy un cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="f0936-108">Cet article explore et illustre hello différentes approches disponibles toodeploy services hautement disponibles basés sur Linux sur Microsoft Azure, en explorant MySQL Server haute disponibilité comme une introduction.</span><span class="sxs-lookup"><span data-stu-id="f0936-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="f0936-109">Une vidéo illustrant cette approche est disponible sur [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="f0936-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="f0936-110">Nous allons présenter une solution haute disponibilité MySQL à maître unique, deux nœuds et sans partage basée sur DRBD, Corosync et Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="f0936-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="f0936-111">Seul un nœud à la fois exécute MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="f0936-112">Lecture et en écriture à partir de hello les ressources DRBD sont également limité tooonly un seul nœud à la fois.</span><span class="sxs-lookup"><span data-stu-id="f0936-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="f0936-113">Il n’est pas nécessaire pour une solution d’adresse IP virtuelle, comme les VL, car vous allez utiliser des jeux dans la détection de fonctionnalité et de point de terminaison de tourniquet tooprovide Microsoft Azure, la suppression et récupération ordonnée de hello VIP d’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="f0936-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="f0936-114">Hello VIP est une adresse IPv4 routable globalement attribuée par Microsoft Azure lorsque vous créez le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="f0936-115">Plusieurs architectures sont possibles pour MySQL, comme NBD Cluster, Percona et Galera, ainsi que plusieurs solutions intermédiaires, notamment au moins une disponible sous forme de machine virtuelle sur [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="f0936-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="f0936-116">Tant que ces solutions peuvent répliquer sur monodiffusion ou la multidiffusion ou la diffusion et ne s’appuient sur un stockage partagé ou de plusieurs interfaces réseau, les scénarios hello doivent être facile toodeploy sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f0936-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="f0936-117">Architectures de cluster peuvent être étendues produits tooother comme PostgreSQL et OpenLDAP de façon similaire.</span><span class="sxs-lookup"><span data-stu-id="f0936-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="f0936-118">Cette procédure d’équilibrage de charge sans partage peut notamment être testée correctement avec OpenLDAP à multiples maîtres. Vous pouvez regarder la vidéo sur le blog Channel 9.</span><span class="sxs-lookup"><span data-stu-id="f0936-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="f0936-119">Se préparer</span><span class="sxs-lookup"><span data-stu-id="f0936-119">Get ready</span></span>
<span data-ttu-id="f0936-120">Vous devez suivant de hello ressources et des capacités :</span><span class="sxs-lookup"><span data-stu-id="f0936-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="f0936-121">Compte d’un Microsoft Azure avec un abonnement valide, en mesure de toocreate au moins deux machines virtuelles (XS a été utilisé dans cet exemple)</span><span class="sxs-lookup"><span data-stu-id="f0936-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="f0936-122">Un réseau et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="f0936-122">A network and a subnet</span></span>
  - <span data-ttu-id="f0936-123">Un groupe d’affinités</span><span class="sxs-lookup"><span data-stu-id="f0936-123">An affinity group</span></span>
  - <span data-ttu-id="f0936-124">Un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="f0936-124">An availability set</span></span>
  - <span data-ttu-id="f0936-125">capacité toocreate disques durs virtuels de Hello en hello même région que le service de cloud computing hello et les joindre les machines virtuelles Linux toohello</span><span class="sxs-lookup"><span data-stu-id="f0936-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="f0936-126">Environnement testé</span><span class="sxs-lookup"><span data-stu-id="f0936-126">Tested environment</span></span>
* <span data-ttu-id="f0936-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="f0936-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="f0936-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="f0936-128">DRBD</span></span>
  * <span data-ttu-id="f0936-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="f0936-129">MySQL Server</span></span>
  * <span data-ttu-id="f0936-130">Corosync et Pacemaker</span><span class="sxs-lookup"><span data-stu-id="f0936-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="f0936-131">Groupe d'affinités</span><span class="sxs-lookup"><span data-stu-id="f0936-131">Affinity group</span></span>
<span data-ttu-id="f0936-132">Créer un groupe d’affinités pour la solution de hello en vous connectant toohello portail Azure classic, en sélectionnant **paramètres**et la création d’un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="f0936-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="f0936-133">Groupe d’affinités de toothis seront attribuées les ressources allouées créés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f0936-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="f0936-134">Réseaux</span><span class="sxs-lookup"><span data-stu-id="f0936-134">Networks</span></span>
<span data-ttu-id="f0936-135">Un nouveau réseau est créé, et un sous-réseau est créé à l’intérieur du réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="f0936-136">Cet exemple utilise un réseau 10.10.10.0/24 avec un seul sous-réseau /24.</span><span class="sxs-lookup"><span data-stu-id="f0936-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="f0936-137">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f0936-137">Virtual machines</span></span>
<span data-ttu-id="f0936-138">Hello premier ordinateur virtuel de 13.10 Ubuntu est créé à l’aide d’une image de galerie d’Ubuntu Endorsed et est appelée `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f0936-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="f0936-139">Un nouveau service cloud est créé dans le processus de hello, appelé hadb.</span><span class="sxs-lookup"><span data-stu-id="f0936-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="f0936-140">Ce nom illustre hello partagé, nature équilibrée, service de hello aura lors de l’ajout de davantage de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0936-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="f0936-141">Hello la création de `hadb01` est se déroule normalement et terminées à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="f0936-142">Un point de terminaison pour SSH est automatiquement créé et réseau hello est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f0936-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="f0936-143">Vous pouvez maintenant créer un groupe à haute disponibilité pour les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="f0936-144">Après la première machine virtuelle est créée (techniquement, lors de la création de service de cloud computing hello) de hello, créer hello deuxième machine virtuelle, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="f0936-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="f0936-145">Pourquoi deuxième machine virtuelle, utilisez Ubuntu 13.10 VM à partir de la galerie de hello à l’aide du portail de hello, mais utiliser un service cloud existant, `hadb.cloudapp.net`, au lieu de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="f0936-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="f0936-146">ensemble de réseau et la disponibilité de Hello doit être sélectionné automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f0936-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="f0936-147">Un point de terminaison SSH est également créé.</span><span class="sxs-lookup"><span data-stu-id="f0936-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="f0936-148">Une fois que les deux ordinateurs virtuels ont été créés, prenez note du port SSH hello `hadb01` (TCP 22) et `hadb02` (affectée automatiquement par Azure).</span><span class="sxs-lookup"><span data-stu-id="f0936-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="f0936-149">Stockage associé</span><span class="sxs-lookup"><span data-stu-id="f0936-149">Attached storage</span></span>
<span data-ttu-id="f0936-150">Attacher un tooboth disque nouvelles machines virtuelles et créer des disques de 5 Go dans les processus hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="f0936-151">les disques Hello sont hébergés dans le conteneur de disque dur virtuel hello en cours d’utilisation pour vos disques de système d’exploitation principal.</span><span class="sxs-lookup"><span data-stu-id="f0936-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="f0936-152">Une fois que les disques sont créés et attachés, n’est pas toorestart besoin Linux car noyau de hello verront la nouvelle unité de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="f0936-153">Cet appareil est généralement `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f0936-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="f0936-154">Vérifiez `dmesg` pour la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="f0936-155">Sur chaque machine virtuelle, créez une partition à l’aide de `cfdisk` (partition principale, de Linux) et d’écriture hello nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="f0936-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="f0936-156">Ne créez pas de système de fichiers sur cette partition.</span><span class="sxs-lookup"><span data-stu-id="f0936-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="f0936-157">Configurer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="f0936-157">Set up hello cluster</span></span>
<span data-ttu-id="f0936-158">Utilisez APT tooinstall Corosync STIMULATEUR et DRBD sur les deux ordinateurs virtuels Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f0936-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="f0936-159">toodo avec `apt-get`, exécutez hello code suivant :</span><span class="sxs-lookup"><span data-stu-id="f0936-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="f0936-160">N’installez pas MySQL pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="f0936-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="f0936-161">Debian et Ubuntu des scripts d’installation initialisera un répertoire de données MySQL sur `/var/lib/mysql`, mais étant donné que le répertoire de hello sera remplacé par un système de fichiers DRBD, vous devez tooinstall MySQL ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f0936-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="f0936-162">Vérifier (à l’aide de `/sbin/ifconfig`) que les deux ordinateurs virtuels utilisent les adresses de sous-réseau de 10.10.10.0/24 hello et que qu’ils peuvent exécuter un ping sur eux par nom.</span><span class="sxs-lookup"><span data-stu-id="f0936-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="f0936-163">Vous pouvez également utiliser `ssh-keygen` et `ssh-copy-id` toomake que les deux ordinateurs virtuels peuvent communiquer via le protocole SSH sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f0936-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="f0936-164">Configurer DRBD</span><span class="sxs-lookup"><span data-stu-id="f0936-164">Set up DRBD</span></span>
<span data-ttu-id="f0936-165">Créer une ressource DRBD qui utilise hello sous-jacent `/dev/sdc1` tooproduce de partitionner un `/dev/drbd1` ressources qui peuvent être mis en forme à l’aide d’ext3 et utilisés dans les nœuds principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="f0936-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="f0936-166">Ouvrez `/etc/drbd.d/r0.res` et hello de la copie après la définition de ressource sur les deux ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="f0936-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="f0936-167">Initialiser les ressources hello à l’aide de `drbdadm` sur les deux ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="f0936-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="f0936-168">Sur hello d’ordinateur virtuel principal (`hadb01`), forcer la propriété (principal) de ressource DRBD hello :</span><span class="sxs-lookup"><span data-stu-id="f0936-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="f0936-169">Si vous examinez le contenu de hello de/proc/drbd (`sudo cat /proc/drbd`) sur les deux ordinateurs virtuels, vous devez voir `Primary/Secondary` sur `hadb01` et `Secondary/Primary` sur `hadb02`, il est cohérent avec la solution hello à ce stade.</span><span class="sxs-lookup"><span data-stu-id="f0936-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="f0936-170">disque de 5 Go Hello est synchronisé sur réseau 10.10.10.0/24 hello aucun toocustomers frais.</span><span class="sxs-lookup"><span data-stu-id="f0936-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="f0936-171">Après la synchronisation de disque de hello, vous pouvez créer le système de fichiers hello sur `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f0936-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="f0936-172">À des fins de test, nous avons utilisé ext2, mais hello suivante de code crée un système de fichiers ext3 :</span><span class="sxs-lookup"><span data-stu-id="f0936-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="f0936-173">Monter hello DRBD ressource</span><span class="sxs-lookup"><span data-stu-id="f0936-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="f0936-174">Vous êtes maintenant prêt toomount ressources DRBD hello `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f0936-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="f0936-175">Le système Debian et ses dérivés utilisent `/var/lib/mysql` en tant que répertoire de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="f0936-176">Étant donné que vous n’avez pas installé MySQL, créer le répertoire de hello et monter hello DRBD ressource.</span><span class="sxs-lookup"><span data-stu-id="f0936-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="f0936-177">tooperform cette option, exécutez hello suivant le code de `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f0936-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="f0936-178">Configurez MySQL</span><span class="sxs-lookup"><span data-stu-id="f0936-178">Set up MySQL</span></span>
<span data-ttu-id="f0936-179">Vous êtes maintenant prêt tooinstall MySQL sur `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f0936-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="f0936-180">Pour `hadb02`, vous avez deux options.</span><span class="sxs-lookup"><span data-stu-id="f0936-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="f0936-181">Vous pouvez installer mysql server, ce qui /var/lib/mysql de créer, remplir avec un nouveau répertoire de données, puis supprimez le contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="f0936-182">tooperform cette option, exécutez hello suivant le code de `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="f0936-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="f0936-183">deuxième option de Hello est toofailover trop`hadb02` , puis installez le serveur mysql il.</span><span class="sxs-lookup"><span data-stu-id="f0936-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="f0936-184">Scripts d’installation remarquerez une installation existante de hello et ne modifie pas.</span><span class="sxs-lookup"><span data-stu-id="f0936-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="f0936-185">Exécution hello code sur Suivant `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f0936-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="f0936-186">Exécution hello code sur Suivant `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="f0936-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="f0936-187">Si vous ne prévoyez pas toofailover DRBD maintenant, hello première option est plus facile, bien que sans doute moins élégante.</span><span class="sxs-lookup"><span data-stu-id="f0936-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="f0936-188">Une fois la configuration terminée, vous pouvez commencer à travailler sur votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="f0936-189">Exécution hello code sur Suivant `hadb02` (ou de serveurs de hello est actif, selon tooDRBD) :</span><span class="sxs-lookup"><span data-stu-id="f0936-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="f0936-190">Cette dernière instruction désactive l’authentification pour l’utilisateur racine de hello dans cette table.</span><span class="sxs-lookup"><span data-stu-id="f0936-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="f0936-191">Elle doit être remplacée par vos instructions GRANT de production et n'est incluse qu'à titre d'exemple.</span><span class="sxs-lookup"><span data-stu-id="f0936-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="f0936-192">Si vous souhaitez remplacer les requêtes toomake à partir d’ordinateurs virtuels en dehors de hello (qui est l’objectif de hello de ce guide), vous devez également tooenable mise en réseau pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="f0936-193">Sur les deux ordinateurs virtuels, ouvrez `/etc/mysql/my.cnf` et accédez trop`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="f0936-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="f0936-194">Modifier l’adresse de hello provenant de 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="f0936-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="f0936-195">Après avoir enregistré le fichier de hello, émettre une `sudo service mysql restart` sur votre serveur principal actuel.</span><span class="sxs-lookup"><span data-stu-id="f0936-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="f0936-196">Créer le jeu d’équilibrage de charge MySQL hello</span><span class="sxs-lookup"><span data-stu-id="f0936-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="f0936-197">Revenir en arrière toohello portail, accédez trop`hadb01`, puis choisissez **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="f0936-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="f0936-198">toocreate un point de terminaison, choisissez MySQL (le port TCP 3306) à partir de la liste déroulante de hello et sélectionnez **créer nouveau jeu d’équilibrage**.</span><span class="sxs-lookup"><span data-stu-id="f0936-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="f0936-199">Point de terminaison nom hello équilibrés en charge `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="f0936-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="f0936-200">Définissez **temps** too5 secondes minimum.</span><span class="sxs-lookup"><span data-stu-id="f0936-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="f0936-201">Après avoir créé le point de terminaison hello, accédez trop`hadb02`, choisissez **points de terminaison**et créer un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f0936-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="f0936-202">Choisissez `lb-mysql`, puis sélectionnez MySQL à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="f0936-203">Vous pouvez également utiliser hello CLI d’Azure pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="f0936-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="f0936-204">Vous avez maintenant tout ce dont vous avez besoin pour une opération manuelle du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="f0936-205">Test d’un jeu d’équilibrage de la charge hello</span><span class="sxs-lookup"><span data-stu-id="f0936-205">Test hello load-balanced set</span></span>
<span data-ttu-id="f0936-206">Il est possible d’exécuter des tests à partir d’une machine externe à l’aide d’un client MySQL, ou à l’aide de certaines applications, telles que phpMyAdmin exécutée en tant que site web Azure.</span><span class="sxs-lookup"><span data-stu-id="f0936-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="f0936-207">Dans ce cas, vous avez utilisé l’outil de ligne de commande de MySQL sur une autre boîte Linux :</span><span class="sxs-lookup"><span data-stu-id="f0936-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="f0936-208">Basculement manuel</span><span class="sxs-lookup"><span data-stu-id="f0936-208">Manually failing over</span></span>
<span data-ttu-id="f0936-209">Vous pouvez simuler des basculements en arrêtant MySQL, en commutant la machine virtuelle principale de DRBD et en redémarrant MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0936-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="f0936-210">tooperform cette tâche, exécutez hello suivant de code de hadb01 :</span><span class="sxs-lookup"><span data-stu-id="f0936-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="f0936-211">Puis, sur hadb02 :</span><span class="sxs-lookup"><span data-stu-id="f0936-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="f0936-212">Après un basculement manuel, vous pouvez répéter votre requête à distance. Elle devrait fonctionner parfaitement.</span><span class="sxs-lookup"><span data-stu-id="f0936-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="f0936-213">Configurer Corosync</span><span class="sxs-lookup"><span data-stu-id="f0936-213">Set up Corosync</span></span>
<span data-ttu-id="f0936-214">Corosync est requis pour STIMULATEUR toowork l’infrastructure cluster sous-jacent hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="f0936-215">Pour les pulsations (et autres méthodes comme Ultramonkey), Corosync est un fractionnement des fonctionnalités CRM hello, tandis que STIMULATEUR reste tooHeartbeat ressemble davantage de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f0936-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="f0936-216">Hello principale contrainte pour Corosync sur Azure est que Corosync préfère multidiffusion diffusion sur les communications de monodiffusion, mais mise en réseau de Microsoft Azure prend uniquement en charge la monodiffusion.</span><span class="sxs-lookup"><span data-stu-id="f0936-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="f0936-217">Heureusement, Corosync dispose d’un mode de monodiffusion fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="f0936-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="f0936-218">Hello seule véritable contrainte est comme tous les nœuds ne sont pas communiquer entre eux, vous devez les nœuds de hello toodefine dans vos fichiers de configuration, y compris leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="f0936-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="f0936-219">Nous pouvons utiliser des fichiers d’exemple hello Corosync pour la monodiffusion et la modification de lier l’adresse, les listes de nœud et les répertoires de journalisation (Ubuntu utilise `/var/log/corosync` tandis que hello exemple fichiers utilisent `/var/log/cluster`) et activer les outils de quorum.</span><span class="sxs-lookup"><span data-stu-id="f0936-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="f0936-220">Utilisez hello suit `transport: udpu` directive et hello définies manuellement les adresses IP pour les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="f0936-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="f0936-221">Exécution hello code sur Suivant `/etc/corosync/corosync.conf` pour les deux nœuds :</span><span class="sxs-lookup"><span data-stu-id="f0936-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="f0936-222">Copiez ce fichier de configuration sur les deux machines virtuelles et démarrez Corosync dans les deux nœuds :</span><span class="sxs-lookup"><span data-stu-id="f0936-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="f0936-223">Peu après le démarrage du service de hello, cluster de hello doit être établie dans l’anneau d’actuel hello et quorum doit être constitué.</span><span class="sxs-lookup"><span data-stu-id="f0936-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="f0936-224">Nous pouvons vérifier cette fonctionnalité en consultant des journaux ou en hello suivant le code en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="f0936-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="f0936-225">Vous verrez toohello similaire de sortie suivant image :</span><span class="sxs-lookup"><span data-stu-id="f0936-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="f0936-227">Configurer Pacemaker</span><span class="sxs-lookup"><span data-stu-id="f0936-227">Set up Pacemaker</span></span>
<span data-ttu-id="f0936-228">STIMULATEUR utilise hello toomonitor de cluster pour les ressources, définir quand les couleurs primaires sont défaillants et passer ces toosecondaries de ressources.</span><span class="sxs-lookup"><span data-stu-id="f0936-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="f0936-229">Les ressources peuvent notamment être définies à partir d'un ensemble de scripts disponibles ou à partir de script LSB (de type init).</span><span class="sxs-lookup"><span data-stu-id="f0936-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="f0936-230">Nous souhaitons STIMULATEUR ressource DRBD hello trop « propre », point de montage hello et le service de MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="f0936-231">Si STIMULATEUR peut activer et désactiver DRBD, monter et démonter et puis démarrer ou arrêter MySQL Bonjour bon de commande lorsque quelque chose se produit avec hello principal, le programme d’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="f0936-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="f0936-232">Lors de la première installation de Pacemaker, votre configuration doit être simple. Exemple :</span><span class="sxs-lookup"><span data-stu-id="f0936-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="f0936-233">Vérifier la configuration de hello en exécutant `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="f0936-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="f0936-234">Puis créez un fichier (comme `/tmp/cluster.conf`) avec hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="f0936-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

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

3. <span data-ttu-id="f0936-235">Charger le fichier hello dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="f0936-236">Vous ne devez toodo cela dans un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="f0936-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="f0936-237">Vérifiez que Pacemaker se lance au démarrage dans les deux nœuds :</span><span class="sxs-lookup"><span data-stu-id="f0936-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="f0936-238">À l’aide de `sudo crm_mon –L`, vérifiez qu’un de vos nœuds est devenue master hello pour le cluster de hello et toutes les ressources hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f0936-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="f0936-239">Vous pouvez utiliser toocheck de montage et ps des ressources de hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f0936-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="f0936-240">Hello ci-dessous capture d’écran illustre `crm_mon` avec un seul nœud est arrêté (sortie en sélectionnant Ctrl + C) :</span><span class="sxs-lookup"><span data-stu-id="f0936-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="f0936-242">Cette capture d'écran montre les deux nœuds, avec un maître et un esclave :</span><span class="sxs-lookup"><span data-stu-id="f0936-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="f0936-244">Test</span><span class="sxs-lookup"><span data-stu-id="f0936-244">Testing</span></span>
<span data-ttu-id="f0936-245">Vous êtes prêts pour une simulation de basculement automatique.</span><span class="sxs-lookup"><span data-stu-id="f0936-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="f0936-246">Il existe deux façons toodo cela : conditionnelle et inconditionnelle.</span><span class="sxs-lookup"><span data-stu-id="f0936-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="f0936-247">fonction d’arrêt du cluster hello utilise Hello moyen souple : ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="f0936-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="f0936-248">Si vous utilisez ce paramètre sur le contrôleur de hello, esclave de hello adopte.</span><span class="sxs-lookup"><span data-stu-id="f0936-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="f0936-249">N’oubliez pas de tooset cette toooff précédent.</span><span class="sxs-lookup"><span data-stu-id="f0936-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="f0936-250">Dans le cas contraire, crm_mon affichera un nœud en veille.</span><span class="sxs-lookup"><span data-stu-id="f0936-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="f0936-251">Hello dépens est en cours d’arrêt vers le bas hello ordinateur virtuel principal (hadb01) via le portail de hello ou en modifiant hello le niveau d’exécution sur hello VM (autrement dit, arrêt, arrêt).</span><span class="sxs-lookup"><span data-stu-id="f0936-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="f0936-252">Ainsi, Corosync et STIMULATEUR en échangeant les cours de ce masque hello vers le bas.</span><span class="sxs-lookup"><span data-stu-id="f0936-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="f0936-253">Vous pouvez tester cela (utile pour les fenêtres de maintenance), mais vous pouvez également forcer le scénario de hello en figeant hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f0936-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="f0936-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="f0936-254">STONITH</span></span>
<span data-ttu-id="f0936-255">Il doit être possible de tooissue un arrêt de la machine virtuelle via hello CLI d’Azure à la place d’un script STONITH qui contrôle un périphérique physique.</span><span class="sxs-lookup"><span data-stu-id="f0936-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="f0936-256">Vous pouvez utiliser `/usr/lib/stonith/plugins/external/ssh` en tant que base et activer STONITH dans la configuration du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="f0936-257">CLI Azure doit être installé globalement et paramètres de publication hello et profil doit être chargée pour les utilisateurs du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="f0936-258">Exemple de code pour la ressource de hello est disponible sur [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="f0936-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="f0936-259">Modifier la configuration du cluster hello en ajoutant hello suivant trop`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="f0936-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="f0936-260">script de Hello n’effectue pas contrôles vers le haut/bas.</span><span class="sxs-lookup"><span data-stu-id="f0936-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="f0936-261">ressource SSH Hello d’origine avait 15 chèques ping, mais des temps de récupération pour une machine virtuelle Azure peuvent être plus variable.</span><span class="sxs-lookup"><span data-stu-id="f0936-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="f0936-262">Limites</span><span class="sxs-lookup"><span data-stu-id="f0936-262">Limitations</span></span>
<span data-ttu-id="f0936-263">Hello limites suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="f0936-263">hello following limitations apply:</span></span>

* <span data-ttu-id="f0936-264">Hello linbit DRBD ressource script qui gère DRBD en tant que ressource dans les utilisations STIMULATEUR `drbdadm down` lors de l’arrêt d’un nœud, même si le nœud de hello est simplement se mettre en veille.</span><span class="sxs-lookup"><span data-stu-id="f0936-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="f0936-265">Ce n’est pas idéale, car les esclave hello ne va pas synchroniser ressource DRBD de hello alors que le maître de hello Obtient des écritures.</span><span class="sxs-lookup"><span data-stu-id="f0936-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="f0936-266">Si le maître de hello n’échoue pas gracieusement, esclave de hello peut prendre sur un état de système de fichiers plus anciens.</span><span class="sxs-lookup"><span data-stu-id="f0936-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="f0936-267">Cela peut être résolu de deux façons :</span><span class="sxs-lookup"><span data-stu-id="f0936-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="f0936-268">En appliquant un `drbdadm up r0` dans tous les nœuds du cluster grâce à une surveillance locale (non groupée)</span><span class="sxs-lookup"><span data-stu-id="f0936-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="f0936-269">En modifiant le script DRBD linbit hello et en faisant en sorte que `down` n’est pas appelée`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="f0936-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="f0936-270">équilibrage de charge Hello nécessitant au moins cinq secondes toorespond, applications doivent être adaptée aux clusters et être plus tolérant vis-à-vis du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="f0936-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="f0936-271">D’autres architectures peuvent également aider, par exemple les files d’attente intégrées et les intergiciels de requête.</span><span class="sxs-lookup"><span data-stu-id="f0936-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="f0936-272">MySQL de paramétrage est tooensure nécessaire que l’écriture est effectuée à un rythme gérable et les caches sont vidé toodisk aussi souvent que possible toominimize une perte de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="f0936-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="f0936-273">Écrire des performances dépend de la machine virtuelle, car le mécanisme de hello utilisé par le périphérique de hello DRBD tooreplicate d’interconnexion dans un commutateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="f0936-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
