---
title: "Attacher un disque de données à une machine virtuelle Windows dans Azure à l’aide de PowerShell | Microsoft Docs"
description: "Découvrez comment attacher un disque de données nouveau ou existant à une machine virtuelle Windows à l’aide de PowerShell avec le modèle de déploiement Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="5b3e3-103">Attacher un disque de données à une machine virtuelle Windows dans Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b3e3-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="5b3e3-104">Cet article vous explique comment attacher des disques nouveaux et existants à une machine virtuelle Windows à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="5b3e3-105">Si votre machine virtuelle utilise des disques gérés, vous pouvez attacher des disques de données gérés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="5b3e3-106">Vous pouvez également attacher des disques de données non gérés à une machine virtuelle qui utilise des disques non gérés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="5b3e3-107">Avant cela, passez en revue les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="5b3e3-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="5b3e3-108">La taille de la machine virtuelle détermine le nombre de disques de données que vous pouvez attacher .</span><span class="sxs-lookup"><span data-stu-id="5b3e3-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5b3e3-109">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b3e3-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5b3e3-110">Pour utiliser le stockage Premium, vous avez besoin d’une machine virtuelle de série DS ou GS, compatible avec ce type de stockage.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5b3e3-111">Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="5b3e3-112">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5b3e3-113">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b3e3-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b3e3-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5b3e3-114">Before you begin</span></span>
<span data-ttu-id="5b3e3-115">Si vous utilisez PowerShell, assurez-vous que vous disposez de la dernière version du module PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5b3e3-116">Exécutez la commande suivante pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5b3e3-117">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b3e3-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="5b3e3-118">Ajouter un disque de données vide à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b3e3-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="5b3e3-119">Cet exemple montre comment ajouter un disque de données vide à une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="5b3e3-120">Utilisation de disques gérés</span><span class="sxs-lookup"><span data-stu-id="5b3e3-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="5b3e3-121">Utilisation de disques non gérés dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5b3e3-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="5b3e3-122">Initialiser le disque</span><span class="sxs-lookup"><span data-stu-id="5b3e3-122">Initialize the disk</span></span>

<span data-ttu-id="5b3e3-123">Après avoir ajouté un disque vide, vous devez l’initialiser.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="5b3e3-124">Pour initialiser le disque, vous pouvez vous connecter à une machine virtuelle et utiliser la gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="5b3e3-125">Si vous avez activé WinRM et un certificat sur la machine virtuelle lors de sa création, vous pouvez utiliser PowerShell à distance pour initialiser le disque.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="5b3e3-126">Vous pouvez également utiliser une extension de script personnalisée :</span><span class="sxs-lookup"><span data-stu-id="5b3e3-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="5b3e3-127">Le fichier de script peut contenir les éléments de code suivants pour initialiser les disques :</span><span class="sxs-lookup"><span data-stu-id="5b3e3-127">The script file can contain something like this code to initialize the disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="5b3e3-128">Ajouter un disque de données existant à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b3e3-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="5b3e3-129">Vous pouvez également attacher un disque dur virtuel existant en tant que disque de données géré à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5b3e3-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="5b3e3-130">Utilisation de disques gérés</span><span class="sxs-lookup"><span data-stu-id="5b3e3-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="5b3e3-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b3e3-131">Next steps</span></span>

<span data-ttu-id="5b3e3-132">Créer une [capture instantanée](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5b3e3-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
