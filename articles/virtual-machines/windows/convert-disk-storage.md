---
title: Convertir le stockage Managed Disks Azure de standard en premium, et vice versa | Microsoft Docs
description: "Comment convertir les disques gérés Azure de standard en premium, et vice versa, à l’aide de Microsoft Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 9e5c73ceb0ff7d9c18c9cf7128b69e40b9796874
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="64509-103">Convertir le stockage Managed Disks Azure de standard en premium, et vice versa</span><span class="sxs-lookup"><span data-stu-id="64509-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="64509-104">Managed Disks propose deux options de stockage : [Premium](../../storage/storage-premium-storage.md) (SSD) et [Standard](../../storage/storage-standard-storage.md) (HDD).</span><span class="sxs-lookup"><span data-stu-id="64509-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="64509-105">Il vous permet de basculer facilement entre les deux options avec une interruption minimale adaptée à vos besoins de performances.</span><span class="sxs-lookup"><span data-stu-id="64509-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="64509-106">Cette fonctionnalité n’est pas disponible pour les disques non gérés.</span><span class="sxs-lookup"><span data-stu-id="64509-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="64509-107">Toutefois, vous pouvez facilement [effectuer des conversions en disques gérés](convert-unmanaged-to-managed-disks.md) pour basculer facilement entre les deux options.</span><span class="sxs-lookup"><span data-stu-id="64509-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="64509-108">Cet article vous montre comment convertir des disques gérés de standard en premium, et vice versa, à l’aide de Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64509-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="64509-109">Si vous devez installer ou mettre à niveau ce dernier, consultez [Installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="64509-109">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="64509-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="64509-110">Before you begin</span></span>

* <span data-ttu-id="64509-111">La conversion nécessite un redémarrage de la machine virtuelle. Par conséquent, planifiez la migration de vos stockages sur disques au cours d’une fenêtre de maintenance préexistante.</span><span class="sxs-lookup"><span data-stu-id="64509-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="64509-112">Si vous utilisez des disques non gérés, tout d’abord [effectuez des conversions en disques gérés](convert-unmanaged-to-managed-disks.md) afin d’utiliser cet article pour basculer entre les deux options de stockage.</span><span class="sxs-lookup"><span data-stu-id="64509-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="64509-113">Convertir tous les disques gérés d’une machine virtuelle de standard en premium, et vice versa</span><span class="sxs-lookup"><span data-stu-id="64509-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="64509-114">Dans l’exemple suivant, nous montrons comment faire passer tous les disques d’une machine virtuelle du stockage standard au stockage premium.</span><span class="sxs-lookup"><span data-stu-id="64509-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="64509-115">Pour utiliser des disques gérés premium, votre machine virtuelle doit utiliser une [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="64509-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="64509-116">Cet exemple passe également à une taille prenant en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="64509-116">This example also switches to a size that supports premium storage.</span></span>

```powershell
# Name of the resource group that contains the VM
$rgName = 'yourResourceGroup'

# Name of the your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard to premium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate the VM before changing the size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in the resource group of the VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong to the selected VM, convert to premium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="64509-117">Convertir un disque géré de standard en premium, et vice versa</span><span class="sxs-lookup"><span data-stu-id="64509-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="64509-118">Pour votre charge de travail de développement/test, vous souhaiterez peut-être mélanger disques standard et disques premium pour réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="64509-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="64509-119">Vous pouvez le faire en effectuant une mise à niveau vers le stockage premium, uniquement pour les disques qui nécessitent de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="64509-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="64509-120">Dans l’exemple suivant, nous montrons comment faire passer un seul disque d’une machine virtuelle du stockage standard au stockage premium, et vice versa.</span><span class="sxs-lookup"><span data-stu-id="64509-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="64509-121">Pour utiliser des disques gérés premium, votre machine virtuelle doit utiliser une [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="64509-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="64509-122">Cet exemple passe également à une taille prenant en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="64509-122">This example also switches to a size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains the managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get the ARM resource to get name and resource group of the VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate the VM before changing the storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update the storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="64509-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64509-123">Next steps</span></span>

<span data-ttu-id="64509-124">Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="64509-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

