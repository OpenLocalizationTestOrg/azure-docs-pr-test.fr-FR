---
title: "aaaCreate un managé Azure VM à partir d’un disque dur virtuel généralisé local | Documents Microsoft"
description: "Télécharger un tooAzure de disque dur virtuel généralisé et utilisez-le toocreate nouvelles machines virtuelles, dans le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="a4f01-103">Télécharger un disque dur virtuel généralisé et utilisez-le toocreate nouvelles machines virtuelles dans Azure</span><span class="sxs-lookup"><span data-stu-id="a4f01-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="a4f01-104">Cette rubrique vous guide à l’aide de PowerShell tooupload un disque dur virtuel d’un tooAzure de machine virtuelle généralisée, créer une image de disque dur virtuel de hello et créer une machine virtuelle à partir de cette image.</span><span class="sxs-lookup"><span data-stu-id="a4f01-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="a4f01-105">Vous pouvez charger un disque dur virtuel exporté à partir d’un outil de virtualisation local ou d’un autre cloud.</span><span class="sxs-lookup"><span data-stu-id="a4f01-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="a4f01-106">À l’aide de [disques gérés](managed-disks-overview.md) pour hello nouvelle machine virtuelle simplifie la gestion des ordinateurs virtuels hello et fournit une meilleure disponibilité lorsque hello VM est placé dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="a4f01-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="a4f01-107">Si vous souhaitez toouse un exemple de script, consultez [exemple tooupload de script un tooAzure de disque dur virtuel et créer une machine virtuelle](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="a4f01-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a4f01-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a4f01-108">Before you begin</span></span>

