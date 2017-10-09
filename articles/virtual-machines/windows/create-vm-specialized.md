---
title: "aaaCreate une machine virtuelle de Windows à partir d’un disque dur virtuel spécialisé dans Azure | Documents Microsoft"
description: "Créez une machine virtuelle Windows en attachant un disque spécialisé de géré en tant que disque de système d’exploitation hello à l’aide dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="7e488-103">Créer une machine virtuelle Windows à partir d’un disque spécialisé</span><span class="sxs-lookup"><span data-stu-id="7e488-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="7e488-104">Créer une machine virtuelle en attachant un disque spécialisé de géré en tant que disque de système d’exploitation hello à l’aide de Powershell.</span><span class="sxs-lookup"><span data-stu-id="7e488-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="7e488-105">Un disque spécialisé est une copie du disque dur virtuel (VHD) à partir d’une machine virtuelle existante qui gère les comptes d’utilisateur hello, applications et autres données d’état à partir de votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="7e488-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="7e488-106">Lorsque vous utilisez un toocreate de disque dur virtuel une machine virtuelle spécialisée, hello nouvelle machine virtuelle conserve le nom de l’ordinateur de hello hello ordinateur virtuel d’origine.</span><span class="sxs-lookup"><span data-stu-id="7e488-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="7e488-107">D’autres informations spécifiques de l’ordinateur sont également conservées et, dans certains cas, ces informations en double pourraient entraîner des problèmes.</span><span class="sxs-lookup"><span data-stu-id="7e488-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="7e488-108">Lors de la copie d’une machine virtuelle, vous devez connaître les types d’informations spécifiques de l’ordinateur dont vos applications dépendent.</span><span class="sxs-lookup"><span data-stu-id="7e488-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="7e488-109">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="7e488-109">You have two options:</span></span>
* [<span data-ttu-id="7e488-110">Charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="7e488-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="7e488-111">Copier une machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="7e488-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="7e488-112">Cette rubrique vous montre comment toouse des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="7e488-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="7e488-113">Si vous avez un déploiement hérité qui requiert l’utilisation d’un compte de stockage, voir [Créer une machine virtuelle à partir d’un disque dur virtuel spécialisé dans un compte de stockage](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="7e488-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7e488-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7e488-114">Before you begin</span></span>
<span data-ttu-id="7e488-115">Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="7e488-116">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e488-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="7e488-117">Option 1 : Charger un disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="7e488-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="7e488-118">Vous pouvez télécharger hello que disque dur virtuel à partir d’une machine virtuelle spécialisée créé avec un outil de virtualisation sur site, telles que Hyper-V ou un ordinateur virtuel exporté à partir d’un autre cloud.</span><span class="sxs-lookup"><span data-stu-id="7e488-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="7e488-119">Préparer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e488-119">Prepare hello VM</span></span>
<span data-ttu-id="7e488-120">Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée.</span><span class="sxs-lookup"><span data-stu-id="7e488-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="7e488-121">[Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e488-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7e488-122">**Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="7e488-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="7e488-123">Supprimer les outils de virtualisation invité et les agents installés sur hello machine virtuelle (par exemple, les outils VMware).</span><span class="sxs-lookup"><span data-stu-id="7e488-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="7e488-124">Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP.</span><span class="sxs-lookup"><span data-stu-id="7e488-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="7e488-125">Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage.</span><span class="sxs-lookup"><span data-stu-id="7e488-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="7e488-126">Obtenir le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="7e488-126">Get hello storage account</span></span>
<span data-ttu-id="7e488-127">Vous avez besoin d’un stockage compte dans Azure toostore hello téléchargé le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e488-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="7e488-128">Vous pouvez utiliser un compte de stockage existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="7e488-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="7e488-129">comptes de stockage disponibles hello tooshow, tapez :</span><span class="sxs-lookup"><span data-stu-id="7e488-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="7e488-130">Si vous voulez toouse un compte de stockage existant, passez toohello [téléchargement hello VHD](#upload-the-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="7e488-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="7e488-131">Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e488-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="7e488-132">Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="7e488-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="7e488-133">toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :</span><span class="sxs-lookup"><span data-stu-id="7e488-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="7e488-134">toocreate un groupe de ressources nommé *myResourceGroup* Bonjour *ouest des États-Unis* région, tapez :</span><span class="sxs-lookup"><span data-stu-id="7e488-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="7e488-135">Créer un compte de stockage nommé *mystorageaccount* dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="7e488-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="7e488-136">Télécharger le compte de stockage tooyour hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="7e488-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="7e488-137">Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur applet de commande tooupload hello VHD tooa dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e488-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="7e488-138">Cet exemple montre comment les téléchargements hello fichier *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé *mystorageaccount* Bonjour *myResourceGroup* groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7e488-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="7e488-139">fichier de Hello est stocké dans le conteneur hello nommé *mycontainer* et nouveau nom de fichier hello seront *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="7e488-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="7e488-140">En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="7e488-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="7e488-141">Selon votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, cette commande peut prendre un certain temps toocomplete</span><span class="sxs-lookup"><span data-stu-id="7e488-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="7e488-142">Créer un disque de managé à partir de hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="7e488-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="7e488-143">Créer un disque de managé à partir de hello spécialisé de disque dur virtuel dans votre compte de stockage à l’aide de [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="7e488-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="7e488-144">Cet exemple utilise **myOSDisk1** pour le nom du disque hello, place hello disque dans *StandardLRS* de stockage et utilise *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* comme hello URI pour le disque dur virtuel de la source hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="7e488-145">Créer un groupe de ressources pour hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e488-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="7e488-146">Créer nouveau disque de système d’exploitation hello de hello téléchargé le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e488-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="7e488-147">Option 2 : Copier une machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="7e488-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="7e488-148">Vous pouvez créer une copie d’une machine virtuelle qu’utilise des disques gérés par une capture instantanée de hello machine virtuelle, puis à l’aide de ce toocreate instantané un nouveau gérés disque et une nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e488-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="7e488-149">Prenez un instantané du disque du système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="7e488-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="7e488-150">Vous pouvez prendre une capture instantanée d’une machine virtuelle entière (y compris tous les disques) ou d’un seul disque.</span><span class="sxs-lookup"><span data-stu-id="7e488-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="7e488-151">Hello étapes suivantes vous montrent comment une capture instantanée du disque juste de hello du système d’exploitation de votre machine virtuelle à l’aide de tootake hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="7e488-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="7e488-152">Définissez certains paramètres.</span><span class="sxs-lookup"><span data-stu-id="7e488-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="7e488-153">Obtenir l’objet d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="7e488-154">Obtenir le nom du disque hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7e488-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="7e488-155">Créer la configuration de capture instantanée hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="7e488-156">Prendre un instantané hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="7e488-157">Si vous envisagez toouse hello instantané toocreate une machine virtuelle qui doit toobe hautement performants, utilisez le paramètre hello `-AccountType Premium_LRS` avec la commande hello AzureRmSnapshot de nouveau.</span><span class="sxs-lookup"><span data-stu-id="7e488-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="7e488-158">paramètre Hello crée l’instantané d’hello afin qu’il est stocké comme disque Premium gérés.</span><span class="sxs-lookup"><span data-stu-id="7e488-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="7e488-159">Les disques gérés Premium sont plus chers que les disques gérés Standard.</span><span class="sxs-lookup"><span data-stu-id="7e488-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="7e488-160">Veillez à ce que vous avez vraiment besoin Premium avant d’utiliser le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="7e488-161">Créer un nouveau disque à partir de l’instantané d’hello</span><span class="sxs-lookup"><span data-stu-id="7e488-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="7e488-162">Créer un disque géré à partir de hello à l’aide de la capture instantanée [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="7e488-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="7e488-163">Cet exemple utilise *myOSDisk* pour le nom du disque hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="7e488-164">Créer un groupe de ressources pour hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e488-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="7e488-165">Définissez le nom du disque hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7e488-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="7e488-166">Créer un disque géré de hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="7e488-167">Créer hello nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e488-167">Create hello new VM</span></span> 

<span data-ttu-id="7e488-168">Créer la mise en réseau et autres toobe de ressources de machine virtuelle utilisée par hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e488-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="7e488-169">Créer le réseau virtuel et le sous-réseau de hello</span><span class="sxs-lookup"><span data-stu-id="7e488-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="7e488-170">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e488-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="7e488-171">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-171">Create hello subNet.</span></span> <span data-ttu-id="7e488-172">Cet exemple crée un sous-réseau nommé **mySubNet**, dans le groupe de ressources hello **myDestinationResourceGroup**, et les jeux de hello préfixe d’adresse de sous-réseau trop**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="7e488-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="7e488-173">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-173">Create hello vNet.</span></span> <span data-ttu-id="7e488-174">Cet exemple définit hello toobe de nom de réseau virtuel **myVnetName**, hello emplacement trop**ouest des États-Unis**, et hello trop de préfixe d’adresse de réseau virtuel de hello**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="7e488-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="7e488-175">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="7e488-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="7e488-176">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="7e488-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="7e488-177">Étant donné que hello du disque dur virtuel pour hello nouvelle machine virtuelle a été créé à partir d’un ordinateur virtuel de spécialisé existant, vous pouvez utiliser un compte d’ordinateur virtuel de source hello pour RDP.</span><span class="sxs-lookup"><span data-stu-id="7e488-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="7e488-178">Cet exemple définit hello nom du groupe de sécurité réseau trop**myNsg** et nom de la règle hello RDP trop**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="7e488-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="7e488-179">Pour plus d’informations sur les points de terminaison et les règles du groupe de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e488-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="7e488-180">Créer une adresse IP publique et une carte réseau</span><span class="sxs-lookup"><span data-stu-id="7e488-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="7e488-181">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="7e488-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="7e488-182">Créer l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-182">Create hello public IP.</span></span> <span data-ttu-id="7e488-183">Dans cet exemple, le nom d’adresse IP publique hello est défini trop**myIP**.</span><span class="sxs-lookup"><span data-stu-id="7e488-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="7e488-184">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-184">Create hello NIC.</span></span> <span data-ttu-id="7e488-185">Dans cet exemple, le nom de carte réseau hello est défini trop**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="7e488-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="7e488-186">Nom d’ordinateur virtuel hello et la taille</span><span class="sxs-lookup"><span data-stu-id="7e488-186">Set hello VM name and size</span></span>

<span data-ttu-id="7e488-187">Cet exemple définit hello nom d’ordinateur virtuel trop*myVM* et la taille de machine virtuelle de hello trop*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="7e488-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="7e488-188">Ajouter hello NIC</span><span class="sxs-lookup"><span data-stu-id="7e488-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="7e488-189">Ajouter le disque de hello du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="7e488-189">Add hello OS disk</span></span> 

<span data-ttu-id="7e488-190">Ajouter à l’aide de hello du système d’exploitation disque toohello configuration [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="7e488-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="7e488-191">Cet exemple définit taille hello du disque de hello trop*128 Go* et attache le disque hello managé comme un *Windows* disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7e488-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="7e488-192">Machine virtuelle de hello terminée</span><span class="sxs-lookup"><span data-stu-id="7e488-192">Complete hello VM</span></span> 

<span data-ttu-id="7e488-193">Créer à l’aide de machine virtuelle hello [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello les configurations que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="7e488-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="7e488-194">Si la commande a été exécutée avec succès, vous obtiendrez une sortie similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="7e488-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="7e488-195">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="7e488-195">Verify that hello VM was created</span></span>
<span data-ttu-id="7e488-196">Vous devez voir hello nouvellement créées VM dans hello [portail Azure](https://portal.azure.com), sous **Parcourir** > **virtuels**, ou à l’aide de hello suivant PowerShell commandes :</span><span class="sxs-lookup"><span data-stu-id="7e488-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="7e488-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e488-197">Next steps</span></span>
<span data-ttu-id="7e488-198">toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello.</span><span class="sxs-lookup"><span data-stu-id="7e488-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="7e488-199">Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="7e488-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="7e488-200">Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7e488-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

