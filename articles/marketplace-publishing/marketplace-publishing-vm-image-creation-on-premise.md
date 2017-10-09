---
title: aaaCreating une image de machine virtuelle locale pour hello Azure Marketplace | Documents Microsoft
description: "Comprendre et déployer toohello Azure Marketplace pour d’autres utilisateurs et exécutez hello étapes toocreate une image de machine virtuelle locale toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="cc94b-103">Développer une image de machine virtuelle locale pour hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cc94b-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="cc94b-104">Nous vous recommandons fortement de développer des disques durs virtuels (VHD) Azure directement dans le cloud de hello à l’aide du protocole Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cc94b-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="cc94b-105">Toutefois, si nécessaire, il est possible de toodownload un disque dur virtuel et son développement à l’aide de l’infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="cc94b-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="cc94b-106">Pour le développement local, vous devez télécharger le système d’exploitation de hello disque dur virtuel de hello créé machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc94b-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="cc94b-107">Ces étapes s’intègrent à l’étape 3.3 présentée plus haut.</span><span class="sxs-lookup"><span data-stu-id="cc94b-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="cc94b-108">Télécharger une image de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="cc94b-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="cc94b-109">Localiser une URL d’objet blob</span><span class="sxs-lookup"><span data-stu-id="cc94b-109">Locate a blob URL</span></span>
<span data-ttu-id="cc94b-110">Bonjour toodownload de commande disque dur virtuel, d’abord localiser les URL de blob hello pour le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="cc94b-111">Recherchez les URL de blob hello de hello nouvelle [portail Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="cc94b-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="cc94b-112">Accédez trop**Parcourir** > **machines virtuelles**, et puis sélectionnez hello déployé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc94b-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="cc94b-113">Sous **configurer**, sélectionnez hello **disques** vignette, qui ouvre le panneau des disques hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="cc94b-115">Sélectionnez hello **disque de système d’exploitation**, qui ouvre un autre panneau qui affiche les propriétés du disque, y compris l’emplacement du disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="cc94b-116">Copiez cette URL d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="cc94b-116">Copy this blob URL.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="cc94b-118">Supprimez maintenant, hello déployé la machine virtuelle sans supprimer les disques de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="cc94b-119">Vous pouvez également arrêter hello VM au lieu de sa suppression.</span><span class="sxs-lookup"><span data-stu-id="cc94b-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="cc94b-120">Ne pas télécharger les VHD de système d’exploitation hello lorsque hello machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cc94b-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="cc94b-122">Télécharger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="cc94b-122">Download a VHD</span></span>
<span data-ttu-id="cc94b-123">Une fois que vous connaissez les URL de blob hello, vous pouvez télécharger hello disque dur virtuel à l’aide de hello [portail Azure](http://manage.windowsazure.com/) ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc94b-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="cc94b-124">Au moment de hello de la création de ce guide, toodownload de fonctionnalité hello un disque dur virtuel n’est pas encore présente dans le nouveau portail de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="cc94b-125">**Télécharger hello, système d’exploitation VHD via hello actuel [portail Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="cc94b-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="cc94b-126">Connectez-vous toohello portail Azure, si vous n'avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="cc94b-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="cc94b-127">Cliquez sur hello **stockage** onglet.</span><span class="sxs-lookup"><span data-stu-id="cc94b-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="cc94b-128">Sélectionnez le compte de stockage hello dans le hello disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="cc94b-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="cc94b-130">Les propriétés du compte de stockage s’affichent.</span><span class="sxs-lookup"><span data-stu-id="cc94b-130">This displays storage account properties.</span></span> <span data-ttu-id="cc94b-131">Sélectionnez hello **conteneurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="cc94b-131">Select hello **Containers** tab.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="cc94b-133">Sélectionnez le conteneur hello dans le hello disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="cc94b-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="cc94b-134">Par défaut, lors de la création à partir du portail de hello, hello disque dur virtuel est stocké dans un conteneur de disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="cc94b-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="cc94b-136">Sélectionnez le disque dur virtuel du système d’exploitation correct hello en comparant les toohello URL hello une que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="cc94b-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="cc94b-137">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-137">Click **Download**.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="cc94b-139">Télécharger un disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc94b-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="cc94b-140">En outre toousing hello portail Azure, vous pouvez utiliser hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) système d’exploitation disque dur virtuel d’applet de commande toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="cc94b-141">Par exemple, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="cc94b-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="cc94b-142">**Save-AzureVhd** a également un **NumberOfThreads** option qui peut être utilisé tooincrease parallélisme toomake hello meilleure utilisation de la bande passante disponible pour le téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc94b-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="cc94b-143">Télécharger le compte de stockage Azure tooan de disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="cc94b-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="cc94b-144">Si vous avez préparé vos disques durs virtuels locaux, vous devez tooupload dans un stockage de compte dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cc94b-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="cc94b-145">Cette étape a lieu après la création de votre disque dur virtuel local, mais avant d’obtenir la certification pour votre image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc94b-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="cc94b-146">Créer un compte de stockage et un conteneur</span><span class="sxs-lookup"><span data-stu-id="cc94b-146">Create a storage account and container</span></span>
<span data-ttu-id="cc94b-147">Nous vous recommandons de télécharger des disques durs virtuels dans un compte de stockage dans une région de hello aux États-Unis.</span><span class="sxs-lookup"><span data-stu-id="cc94b-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="cc94b-148">Tous les disques durs virtuels pour une seule référence doivent être placés dans un seul conteneur au sein d’un seul compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc94b-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="cc94b-149">toocreate un compte de stockage, vous pouvez utiliser hello [portail Microsoft Azure](https://portal.azure.com/), PowerShell, ou l’outil de ligne de commande hello Linux.</span><span class="sxs-lookup"><span data-stu-id="cc94b-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="cc94b-150">**Créer un compte de stockage à partir du portail Microsoft Azure hello**</span><span class="sxs-lookup"><span data-stu-id="cc94b-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="cc94b-151">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-151">Click **New**.</span></span>
2. <span data-ttu-id="cc94b-152">Sélectionnez **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-152">Select **Storage**.</span></span>
3. <span data-ttu-id="cc94b-153">Renseignez le nom de compte de stockage hello et sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="cc94b-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="cc94b-155">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-155">Click **Create**.</span></span>
5. <span data-ttu-id="cc94b-156">panneau Hello pour hello créé le compte de stockage doit être ouvert.</span><span class="sxs-lookup"><span data-stu-id="cc94b-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="cc94b-157">Dans le cas contraire, sélectionnez **Parcourir** > **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="cc94b-158">Sur le stockage de hello compte panneau, sélectionnez le compte de stockage hello créé.</span><span class="sxs-lookup"><span data-stu-id="cc94b-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="cc94b-159">Sélectionnez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="cc94b-159">Select **Containers**.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="cc94b-161">Dans le panneau de conteneurs hello, sélectionnez **ajouter**, puis entrez un conteneur hello et nom de conteneur des autorisations.</span><span class="sxs-lookup"><span data-stu-id="cc94b-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="cc94b-162">Sélectionnez **Privé** pour les autorisations du conteneur.</span><span class="sxs-lookup"><span data-stu-id="cc94b-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="cc94b-163">Nous vous recommandons de créer un conteneur par référence (SKU) que vous envisagez de toopublish.</span><span class="sxs-lookup"><span data-stu-id="cc94b-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="cc94b-165">Créer un compte de stockage à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc94b-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="cc94b-166">À l’aide de PowerShell, créer un compte de stockage à l’aide de hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc94b-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="cc94b-167">Vous pouvez ensuite créer un conteneur au sein de ce compte de stockage à l’aide de hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc94b-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="cc94b-168">Ces commandes supposent que ce contexte de compte de stockage actuel hello a déjà été défini dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc94b-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="cc94b-169">Consultez trop[configurer Azure PowerShell](marketplace-publishing-powershell-setup.md) pour plus d’informations sur le programme d’installation de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc94b-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="cc94b-170">Créer un compte de stockage en utilisant l’outil de ligne de commande hello pour Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="cc94b-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="cc94b-171">Dans l’ [outil en ligne de commande Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), créez un compte de stockage comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc94b-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="cc94b-172">Créez un conteneur comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc94b-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="cc94b-173">Télécharger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="cc94b-173">Upload a VHD</span></span>
<span data-ttu-id="cc94b-174">Une fois que le compte de stockage hello et un conteneur sont créés, vous pouvez télécharger vos disques durs virtuels préparés.</span><span class="sxs-lookup"><span data-stu-id="cc94b-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="cc94b-175">Vous pouvez utiliser PowerShell, outil de ligne de commande hello Linux ou autres outils de gestion du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cc94b-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="cc94b-176">Télécharger un disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc94b-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="cc94b-177">Hello d’utilisation [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc94b-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="cc94b-178">Télécharger un disque dur virtuel en utilisant l’outil de ligne de commande hello pour Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="cc94b-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="cc94b-179">Avec hello [outil de ligne de commande Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilisez hello suivante : créer des images de machine virtuelle azure <image name> --emplacement <Location of hello data center> --système d’exploitation Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="cc94b-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="cc94b-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cc94b-180">See also</span></span>
* [<span data-ttu-id="cc94b-181">Création d’une image de machine virtuelle pour hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="cc94b-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="cc94b-182">Configuration d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc94b-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

