---
title: "aaaAttach un tooa de disque de données Windows VM dans Azure à l’aide de PowerShell | Documents Microsoft"
description: "Les données nouvelles ou existantes tooattach disque tooa machine virtuelle Windows à l’aide de PowerShell avec le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="279b8-103">Attacher un tooa de disque de données machine virtuelle Windows à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="279b8-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="279b8-104">Cet article vous explique comment tooattach des disques virtuels tooa Windows à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="279b8-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="279b8-105">Si votre machine virtuelle utilise des disques gérés, vous pouvez attacher des disques de données gérés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="279b8-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="279b8-106">Vous pouvez également attacher des disques de données non managées tooa machine virtuelle qui utilise des disques non managés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="279b8-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="279b8-107">Avant cela, passez en revue les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="279b8-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="279b8-108">taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données.</span><span class="sxs-lookup"><span data-stu-id="279b8-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="279b8-109">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="279b8-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="279b8-110">toouse stockage Premium, vous aurez besoin un stockage Premium activée de taille de machine virtuelle comme hello série DS ou GS-series l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="279b8-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="279b8-111">Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="279b8-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="279b8-112">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="279b8-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="279b8-113">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="279b8-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="279b8-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="279b8-114">Before you begin</span></span>
<span data-ttu-id="279b8-115">Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="279b8-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="279b8-116">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="279b8-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="279b8-117">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="279b8-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="279b8-118">Ajouter un ordinateur virtuel de données vide disque tooa</span><span class="sxs-lookup"><span data-stu-id="279b8-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="279b8-119">Cet exemple montre l’ordinateur virtuel existant de tooan de disque tooadd une données vide.</span><span class="sxs-lookup"><span data-stu-id="279b8-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="279b8-120">Utilisation de disques gérés</span><span class="sxs-lookup"><span data-stu-id="279b8-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="279b8-121">Utilisation de disques non gérés dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="279b8-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="279b8-122">Initialiser le disque de hello</span><span class="sxs-lookup"><span data-stu-id="279b8-122">Initialize hello disk</span></span>

<span data-ttu-id="279b8-123">Après avoir ajouté un disque vide, vous devez tooinitialize il.</span><span class="sxs-lookup"><span data-stu-id="279b8-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="279b8-124">disque de hello tooinitialize, vous pouvez vous connecter tooa machine virtuelle et utiliser Gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="279b8-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="279b8-125">Si vous avez activé WinRM et un certificat sur la machine virtuelle de hello lors de sa création, vous pouvez utiliser le disque de hello tooinitialize PowerShell distant.</span><span class="sxs-lookup"><span data-stu-id="279b8-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="279b8-126">Vous pouvez également utiliser une extension de script personnalisée :</span><span class="sxs-lookup"><span data-stu-id="279b8-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="279b8-127">fichier de script Hello peut contenir quelque chose comme ce code tooinitialize les disques hello :</span><span class="sxs-lookup"><span data-stu-id="279b8-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="279b8-128">Attacher un tooa de disque de données existant machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="279b8-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="279b8-129">Vous pouvez également attacher un disque dur virtuel existant comme un ordinateur virtuel de données managées disque tooa.</span><span class="sxs-lookup"><span data-stu-id="279b8-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="279b8-130">Utilisation de disques gérés</span><span class="sxs-lookup"><span data-stu-id="279b8-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="279b8-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="279b8-131">Next steps</span></span>

<span data-ttu-id="279b8-132">Créer une [capture instantanée](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="279b8-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
