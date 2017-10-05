---
title: "Utilisation de l’Explorateur de stockage (version préliminaire) avec Azure Stockage Fichier | Microsoft Docs"
description: "Apprenez à utiliser l’Explorateur de stockage (version préliminaire) pour travailler avec des fichiers et des partages de fichiers."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="22ce1-103">Utilisation de l’Explorateur de stockage (version préliminaire) avec Azure Stockage Fichier</span><span class="sxs-lookup"><span data-stu-id="22ce1-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="22ce1-104">Azure Stockage Fichier est un service qui propose des partages de fichiers dans le cloud en utilisant le protocole SMB standard.</span><span class="sxs-lookup"><span data-stu-id="22ce1-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="22ce1-105">Les protocoles SMB 2.1 et SMB 3.0 sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="22ce1-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="22ce1-106">Avec le stockage de fichiers Azure, vous pouvez migrer vers Azure des applications héritées qui s’appuient sur des partages de fichiers, rapidement et sans réécritures onéreuses.</span><span class="sxs-lookup"><span data-stu-id="22ce1-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="22ce1-107">Vous pouvez utiliser Stockage Fichier pour exposer les données publiquement au monde ou pour le stockage privé de données d’applications.</span><span class="sxs-lookup"><span data-stu-id="22ce1-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="22ce1-108">Dans cet article, vous allez apprendre à utiliser l’Explorateur de stockage (version préliminaire) pour travailler avec des fichiers et des partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22ce1-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="22ce1-109">Prerequisites</span></span>

<span data-ttu-id="22ce1-110">Pour pouvoir suivre les étapes de cet article, vous devrez :</span><span class="sxs-lookup"><span data-stu-id="22ce1-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="22ce1-111">Télécharger et installer l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="22ce1-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="22ce1-112">Vous connecter à un service ou un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="22ce1-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="22ce1-113">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-113">Create a File Share</span></span>

