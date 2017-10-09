---
title: aaaCreate une machine virtuelle avec une adresse IP publique statique - Azure PowerShell | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle avec une adresse IP publique statique d’adresses à l’aide de PowerShell."
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
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="4922b-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4922b-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4922b-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4922b-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="4922b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4922b-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="4922b-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4922b-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="4922b-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="4922b-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="4922b-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="4922b-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="4922b-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4922b-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4922b-110">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="4922b-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="4922b-111">Étape 1 : démarrer votre script</span><span class="sxs-lookup"><span data-stu-id="4922b-111">Step 1 - Start your script</span></span>
<span data-ttu-id="4922b-112">Vous pouvez télécharger le script PowerShell complet hello utilisé [ici](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="4922b-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="4922b-113">Suivez les étapes de hello ci-dessous toochange hello script toowork dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4922b-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="4922b-114">Modifier les valeurs hello de variables hello ci-dessous en fonction des valeurs de hello souhaité toouse pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="4922b-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="4922b-115">Hello valeurs carte toohello scénario utilisé dans cet article :</span><span class="sxs-lookup"><span data-stu-id="4922b-115">hello following values map toohello scenario used in this article:</span></span>

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

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="4922b-116">Étape 2 : créer des ressources nécessaires hello pour votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4922b-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="4922b-117">Avant de créer une machine virtuelle, vous avez besoin d’un groupe de ressources, réseau virtuel, publique IP et réseau toobe utilisé par hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="4922b-118">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4922b-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="4922b-119">Créer hello réseau virtuel et le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4922b-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="4922b-120">Créer la ressource IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="4922b-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="4922b-121">Créez l’interface de réseau de hello (NIC) pour hello machine virtuelle dans un sous-réseau hello créé ci-dessus, avec l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="4922b-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="4922b-122">Notez hello première applet de commande récupérant hello réseau virtuel Azure, cela est nécessaire, car un `Set-AzureRmVirtualNetwork` a été exécutée toochange hello réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="4922b-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="4922b-123">Créer un hello de toohost de compte de stockage lecteur du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="4922b-124">Étape 3 : création de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4922b-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="4922b-125">Une fois toutes les ressources nécessaires en place, vous pouvez créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="4922b-126">Créer un objet de configuration de hello pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="4922b-127">Obtenir des informations d’identification pour hello compte administrateur local d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="4922b-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="4922b-128">Créez un objet de configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="4922b-129">Définir l’image de système d’exploitation hello pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="4922b-130">Configurer le disque de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="4922b-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="4922b-131">Ajoutez hello toohello de carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="4922b-132">Créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4922b-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="4922b-133">Enregistrez le fichier de script hello.</span><span class="sxs-lookup"><span data-stu-id="4922b-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="4922b-134">Étape 4 : exécution hello script</span><span class="sxs-lookup"><span data-stu-id="4922b-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="4922b-135">Une fois vos modifications et que vous comprenez le script de hello afficher au-dessus, exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="4922b-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="4922b-136">À partir d’une console PowerShell ou PowerShell ISE, exécutez le script hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4922b-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="4922b-137">Hello suivant la sortie doit s’afficher après quelques minutes :</span><span class="sxs-lookup"><span data-stu-id="4922b-137">hello following output should be displayed after a few minutes:</span></span>
   
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

