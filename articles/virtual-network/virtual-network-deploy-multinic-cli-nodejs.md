---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="bf32d-103">Créer une machine virtuelle avec plusieurs cartes réseau à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bf32d-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bf32d-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf32d-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="bf32d-105">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf32d-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="bf32d-106">étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="bf32d-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="bf32d-107">Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 1.0 (cet article) ou hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf32d-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="bf32d-108">Hello dans les valeurs « » pour les variables hello dans les étapes de hello qui suivent créer des ressources avec les paramètres d’un scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="bf32d-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="bf32d-109">Modifier les valeurs hello, comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="bf32d-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf32d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf32d-110">Prerequisites</span></span>
<span data-ttu-id="bf32d-111">Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="bf32d-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="bf32d-112">fin de ces ressources, toocreate hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf32d-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="bf32d-113">Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="bf32d-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="bf32d-114">Dans la page de modèle hello, toohello à droite de **groupe de ressources Parent**, cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="bf32d-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="bf32d-115">Si nécessaire, modifiez les valeurs de paramètre hello, puis suivez les étapes de hello hello Azure en version préliminaire toodeploy portail hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf32d-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf32d-116">Assurez-vous que vos noms de compte de stockage sont uniques.</span><span class="sxs-lookup"><span data-stu-id="bf32d-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="bf32d-117">Vous ne pouvez pas avoir des noms de compte de stockage en double dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bf32d-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="bf32d-118">Créer des machines virtuelles de back-end hello</span><span class="sxs-lookup"><span data-stu-id="bf32d-118">Create hello back-end VMs</span></span>
<span data-ttu-id="bf32d-119">Hello machines virtuelles du serveur principal dépendent de la création de hello Hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="bf32d-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="bf32d-120">**Compte de stockage pour les disques de données**.</span><span class="sxs-lookup"><span data-stu-id="bf32d-120">**Storage account for data disks**.</span></span> <span data-ttu-id="bf32d-121">Pour de meilleures performances, les disques de données hello sur les serveurs de base de données hello utilisera (SSD) de lecteur SSD, ce qui nécessite un compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="bf32d-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="bf32d-122">Vérifiez que hello emplacement Azure que vous déployez le stockage de premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="bf32d-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="bf32d-123">**Cartes réseau**.</span><span class="sxs-lookup"><span data-stu-id="bf32d-123">**NICs**.</span></span> <span data-ttu-id="bf32d-124">Chaque machine virtuelle a deux cartes réseau, une pour l’accès à la base de données et l’autre pour la gestion.</span><span class="sxs-lookup"><span data-stu-id="bf32d-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="bf32d-125">**Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="bf32d-125">**Availability set**.</span></span> <span data-ttu-id="bf32d-126">Tous les serveurs de base de données seront ajoutés à haute disponibilité unique tooa, tooensure au moins une des machines virtuelles de hello est en cours d’exécution lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="bf32d-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="bf32d-127">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="bf32d-127">Step 1 - Start your script</span></span>
<span data-ttu-id="bf32d-128">Vous pouvez télécharger le script d’un interpréteur de commandes complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="bf32d-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="bf32d-129">Suivez les étapes de hello ci-dessous toochange hello script toowork dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="bf32d-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="bf32d-130">Modifier les valeurs hello de variables hello ci-dessous en fonction de votre groupe de ressources existant déployé ci-dessus dans [conditions préalables](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="bf32d-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="bf32d-131">Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="bf32d-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="bf32d-132">Extraire l’ID de hello pour hello `BackEnd` sous-réseau où hello machines virtuelles doivent être créé.</span><span class="sxs-lookup"><span data-stu-id="bf32d-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="bf32d-133">Vous besoin toodo étant hello NIC toobe associé toothis sous-réseau dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf32d-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="bf32d-134">Hello la première commande ci-dessus utilise [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) et [la manipulation des chaînes](http://tldp.org/LDP/abs/html/string-manipulation.html) (plus spécifiquement, la suppression de sous-chaîne).</span><span class="sxs-lookup"><span data-stu-id="bf32d-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="bf32d-135">Extraire l’ID de hello pour hello `NSG-RemoteAccess` groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bf32d-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="bf32d-136">Vous avez besoin toodo cela puisque hello toobe de cartes réseau associées toothis groupe de sécurité réseau sont dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bf32d-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="bf32d-137">Étape 2 : création des ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bf32d-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="bf32d-138">Créez un groupe de ressources pour toutes les ressources de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="bf32d-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="bf32d-139">Utilisation de hello avis de hello `$backendRGName` variable pour le nom du groupe de ressources de hello, et `$location` pour hello région Azure.</span><span class="sxs-lookup"><span data-stu-id="bf32d-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="bf32d-140">Créez un compte de stockage premium pour hello du système d’exploitation et les toobe de disques de données utilisé par les vôtres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bf32d-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="bf32d-141">Créer un groupe à haute disponibilité pour les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="bf32d-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="bf32d-142">Étape 3 : création de hello NIC et les machines virtuelles de serveur principal</span><span class="sxs-lookup"><span data-stu-id="bf32d-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="bf32d-143">Démarrer une boucle toocreate plusieurs machines virtuelles, en fonction de hello `numberOfVMs` variables.</span><span class="sxs-lookup"><span data-stu-id="bf32d-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="bf32d-144">Pour chaque machine virtuelle, créez une carte réseau pour l'accès de la base de données.</span><span class="sxs-lookup"><span data-stu-id="bf32d-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="bf32d-145">Pour chaque machine virtuelle, créez une carte réseau pour l'accès à distance.</span><span class="sxs-lookup"><span data-stu-id="bf32d-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="bf32d-146">Hello d’avis `--network-security-group` paramètre tooassociate utilisé hello NIC tooan groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bf32d-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="bf32d-147">Créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf32d-147">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="bf32d-148">Pour chaque machine virtuelle, créez des disques de deux données et terminer la boucle hello avec hello `done` commande.</span><span class="sxs-lookup"><span data-stu-id="bf32d-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="bf32d-149">Étape 4 : exécution hello script</span><span class="sxs-lookup"><span data-stu-id="bf32d-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="bf32d-150">Maintenant que vous avez téléchargé et modifié le script hello selon vos besoins, exécuter une sauvegarde hello de toocreate script hello fin des machines virtuelles de base de données avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="bf32d-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="bf32d-151">Enregistrez votre script et exécutez-le à partir de votre terminal **Bash** .</span><span class="sxs-lookup"><span data-stu-id="bf32d-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="bf32d-152">Vous verrez un résultat initial de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf32d-152">You will see hello initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="bf32d-153">Après quelques minutes, hello exécution va se terminer et vous verrez reste hello de sortie hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf32d-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

