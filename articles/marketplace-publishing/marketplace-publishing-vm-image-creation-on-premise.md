---
title: "Création d’une image de machine virtuelle locale pour Azure Marketplace | Microsoft Docs"
description: "Découvrez et exécutez les étapes de création d’une image de machine virtuelle locale et déployez-la dans Azure Marketplace pour que d’autres utilisateurs puissent l’acheter."
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
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="09581-103">Développer une image de machine virtuelle locale pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="09581-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="09581-104">Nous vous recommandons fortement de développer les disques durs virtuels (VHD) Azure directement dans le cloud à l’aide du protocole RDP.</span><span class="sxs-lookup"><span data-stu-id="09581-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="09581-105">Toutefois, si nécessaire, vous pouvez télécharger un disque dur virtuel et le développer à l’aide d’une infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="09581-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="09581-106">Pour le développement local, vous devez télécharger le disque dur virtuel de système d’exploitation de la machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="09581-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="09581-107">Ces étapes s’intègrent à l’étape 3.3 présentée plus haut.</span><span class="sxs-lookup"><span data-stu-id="09581-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="09581-108">Télécharger une image de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="09581-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="09581-109">Localiser une URL d’objet blob</span><span class="sxs-lookup"><span data-stu-id="09581-109">Locate a blob URL</span></span>
<span data-ttu-id="09581-110">Pour télécharger le disque dur virtuel, vous devez d’abord localiser l’URL d’objet blob du disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="09581-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="09581-111">Recherchez l’URL d’objet blob à partir du nouveau [portail Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="09581-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="09581-112">Accédez à **Parcourir** > **Machines virtuelles**, puis sélectionnez la machine virtuelle déployée.</span><span class="sxs-lookup"><span data-stu-id="09581-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="09581-113">Sous **Configurer**, sélectionnez la vignette **Disques** qui ouvre le panneau Disques.</span><span class="sxs-lookup"><span data-stu-id="09581-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![dessin](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="09581-115">Sélectionnez le **disque de système d’exploitation**, qui ouvre un autre panneau indiquant les propriétés du disque, y compris l’emplacement du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="09581-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="09581-116">Copiez cette URL d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="09581-116">Copy this blob URL.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="09581-118">Supprimez la machine virtuelle déployée, sans supprimer les disques de stockage.</span><span class="sxs-lookup"><span data-stu-id="09581-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="09581-119">Vous pouvez également arrêter la machine virtuelle au lieu de la supprimer.</span><span class="sxs-lookup"><span data-stu-id="09581-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="09581-120">Ne téléchargez pas le disque dur virtuel de système d’exploitation quand la machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="09581-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="09581-122">Télécharger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="09581-122">Download a VHD</span></span>
<span data-ttu-id="09581-123">Une fois que vous connaissez l’URL d’objet blob, vous pouvez télécharger le disque dur virtuel à l’aide du [portail Azure](http://manage.windowsazure.com/) ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09581-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="09581-124">Au moment de la création de ce guide, la fonctionnalité de téléchargement d’un disque dur virtuel n’est pas encore présente dans le nouveau portail Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="09581-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="09581-125">**Télécharger le disque dur virtuel de système d’exploitation à partir du [portail Azure](http://manage.windowsazure.com/) actuel**</span><span class="sxs-lookup"><span data-stu-id="09581-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="09581-126">Si ce n’est pas déjà fait, connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09581-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="09581-127">Cliquez sur l’onglet **Stockage** .</span><span class="sxs-lookup"><span data-stu-id="09581-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="09581-128">Sélectionnez le compte de stockage dans lequel est stocké le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="09581-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="09581-130">Les propriétés du compte de stockage s’affichent.</span><span class="sxs-lookup"><span data-stu-id="09581-130">This displays storage account properties.</span></span> <span data-ttu-id="09581-131">Sélectionnez l’onglet **Conteneurs** .</span><span class="sxs-lookup"><span data-stu-id="09581-131">Select the **Containers** tab.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="09581-133">Sélectionnez le conteneur dans lequel est stocké le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="09581-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="09581-134">Par défaut, quand il est créé à partir du portail, le disque dur virtuel est stocké dans un conteneur de disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="09581-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="09581-136">Sélectionnez le disque dur virtuel de système d’exploitation approprié en comparant l’URL à celle que vous avez enregistrée.</span><span class="sxs-lookup"><span data-stu-id="09581-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="09581-137">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="09581-137">Click **Download**.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="09581-139">Télécharger un disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="09581-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="09581-140">Outre le portail Azure, vous pouvez utiliser l’applet de commande [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) pour télécharger le disque dur virtuel de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="09581-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="09581-141">Par exemple, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="09581-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="09581-142">**Save-AzureVhd** a également une option **NumberOfThreads** qui peut servir à augmenter le parallélisme pour tirer le meilleur parti de la bande passante disponible pour le téléchargement.</span><span class="sxs-lookup"><span data-stu-id="09581-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="09581-143">Télécharger des disques durs virtuel dans un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="09581-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="09581-144">Si vous avez préparé vos disques durs virtuels localement, vous devez les télécharger dans un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="09581-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="09581-145">Cette étape a lieu après la création de votre disque dur virtuel local, mais avant d’obtenir la certification pour votre image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09581-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="09581-146">Créer un compte de stockage et un conteneur</span><span class="sxs-lookup"><span data-stu-id="09581-146">Create a storage account and container</span></span>
<span data-ttu-id="09581-147">Comme mentionné précédemment, nous vous recommandons de télécharger les disques durs virtuels dans un compte de stockage dans une région aux États-Unis.</span><span class="sxs-lookup"><span data-stu-id="09581-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="09581-148">Tous les disques durs virtuels pour une seule référence doivent être placés dans un seul conteneur au sein d’un seul compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="09581-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="09581-149">Pour créer un compte de stockage, vous pouvez utiliser le [portail Microsoft Azure](https://portal.azure.com/), PowerShell ou l’outil en ligne de commande Linux.</span><span class="sxs-lookup"><span data-stu-id="09581-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="09581-150">**Créer un compte de stockage à partir du portail Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="09581-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="09581-151">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="09581-151">Click **New**.</span></span>
2. <span data-ttu-id="09581-152">Sélectionnez **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="09581-152">Select **Storage**.</span></span>
3. <span data-ttu-id="09581-153">Renseignez le nom du compte de stockage et sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="09581-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="09581-155">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="09581-155">Click **Create**.</span></span>
5. <span data-ttu-id="09581-156">Le panneau du compte de stockage créé doit être ouvert.</span><span class="sxs-lookup"><span data-stu-id="09581-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="09581-157">Dans le cas contraire, sélectionnez **Parcourir** > **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="09581-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="09581-158">Dans le panneau Compte de stockage, sélectionnez le compte de stockage créé.</span><span class="sxs-lookup"><span data-stu-id="09581-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="09581-159">Sélectionnez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="09581-159">Select **Containers**.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="09581-161">Dans le panneau Conteneurs, sélectionnez **Ajouter**et entrez le nom et les autorisations du conteneur.</span><span class="sxs-lookup"><span data-stu-id="09581-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="09581-162">Sélectionnez **Privé** pour les autorisations du conteneur.</span><span class="sxs-lookup"><span data-stu-id="09581-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="09581-163">Nous vous recommandons de créer un conteneur par référence que vous envisagez de publier.</span><span class="sxs-lookup"><span data-stu-id="09581-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="09581-165">Créer un compte de stockage à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="09581-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="09581-166">À l’aide de PowerShell, créez un compte de stockage au moyen de l’applet de commande [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) .</span><span class="sxs-lookup"><span data-stu-id="09581-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="09581-167">Ensuite, vous pouvez créer un conteneur dans ce compte de stockage au moyen de l’applet de commande [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) .</span><span class="sxs-lookup"><span data-stu-id="09581-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="09581-168">Ces commandes supposent que le contexte actuel du compte de stockage a déjà été défini dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09581-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="09581-169">Reportez-vous à [Configuration d’Azure PowerShell](marketplace-publishing-powershell-setup.md) pour plus d’informations sur la configuration de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09581-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="09581-170">Créer un compte de stockage à l’aide de l’outil en ligne de commande pour Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="09581-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="09581-171">Dans l’ [outil en ligne de commande Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), créez un compte de stockage comme suit :</span><span class="sxs-lookup"><span data-stu-id="09581-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="09581-172">Créez un conteneur comme suit :</span><span class="sxs-lookup"><span data-stu-id="09581-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="09581-173">Télécharger un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="09581-173">Upload a VHD</span></span>
<span data-ttu-id="09581-174">Une fois le compte de stockage et le conteneur créés, vous pouvez télécharger vos disques durs virtuels préparés.</span><span class="sxs-lookup"><span data-stu-id="09581-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="09581-175">Vous pouvez utiliser PowerShell, l’outil en ligne de commande Linux ou d’autres outils de gestion Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="09581-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="09581-176">Télécharger un disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="09581-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="09581-177">Utilisez l’applet de commande [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="09581-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="09581-178">Télécharger un disque dur virtuel à l’aide de l’outil en ligne de commande pour Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="09581-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="09581-179">Avec [l’outil en ligne de commande Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilisez la commande suivante : azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="09581-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="09581-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="09581-180">See also</span></span>
* [<span data-ttu-id="09581-181">Création d’une image de machine virtuelle pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="09581-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="09581-182">Configuration d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09581-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

