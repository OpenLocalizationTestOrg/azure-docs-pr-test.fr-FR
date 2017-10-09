---
title: aaaUpload un toocreate de disque dur virtuel generalize plusieurs machines virtuelles dans Azure | Documents Microsoft
description: "Télécharger un généralisée toocreate VHD tooan stockage Azure compte un toouse machine virtuelle Windows avec le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="d01ac-103">Télécharger un toocreate de tooAzure de disque dur virtuel généralisé une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d01ac-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="d01ac-104">Cette rubrique décrit le téléchargement d’un compte de stockage de disque non managé généralisé tooa, puis en créant une nouvelle machine virtuelle à l’aide du disque de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d01ac-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="d01ac-105">Toutes les informations de votre compte personnel sont supprimées d’une image de disque dur virtuel généralisé à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d01ac-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="d01ac-106">Si vous souhaitez toocreate une machine virtuelle à partir d’un disque dur virtuel spécialisée dans un compte de stockage, consultez [créer une machine virtuelle à partir d’un disque dur virtuel spécialisé](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="d01ac-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="d01ac-107">Cette rubrique couvre l’utilisation de comptes de stockage, mais nous vous recommandons des clients déplacent des disques gérés toousing à la place.</span><span class="sxs-lookup"><span data-stu-id="d01ac-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="d01ac-108">Pour une procédure pas à pas complète tooprepare, télécharger et créer une nouvelle machine virtuelle en utilisant des disques gérés, consultez [créer une machine virtuelle à partir d’un tooAzure de disque dur virtuel téléchargé généralisé à l’aide de disques gérés](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="d01ac-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="d01ac-109">Préparer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d01ac-109">Prepare hello VM</span></span>

