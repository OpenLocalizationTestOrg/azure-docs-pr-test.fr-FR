---
title: "Créer une machine virtuelle avec une adresse IP publique statique - Azure PowerShell | Microsoft Docs"
description: "Découvrez comment créer une machine virtuelle avec une adresse IP publique statique à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e4c413d3cb5c242a16f3e534dafe322785a35141
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="f4ed3-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ed3-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4ed3-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4ed3-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f4ed3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ed3-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f4ed3-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f4ed3-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f4ed3-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="f4ed3-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f4ed3-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f4ed3-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f4ed3-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f4ed3-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4ed3-110">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="f4ed3-111">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="f4ed3-111">Step 1 - Start your script</span></span>
<span data-ttu-id="f4ed3-112">Vous pouvez télécharger le script PowerShell complet utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="f4ed3-112">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="f4ed3-113">Suivez les étapes ci-dessous pour modifier le script afin qu’il fonctionne dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-113">Follow the steps below to change the script to work in your environment.</span></span>

<span data-ttu-id="f4ed3-114">Remplacez les valeurs des variables suivantes par celles que vous souhaitez utiliser pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-114">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="f4ed3-115">Les valeurs suivantes mappent au scénario utilisé dans cet article :</span><span class="sxs-lookup"><span data-stu-id="f4ed3-115">The following values map to the scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="f4ed3-116">Étape 2 : créer les ressources nécessaires pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f4ed3-116">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="f4ed3-117">Avant de créer une machine virtuelle, vous devez mettre à sa disposition un groupe de ressources, un réseau virtuel, une adresse IP publique et une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="f4ed3-118">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="f4ed3-119">Créez le réseau virtuel et le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-119">Create the VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="f4ed3-120">Créez la ressource IP publique.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-120">Create the public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="f4ed3-121">Créez la carte réseau pour la machine virtuelle dans le sous-réseau créé ci-dessus, avec l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-121">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="f4ed3-122">Notez que la première applet de commande récupère le réseau virtuel d’Azure. Cette opération est nécessaire dans la mesure où l’applet de commande `Set-AzureRmVirtualNetwork` a été exécutée pour modifier le réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-122">Notice the first cmdlet retrieving the VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed to change the existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="f4ed3-123">Créez un compte de stockage pour héberger le lecteur du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-123">Create a storage account to host the VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="f4ed3-124">Étape 3 : créer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f4ed3-124">Step 3 - Create the VM</span></span>
<span data-ttu-id="f4ed3-125">Une fois toutes les ressources nécessaires en place, vous pouvez créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="f4ed3-126">Créez l’objet de configuration pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-126">Create the configuration object for the VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="f4ed3-127">Obtenez les informations d’identification du compte d’administrateur local de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-127">Get credentials for the VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

3. <span data-ttu-id="f4ed3-128">Créez un objet de configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="f4ed3-129">Définissez l’image du système d’exploitation pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-129">Set the operating system image for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="f4ed3-130">Configurez le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-130">Configure the OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="f4ed3-131">Ajoutez la carte réseau à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-131">Add the NIC to the VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="f4ed3-132">Créez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-132">Create the VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="f4ed3-133">Enregistrez le fichier de script.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-133">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="f4ed3-134">Étape 4 : exécution du script</span><span class="sxs-lookup"><span data-stu-id="f4ed3-134">Step 4 - Run the script</span></span>
<span data-ttu-id="f4ed3-135">Une fois que vous avez effectué les modifications nécessaires et compris le script ci-dessus, exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-135">After making any necessary changes, and understanding the script show above, run the script.</span></span> 

1. <span data-ttu-id="f4ed3-136">À partir d’une console PowerShell ou de PowerShell ISE, exécutez le script ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f4ed3-136">From a PowerShell console, or PowerShell ISE, run the script above.</span></span>
2. <span data-ttu-id="f4ed3-137">La sortie suivante doit s’afficher après quelques minutes :</span><span class="sxs-lookup"><span data-stu-id="f4ed3-137">The following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

