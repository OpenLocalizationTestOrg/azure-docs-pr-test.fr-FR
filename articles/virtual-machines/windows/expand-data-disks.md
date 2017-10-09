---
title: "aaaExpand un disque de données attaché tooa Windows VM dans Azure | Documents Microsoft"
description: "Développez la taille hello d’un disque de données est attachée tooa Windows virtual machine à l’aide de PowerShell."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="2bba7-103">Augmentez la taille d’un disque de données hello attaché tooa machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="2bba7-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="2bba7-104">Si vous avez besoin de taille de hello tooincrease de machine virtuelle de hello données disque attaché tooyour, vous pouvez augmenter la taille de hello à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bba7-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="2bba7-105">Après avoir augmenté la taille de hello hello du disque de données dans les paramètres de machine virtuelle Azure hello, vous devez également tooallocate hello nouvel espace disque dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2bba7-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="2bba7-106">Utiliser Powershell tooincrease hello taille d’un disque de données managées</span><span class="sxs-lookup"><span data-stu-id="2bba7-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="2bba7-107">taille de hello tooincrease d’un disque de données managées, hello utilisation suivant d’applets de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2bba7-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="2bba7-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="2bba7-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="2bba7-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="2bba7-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="2bba7-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2bba7-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="2bba7-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="2bba7-113">Hello script suivant vous aidera à Obtention d’informations sur les ordinateurs virtuels de hello, en sélectionnant le disque de données hello et en spécifiant la nouvelle taille de hello.</span><span class="sxs-lookup"><span data-stu-id="2bba7-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="2bba7-114">Utiliser PowerShell tooincrease hello taille d’un disque de données non managées</span><span class="sxs-lookup"><span data-stu-id="2bba7-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="2bba7-115">taille de hello tooincrease de disques de données non managées dans un compte de stockage, hello utilisation suivant d’applets de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2bba7-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="2bba7-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="2bba7-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="2bba7-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="2bba7-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="2bba7-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="2bba7-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="2bba7-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="2bba7-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2bba7-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="2bba7-122">Hello script suivant vous guide dans l’obtention des informations de compte de stockage et de la machine virtuelle hello, en sélectionnant le disque de données hello et en spécifiant la nouvelle taille de hello.</span><span class="sxs-lookup"><span data-stu-id="2bba7-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="2bba7-123">Allocation d’espace disque non alloué de hello</span><span class="sxs-lookup"><span data-stu-id="2bba7-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="2bba7-124">Une fois que vous avez effectué un lecteur de hello plus volumineux, vous devez tooallocate hello nouvel espace non alloué à partir de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2bba7-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="2bba7-125">espace de hello tooallocate, utilisation de machine virtuelle toohello gestion des disques (diskmgmt.msc) peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="2bba7-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="2bba7-126">Ou, si vous avez activé WinRM et un certificat sur la machine virtuelle de hello lors de sa création, vous pouvez utiliser le disque de hello tooinitialize PowerShell distant.</span><span class="sxs-lookup"><span data-stu-id="2bba7-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="2bba7-127">Vous pouvez également utiliser une extension de script personnalisée :</span><span class="sxs-lookup"><span data-stu-id="2bba7-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="2bba7-128">fichier de script Hello peut contenir un nom tel que ce code tooincrease hello lecteur d’allocation toohello maximale hello disques de taille :</span><span class="sxs-lookup"><span data-stu-id="2bba7-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="2bba7-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bba7-129">Next Steps</span></span>
- [<span data-ttu-id="2bba7-130">En savoir plus sur les disques et disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="2bba7-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
