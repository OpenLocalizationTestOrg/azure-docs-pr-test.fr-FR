---
title: "aaaCreate machine virtuelle à partir d’un disque spécialisé dans Azure | Documents Microsoft"
description: "Créer une machine virtuelle en attachant un disque spécialisé non managé, dans le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="5ab50-103">Création d’une machine virtuelle à partir d’un disque dur virtuel spécialisé dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5ab50-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="5ab50-104">Créer une machine virtuelle en attachant un disque spécialisé de non managé en tant que disque de système d’exploitation hello à l’aide de Powershell.</span><span class="sxs-lookup"><span data-stu-id="5ab50-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="5ab50-105">Un disque spécialisé est une copie du disque dur virtuel à partir d’une machine virtuelle existante qui gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="5ab50-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="5ab50-106">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="5ab50-106">You have two options:</span></span>
* [<span data-ttu-id="5ab50-107">Charger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="5ab50-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="5ab50-108">Copiez hello disque dur virtuel d’une machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="5ab50-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="5ab50-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5ab50-109">Before you begin</span></span>
<span data-ttu-id="5ab50-110">Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5ab50-111">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="5ab50-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="5ab50-112">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5ab50-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="5ab50-113">Option 1 : Charger un disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="5ab50-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="5ab50-114">Vous pouvez télécharger hello que disque dur virtuel à partir d’une machine virtuelle spécialisée créé avec un outil de virtualisation sur site, telles que Hyper-V ou un ordinateur virtuel exporté à partir d’un autre cloud.</span><span class="sxs-lookup"><span data-stu-id="5ab50-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="5ab50-115">Préparer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ab50-115">Prepare hello VM</span></span>
<span data-ttu-id="5ab50-116">Vous pouvez charger un disque dur virtuel spécialisé créé à l’aide d’une machine virtuelle sur site ou un disque dur virtuel exporté à partir d’un autre cloud.</span><span class="sxs-lookup"><span data-stu-id="5ab50-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="5ab50-117">Un disque dur virtuel spécialisé gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="5ab50-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="5ab50-118">Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée.</span><span class="sxs-lookup"><span data-stu-id="5ab50-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="5ab50-119">[Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ab50-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5ab50-120">**Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="5ab50-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="5ab50-121">Supprimer les outils de virtualisation invité et les agents installés sur hello VM (autrement dit, les outils VMware).</span><span class="sxs-lookup"><span data-stu-id="5ab50-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="5ab50-122">Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP.</span><span class="sxs-lookup"><span data-stu-id="5ab50-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="5ab50-123">Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage.</span><span class="sxs-lookup"><span data-stu-id="5ab50-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="5ab50-124">Obtenir le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="5ab50-124">Get hello storage account</span></span>
<span data-ttu-id="5ab50-125">Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="5ab50-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="5ab50-126">Vous pouvez utiliser un compte de stockage existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="5ab50-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="5ab50-127">comptes de stockage disponibles hello tooshow, tapez :</span><span class="sxs-lookup"><span data-stu-id="5ab50-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="5ab50-128">Si vous voulez toouse un compte de stockage existant, passez toohello [image de machine virtuelle téléchargement hello](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="5ab50-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="5ab50-129">Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ab50-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="5ab50-130">Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="5ab50-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="5ab50-131">toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :</span><span class="sxs-lookup"><span data-stu-id="5ab50-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="5ab50-132">toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **ouest des États-Unis** région, tapez :</span><span class="sxs-lookup"><span data-stu-id="5ab50-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="5ab50-133">Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="5ab50-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="5ab50-134">Télécharger le compte de stockage tooyour hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="5ab50-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="5ab50-135">Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur tooa d’images de hello tooupload applet de commande dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5ab50-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="5ab50-136">Cet exemple montre comment les téléchargements hello fichier **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé **mystorageaccount** Bonjour **myResourceGroup** groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5ab50-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="5ab50-137">fichier de Hello est placé dans le conteneur hello nommé **mycontainer** et nouveau nom de fichier hello seront **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="5ab50-138">En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="5ab50-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="5ab50-139">Cette commande peut prendre du temps en fonction de votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5ab50-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="5ab50-140">Option 2 : Copiez hello disque dur virtuel à partir d’une machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="5ab50-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="5ab50-141">Vous pouvez copier un toouse de compte de stockage tooanother disque dur virtuel lors de la création d’une machine virtuelle au nouveau, en double.</span><span class="sxs-lookup"><span data-stu-id="5ab50-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="5ab50-142">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5ab50-142">Before you begin</span></span>
<span data-ttu-id="5ab50-143">Veillez à :</span><span class="sxs-lookup"><span data-stu-id="5ab50-143">Make sure that you:</span></span>

* <span data-ttu-id="5ab50-144">Informations sur hello **comptes de stockage source et destination**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="5ab50-145">Pour la source de hello machine virtuelle, vous devez toohave hello compte conteneur de noms de stockage et.</span><span class="sxs-lookup"><span data-stu-id="5ab50-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="5ab50-146">En règle générale, le nom du conteneur hello sera **disques durs virtuels**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="5ab50-147">Vous devez également toohave un compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="5ab50-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="5ab50-148">Si vous n’en avez déjà, vous pouvez créer un à l’aide de des portails hello (**plus Services** > comptes de stockage > Add) ou à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="5ab50-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="5ab50-149">Téléchargé et installé hello [outil AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5ab50-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="5ab50-150">Désallouer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ab50-150">Deallocate hello VM</span></span>
<span data-ttu-id="5ab50-151">Désallouer hello machine virtuelle, ce qui libère des hello toobe de disque dur virtuel copié.</span><span class="sxs-lookup"><span data-stu-id="5ab50-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="5ab50-152">**Portail** : cliquez sur **Machines virtuelles** > **myVM** &gt; Arrêter</span><span class="sxs-lookup"><span data-stu-id="5ab50-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="5ab50-153">**PowerShell**: utilisez [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (désallouer) hello d’ordinateur virtuel nommé **myVM** dans le groupe de ressources **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="5ab50-154">Hello **état** pour hello VM Bonjour Azure portal passe de **arrêté** trop**arrêté (désallouée)**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="5ab50-155">Obtenir l’URL de compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="5ab50-155">Get hello storage account URLs</span></span>
<span data-ttu-id="5ab50-156">Vous devez URL hello hello source et destination de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="5ab50-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="5ab50-157">Hello URL ressembler à : `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="5ab50-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="5ab50-158">Si vous connaissez déjà le nom de compte et conteneur de stockage hello, vous pouvez simplement remplacer informations hello entre hello crochets toocreate votre URL.</span><span class="sxs-lookup"><span data-stu-id="5ab50-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="5ab50-159">Vous pouvez utiliser hello portail Azure ou Azure Powershell tooget hello URL :</span><span class="sxs-lookup"><span data-stu-id="5ab50-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="5ab50-160">**Portail**: cliquez sur hello  **>**  pour **davantage de services** > **comptes de stockage**  >   *compte de stockage* > **BLOB** et votre fichier de disque dur virtuel source est probablement Bonjour **disques durs virtuels** conteneur.</span><span class="sxs-lookup"><span data-stu-id="5ab50-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="5ab50-161">Cliquez sur **propriétés** pour le conteneur de hello et copier le texte hello étiqueté **URL**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="5ab50-162">Vous aurez besoin des URL hello de deux conteneurs de hello source et de destination.</span><span class="sxs-lookup"><span data-stu-id="5ab50-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="5ab50-163">**PowerShell**: utilisez [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget les informations de hello pour l’ordinateur virtuel nommé **myVM** dans le groupe de ressources hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5ab50-164">Dans les résultats de hello, recherchez dans hello **profil de stockage** section pour hello **Vhd Uri**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="5ab50-165">Hello première partie de hello Uri est le conteneur de toohello URL hello et hello dernière partie est hello nom de disque dur virtuel du système d’exploitation pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ab50-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="5ab50-166">Obtenir les clés d’accès de stockage de hello</span><span class="sxs-lookup"><span data-stu-id="5ab50-166">Get hello storage access keys</span></span>
<span data-ttu-id="5ab50-167">Rechercher des clés d’accès hello pour hello comptes de stockage source et de destination.</span><span class="sxs-lookup"><span data-stu-id="5ab50-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="5ab50-168">Pour plus d’informations sur les clés d’accès, consultez la page [À propos des comptes de stockage Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5ab50-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="5ab50-169">**Portail** : cliquez sur **Plus de services** > **Comptes de stockage** > *compte de stockage* > **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="5ab50-170">Copier la clé hello étiquetés comme **key1**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="5ab50-171">**PowerShell**: utilisez [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello stockage clé hello compte de stockage **mystorageaccount** dans le groupe de ressources hello  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5ab50-172">Copier la clé hello étiquetée **key1**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="5ab50-173">Copiez hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="5ab50-173">Copy hello VHD</span></span>
<span data-ttu-id="5ab50-174">Vous pouvez copier des fichiers entre comptes de stockage avec AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5ab50-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="5ab50-175">Pour le conteneur de destination hello, si le conteneur spécifié de hello n’existe pas, elle sera créée pour vous.</span><span class="sxs-lookup"><span data-stu-id="5ab50-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="5ab50-176">toouse AzCopy, ouvrez une invite de commandes sur votre ordinateur local et l’exploration du dossier toohello où AzCopy est installé.</span><span class="sxs-lookup"><span data-stu-id="5ab50-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="5ab50-177">Elle sera semblable trop*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="5ab50-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="5ab50-178">toocopy hello tous les fichiers dans un conteneur, vous utilisez hello **/S** basculer.</span><span class="sxs-lookup"><span data-stu-id="5ab50-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="5ab50-179">Cela peut être utilisé toocopy hello disque dur virtuel du système d’exploitation et tous les disques de données hello s’ils sont en hello même conteneur.</span><span class="sxs-lookup"><span data-stu-id="5ab50-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="5ab50-180">Cet exemple montre comment toocopy hello tous les fichiers dans le conteneur de hello **mysourcecontainer** dans le compte de stockage **mysourcestorageaccount** toohello conteneur **mydestinationcontainer**  Bonjour **mydestinationstorageaccount** compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5ab50-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="5ab50-181">Remplacez les noms de hello des comptes de stockage hello et des conteneurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="5ab50-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="5ab50-182">Remplacez `<sourceStorageAccountKey1>` et `<destinationStorageAccountKey1>` par vos propres clés.</span><span class="sxs-lookup"><span data-stu-id="5ab50-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="5ab50-183">Si vous souhaitez uniquement toocopy un disque dur virtuel spécifique dans un conteneur avec plusieurs fichiers, vous pouvez également spécifier le nom du fichier à l’aide du commutateur de /Pattern hello hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="5ab50-184">Dans cet exemple, uniquement hello fichier nommé **myFileName.vhd** seront copiés.</span><span class="sxs-lookup"><span data-stu-id="5ab50-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="5ab50-185">Une fois la copie terminée, vous recevez un message du type :</span><span class="sxs-lookup"><span data-stu-id="5ab50-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="5ab50-186">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="5ab50-186">Troubleshooting</span></span>
* <span data-ttu-id="5ab50-187">Lorsque vous utilisez AZCopy, si vous voyez hello erreur « Échec de demande de hello tooauthenticate de serveur », assurez-vous que valeur hello de l’en-tête d’autorisation hello est formé correctement, notamment la signature de hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="5ab50-188">Si vous utilisez la clé de 2 ou la clé de stockage secondaire hello, essayez d’utiliser la clé de stockage principal ou le 1er hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="5ab50-189">Créer hello nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ab50-189">Create hello new VM</span></span> 

<span data-ttu-id="5ab50-190">Vous avez besoin de mise en réseau toocreate et autres toobe de ressources de machine virtuelle utilisée par hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ab50-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="5ab50-191">Créer le réseau virtuel et le sous-réseau de hello</span><span class="sxs-lookup"><span data-stu-id="5ab50-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="5ab50-192">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ab50-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="5ab50-193">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-193">Create hello subNet.</span></span> <span data-ttu-id="5ab50-194">Cet exemple crée un sous-réseau nommé **mySubNet**, dans le groupe de ressources hello **myResourceGroup**, et les jeux de hello préfixe d’adresse de sous-réseau trop**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="5ab50-195">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-195">Create hello vNet.</span></span> <span data-ttu-id="5ab50-196">Cet exemple définit hello toobe de nom de réseau virtuel **myVnetName**, hello emplacement trop**ouest des États-Unis**, et hello trop de préfixe d’adresse de réseau virtuel de hello**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="5ab50-197">Créer une adresse IP publique et une carte réseau</span><span class="sxs-lookup"><span data-stu-id="5ab50-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="5ab50-198">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="5ab50-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="5ab50-199">Créer l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-199">Create hello public IP.</span></span> <span data-ttu-id="5ab50-200">Dans cet exemple, le nom d’adresse IP publique hello est défini trop**myIP**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="5ab50-201">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-201">Create hello NIC.</span></span> <span data-ttu-id="5ab50-202">Dans cet exemple, le nom de carte réseau hello est défini trop**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="5ab50-203">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="5ab50-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="5ab50-204">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="5ab50-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="5ab50-205">Car hello disque dur virtuel pour hello que nouvel ordinateur virtuel a été créé à partir d’un fichier spécialisé machine virtuelle, après que hello machine virtuelle est créée, vous pouvez utiliser un compte existant à partir de l’ordinateur virtuel source hello avait toolog d’autorisation sur l’utilisation de RDP.</span><span class="sxs-lookup"><span data-stu-id="5ab50-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="5ab50-206">Cet exemple définit hello nom du groupe de sécurité réseau trop**myNsg** et nom de la règle hello RDP trop**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="5ab50-207">Pour plus d’informations sur les points de terminaison et les règles du groupe de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ab50-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="5ab50-208">Nom d’ordinateur virtuel hello et la taille</span><span class="sxs-lookup"><span data-stu-id="5ab50-208">Set hello VM name and size</span></span>

<span data-ttu-id="5ab50-209">Cet exemple définit hello nom d’ordinateur virtuel trop « myVM » et hello VM taille trop « Standard_A2 ».</span><span class="sxs-lookup"><span data-stu-id="5ab50-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="5ab50-210">Ajouter hello NIC</span><span class="sxs-lookup"><span data-stu-id="5ab50-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="5ab50-211">Configurer le disque de hello du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="5ab50-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="5ab50-212">Définissez hello URI pour hello disque dur virtuel que vous avez téléchargé ou copié.</span><span class="sxs-lookup"><span data-stu-id="5ab50-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="5ab50-213">Dans cet exemple, hello le fichier de disque dur virtuel nommé **myOsDisk.vhd** est conservée dans un compte de stockage nommé **myStorageAccount** dans un conteneur nommé **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="5ab50-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="5ab50-214">Ajouter un disque de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5ab50-214">Add hello OS disk.</span></span> <span data-ttu-id="5ab50-215">Dans cet exemple, lorsque hello disque de système d’exploitation est créé, hello terme « osDisk » est le nom du disque du système d’exploitation nom toocreate hello appened toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ab50-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="5ab50-216">Cet exemple spécifie également que ce disque dur virtuel basé sur Windows doit être attaché toohello machine virtuelle en tant que disque de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5ab50-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="5ab50-217">Facultatif : Si vous avez des disques de données qui toobe besoin attaché toohello VM, ajouter des disques de données hello à l’aide des URL hello de disques durs virtuels de données et hello approprié numéro d’unité logique (Lun).</span><span class="sxs-lookup"><span data-stu-id="5ab50-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="5ab50-218">Lorsque vous utilisez un compte de stockage, les données de salutation et URL de disque de système d’exploitation ressembler à ceci : `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="5ab50-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="5ab50-219">Vous pouvez le trouver sur le portail hello en parcourant le conteneur de stockage cible toohello, en cliquant sur le système d’exploitation de hello ou des données de disque dur virtuel qui a été copié, puis en copiant contenu hello de hello URL.</span><span class="sxs-lookup"><span data-stu-id="5ab50-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="5ab50-220">Machine virtuelle de hello terminée</span><span class="sxs-lookup"><span data-stu-id="5ab50-220">Complete hello VM</span></span> 

<span data-ttu-id="5ab50-221">Créer hello machine virtuelle à l’aide de configurations de hello que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="5ab50-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="5ab50-222">Si la commande a été exécutée avec succès, vous obtiendrez une sortie similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="5ab50-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="5ab50-223">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="5ab50-223">Verify that hello VM was created</span></span>
<span data-ttu-id="5ab50-224">Vous devez voir hello nouvellement créées VM dans hello [portail Azure](https://portal.azure.com), sous **Parcourir** > **virtuels**, ou à l’aide de hello suivant PowerShell commandes :</span><span class="sxs-lookup"><span data-stu-id="5ab50-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="5ab50-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ab50-225">Next steps</span></span>
<span data-ttu-id="5ab50-226">toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello.</span><span class="sxs-lookup"><span data-stu-id="5ab50-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="5ab50-227">Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="5ab50-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="5ab50-228">Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5ab50-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

