---
title: "Télécharger un fichier de disque dur virtuel vers Azure DevTest Labs avec l’Explorateur de stockage Microsoft Azure | Microsoft Docs"
description: "Télécharger le fichier de disque dur virtuel dans le compte de stockage du laboratoire avec l’explorateur de stockage Microsoft Azure"
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
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="00c02-103">Télécharger le fichier de disque dur virtuel dans le compte de stockage du laboratoire avec l’explorateur de stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="00c02-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="00c02-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisés pour créer des images personnalisées, qui servent à approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="00c02-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="00c02-105">Cet article montre comment utiliser l’[Explorateur de stockage Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) pour charger un fichier de disque dur virtuel vers le compte de stockage d’un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="00c02-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="00c02-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, consultez la [section Étapes suivantes](#next-steps) qui répertorie quelques articles qui expliquent comment créer une image personnalisée à partir du fichier de disque dur virtuel téléchargé.</span><span class="sxs-lookup"><span data-stu-id="00c02-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="00c02-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="00c02-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="00c02-108">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="00c02-108">Step-by-step instructions</span></span>

<span data-ttu-id="00c02-109">Les étapes suivantes vous guident lors du téléchargement d’un fichier de disque dur virtuel dans Azure DevTest Labs avec l’[Explorateur de stockage Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="00c02-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="00c02-110">[Téléchargez et installez la version la plus récente de l’Explorateur de stockage Microsoft Azure](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="00c02-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="00c02-111">Obtenez le nom du compte de stockage du laboratoire à l’aide du portail Azure :</span><span class="sxs-lookup"><span data-stu-id="00c02-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="00c02-112">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="00c02-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="00c02-113">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="00c02-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="00c02-114">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="00c02-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="00c02-115">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="00c02-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="00c02-116">Dans le panneau **Configuration** du laboratoire, sélectionnez **Custom images (VHDs)** (Images personnalisées (disques durs virtuels)).</span><span class="sxs-lookup"><span data-stu-id="00c02-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="00c02-117">Dans le panneau **Images personnalisées**, sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="00c02-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="00c02-118">Dans le panneau **Image personnalisée**, sélectionnez **Disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="00c02-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="00c02-119">Dans le panneau **Disque dur virtuel**, sélectionnez **Upload a VHD using PowerShell** (Télécharger un disque dur virtuel à l’aide de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="00c02-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Télécharger un disque dur virtuel à l’aide de PowerShell][0]
    
    1. <span data-ttu-id="00c02-121">Le panneau **Upload an image using PowerShell** (Télécharger une image à l’aide de PowerShell) affiche un appel à l’applet de commande **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="00c02-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="00c02-122">Le premier paramètre (*Destination*) contient le nom du compte de stockage du laboratoire au format suivant :</span><span class="sxs-lookup"><span data-stu-id="00c02-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="00c02-123">https://<NOM-COMPTE-STOCKAGE>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="00c02-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="00c02-124">Prenez note du nom du compte de stockage, car vous en aurez besoin dans des étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="00c02-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="00c02-125">Connectez-vous au compte lié à un abonnement Azure à l’aide de l’Explorateur de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="00c02-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="00c02-126">Ce dernier prend en charge plusieurs options de connexion.</span><span class="sxs-lookup"><span data-stu-id="00c02-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="00c02-127">Cette section montre la connexion à un compte de stockage associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="00c02-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="00c02-128">Pour voir les autres options de connexion prises en charge par l’Explorateur de stockage, consultez [Prise en main de l’Explorateur de stockage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="00c02-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="00c02-129">Ouvrez l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="00c02-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="00c02-130">Dans l’Explorateur de stockage, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="00c02-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![paramètres de compte Azure][1]
    
    1. <span data-ttu-id="00c02-132">Le volet gauche affiche les comptes Microsoft auxquels vous vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="00c02-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="00c02-133">Pour vous connecter à un autre compte, sélectionnez **Ajouter un compte**et suivez les indications des boîtes de dialogue pour vous connecter avec un compte Microsoft associé à un ou plusieurs abonnements Azure actifs.</span><span class="sxs-lookup"><span data-stu-id="00c02-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Ajouter un compte][2]
    
    1. <span data-ttu-id="00c02-135">Une fois que vous êtes connecté avec un compte Microsoft, le volet gauche indique les abonnements Azure associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="00c02-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="00c02-136">Sélectionnez les abonnements Azure que vous souhaitez utiliser, puis sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="00c02-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="00c02-137">(La case à cocher **Tous les abonnements** permet de sélectionner ou de désélectionner l’ensemble des abonnements Azure répertoriés.)</span><span class="sxs-lookup"><span data-stu-id="00c02-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Sélectionner les abonnements Azure][3]
    
    1. <span data-ttu-id="00c02-139">Le volet gauche affiche les comptes de stockage associés aux abonnements Azure sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="00c02-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Abonnements Azure sélectionnés][4]

1. <span data-ttu-id="00c02-141">Recherchez le compte de stockage du laboratoire :</span><span class="sxs-lookup"><span data-stu-id="00c02-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="00c02-142">Dans le volet gauche de l’Explorateur de stockage, localisez et développez le nœud de l’abonnement Azure qui possède le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="00c02-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="00c02-143">Sous le nœud de l’abonnement, développez **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="00c02-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="00c02-144">Développez le nœud de compte de stockage du laboratoire pour afficher les nœuds pour **Conteneurs d’objets blob**, **Partages de fichiers**, **Files d’attente** et **Tables**.</span><span class="sxs-lookup"><span data-stu-id="00c02-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="00c02-145">Développez le nœud **Conteneurs d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="00c02-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="00c02-146">Sélectionnez le conteneur d’objets blob de téléchargements (uploads) pour afficher son contenu dans le volet droit.</span><span class="sxs-lookup"><span data-stu-id="00c02-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Répertoire du téléchargement][5]

