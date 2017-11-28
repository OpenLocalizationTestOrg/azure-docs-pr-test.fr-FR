---
title: "Gestion du Stockage Fichier Azure à partir du portail Azure | Microsoft Docs"
description: "Découvrez comment utiliser le portail Azure pour gérer le Stockage Fichier Azure."
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
ms.openlocfilehash: d5ffa7cff0a31e36f5a96aaa4b2d477fa39333fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="1007b-103">Utilisation du Stockage Fichier Azure à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1007b-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="1007b-104">Le [portail Azure](https://portal.azure.com) offre une interface utilisateur permettant de gérer le Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="1007b-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="1007b-105">Vous pouvez effectuer les actions suivantes à partir de votre navigateur web :</span><span class="sxs-lookup"><span data-stu-id="1007b-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="1007b-106">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="1007b-106">Create a File Share</span></span>
* <span data-ttu-id="1007b-107">Charger et télécharger des fichiers vers et à partir de votre partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="1007b-108">Surveiller l'utilisation réelle de chaque partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="1007b-109">Ajuster le quota de la taille de partage.</span><span class="sxs-lookup"><span data-stu-id="1007b-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="1007b-110">Copiez les commandes de montage servant à monter votre partage de fichiers à partir d’un client Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1007b-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="1007b-111">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="1007b-111">Create file share</span></span>
1. <span data-ttu-id="1007b-112">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1007b-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="1007b-113">Dans le menu de navigation, cliquez sur **Comptes de stockage** ou sur **Comptes de stockage (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="1007b-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Capture d’écran montrant comment créer un partage de fichiers dans le portail](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="1007b-115">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1007b-115">Choose your storage account.</span></span>

    ![Capture d’écran montrant comment créer un partage de fichiers dans le portail](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="1007b-117">Choisissez le service Fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-117">Choose "Files" service.</span></span>

    ![Capture d’écran montrant comment créer un partage de fichiers dans le portail](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="1007b-119">Cliquez sur Partages de fichiers et suivez le lien pour créer votre premier partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Capture d’écran montrant comment créer un partage de fichiers dans le portail](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="1007b-121">Renseignez le nom du partage de fichiers ainsi que sa taille (jusqu’à 5 120 Go) pour créer votre premier partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="1007b-122">Une fois le partage de fichiers créé, vous pouvez le monter à partir de n’importe quel système de fichiers prenant en charge SMB 2.1 ou SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="1007b-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="1007b-123">Vous pouvez cliquer sur **Quota** sur le partage de fichiers pour modifier la taille du fichier jusqu’à 5 120 Go.</span><span class="sxs-lookup"><span data-stu-id="1007b-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="1007b-124">Reportez-vous à la [Calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/) pour estimer le coût de stockage lié à l’utilisation du Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="1007b-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Capture d’écran montrant comment créer un partage de fichiers dans le portail](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="1007b-126">Charger et télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="1007b-126">Upload and download files</span></span>
1. <span data-ttu-id="1007b-127">Choisissez un partage de fichiers que vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="1007b-127">Choose one file share your have already created.</span></span>

    ![Capture d’écran montrant comment charger et télécharger des fichiers à partir du portail](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="1007b-129">Cliquez sur **Charger** pour ouvrir l’interface utilisateur pour le chargement des fichiers.</span><span class="sxs-lookup"><span data-stu-id="1007b-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Capture d’écran montrant comment charger des fichiers à partir du portail](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="1007b-131">Connexion au partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="1007b-131">Connect to file share</span></span>
-  <span data-ttu-id="1007b-132">Cliquez sur **Se connecter** pour accéder à la ligne de commande permettant de monter le partage de fichiers à partir de Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="1007b-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="1007b-133">Pour les utilisateurs Linux, vous pouvez également consulter [Utilisation du Stockage Fichier Azure avec Linux](../storage-how-to-use-files-linux.md) pour obtenir des instructions de montage supplémentaires pour les autres distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="1007b-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Capture d’écran montrant comment monter le partage de fichiers](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="1007b-135">Vous pouvez copier les commandes servant à monter le partage de fichiers sous Windows ou Linux et exécuter ce dernier à partir de votre machine virtuelle Azure ou de votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="1007b-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Capture d’écran qui montre les commandes de montage pour Windows et Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="1007b-137">**Conseil :**</span><span class="sxs-lookup"><span data-stu-id="1007b-137">**Tip:**</span></span>  
<span data-ttu-id="1007b-138">Pour obtenir la clé d’accès du compte de stockage permettant le montage, cliquez sur **Afficher les clés d’accès pour ce compte de stockage** au bas de la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="1007b-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="1007b-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1007b-139">See also</span></span>
<span data-ttu-id="1007b-140">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="1007b-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="1007b-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="1007b-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="1007b-142">Résolution des problèmes sur Windows</span><span class="sxs-lookup"><span data-stu-id="1007b-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="1007b-143">Résolution des problèmes sur Linux</span><span class="sxs-lookup"><span data-stu-id="1007b-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    