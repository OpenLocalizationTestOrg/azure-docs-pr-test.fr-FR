---
title: "aaaCreate une machine virtuelle (classique) avec plusieurs cartes réseau - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="bf486-103">Créer une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf486-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="bf486-104">Vous pouvez créer des machines virtuelles (VM) dans Azure et attacher plusieurs tooeach de cartes réseau de vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="bf486-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="bf486-105">Plusieurs cartes réseau permettent la séparation des types de trafic entre les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="bf486-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="bf486-106">Par exemple, une que carte réseau peut communiquer avec hello Internet, tandis que l’autre communique uniquement avec les ressources internes non connecté toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="bf486-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="bf486-107">Hello capacité tooseparate le trafic entre plusieurs cartes réseau est requis pour les nombreux équipements virtuels réseau, telles que la remise des applications et des solutions d’optimisation de réseau étendu.</span><span class="sxs-lookup"><span data-stu-id="bf486-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf486-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf486-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf486-109">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="bf486-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="bf486-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bf486-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bf486-111">Découvrez comment tooperform ces étapes à l’aide de hello [modèle de déploiement de gestionnaire de ressources](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bf486-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="bf486-112">étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="bf486-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf486-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf486-113">Prerequisites</span></span>

<span data-ttu-id="bf486-114">Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="bf486-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="bf486-115">toocreate ces ressources, complètes hello étapes qui suivent.</span><span class="sxs-lookup"><span data-stu-id="bf486-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="bf486-116">Créer un réseau virtuel en suivant les étapes de hello Bonjour [créer un réseau virtuel](virtual-networks-create-vnet-classic-netcfg-ps.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="bf486-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="bf486-117">Créer des machines virtuelles de back-end hello</span><span class="sxs-lookup"><span data-stu-id="bf486-117">Create hello back-end VMs</span></span>
<span data-ttu-id="bf486-118">Hello machines virtuelles du serveur principal dépendent de la création de hello Hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="bf486-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="bf486-119">**Sous-réseau principal**.</span><span class="sxs-lookup"><span data-stu-id="bf486-119">**Backend subnet**.</span></span> <span data-ttu-id="bf486-120">serveurs de base de données Hello feront partie d’un sous-réseau distinct, le trafic de toosegregate.</span><span class="sxs-lookup"><span data-stu-id="bf486-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="bf486-121">le script ci-dessous Hello attend ce tooexist de sous-réseau dans un réseau virtuel nommé *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="bf486-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="bf486-122">**Compte de stockage pour les disques de données**.</span><span class="sxs-lookup"><span data-stu-id="bf486-122">**Storage account for data disks**.</span></span> <span data-ttu-id="bf486-123">Pour de meilleures performances, les disques de données hello sur les serveurs de base de données hello utilisera (SSD) de lecteur SSD, ce qui nécessite un compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="bf486-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="bf486-124">Vérifiez que hello emplacement Azure que vous déployez le stockage de premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="bf486-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="bf486-125">**Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="bf486-125">**Availability set**.</span></span> <span data-ttu-id="bf486-126">Tous les serveurs de base de données seront ajoutés à haute disponibilité unique tooa, tooensure au moins une des machines virtuelles de hello est en cours d’exécution lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="bf486-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="bf486-127">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="bf486-127">Step 1 - Start your script</span></span>
<span data-ttu-id="bf486-128">Vous pouvez télécharger le script PowerShell complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="bf486-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="bf486-129">Suivez les étapes de hello ci-dessous toochange hello script toowork dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="bf486-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="bf486-130">Modifier les valeurs hello de variables hello ci-dessous en fonction de votre groupe de ressources existant déployé ci-dessus dans [conditions préalables](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="bf486-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="bf486-131">Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="bf486-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="bf486-132">Étape 2 : création des ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bf486-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="bf486-133">Vous devez toocreate compte un nouveau service cloud et un stockage pour les disques de données hello pour toutes les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bf486-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="bf486-134">Vous devez également toospecify d’une image et un compte d’administrateur local pour hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bf486-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="bf486-135">fin de ces ressources, toocreate hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf486-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="bf486-136">Créez un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="bf486-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="bf486-137">Créez un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="bf486-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="bf486-138">Compte de stockage hello jeu créé ci-dessus en tant que compte de stockage actif hello pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf486-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="bf486-139">Sélectionnez une image pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf486-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="bf486-140">Définir les informations d’identification du compte hello administrateur local.</span><span class="sxs-lookup"><span data-stu-id="bf486-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="bf486-141">Étape 3 : création de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bf486-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="bf486-142">Vous devez toouse une toocreate boucle comme de nombreux ordinateurs virtuels que vous souhaitez et créez hello nécessaires des cartes réseau et des machines virtuelles au sein de la boucle de hello.</span><span class="sxs-lookup"><span data-stu-id="bf486-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="bf486-143">toocreate hello cartes réseau et les ordinateurs virtuels, exécutez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="bf486-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="bf486-144">Démarrer un `for` hello toorepeat de boucle commandes toocreate une machine virtuelle et deux cartes réseau comme autant de fois que nécessaire, en fonction de la valeur hello hello `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="bf486-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="bf486-145">Créer un `VMConfig` objet spécifiant hello image, taille et ensemble de disponibilité pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf486-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="bf486-146">Configurer hello machine virtuelle comme une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="bf486-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="bf486-147">Définir la valeur par défaut de hello NIC et attribuez-lui une adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="bf486-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="bf486-148">Ajoutez une deuxième carte réseau pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf486-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="bf486-149">Créer des disques toodata pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bf486-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="bf486-150">Créer chaque machine virtuelle et terminer la boucle hello.</span><span class="sxs-lookup"><span data-stu-id="bf486-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="bf486-151">Étape 4 : exécution hello script</span><span class="sxs-lookup"><span data-stu-id="bf486-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="bf486-152">Maintenant que vous avez téléchargé et modifié le script de hello selon vos besoins, exécutez il script de base de données principale toocreate hello machines virtuelles avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="bf486-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="bf486-153">Enregistrez votre script et exécutez-le à partir de hello **PowerShell** invite de commandes, ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="bf486-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="bf486-154">Vous verrez un résultat initial de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bf486-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="bf486-155">Remplissez les informations hello nécessaires dans l’invite d’informations d’identification hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf486-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="bf486-156">Hello ci-dessous est retourné.</span><span class="sxs-lookup"><span data-stu-id="bf486-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
