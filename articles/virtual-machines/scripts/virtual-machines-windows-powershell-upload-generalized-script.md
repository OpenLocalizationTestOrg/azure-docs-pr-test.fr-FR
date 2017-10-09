---
title: "aaaUpload un tooAzure de disque dur virtuel généralisé exemple de Script PowerShell | Documents Microsoft"
description: "PowerShell exemple tooupload de script un tooAzure de disque dur virtuel généralisé et créer une machine virtuelle à l’aide du modèle de déploiement du Gestionnaire de ressources hello et disques gérés."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="1feb4-103">Exemple de script tooupload un tooAzure de disque dur virtuel et créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1feb4-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="1feb4-104">Ce script accepte un fichier .vhd local à partir d’une machine virtuelle généralisée et télécharge tooAzure, crée une image de disque de géré et utilise hello toocreate une nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1feb4-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1feb4-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1feb4-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="1feb4-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="1feb4-106">Clean up deployment</span></span> 

<span data-ttu-id="1feb4-107">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="1feb4-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1feb4-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1feb4-108">Script explanation</span></span>

<span data-ttu-id="1feb4-109">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1feb4-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1feb4-110">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="1feb4-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1feb4-111">Commande</span><span class="sxs-lookup"><span data-stu-id="1feb4-111">Command</span></span>                                                                                                             | <span data-ttu-id="1feb4-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="1feb4-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="1feb4-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1feb4-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="1feb4-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1feb4-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="1feb4-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="1feb4-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="1feb4-116">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1feb4-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="1feb4-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="1feb4-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="1feb4-118">Télécharge un disque dur virtuel à partir d’un objet blob à la tooa de la machine virtuelle locale dans un compte de stockage cloud dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1feb4-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="1feb4-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="1feb4-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="1feb4-120">Crée un objet image configurable.</span><span class="sxs-lookup"><span data-stu-id="1feb4-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="1feb4-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="1feb4-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="1feb4-122">Définit des propriétés de disque de système d’exploitation de hello sur un objet image.</span><span class="sxs-lookup"><span data-stu-id="1feb4-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="1feb4-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="1feb4-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="1feb4-124">Crée une image.</span><span class="sxs-lookup"><span data-stu-id="1feb4-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="1feb4-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1feb4-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1feb4-126">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="1feb4-126">Creates a subnet configuration.</span></span> <span data-ttu-id="1feb4-127">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="1feb4-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="1feb4-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1feb4-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="1feb4-129">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1feb4-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="1feb4-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="1feb4-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="1feb4-131">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="1feb4-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="1feb4-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1feb4-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="1feb4-133">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="1feb4-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="1feb4-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1feb4-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="1feb4-135">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1feb4-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="1feb4-136">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1feb4-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="1feb4-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="1feb4-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="1feb4-138">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1feb4-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="1feb4-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1feb4-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="1feb4-140">Obtient un réseau virtuel dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1feb4-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="1feb4-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="1feb4-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="1feb4-142">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1feb4-142">Creates a VM configuration.</span></span> <span data-ttu-id="1feb4-143">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="1feb4-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="1feb4-144">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1feb4-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="1feb4-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="1feb4-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="1feb4-146">Spécifie une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1feb4-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="1feb4-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="1feb4-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="1feb4-148">Définit des propriétés d’un disque de système d’exploitation de hello sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1feb4-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="1feb4-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="1feb4-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="1feb4-150">Définit des propriétés d’un disque de système d’exploitation de hello sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1feb4-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="1feb4-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1feb4-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="1feb4-152">Ajoute un ordinateur virtuel de réseau interface tooa.</span><span class="sxs-lookup"><span data-stu-id="1feb4-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="1feb4-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="1feb4-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="1feb4-154">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1feb4-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="1feb4-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1feb4-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="1feb4-156">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="1feb4-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="1feb4-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1feb4-157">Next steps</span></span>

<span data-ttu-id="1feb4-158">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1feb4-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1feb4-159">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1feb4-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
