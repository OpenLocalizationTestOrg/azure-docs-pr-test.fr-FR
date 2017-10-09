---
title: "aaaCreate une machine virtuelle (classique) avec plusieurs cartes réseau - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de hello Azure interface de ligne de commande (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="bf0c9-103">Créer une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bf0c9-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="bf0c9-104">Vous pouvez créer des machines virtuelles (VM) dans Azure et attacher plusieurs tooeach de cartes réseau de vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="bf0c9-105">Plusieurs cartes réseau permettent la séparation des types de trafic entre les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="bf0c9-106">Par exemple, une que carte réseau peut communiquer avec hello Internet, tandis que l’autre communique uniquement avec les ressources internes non connecté toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="bf0c9-107">Hello capacité tooseparate le trafic entre plusieurs cartes réseau est requis pour les nombreux équipements virtuels réseau, telles que la remise des applications et des solutions d’optimisation de réseau étendu.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf0c9-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf0c9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf0c9-109">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="bf0c9-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bf0c9-111">Découvrez comment tooperform ces étapes à l’aide de hello [modèle de déploiement de gestionnaire de ressources](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf0c9-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="bf0c9-112">étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf0c9-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf0c9-113">Prerequisites</span></span>
<span data-ttu-id="bf0c9-114">Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="bf0c9-115">toocreate ces ressources, complètes hello étapes qui suivent.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="bf0c9-116">Créer un réseau virtuel en suivant les étapes de hello Bonjour [créer un réseau virtuel](virtual-networks-create-vnet-classic-cli.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="bf0c9-117">Déployer les principaux hello machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bf0c9-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="bf0c9-118">Hello machines virtuelles du serveur principal dépendent de la création de hello Hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="bf0c9-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="bf0c9-119">**Compte de stockage pour les disques de données**.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-119">**Storage account for data disks**.</span></span> <span data-ttu-id="bf0c9-120">Pour de meilleures performances, les disques de données hello sur les serveurs de base de données hello utilisera (SSD) de lecteur SSD, ce qui nécessite un compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="bf0c9-121">Vérifiez que hello emplacement Azure que vous déployez le stockage de premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="bf0c9-122">**Cartes réseau**.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-122">**NICs**.</span></span> <span data-ttu-id="bf0c9-123">Chaque machine virtuelle a deux cartes réseau, une pour l’accès à la base de données et l’autre pour la gestion.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="bf0c9-124">**Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-124">**Availability set**.</span></span> <span data-ttu-id="bf0c9-125">Tous les serveurs de base de données seront ajoutés à haute disponibilité unique tooa, tooensure au moins une des machines virtuelles de hello est en cours d’exécution lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="bf0c9-126">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="bf0c9-126">Step 1 - Start your script</span></span>
<span data-ttu-id="bf0c9-127">Vous pouvez télécharger le script d’un interpréteur de commandes complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="bf0c9-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="bf0c9-128">Hello complet suivant les étapes toochange hello script toowork dans votre environnement :</span><span class="sxs-lookup"><span data-stu-id="bf0c9-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="bf0c9-129">Modifier les valeurs hello de variables hello ci-dessous en fonction de votre groupe de ressources existant déployé ci-dessus dans [conditions préalables](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="bf0c9-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="bf0c9-130">Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="bf0c9-131">Étape 2 : création des ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bf0c9-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="bf0c9-132">Créez un service cloud pour toutes les machines virtuelles principales.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="bf0c9-133">Utilisation de hello avis de hello `$backendCSName` variable pour le nom du groupe de ressources de hello, et `$location` pour hello région Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="bf0c9-134">Créez un compte de stockage premium pour hello du système d’exploitation et les toobe de disques de données utilisé par les vôtres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="bf0c9-135">Étape 3 : création de machines virtuelles avec plusieurs cartes d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="bf0c9-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="bf0c9-136">Démarrer une boucle toocreate plusieurs machines virtuelles, en fonction de hello `numberOfVMs` variables.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="bf0c9-137">Pour chaque machine virtuelle, spécifiez le nom de hello et adresse IP de chacune des cartes réseau de hello deux.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="bf0c9-138">Créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-138">Create hello VM.</span></span> <span data-ttu-id="bf0c9-139">Notez l’utilisation de hello Hello `--nic-config` paramètre, contenant une liste de toutes les cartes réseau avec le nom de sous-réseau et adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="bf0c9-140">Pour chaque machine virtuelle, créez deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="bf0c9-141">Étape 4 : exécution hello script</span><span class="sxs-lookup"><span data-stu-id="bf0c9-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="bf0c9-142">Maintenant que vous avez téléchargé et modifié le script hello selon vos besoins, exécuter une sauvegarde hello de toocreate script hello fin des machines virtuelles de base de données avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="bf0c9-143">Enregistrez votre script et exécutez-le à partir de votre terminal **Bash** .</span><span class="sxs-lookup"><span data-stu-id="bf0c9-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="bf0c9-144">Vous verrez un résultat initial de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="bf0c9-145">Après quelques minutes, hello exécution va se terminer et vous verrez reste hello de sortie hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf0c9-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
