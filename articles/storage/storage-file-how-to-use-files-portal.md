---
title: "aaaHow toomanage stockage Azure Files à partir de hello portail Azure | Documents Microsoft"
description: "Découvrez le stockage de fichiers Azure toouse hello toomanage portail Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="01be7-103">Comment le stockage de fichier Azure toouse de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="01be7-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="01be7-104">Hello [portail Azure](https://portal.azure.com) fournit une interface utilisateur pour la gestion du stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="01be7-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="01be7-105">Vous pouvez effectuer hello suivant des actions dans votre navigateur web :</span><span class="sxs-lookup"><span data-stu-id="01be7-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="01be7-106">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="01be7-106">Create a File Share</span></span>
* <span data-ttu-id="01be7-107">Télécharger des fichiers tooand à partir de votre partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="01be7-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="01be7-108">Surveillez l’utilisation réelle de hello de chaque partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="01be7-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="01be7-109">Ajustez le quota de taille de partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="01be7-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="01be7-110">Copiez hello montage commandes toouse toomount de partage de vos fichiers à partir d’un client Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="01be7-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="01be7-111">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="01be7-111">Create file share</span></span>
1. <span data-ttu-id="01be7-112">Se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="01be7-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="01be7-113">Dans le menu de navigation hello, cliquez sur **comptes de stockage** ou **comptes de stockage (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="01be7-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="01be7-115">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="01be7-115">Choose your storage account.</span></span>

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="01be7-117">Choisissez le service Fichiers.</span><span class="sxs-lookup"><span data-stu-id="01be7-117">Choose "Files" service.</span></span>

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="01be7-119">Cliquez sur « Partages de fichiers » et suivez les toocreate de lien de hello partager de votre premier fichier.</span><span class="sxs-lookup"><span data-stu-id="01be7-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="01be7-121">Renseignez nom de partage de fichiers hello et taille hello de toocreate de partage (haut too5120 Go) fichier hello votre première partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="01be7-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="01be7-122">Une fois que le partage de fichiers hello a été créé, vous pouvez le monter à partir de n’importe quel système de fichiers qui prend en charge SMB 2.1 ou SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="01be7-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="01be7-123">Vous pouvez cliquer sur **Quota** hello taille de fichier partage toochange hello du fichier hello des too5120 go.</span><span class="sxs-lookup"><span data-stu-id="01be7-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="01be7-124">Reportez-vous trop[calculatrice de tarification Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello stockage à moindre coût de l’utilisation du stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="01be7-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Capture d’écran qui montre comment partager des fichiers de toocreate dans le portail de hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="01be7-126">Charger et télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="01be7-126">Upload and download files</span></span>
1. <span data-ttu-id="01be7-127">Choisissez un partage de fichiers que vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="01be7-127">Choose one file share your have already created.</span></span>

    ![Capture d’écran qui illustre comment tooupload et téléchargez des fichiers à partir de hello portail](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="01be7-129">Cliquez sur **télécharger** pour ouvrir l’interface utilisateur de hello pour télécharger les fichiers.</span><span class="sxs-lookup"><span data-stu-id="01be7-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Capture d’écran qui illustre comment les fichiers à partir du portail de hello tooupload](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="01be7-131">Se connecter toofile partage</span><span class="sxs-lookup"><span data-stu-id="01be7-131">Connect toofile share</span></span>
-  <span data-ttu-id="01be7-132">Cliquez sur **connexion** pour obtenir la ligne de commande hello montage hello partage de fichiers à partir de Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="01be7-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="01be7-133">Pour les utilisateurs Linux, vous pouvez également faire référence trop[comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md) pour plus d’instructions de montage pour les autres distributions de Linux.</span><span class="sxs-lookup"><span data-stu-id="01be7-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Capture d’écran qui illustre comment toomount hello partage de fichiers](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="01be7-135">Vous pouvez copier hello commandes permettant de monter le fichier de partage sous Windows ou Linux et exécuter de votre ordinateur local ou de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="01be7-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Capture d’écran qui affiche les commandes de montage hello pour Windows et Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="01be7-137">**Conseil :**</span><span class="sxs-lookup"><span data-stu-id="01be7-137">**Tip:**</span></span>  
<span data-ttu-id="01be7-138">clé toofind hello accès de montage, cliquez sur **clés d’accès en lecture pour ce compte de stockage** bas hello hello page de connexion.</span><span class="sxs-lookup"><span data-stu-id="01be7-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="01be7-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="01be7-139">See also</span></span>
<span data-ttu-id="01be7-140">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="01be7-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="01be7-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="01be7-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="01be7-142">Dépannage</span><span class="sxs-lookup"><span data-stu-id="01be7-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)