<span data-ttu-id="d01ac-110">Toutes les informations de votre compte personnel sont supprimées d’un disque dur virtuel généralisé à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d01ac-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="d01ac-111">Si vous envisagez de toouse hello disque dur virtuel en tant qu’une image de toocreate nouvelles machines virtuelles à partir de, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d01ac-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="d01ac-112">[Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="d01ac-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="d01ac-113">Généraliser l’ordinateur virtuel de hello à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="d01ac-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="d01ac-114">Généraliser une machine virtuelle Windows avec Sysprep</span><span class="sxs-lookup"><span data-stu-id="d01ac-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="d01ac-115">Cette section vous montre comment toogeneralize votre machine virtuelle de Windows pour une utilisation en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="d01ac-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="d01ac-116">Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="d01ac-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="d01ac-117">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d01ac-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="d01ac-118">Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d01ac-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="d01ac-119">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="d01ac-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d01ac-120">Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d01ac-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="d01ac-121">Se connecter toohello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="d01ac-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="d01ac-122">Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d01ac-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="d01ac-123">Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="d01ac-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="d01ac-124">Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="d01ac-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="d01ac-125">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="d01ac-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-126">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="d01ac-128">Quand Sysprep se termine, il arrête de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d01ac-129">Ne redémarrez pas hello machine virtuelle jusqu'à ce que vous avez terminé tooAzure de disque dur virtuel hello téléchargement ou de la création d’une image à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="d01ac-130">Si hello VM obtient accidentellement redémarré, exécutez Sysprep toogeneralize nouveau.</span><span class="sxs-lookup"><span data-stu-id="d01ac-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="d01ac-131">Télécharger hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="d01ac-131">Upload hello VHD</span></span>

<span data-ttu-id="d01ac-132">Téléchargez le compte de stockage Azure tooan hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="d01ac-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="d01ac-133">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="d01ac-133">Log in tooAzure</span></span>
<span data-ttu-id="d01ac-134">Si vous n’avez pas encore PowerShell version 1.4 ou version ultérieure installé, lire [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d01ac-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="d01ac-135">Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d01ac-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="d01ac-136">Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d01ac-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="d01ac-137">Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="d01ac-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="d01ac-138">Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="d01ac-139">Remplacez `<subscriptionID>` avec l’ID de hello Hello corriger l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d01ac-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="d01ac-140">Obtenir le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="d01ac-140">Get hello storage account</span></span>
<span data-ttu-id="d01ac-141">Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d01ac-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="d01ac-142">Vous pouvez utiliser un compte de stockage existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="d01ac-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="d01ac-143">comptes de stockage disponibles hello tooshow, tapez :</span><span class="sxs-lookup"><span data-stu-id="d01ac-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="d01ac-144">Si vous voulez toouse un compte de stockage existant, passez toohello [image de machine virtuelle téléchargement hello](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="d01ac-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="d01ac-145">Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d01ac-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="d01ac-146">Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="d01ac-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="d01ac-147">toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :</span><span class="sxs-lookup"><span data-stu-id="d01ac-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="d01ac-148">toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **ouest des États-Unis** région, tapez :</span><span class="sxs-lookup"><span data-stu-id="d01ac-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="d01ac-149">Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="d01ac-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="d01ac-150">Démarrer le téléchargement de hello</span><span class="sxs-lookup"><span data-stu-id="d01ac-150">Start hello upload</span></span> 

<span data-ttu-id="d01ac-151">Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur tooa d’images de hello tooupload applet de commande dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d01ac-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="d01ac-152">Cet exemple montre comment les téléchargements hello fichier **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé **mystorageaccount** Bonjour **myResourceGroup** groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d01ac-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="d01ac-153">fichier de Hello est placé dans le conteneur hello nommé **mycontainer** et nouveau nom de fichier hello seront **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="d01ac-154">En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="d01ac-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="d01ac-155">Cette commande peut prendre du temps en fonction de votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d01ac-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="d01ac-156">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d01ac-156">Create a new VM</span></span> 

<span data-ttu-id="d01ac-157">Vous pouvez maintenant utiliser hello téléchargé toocreate de disque dur virtuel une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d01ac-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="d01ac-158">Ensemble hello URI de disque dur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="d01ac-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="d01ac-159">Hello URI pour toouse de disque dur virtuel hello est au format de hello : https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="d01ac-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="d01ac-160">Dans cet exemple hello disque dur virtuel nommé **myVHD** est dans un compte de stockage hello **mystorageaccount** dans le conteneur de hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="d01ac-161">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d01ac-161">Create a virtual network</span></span>
<span data-ttu-id="d01ac-162">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d01ac-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d01ac-163">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-163">Create hello subnet.</span></span> <span data-ttu-id="d01ac-164">Hello exemple suivant crée un sous-réseau nommé **mySubnet** dans le groupe de ressources hello **myResourceGroup** avec un préfixe d’adresse de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d01ac-165">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-165">Create hello virtual network.</span></span> <span data-ttu-id="d01ac-166">Hello exemple suivant crée un réseau virtuel nommé **myVnet** Bonjour **ouest des États-Unis** emplacement avec un préfixe d’adresse de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="d01ac-167">Création d'une adresse IP publique et une interface réseau</span><span class="sxs-lookup"><span data-stu-id="d01ac-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="d01ac-168">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="d01ac-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d01ac-169">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d01ac-169">Create a public IP address.</span></span> <span data-ttu-id="d01ac-170">Cet exemple crée une adresse IP publique nommée **myPip**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d01ac-171">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-171">Create hello NIC.</span></span> <span data-ttu-id="d01ac-172">Cet exemple crée une carte réseau nommée **myNic**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d01ac-173">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="d01ac-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="d01ac-174">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="d01ac-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="d01ac-175">Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="d01ac-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="d01ac-176">Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d01ac-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="d01ac-177">Créez une variable pour le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="d01ac-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="d01ac-178">Créez une variable pour le réseau virtuel de hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="d01ac-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="d01ac-179">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d01ac-179">Create hello VM</span></span>
<span data-ttu-id="d01ac-180">Hello script PowerShell suivant montre comment tooset les configurations d’ordinateur virtuel hello et utilisez hello téléchargé l’image de machine virtuelle en tant que source de hello pour une nouvelle installation de hello.</span><span class="sxs-lookup"><span data-stu-id="d01ac-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="d01ac-181">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="d01ac-181">Verify that hello VM was created</span></span>
<span data-ttu-id="d01ac-182">Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d01ac-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d01ac-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d01ac-183">Next steps</span></span>
<span data-ttu-id="d01ac-184">reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [gérer des ordinateurs virtuels à l’aide du Gestionnaire de ressources Azure et PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d01ac-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