1. <span data-ttu-id="00c02-148">Téléchargez le fichier de disque dur virtuel à l’aide de l’Explorateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="00c02-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="00c02-149">Dans le volet droit de l’Explorateur de stockage, vous devez voir une liste de blobs dans le conteneur de blobs **uploads** du compte de stockage du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="00c02-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="00c02-150">Dans la barre d’outils de l’éditeur de blobs, sélectionnez **Télécharger**</span><span class="sxs-lookup"><span data-stu-id="00c02-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Bouton Télécharger][6]
    
    1. <span data-ttu-id="00c02-152">Dans le menu déroulant **Télécharger**, sélectionnez **Télécharger des fichiers...**.</span><span class="sxs-lookup"><span data-stu-id="00c02-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="00c02-153">Dans la boîte de dialogue **Télécharger des fichiers**, sélectionnez les points de suspension.</span><span class="sxs-lookup"><span data-stu-id="00c02-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Sélectionner un fichier][8]  

    1. <span data-ttu-id="00c02-155">Dans la boîte de dialogue **Sélectionner les fichiers à télécharger**, recherchez le fichier de disque dur virtuel souhaité, sélectionnez-le, puis sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="00c02-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="00c02-156">Lorsque vous êtes à nouveau dans la boîte de dialogue **Télécharger des fichiers**, définissez **Type d’objet BLOB** sur **Objet blob de pages**.</span><span class="sxs-lookup"><span data-stu-id="00c02-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="00c02-157">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="00c02-157">Select **Upload**.</span></span>

        ![Sélectionner un fichier][9]  
    
    1. <span data-ttu-id="00c02-159">Le volet **Journal d’activité** de l’Explorateur de stockage affiche l’état du téléchargement (ainsi que des liens permettant d’annuler le téléchargement).</span><span class="sxs-lookup"><span data-stu-id="00c02-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="00c02-160">Le processus de téléchargement d’un fichier de disque dur virtuel peut durer un certain temps en fonction de sa taille et de votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="00c02-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![État du téléchargement de fichier][10]  

## <a name="next-steps"></a><span data-ttu-id="00c02-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00c02-162">Next steps</span></span>

- [<span data-ttu-id="00c02-163">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="00c02-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="00c02-164">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="00c02-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
