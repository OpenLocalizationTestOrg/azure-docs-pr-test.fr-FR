---
title: "aaaUpload disque dur virtuel du fichier à l’aide de Microsoft Azure Storage Explorer de tooAzure DevTest Labs | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de l’Explorateur de stockage Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="9e33f-103">Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de l’Explorateur de stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9e33f-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="9e33f-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé.</span><span class="sxs-lookup"><span data-stu-id="9e33f-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="9e33f-105">Cet article explique comment toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) compte de stockage du laboratoire tooa de fichiers tooupload un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9e33f-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="9e33f-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9e33f-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="9e33f-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="9e33f-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="9e33f-108">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="9e33f-108">Step-by-step instructions</span></span>

<span data-ttu-id="9e33f-109">Hello après le parcours des étapes vous aide à télécharger un disque dur virtuel laboratoires tooDevTest à l’aide du fichier [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9e33f-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="9e33f-110">[Téléchargez et installez la version la plus récente de Microsoft Azure Storage Explorer de hello hello](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="9e33f-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="9e33f-111">Obtenir le nom de hello de du laboratoire hello compte de stockage à l’aide de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="9e33f-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="9e33f-112">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9e33f-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="9e33f-113">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="9e33f-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="9e33f-114">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="9e33f-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="9e33f-115">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="9e33f-116">Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="9e33f-117">Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="9e33f-118">Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="9e33f-119">Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Télécharger un disque dur virtuel à l’aide de PowerShell][0]
    
    1. <span data-ttu-id="9e33f-121">Hello **télécharger une image à l’aide de PowerShell** panneau affiche un appel toohello **Add-AzureVhd** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e33f-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="9e33f-122">Hello du premier paramètre (*Destination*) contient le nom de compte de stockage hello pour laboratoire hello Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="9e33f-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="9e33f-123">https://<NOM-COMPTE-STOCKAGE>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="9e33f-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="9e33f-124">Prenez note du nom de compte de stockage hello qu’il est utilisé dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9e33f-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="9e33f-125">Se connecter tooan compte d’abonnement Azure à l’aide de l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="9e33f-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="9e33f-126">Ce dernier prend en charge plusieurs options de connexion.</span><span class="sxs-lookup"><span data-stu-id="9e33f-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="9e33f-127">Cette section illustre le compte de stockage qui se connecte tooa associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9e33f-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="9e33f-128">toosee hello d’autres options de connexion pris en charge par l’Explorateur de stockage, consultez l’article toohello [prise en main de l’Explorateur de stockage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9e33f-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="9e33f-129">Ouvrez l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="9e33f-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="9e33f-130">Dans l’Explorateur de stockage, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![paramètres de compte Azure][1]
    
    1. <span data-ttu-id="9e33f-132">volet de gauche de Hello affiche les comptes Microsoft hello que vous avez ouvert une session.</span><span class="sxs-lookup"><span data-stu-id="9e33f-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="9e33f-133">tooconnect tooanother compte, sélectionnez **ajouter un compte**et suivez les toosign de boîtes de dialogue hello avec un compte Microsoft associé au moins un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9e33f-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Ajouter un compte][2]
    
    1. <span data-ttu-id="9e33f-135">Une fois que vous vous connectez avec succès avec un compte Microsoft, volet de gauche hello remplit avec hello Azure abonnements associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="9e33f-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="9e33f-136">Sélectionnez hello abonnements Azure avec lequel vous souhaitez toowork, puis sélectionnez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="9e33f-137">(En sélectionnant **tous les abonnements** bascules hello sélection de l’ensemble ou aucun des hello répertorié abonnements Azure.)</span><span class="sxs-lookup"><span data-stu-id="9e33f-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Sélectionner les abonnements Azure][3]
    
    1. <span data-ttu-id="9e33f-139">volet de gauche Hello affiche les comptes de stockage hello associées aux abonnements Azure de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9e33f-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Abonnements Azure sélectionnés][4]

1. <span data-ttu-id="9e33f-141">Recherchez le compte de stockage du laboratoire hello :</span><span class="sxs-lookup"><span data-stu-id="9e33f-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="9e33f-142">Dans le volet gauche de l’Explorateur de stockage hello, recherchez et développez le nœud hello pour hello abonnement Azure propriétaire du lab de hello.</span><span class="sxs-lookup"><span data-stu-id="9e33f-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="9e33f-143">Sous le nœud de l’abonnement hello, développez **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="9e33f-144">Développez les nœuds de tooreveal du laboratoire hello stockage compte nœud pour **conteneurs d’objets Blob**, **des partages de fichiers**, **les files d’attente**, et **Tables**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="9e33f-145">Développez hello **conteneurs d’objets Blob** nœud.</span><span class="sxs-lookup"><span data-stu-id="9e33f-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="9e33f-146">Sélectionnez hello téléchargements blob conteneur toodisplay son contenu dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="9e33f-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Répertoire du téléchargement][5]

1. <span data-ttu-id="9e33f-148">Téléchargez le fichier de disque dur virtuel de hello à l’aide de l’Explorateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="9e33f-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="9e33f-149">Dans le volet droit de l’Explorateur de stockage hello, vous devez voir une liste d’objets BLOB de hello Bonjour **télécharge** conteneur d’objets blob de du laboratoire hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9e33f-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="9e33f-150">Dans la barre d’outils de l’éditeur hello blob, sélectionnez **télécharger**</span><span class="sxs-lookup"><span data-stu-id="9e33f-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Bouton Télécharger][6]
    
    1. <span data-ttu-id="9e33f-152">À partir de hello **télécharger** menu déroulant, sélectionnez **télécharger des fichiers...** .</span><span class="sxs-lookup"><span data-stu-id="9e33f-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="9e33f-153">Sur hello **télécharger des fichiers** boîte de dialogue, les points de suspension hello select.</span><span class="sxs-lookup"><span data-stu-id="9e33f-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Sélectionner un fichier][8]  

    1. <span data-ttu-id="9e33f-155">Sur hello **tooupload de sélection de fichiers** boîte de dialogue Parcourir toohello souhaité fichier VHD, sélectionnez-le, puis sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="9e33f-156">Lorsque retourné toohello **télécharger des fichiers** boîte de dialogue, modification **type d’objets Blob** trop**objet Blob de pages**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="9e33f-157">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="9e33f-157">Select **Upload**.</span></span>

        ![Sélectionner un fichier][9]  
    
    1. <span data-ttu-id="9e33f-159">Hello Explorateur de stockage **le journal d’activité** volet affiche l’état du téléchargement hello (ainsi que des liens toocancel hello chargement).</span><span class="sxs-lookup"><span data-stu-id="9e33f-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="9e33f-160">processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="9e33f-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![État du téléchargement de fichier][10]  

## <a name="next-steps"></a><span data-ttu-id="9e33f-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e33f-162">Next steps</span></span>

- [<span data-ttu-id="9e33f-163">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9e33f-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="9e33f-164">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e33f-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