- <span data-ttu-id="a4f01-109">Avant de télécharger tout tooAzure de disque dur virtuel, vous devez suivre [préparer un tooAzure tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a4f01-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="a4f01-110">Révision [planifier la migration de hello de disques de tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) avant de commencer votre migration trop[disques gérés](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4f01-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="a4f01-111">Assurez-vous que vous avez hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a4f01-112">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="a4f01-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="a4f01-113">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4f01-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="a4f01-114">Généraliser hello virtuelle Windows à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="a4f01-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="a4f01-115">Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="a4f01-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a4f01-116">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4f01-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a4f01-117">Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a4f01-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="a4f01-118">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="a4f01-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4f01-119">Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a4f01-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="a4f01-120">Se connecter toohello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="a4f01-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="a4f01-121">Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a4f01-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a4f01-122">Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="a4f01-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a4f01-123">Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="a4f01-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a4f01-124">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="a4f01-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a4f01-125">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4f01-125">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a4f01-127">Quand Sysprep se termine, il arrête de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="a4f01-128">Ne redémarrez pas hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a4f01-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="a4f01-129">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="a4f01-129">Log in tooAzure</span></span>
<span data-ttu-id="a4f01-130">Si vous n’avez pas encore PowerShell version 1.4 ou version ultérieure installé, lire [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4f01-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="a4f01-131">Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f01-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="a4f01-132">Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f01-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="a4f01-133">Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="a4f01-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="a4f01-134">Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="a4f01-135">Remplacez  *<subscriptionID>*  avec l’ID de hello Hello corriger l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a4f01-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="a4f01-136">Obtenir le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="a4f01-136">Get hello storage account</span></span>
<span data-ttu-id="a4f01-137">Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a4f01-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="a4f01-138">Vous pouvez utiliser un compte de stockage existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="a4f01-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="a4f01-139">Si vous utilisez hello toocreate de disque dur virtuel un disque géré pour une machine virtuelle, emplacement du compte de stockage hello doit être même hello où vous allez créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a4f01-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="a4f01-140">comptes de stockage disponibles hello tooshow, tapez :</span><span class="sxs-lookup"><span data-stu-id="a4f01-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="a4f01-141">Si vous voulez toouse un compte de stockage existant, passez toohello [image de machine virtuelle téléchargement hello](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="a4f01-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="a4f01-142">Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4f01-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="a4f01-143">Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="a4f01-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="a4f01-144">toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :</span><span class="sxs-lookup"><span data-stu-id="a4f01-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="a4f01-145">toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **États-Unis** région, tapez :</span><span class="sxs-lookup"><span data-stu-id="a4f01-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="a4f01-146">Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a4f01-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="a4f01-147">Les valeurs valides pour -SkuName sont :</span><span class="sxs-lookup"><span data-stu-id="a4f01-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="a4f01-148">**Standard_LRS** - Stockage localement redondant.</span><span class="sxs-lookup"><span data-stu-id="a4f01-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="a4f01-149">**Standard_ZRS** - Stockage redondant dans une zone.</span><span class="sxs-lookup"><span data-stu-id="a4f01-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="a4f01-150">**Standard_GRS** - Stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="a4f01-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="a4f01-151">**Standard_RAGRS** - Stockage géo-redondant avec accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="a4f01-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="a4f01-152">**Premium_LRS** - Stockage Premium localement redondant.</span><span class="sxs-lookup"><span data-stu-id="a4f01-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="a4f01-153">Télécharger le compte de stockage tooyour hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="a4f01-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="a4f01-154">Hello d’utilisation [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) conteneur applet de commande tooupload hello VHD tooa dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a4f01-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="a4f01-155">Cet exemple téléchargements hello fichier *myVHD.vhd* de *» des disques durs C:\Users\Public\Documents\Virtual\"*  tooa compte de stockage nommé *mystorageaccount*Bonjour *myResourceGroup* groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a4f01-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="a4f01-156">fichier de Hello est placé dans le conteneur hello nommé *mycontainer* et nouveau nom de fichier hello seront *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="a4f01-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="a4f01-157">En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="a4f01-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="a4f01-158">Selon votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, cette commande peut prendre un certain temps toocomplete</span><span class="sxs-lookup"><span data-stu-id="a4f01-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="a4f01-159">Enregistrer hello **URI de Destination** toouse de chemin d’accès plus tard si vous vous apprêtez toocreate un disque géré ou un nouvel ordinateur virtuel à l’aide de hello téléchargé le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a4f01-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="a4f01-160">Autres options de téléchargement d’un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="a4f01-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="a4f01-161">Vous pouvez également télécharger un compte de stockage de tooyour de disque dur virtuel à l’aide de valeurs hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a4f01-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="a4f01-162">AZCopy</span><span class="sxs-lookup"><span data-stu-id="a4f01-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="a4f01-163">API de copie d’un objet blob de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="a4f01-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="a4f01-164">Téléchargement d’objets blob dans Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="a4f01-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="a4f01-165">Référence sur l’API REST du service Import/Export Storage</span><span class="sxs-lookup"><span data-stu-id="a4f01-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="a4f01-166">Nous recommandons l’utilisation de du service d’importation/exportation si l’estimation du temps de téléchargement est de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="a4f01-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="a4f01-167">Vous pouvez utiliser [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate les temps de hello à partir de l’unité de taille et de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="a4f01-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="a4f01-168">Importation/exportation peut être utilisé le compte de stockage standard toocopy tooa.</span><span class="sxs-lookup"><span data-stu-id="a4f01-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="a4f01-169">Vous devez toocopy de compte de stockage toopremium de stockage standard à l’aide d’un outil tel que AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a4f01-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="a4f01-170">Créer un objet image à partir de hello téléchargé le disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="a4f01-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="a4f01-171">Créez une image managée à l’aide de votre disque dur virtuel généralisé de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a4f01-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="a4f01-172">Remplacez les valeurs hello par vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="a4f01-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="a4f01-173">Tout d’abord, définissez les paramètres communs hello :</span><span class="sxs-lookup"><span data-stu-id="a4f01-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="a4f01-174">Créer l’image de hello à l’aide de votre disque dur virtuel du système d’exploitation généralisé.</span><span class="sxs-lookup"><span data-stu-id="a4f01-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="a4f01-175">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="a4f01-175">Create a virtual network</span></span>
<span data-ttu-id="a4f01-176">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4f01-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a4f01-177">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-177">Create hello subnet.</span></span> <span data-ttu-id="a4f01-178">Cet exemple crée un sous-réseau nommé *mySubnet* avec le préfixe d’adresse de hello *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a4f01-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a4f01-179">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-179">Create hello virtual network.</span></span> <span data-ttu-id="a4f01-180">Cet exemple crée un réseau virtuel nommé *myVnet* avec le préfixe d’adresse de hello *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="a4f01-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a4f01-181">Création d'une adresse IP publique et une interface réseau</span><span class="sxs-lookup"><span data-stu-id="a4f01-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="a4f01-182">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="a4f01-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a4f01-183">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="a4f01-183">Create a public IP address.</span></span> <span data-ttu-id="a4f01-184">Cet exemple crée une adresse IP publique nommée *myPip*.</span><span class="sxs-lookup"><span data-stu-id="a4f01-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a4f01-185">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-185">Create hello NIC.</span></span> <span data-ttu-id="a4f01-186">Cet exemple crée une carte réseau nommée **myNic**.</span><span class="sxs-lookup"><span data-stu-id="a4f01-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a4f01-187">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="a4f01-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="a4f01-188">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité réseau (NSG) qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="a4f01-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a4f01-189">Cet exemple crée un groupe de sécurité réseau nommé *myNsg* qui contient une règle nommée *myRdpRule* autorisant le trafic RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="a4f01-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a4f01-190">Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4f01-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="a4f01-191">Créez une variable pour le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="a4f01-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="a4f01-192">Créez une variable pour le réseau virtuel de hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="a4f01-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="a4f01-193">Obtenir des informations d’identification de hello pour hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a4f01-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="a4f01-194">Hello applet de commande suivante ouvre une fenêtre dans laquelle vous entrerez un toouse nouveau du nom et mot de passe utilisateur en tant que compte d’administrateur local hello pour accéder à distance aux hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a4f01-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="a4f01-195">Ajoutez hello nom d’ordinateur virtuel et configuration d’ordinateur virtuel de taille toohello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="a4f01-196">Image de machine virtuelle hello ensemble en tant qu’image source pour hello nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a4f01-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="a4f01-197">Définir l’image source de hello à l’aide de code hello d’image de machine virtuelle hello géré.</span><span class="sxs-lookup"><span data-stu-id="a4f01-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="a4f01-198">Définir la configuration du système d’exploitation hello et ajouter de carte réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="a4f01-199">Entrez le type de stockage de hello (PremiumLRS ou StandardLRS) et la taille de hello du disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="a4f01-200">Cet exemple définit le type de compte hello trop*PremiumLRS*, hello trop de taille de disque*128 Go* et mise en cache disque trop*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="a4f01-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="a4f01-201">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a4f01-201">Create hello VM</span></span>

<span data-ttu-id="a4f01-202">Créer la nouvelle machine virtuelle à l’aide de la configuration de hello stockée Bonjour hello **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="a4f01-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="a4f01-203">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="a4f01-203">Verify that hello VM was created</span></span>
<span data-ttu-id="a4f01-204">Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a4f01-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a4f01-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4f01-205">Next steps</span></span>

<span data-ttu-id="a4f01-206">toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello.</span><span class="sxs-lookup"><span data-stu-id="a4f01-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="a4f01-207">Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="a4f01-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="a4f01-208">Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4f01-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

