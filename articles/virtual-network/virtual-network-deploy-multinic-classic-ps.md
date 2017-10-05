---
title: "Créer une machine virtuelle (Classic) avec plusieurs cartes réseau - Azure PowerShell | Microsoft Docs"
description: "Apprenez à créer une machine virtuelle (Classic) avec plusieurs cartes réseau à l’aide de PowerShell."
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
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="54e54-103">Créer une machine virtuelle (classique) avec plusieurs cartes réseau à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="54e54-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="54e54-104">Vous pouvez créer des machines virtuelles (VM) dans Azure et joindre plusieurs cartes d’interface réseau (NIC) à chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="54e54-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="54e54-105">Plusieurs cartes réseau permettent la séparation des types de trafic entre les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="54e54-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="54e54-106">Par exemple, une carte réseau peut communiquer avec Internet, tandis qu’une autre communique uniquement avec des ressources internes non connectées à Internet.</span><span class="sxs-lookup"><span data-stu-id="54e54-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="54e54-107">La possibilité de séparer le trafic réseau entre plusieurs cartes réseau est requise pour de nombreuses appliances virtuelles réseau, telles que Application Delivery Network et les solutions d’optimisation WAN.</span><span class="sxs-lookup"><span data-stu-id="54e54-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54e54-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="54e54-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="54e54-109">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="54e54-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="54e54-110">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54e54-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="54e54-111">Découvrez comment effectuer ces étapes à l’aide du [modèle de déploiement Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="54e54-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="54e54-112">Les étapes suivantes utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs web et un groupe de ressources nommé *IaaSStory-BackEnd* pour les serveurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="54e54-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54e54-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54e54-113">Prerequisites</span></span>

<span data-ttu-id="54e54-114">Avant de créer les serveurs de base de données, vous devez créer le groupe de ressources *IaaSStory* avec toutes les ressources nécessaires pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="54e54-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="54e54-115">Pour créer ces ressources, exécutez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="54e54-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="54e54-116">Pour créer un réseau virtuel, suivez les étapes de l’article [Créer un réseau virtuel](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="54e54-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="54e54-117">Créer les machines virtuelles principales</span><span class="sxs-lookup"><span data-stu-id="54e54-117">Create the back-end VMs</span></span>
<span data-ttu-id="54e54-118">Les machines virtuelles principales dépendent de la création des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="54e54-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="54e54-119">**Sous-réseau principal**.</span><span class="sxs-lookup"><span data-stu-id="54e54-119">**Backend subnet**.</span></span> <span data-ttu-id="54e54-120">Les serveurs de base de données font partie d'un sous-réseau distinct, pour répartir le trafic.</span><span class="sxs-lookup"><span data-stu-id="54e54-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="54e54-121">Le script ci-dessous s'attend à ce que le sous-réseau se trouve dans un réseau virtuel nommé *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="54e54-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="54e54-122">**Compte de stockage pour les disques de données**.</span><span class="sxs-lookup"><span data-stu-id="54e54-122">**Storage account for data disks**.</span></span> <span data-ttu-id="54e54-123">Pour optimiser les performances, les disques de données sur les serveurs de base de données utilisent la technologie de disque SSD, qui requiert un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="54e54-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="54e54-124">Assurez-vous que l'emplacement Azure de déploiement prend en charge le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="54e54-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="54e54-125">**Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="54e54-125">**Availability set**.</span></span> <span data-ttu-id="54e54-126">Tous les serveurs de base de données sont ajoutés à un groupe à haute disponibilité, afin de garantir qu’au moins une des machines virtuelles est en cours d’exécution lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="54e54-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="54e54-127">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="54e54-127">Step 1 - Start your script</span></span>
<span data-ttu-id="54e54-128">Vous pouvez télécharger le script PowerShell complet utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="54e54-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="54e54-129">Suivez les étapes ci-dessous pour modifier le script afin qu’il fonctionne dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="54e54-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="54e54-130">Modifiez les valeurs des variables suivantes selon votre groupe de ressources existant déployé ci-dessus dans les [Conditions préalables](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="54e54-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="54e54-131">Modifiez les valeurs des variables suivantes en fonction des valeurs que vous souhaitez utiliser pour le déploiement de votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="54e54-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="54e54-132">Étape 2 : création des ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="54e54-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="54e54-133">Vous devez créer un service cloud et un compte de stockage pour les disques de données pour toutes les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="54e54-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="54e54-134">Vous devez également spécifier une image et un compte d'administrateur local pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="54e54-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="54e54-135">Pour créer ces ressources, exécutez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="54e54-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="54e54-136">Créez un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="54e54-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="54e54-137">Créez un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="54e54-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="54e54-138">Définissez le compte de stockage créé ci-dessus en tant que compte de stockage actif pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="54e54-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="54e54-139">Sélectionnez une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="54e54-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="54e54-140">Définissez les informations d’identification de compte d’administrateur local.</span><span class="sxs-lookup"><span data-stu-id="54e54-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="54e54-141">Étape 3 : création de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="54e54-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="54e54-142">Vous devez utiliser une boucle pour créer le nombre de machines virtuelles que vous voulez et créer les cartes réseau et les machines virtuelles nécessaires au sein de la boucle.</span><span class="sxs-lookup"><span data-stu-id="54e54-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="54e54-143">Pour créer ces cartes réseau et ces machines virtuelles, exécutez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="54e54-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="54e54-144">Lancez une boucle `for` pour répéter les commandes afin de créer une machine virtuelle et deux cartes réseau, autant de fois que nécessaire, selon la valeur de la variable `$numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="54e54-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="54e54-145">Créez un objet `VMConfig` spécifiant l'image, la taille et la haute disponibilité de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="54e54-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="54e54-146">Configurez la machine virtuelle en tant que machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="54e54-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="54e54-147">Définissez la carte réseau par défaut et attribuez-lui une adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="54e54-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="54e54-148">Ajoutez une deuxième carte réseau pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="54e54-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="54e54-149">Pour chaque machine virtuelle, créez deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="54e54-149">Create to data disks for each VM.</span></span>

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

7. <span data-ttu-id="54e54-150">Créez toutes les machines virtuelles et mettez fin à la boucle.</span><span class="sxs-lookup"><span data-stu-id="54e54-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="54e54-151">Étape 4 : exécution du script</span><span class="sxs-lookup"><span data-stu-id="54e54-151">Step 4 - Run the script</span></span>
<span data-ttu-id="54e54-152">Maintenant que vous avez téléchargé et modifié le script selon vos besoins, exécutez le script pour créer les machines virtuelles de base de données principales avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="54e54-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="54e54-153">Enregistrez votre script et exécutez-le à partir de l’invite de commandes **PowerShell** ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="54e54-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="54e54-154">Vous verrez la sortie initiale, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="54e54-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="54e54-155">Complétez les informations nécessaires dans l'invite d'informations d'identification et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="54e54-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="54e54-156">Vous obtenez le résultat ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="54e54-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
