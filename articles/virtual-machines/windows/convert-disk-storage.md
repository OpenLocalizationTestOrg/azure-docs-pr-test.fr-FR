---
title: "le stockage de disques géré d’aaaConvert Azure à partir de toopremium standard et vice versa | Documents Microsoft"
description: "Comment tooconvert Azure des disques gérés à partir de toopremium standard et vice versa, à l’aide d’Azure PowerShell."
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
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Convertir Azure le stockage des disques géré à partir de toopremium standard et vice versa

Managed Disks propose deux options de stockage : [Premium](../../storage/storage-premium-storage.md) (SSD) et [Standard](../../storage/storage-standard-storage.md) (HDD). Il vous permet de basculer tooeasily d’options hello deux avec un temps mort minimal selon vos besoins de performances. Cette fonctionnalité n’est pas disponible pour les disques non gérés. Toutefois, vous pouvez facilement [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) commutateur tooeasily entre les options hello deux.

Cet article explique comment tooconvert des disques gérés par à partir de toopremium standard et vice versa à l’aide d’Azure PowerShell. Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Avant de commencer

* conversion de Hello nécessite un redémarrage de machine virtuelle de hello, par conséquent, planifier la migration de votre stockage de disques hello pendant une fenêtre de maintenance existant. 
* Si vous utilisez des disques non managés, tout d’abord [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch de cet article entre les options de stockage hello deux. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Convertir toutes les hello gérés disques d’une machine virtuelle à partir de toopremium standard et vice versa

Bonjour l’exemple suivant, nous montrons comment tooswitch tous hello disques d’une machine virtuelle à partir du stockage de toopremium standard. des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium. Cet exemple bascule également taille tooa qui prend en charge le stockage premium.

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Convertir un disque géré à partir de toopremium standard et vice versa

Pour votre charge de travail de développement et de test, vous voudrez mélange toohave de disques standard et premium tooreduce votre coût. Vous pouvez l’effectuer en mettant à niveau toopremium stockage, seuls les disques hello qui nécessitent de meilleures performances. Bonjour l’exemple suivant, nous montrons comment tooswitch un seul disque d’un ordinateur virtuel à partir du stockage de toopremium standard et vice versa. des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium. Cet exemple bascule également taille tooa qui prend en charge le stockage premium.

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a>Étapes suivantes

Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).

