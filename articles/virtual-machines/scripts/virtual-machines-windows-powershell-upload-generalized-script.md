---
title: "Exemple de script PowerShell - Chargement d’un disque dur virtuel généralisé sur Azure | Microsoft Docs"
description: "Exemple de script PowerShell pour charger un disque dur virtuel généralisé sur Azure et créer une machine virtuelle à l’aide du modèle de déploiement Resource Manager et de Managed Disks."
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="f2150-103">Exemple de script pour charger un disque dur virtuel spécialisé sur Azure et créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f2150-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="f2150-104">Ce script utilise un fichier .vhd local d’une machine virtuelle généralisée et le charge sur Azure, crée une image de disque géré et l’utilise pour créer une nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f2150-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f2150-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="f2150-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f2150-106">Clean up deployment</span></span> 

<span data-ttu-id="f2150-107">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="f2150-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f2150-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f2150-108">Script explanation</span></span>

<span data-ttu-id="f2150-109">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f2150-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="f2150-110">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f2150-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f2150-111">Commande</span><span class="sxs-lookup"><span data-stu-id="f2150-111">Command</span></span>                                                                                                             | <span data-ttu-id="f2150-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="f2150-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="f2150-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f2150-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="f2150-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f2150-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="f2150-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="f2150-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="f2150-116">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f2150-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="f2150-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="f2150-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="f2150-118">Charge un disque dur virtuel à partir d’une machine virtuelle locale sur un objet blob dans un compte de stockage cloud dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2150-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="f2150-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="f2150-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="f2150-120">Crée un objet image configurable.</span><span class="sxs-lookup"><span data-stu-id="f2150-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="f2150-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="f2150-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="f2150-122">Définit les propriétés du disque du système d’exploitation sur un objet image.</span><span class="sxs-lookup"><span data-stu-id="f2150-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="f2150-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="f2150-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="f2150-124">Crée une image.</span><span class="sxs-lookup"><span data-stu-id="f2150-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="f2150-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f2150-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f2150-126">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f2150-126">Creates a subnet configuration.</span></span> <span data-ttu-id="f2150-127">Cette configuration est utilisée avec le processus de création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f2150-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="f2150-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f2150-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="f2150-129">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f2150-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="f2150-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f2150-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="f2150-131">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f2150-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="f2150-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f2150-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="f2150-133">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="f2150-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="f2150-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f2150-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="f2150-135">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f2150-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="f2150-136">Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f2150-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="f2150-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="f2150-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="f2150-138">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f2150-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="f2150-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f2150-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="f2150-140">Obtient un réseau virtuel dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f2150-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="f2150-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="f2150-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="f2150-142">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-142">Creates a VM configuration.</span></span> <span data-ttu-id="f2150-143">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="f2150-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f2150-144">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f2150-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f2150-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="f2150-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="f2150-146">Spécifie une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="f2150-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="f2150-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="f2150-148">Définit les propriétés du disque du système d’exploitation sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="f2150-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="f2150-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="f2150-150">Définit les propriétés du disque du système d’exploitation sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="f2150-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f2150-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="f2150-152">Ajoute une interface réseau à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2150-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="f2150-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f2150-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="f2150-154">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f2150-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="f2150-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f2150-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="f2150-156">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="f2150-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="f2150-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2150-157">Next steps</span></span>

<span data-ttu-id="f2150-158">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f2150-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f2150-159">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2150-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
