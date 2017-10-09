---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec plusieurs cartes réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="09f01-103">Créer une machine virtuelle avec plusieurs cartes réseau à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="09f01-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09f01-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09f01-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="09f01-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="09f01-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="09f01-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="09f01-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="09f01-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="09f01-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="09f01-108">Interface de ligne de commande Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="09f01-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="09f01-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="09f01-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="09f01-110">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09f01-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="09f01-111">étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="09f01-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09f01-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09f01-112">Prerequisites</span></span>
<span data-ttu-id="09f01-113">Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="09f01-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="09f01-114">fin de ces ressources, toocreate hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="09f01-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="09f01-115">Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="09f01-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="09f01-116">Dans la page de modèle hello, toohello à droite de **groupe de ressources Parent**, cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="09f01-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="09f01-117">Si nécessaire, modifiez les valeurs de paramètre hello, puis suivez les étapes de hello hello Azure en version préliminaire toodeploy portail hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="09f01-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09f01-118">Assurez-vous que vos noms de compte de stockage sont uniques.</span><span class="sxs-lookup"><span data-stu-id="09f01-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="09f01-119">Vous ne pouvez pas avoir des noms de compte de stockage en double dans Azure.</span><span class="sxs-lookup"><span data-stu-id="09f01-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="09f01-120">Créer des machines virtuelles de back-end hello</span><span class="sxs-lookup"><span data-stu-id="09f01-120">Create hello back-end VMs</span></span>
<span data-ttu-id="09f01-121">Hello machines virtuelles du serveur principal dépendent de la création de hello Hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="09f01-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="09f01-122">**Compte de stockage pour les disques de données**.</span><span class="sxs-lookup"><span data-stu-id="09f01-122">**Storage account for data disks**.</span></span> <span data-ttu-id="09f01-123">Pour de meilleures performances, les disques de données hello sur les serveurs de base de données hello utilisera (SSD) de lecteur SSD, ce qui nécessite un compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="09f01-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="09f01-124">Vérifiez que hello emplacement Azure que vous déployez le stockage de premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="09f01-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="09f01-125">**Cartes réseau**.</span><span class="sxs-lookup"><span data-stu-id="09f01-125">**NICs**.</span></span> <span data-ttu-id="09f01-126">Chaque machine virtuelle a deux cartes réseau, une pour l’accès à la base de données et l’autre pour la gestion.</span><span class="sxs-lookup"><span data-stu-id="09f01-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="09f01-127">**Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="09f01-127">**Availability set**.</span></span> <span data-ttu-id="09f01-128">Tous les serveurs de base de données seront ajoutés à haute disponibilité unique tooa, tooensure au moins une des machines virtuelles de hello est en cours d’exécution lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="09f01-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="09f01-129">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="09f01-129">Step 1 - Start your script</span></span>
<span data-ttu-id="09f01-130">Vous pouvez télécharger le script PowerShell complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="09f01-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="09f01-131">Suivez les étapes de hello ci-dessous toochange hello script toowork dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="09f01-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="09f01-132">Modifier les valeurs hello de variables hello ci-dessous en fonction de votre groupe de ressources existant déployé ci-dessus dans [conditions préalables](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="09f01-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="09f01-133">Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="09f01-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="09f01-134">Récupérer les ressources existantes hello requis pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="09f01-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="09f01-135">Étape 2 : création des ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="09f01-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="09f01-136">Vous devez toocreate un nouveau groupe de ressources, un compte de stockage pour les disques de données hello, et un ensemble de disponibilité pour tous les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="09f01-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="09f01-137">Vous inhabituels besoin des informations d’identification du compte hello administrateur local pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09f01-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="09f01-138">l’exécution de ces ressources, toocreate hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="09f01-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="09f01-139">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="09f01-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="09f01-140">Dans le groupe de ressources hello créé ci-dessus, créez un nouveau compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="09f01-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="09f01-141">Créez un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="09f01-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="09f01-142">Obtenir les administrateur local hello toobe d’informations d’identification de compte utilisé pour chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="09f01-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="09f01-143">Étape 3 : création de hello NIC et les machines virtuelles de serveur principal</span><span class="sxs-lookup"><span data-stu-id="09f01-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="09f01-144">Vous devez toouse une toocreate boucle comme de nombreux ordinateurs virtuels que vous souhaitez et créez hello nécessaires des cartes réseau et des machines virtuelles au sein de la boucle de hello.</span><span class="sxs-lookup"><span data-stu-id="09f01-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="09f01-145">toocreate hello cartes réseau et les ordinateurs virtuels, exécutez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="09f01-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="09f01-146">Démarrer un `for` hello toorepeat de boucle commandes toocreate une machine virtuelle et deux cartes réseau comme autant de fois que nécessaire, en fonction de la valeur hello hello `$numberOfVMs` variable.</span><span class="sxs-lookup"><span data-stu-id="09f01-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="09f01-147">Créer hello que carte réseau utilisée pour l’accès de la base de données.</span><span class="sxs-lookup"><span data-stu-id="09f01-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="09f01-148">Créer hello que carte réseau utilisée pour l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="09f01-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="09f01-149">Notez comment cette carte réseau a une tooit de groupe de sécurité réseau associé.</span><span class="sxs-lookup"><span data-stu-id="09f01-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="09f01-150">Créez l'objet `vmConfig` .</span><span class="sxs-lookup"><span data-stu-id="09f01-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="09f01-151">Créez deux disques de données pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09f01-151">Create two data disks per VM.</span></span> <span data-ttu-id="09f01-152">Notez que les disques de données hello sont dans le compte de stockage premium hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="09f01-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="09f01-153">Configurer le système d’exploitation de hello et toobe image utilisé pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09f01-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="09f01-154">Ajouter des cartes réseau de hello deux créé ci-dessus toohello `vmConfig` objet.</span><span class="sxs-lookup"><span data-stu-id="09f01-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="09f01-155">Créez le disque du système d’exploitation hello et hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09f01-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="09f01-156">Hello d’avis `}` fin hello `for` boucle.</span><span class="sxs-lookup"><span data-stu-id="09f01-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="09f01-157">Étape 4 : exécution hello script</span><span class="sxs-lookup"><span data-stu-id="09f01-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="09f01-158">Maintenant que vous avez téléchargé et modifié le script de hello selon vos besoins, exécutez il script de base de données principale toocreate hello machines virtuelles avec plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="09f01-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="09f01-159">Enregistrez votre script et exécutez-le à partir de hello **PowerShell** invite de commandes, ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="09f01-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="09f01-160">Vous verrez un résultat initial de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="09f01-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="09f01-161">Après quelques minutes, remplir invite des informations d’identification hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="09f01-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="09f01-162">sortie Hello ci-dessous représente une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09f01-162">hello output below represents a single VM.</span></span> <span data-ttu-id="09f01-163">Avis hello tout processus a duré toocomplete de 8 minutes.</span><span class="sxs-lookup"><span data-stu-id="09f01-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