<span data-ttu-id="22ce1-114">Tous les fichiers doivent résider dans un partage de fichiers, c’est-à-dire un simple regroupement logique de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="22ce1-115">Un compte peut contenir un nombre illimité de partages de fichiers, et chaque partage de fichiers peut stocker un nombre illimité de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="22ce1-116">Les étapes suivantes expliquent comment créer un partage de fichiers dans l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="22ce1-117">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-118">Dans le volet gauche, développez le compte de stockage dans lequel vous souhaitez créer le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="22ce1-119">Cliquez avec le bouton droit sur **Partages de fichiers**, puis sélectionnez **Créer un partage de fichiers** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="22ce1-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Créer un partage de fichiers](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="22ce1-121">Une zone de texte apparaît sous le dossier **Partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="22ce1-122">Entrez le nom de votre partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-122">Enter the name for your file share.</span></span> <span data-ttu-id="22ce1-123">Consultez la section relative aux [règles d’affectation des noms de partages de fichiers](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) pour obtenir la liste des règles et restrictions applicables aux noms de partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Affectation d’un nom au partage](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="22ce1-125">Appuyez ensuite sur **Entrée** pour créer le partage de fichiers, ou sur **ÉCHAP** pour annuler.</span><span class="sxs-lookup"><span data-stu-id="22ce1-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="22ce1-126">Une fois le partage de fichiers créé, il apparaît sous le dossier **Partages de fichiers** correspondant au compte de stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="22ce1-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![Nouveau partage](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="22ce1-128">Afficher le contenu d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-128">View a file share's contents</span></span>

<span data-ttu-id="22ce1-129">Les partages de fichiers contiennent des fichiers et des dossiers (qui peuvent également contenir des fichiers).</span><span class="sxs-lookup"><span data-stu-id="22ce1-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="22ce1-130">Les étapes suivantes expliquent comment afficher le contenu d’un partage de fichiers dans l’Explorateur de stockage (version préliminaire) :</span><span class="sxs-lookup"><span data-stu-id="22ce1-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="22ce1-131">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-132">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="22ce1-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="22ce1-133">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="22ce1-134">Cliquez avec le bouton droit sur le partage de fichiers que vous souhaitez afficher puis, dans le menu contextuel, sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="22ce1-135">Vous pouvez également double-cliquer sur le partage de fichiers que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="22ce1-135">You can also double-click the file share you wish to view.</span></span>

    ![Ouvrir le partage](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="22ce1-137">Le volet principal affiche le contenu du partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-137">The main pane will display the file share's contents.</span></span>
    
    ![Contenu d’un partage de fichiers](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="22ce1-139">Supprimer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-139">Delete a file share</span></span>

<span data-ttu-id="22ce1-140">Vous pouvez facilement créer et supprimer des partages de fichiers selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="22ce1-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="22ce1-141">(pour savoir comment supprimer des fichiers, reportez-vous à la section [Gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="22ce1-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="22ce1-142">Les étapes suivantes expliquent comment supprimer un partage de fichiers dans l’Explorateur de stockage (version préliminaire) :</span><span class="sxs-lookup"><span data-stu-id="22ce1-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="22ce1-143">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-144">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="22ce1-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="22ce1-145">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="22ce1-146">Cliquez avec le bouton droit sur le partage de fichiers que vous souhaitez supprimer puis, dans le menu contextuel, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="22ce1-147">Vous pouvez également appuyer sur **Supprimer** pour supprimer le partage de fichiers actuellement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="22ce1-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Supprimer](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="22ce1-149">Cliquez sur **Oui** dans la boîte de dialogue de confirmation.</span><span class="sxs-lookup"><span data-stu-id="22ce1-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Boîte de dialogue de confirmation](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="22ce1-151">Copier un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-151">Copy a file share</span></span>

<span data-ttu-id="22ce1-152">L’Explorateur de stockage (version préliminaire) vous permet de copier un partage de fichiers dans le Presse-papiers, puis de coller ce partage de fichiers dans un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="22ce1-153">(pour savoir comment copier des fichiers, reportez-vous à la section [Gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="22ce1-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="22ce1-154">Les étapes suivantes expliquent comment copier un partage de fichiers d’un compte de stockage à un autre.</span><span class="sxs-lookup"><span data-stu-id="22ce1-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="22ce1-155">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-156">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers que vous souhaitez copier.</span><span class="sxs-lookup"><span data-stu-id="22ce1-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="22ce1-157">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="22ce1-158">Cliquez avec le bouton droit sur le partage de fichiers que vous souhaitez copier puis, dans le menu contextuel, sélectionnez **Copy File Share** (Copier le partage de fichiers).</span><span class="sxs-lookup"><span data-stu-id="22ce1-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Copier le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="22ce1-160">Cliquez avec le bouton droit sur le compte de stockage cible dans lequel vous souhaitez coller le partage de fichiers puis, dans le menu contextuel, sélectionnez **Paste File Share** (Coller le partage de fichiers).</span><span class="sxs-lookup"><span data-stu-id="22ce1-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Coller le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="22ce1-162">Obtenir la signature d’accès partagé (SAP) pour un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-162">Get the SAS for a file share</span></span>

<span data-ttu-id="22ce1-163">Une [signature d’accès partagé (SAP)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fournit un accès délégué aux ressources de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="22ce1-164">Cela vous permet d’octroyer à un client des autorisations d’accès limité à des objets de votre compte de stockage pendant une période donnée et avec un ensemble défini d’autorisations, sans partager les clés d’accès de votre compte.</span><span class="sxs-lookup"><span data-stu-id="22ce1-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="22ce1-165">Les étapes suivantes expliquent comment créer une signature d’accès partagé pour un partage de fichiers :</span><span class="sxs-lookup"><span data-stu-id="22ce1-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="22ce1-166">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-167">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers pour lequel vous souhaitez obtenir une SAP.</span><span class="sxs-lookup"><span data-stu-id="22ce1-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="22ce1-168">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="22ce1-169">Cliquez avec le bouton droit sur le partage de fichiers puis, dans le menu contextuel, sélectionnez **Get Shared Access Signature** (Obtenir une signature d’accès partagé).</span><span class="sxs-lookup"><span data-stu-id="22ce1-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Obtenir une signature d’accès partagé](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="22ce1-171">Dans la boîte de dialogue **Signature d’accès partagé** , spécifiez la stratégie, les dates de début et d’expiration, le fuseau horaire et les niveaux d’accès de la ressource.</span><span class="sxs-lookup"><span data-stu-id="22ce1-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![Boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="22ce1-173">Une fois les options SAP spécifiées, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="22ce1-174">Vous accédez alors à une deuxième boîte de dialogue **Signature d’accès partagé** dans laquelle vous pouvez visualiser le partage de fichiers, ainsi que les URL et les chaînes de requête que vous pouvez utiliser pour accéder à la ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="22ce1-175">Sélectionnez **Copier** en regard de l’URL que vous souhaitez copier dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Deuxième boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="22ce1-177">Lorsque vous avez terminé, sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="22ce1-178">Gérer les stratégies d’accès d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="22ce1-179">Les étapes suivantes montrent comment gérer (ajouter et supprimer) les stratégies d’accès d’un partage de fichiers :</span><span class="sxs-lookup"><span data-stu-id="22ce1-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="22ce1-180">Les stratégies d’accès sont utilisées pour créer des URL SAP permettant d’accéder à la ressource du fichier de stockage pendant une période définie.</span><span class="sxs-lookup"><span data-stu-id="22ce1-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="22ce1-181">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="22ce1-182">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers pour lequel vous souhaitez gérer les stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="22ce1-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="22ce1-183">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="22ce1-184">Sélectionnez le partage de fichiers souhaité puis, dans le menu contextuel, sélectionnez **Manage Access Policies** (Gérer les stratégies d’accès).</span><span class="sxs-lookup"><span data-stu-id="22ce1-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Gérer les stratégies d’accès - Menu contextuel](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="22ce1-186">La boîte de dialogue **Stratégies d’accès** répertorie les stratégies d’accès déjà créées pour le partage de fichiers sélectionné.</span><span class="sxs-lookup"><span data-stu-id="22ce1-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Stratégies d’accès](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="22ce1-188">Suivez ces étapes en fonction de la tâche de gestion des stratégies d’accès :</span><span class="sxs-lookup"><span data-stu-id="22ce1-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="22ce1-189">**Ajouter une nouvelle stratégie d’accès** : sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="22ce1-190">Une fois la stratégie générée, la boîte de dialogue **Stratégies d’accès** affiche la stratégie d’accès que vous venez d’ajouter (avec les paramètres par défaut).</span><span class="sxs-lookup"><span data-stu-id="22ce1-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="22ce1-191">**Modifier une stratégie d’accès** : apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="22ce1-192">**Supprimer une stratégie d’accès** : sélectionnez **Supprimer** en regard de la stratégie d’accès à supprimer.</span><span class="sxs-lookup"><span data-stu-id="22ce1-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="22ce1-193">Créez une URL de SAP à l’aide de la stratégie d’accès que vous avez élaborée précédemment :</span><span class="sxs-lookup"><span data-stu-id="22ce1-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Obtenir une SAP](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Propriétés et nom de la SAP](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="22ce1-196">Gestion des fichiers dans un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="22ce1-196">Managing files in a file share</span></span>

<span data-ttu-id="22ce1-197">Une fois que vous avez créé un partage de fichiers, vous pouvez effectuer de nombreuses tâches, par exemple charger un fichier dans ce partage de fichiers, télécharger un fichier sur votre ordinateur local, ouvrir un fichier sur votre ordinateur local, etc.</span><span class="sxs-lookup"><span data-stu-id="22ce1-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="22ce1-198">Les étapes suivantes expliquent comment gérer les fichiers (et les dossiers) dans un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="22ce1-199">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="22ce1-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="22ce1-200">Dans le volet gauche, développez le compte de stockage contenant le partage de fichiers que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="22ce1-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="22ce1-201">Développez le dossier **Partages de fichiers** du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22ce1-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="22ce1-202">Double-cliquez sur le partage de fichiers que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="22ce1-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="22ce1-203">Le volet principal affiche le contenu du partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-203">The main pane will display the file share's contents.</span></span>

    ![Contenu d’un partage de fichiers](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="22ce1-205">Le volet principal affiche le contenu du partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="22ce1-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="22ce1-206">Suivez ces étapes en fonction de la tâche que vous souhaitez effectuer :</span><span class="sxs-lookup"><span data-stu-id="22ce1-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="22ce1-207">**Charger des fichiers dans un partage de fichiers**</span><span class="sxs-lookup"><span data-stu-id="22ce1-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="22ce1-208">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-208">a.</span></span>  <span data-ttu-id="22ce1-209">Dans la barre d’outils du volet principal, sélectionnez **Télécharger**, puis **Télécharger des fichiers** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="22ce1-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Charger des fichiers](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="22ce1-211">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-211">b.</span></span> <span data-ttu-id="22ce1-212">Dans la boîte de dialogue **Télécharger des fichiers**, sélectionnez le bouton des points de suspension (**…**) situé sur le côté droit de la zone **Fichiers** pour sélectionner les fichiers que vous souhaitez charger.</span><span class="sxs-lookup"><span data-stu-id="22ce1-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Ajout de fichiers](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="22ce1-214">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-214">c.</span></span> <span data-ttu-id="22ce1-215">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-215">Select **Upload**.</span></span>

    - <span data-ttu-id="22ce1-216">**Charger un dossier dans un partage de fichiers**</span><span class="sxs-lookup"><span data-stu-id="22ce1-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="22ce1-217">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-217">a.</span></span> <span data-ttu-id="22ce1-218">Dans la barre d’outils du volet principal, sélectionnez **Télécharger**, puis **Télécharger un dossier** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="22ce1-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Télécharger un dossier - Menu](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="22ce1-220">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-220">b.</span></span> <span data-ttu-id="22ce1-221">Dans la boîte de dialogue **Télécharger un dossier**, sélectionnez le bouton des points de suspension (**…**) situé sur le côté droit de la zone **Dossier** pour sélectionner le dossier que vous souhaitez charger.</span><span class="sxs-lookup"><span data-stu-id="22ce1-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="22ce1-222">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-222">c.</span></span> <span data-ttu-id="22ce1-223">Si vous le souhaitez, spécifiez un dossier cible dans lequel charger le contenu du dossier sélectionné.</span><span class="sxs-lookup"><span data-stu-id="22ce1-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="22ce1-224">Si le dossier cible n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="22ce1-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="22ce1-225">d.</span><span class="sxs-lookup"><span data-stu-id="22ce1-225">d.</span></span> <span data-ttu-id="22ce1-226">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-226">Select **Upload**.</span></span>

    - <span data-ttu-id="22ce1-227">**Télécharger un fichier sur votre ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="22ce1-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="22ce1-228">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-228">a.</span></span> <span data-ttu-id="22ce1-229">Sélectionnez le fichier que vous souhaitez télécharger.</span><span class="sxs-lookup"><span data-stu-id="22ce1-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="22ce1-230">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-230">b.</span></span> <span data-ttu-id="22ce1-231">Dans la barre d’outils du volet principal, sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="22ce1-232">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-232">c.</span></span> <span data-ttu-id="22ce1-233">Dans la boîte de dialogue **Specify where to save the downloaded file** (Indiquer où enregistrer le fichier téléchargé), spécifiez l’emplacement dans lequel vous souhaitez enregistrer le fichier téléchargé ainsi que le nom que vous souhaitez lui donner.</span><span class="sxs-lookup"><span data-stu-id="22ce1-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="22ce1-234">d.</span><span class="sxs-lookup"><span data-stu-id="22ce1-234">d.</span></span> <span data-ttu-id="22ce1-235">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-235">Select **Save**.</span></span>

    - <span data-ttu-id="22ce1-236">**Ouvrir un fichier sur votre ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="22ce1-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="22ce1-237">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-237">a.</span></span>  <span data-ttu-id="22ce1-238">Sélectionnez le fichier que vous souhaitez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="22ce1-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="22ce1-239">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-239">b.</span></span>  <span data-ttu-id="22ce1-240">Dans la barre d’outils du volet principal, sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="22ce1-241">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-241">c.</span></span>  <span data-ttu-id="22ce1-242">Le fichier est téléchargé et ouvert à l’aide de l’application associée au type de fichier sous-jacent du fichier.</span><span class="sxs-lookup"><span data-stu-id="22ce1-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="22ce1-243">**Copier un fichier dans le Presse-papiers**</span><span class="sxs-lookup"><span data-stu-id="22ce1-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="22ce1-244">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-244">a.</span></span> <span data-ttu-id="22ce1-245">Sélectionnez le fichier que vous souhaitez copier.</span><span class="sxs-lookup"><span data-stu-id="22ce1-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="22ce1-246">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-246">b.</span></span> <span data-ttu-id="22ce1-247">Dans la barre d’outils du volet principal, sélectionnez **Copier**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="22ce1-248">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-248">c.</span></span> <span data-ttu-id="22ce1-249">Dans le volet de gauche, accédez à un autre partage de fichiers et double-cliquez dessus pour l’afficher dans le volet principal.</span><span class="sxs-lookup"><span data-stu-id="22ce1-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="22ce1-250">d.</span><span class="sxs-lookup"><span data-stu-id="22ce1-250">d.</span></span> <span data-ttu-id="22ce1-251">Dans la barre d’outils du volet principal, sélectionnez **Coller** pour créer une copie du fichier.</span><span class="sxs-lookup"><span data-stu-id="22ce1-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="22ce1-252">**Supprimer un fichier**</span><span class="sxs-lookup"><span data-stu-id="22ce1-252">**Delete a file**</span></span>

        <span data-ttu-id="22ce1-253">a.</span><span class="sxs-lookup"><span data-stu-id="22ce1-253">a.</span></span> <span data-ttu-id="22ce1-254">Sélectionnez le fichier que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="22ce1-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="22ce1-255">b.</span><span class="sxs-lookup"><span data-stu-id="22ce1-255">b.</span></span> <span data-ttu-id="22ce1-256">Dans la barre d’outils du volet principal, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="22ce1-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="22ce1-257">c.</span><span class="sxs-lookup"><span data-stu-id="22ce1-257">c.</span></span> <span data-ttu-id="22ce1-258">Cliquez sur **Oui** dans la boîte de dialogue de confirmation.</span><span class="sxs-lookup"><span data-stu-id="22ce1-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22ce1-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="22ce1-259">Next steps</span></span>

- <span data-ttu-id="22ce1-260">Consultez les [dernières notes de publication et vidéos de l’Explorateur de stockage (version préliminaire)](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="22ce1-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="22ce1-261">Découvrez comment [créer des applications à l’aide d'objets blob, de tables, de files d’attente et de fichiers Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="22ce1-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
