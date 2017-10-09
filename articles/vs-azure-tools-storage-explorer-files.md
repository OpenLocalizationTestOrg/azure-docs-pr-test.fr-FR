---
title: "aaaUsing Explorateur de stockage (version préliminaire) avec le stockage de fichiers Azure | Documents Microsoft"
description: "Découvrez comment savoir comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec fichier de partage et de fichiers."
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
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="dec97-103">Utilisation de l’Explorateur de stockage (version préliminaire) avec Azure Stockage Fichier</span><span class="sxs-lookup"><span data-stu-id="dec97-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="dec97-104">Le stockage est un service qui offre le fichier partages dans hello cloud à l’aide de fichiers Azure hello protocole Server Message Block (SMB) standard.</span><span class="sxs-lookup"><span data-stu-id="dec97-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="dec97-105">Les protocoles SMB 2.1 et SMB 3.0 sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dec97-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="dec97-106">Avec le stockage de fichiers Azure, vous pouvez migrer des applications héritées qui s’appuient sur tooAzure de partages de fichiers rapidement et sans réécritures coûteux.</span><span class="sxs-lookup"><span data-stu-id="dec97-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="dec97-107">Vous pouvez utiliser les données de tooexpose de stockage de fichier publiquement toohello world ou les données d’application toostore en privé.</span><span class="sxs-lookup"><span data-stu-id="dec97-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="dec97-108">Dans cet article, vous allez apprendre comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec fichier de partage et de fichiers.</span><span class="sxs-lookup"><span data-stu-id="dec97-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dec97-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dec97-109">Prerequisites</span></span>

<span data-ttu-id="dec97-110">toocomplete hello étapes décrites dans cet article, vous allez hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="dec97-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="dec97-111">Télécharger et installer l’explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="dec97-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="dec97-112">Connexion de compte de stockage Azure tooa ou service</span><span class="sxs-lookup"><span data-stu-id="dec97-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="dec97-113">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-113">Create a File Share</span></span>

<span data-ttu-id="dec97-114">Tous les fichiers doivent résider dans un partage de fichiers, c’est-à-dire un simple regroupement logique de fichiers.</span><span class="sxs-lookup"><span data-stu-id="dec97-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="dec97-115">Un compte peut contenir un nombre illimité de partages de fichiers, et chaque partage de fichiers peut stocker un nombre illimité de fichiers.</span><span class="sxs-lookup"><span data-stu-id="dec97-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="dec97-116">Hello suit illustre comment toocreate un partage de fichiers dans l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="dec97-117">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-118">Dans le volet gauche de hello, développez le compte de stockage hello dans lequel vous souhaitez toocreate hello partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="dec97-119">Avec le bouton droit **des partages de fichiers**et - dans le menu contextuel de hello - sélectionnez **créer un partage de fichier**.</span><span class="sxs-lookup"><span data-stu-id="dec97-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Créer un partage de fichiers](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="dec97-121">Une zone de texte s’affichera sous hello **des partages de fichiers** dossier.</span><span class="sxs-lookup"><span data-stu-id="dec97-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="dec97-122">Entrez le nom hello pour le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="dec97-122">Enter hello name for your file share.</span></span> <span data-ttu-id="dec97-123">Consultez hello [partager des règles d’affectation de noms](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section pour obtenir la liste de règles et les restrictions d’affectation de noms des partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="dec97-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Partage de hello d’affectation de noms](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="dec97-125">Appuyez sur **entrée** lorsque toocreate terminé hello partage de fichiers, ou **ÉCHAP** toocancel.</span><span class="sxs-lookup"><span data-stu-id="dec97-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="dec97-126">Une fois que le partage de fichiers hello a été créé avec succès, il sera affiché sous hello **des partages de fichiers** dossier pour hello sélectionné compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dec97-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![nouveau partage de Hello](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="dec97-128">Afficher le contenu d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-128">View a file share's contents</span></span>

<span data-ttu-id="dec97-129">Les partages de fichiers contiennent des fichiers et des dossiers (qui peuvent également contenir des fichiers).</span><span class="sxs-lookup"><span data-stu-id="dec97-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="dec97-130">Hello étapes suivantes illustrent comment partage du contenu de hello tooview d’un fichier dans l’Explorateur de stockage (version préliminaire) : +</span><span class="sxs-lookup"><span data-stu-id="dec97-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="dec97-131">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-132">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="dec97-133">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="dec97-134">Partage de fichiers avec le bouton hello vous le souhaitez tooview et - dans le menu contextuel de hello - sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="dec97-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="dec97-135">Vous pouvez également double-cliquer sur le partage de fichiers hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Ouvrir le partage](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="dec97-137">volet principal de Hello affiche les contenu du partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-137">hello main pane will display hello file share's contents.</span></span>
    
    ![contenu du partage de Hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="dec97-139">Supprimer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-139">Delete a file share</span></span>

<span data-ttu-id="dec97-140">Vous pouvez facilement créer et supprimer des partages de fichiers selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="dec97-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="dec97-141">(toosee comment toodelete des fichiers individuels, consultez section toohello [la gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="dec97-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="dec97-142">Hello suit illustre comment toodelete un partage de fichiers dans l’Explorateur de stockage (version préliminaire) :</span><span class="sxs-lookup"><span data-stu-id="dec97-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="dec97-143">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-144">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="dec97-145">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="dec97-146">Partage de fichiers avec le bouton hello vous le souhaitez toodelete et - dans le menu contextuel de hello - sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="dec97-147">Vous pouvez également appuyer sur **supprimer** partage de fichier actuellement sélectionné toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Supprimer](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="dec97-149">Sélectionnez **Oui** boîte de dialogue de confirmation toohello.</span><span class="sxs-lookup"><span data-stu-id="dec97-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Boîte de dialogue de confirmation](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="dec97-151">Copier un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-151">Copy a file share</span></span>

<span data-ttu-id="dec97-152">Explorateur de stockage (version préliminaire) vous permet de toocopy un Presse-papiers toohello du partage de fichier, puis collez ce partage de fichiers dans un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dec97-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="dec97-153">(toosee comment toocopy des fichiers individuels, consultez section toohello [la gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="dec97-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="dec97-154">Hello suit illustre comment partager des toocopy un fichier à partir d’un tooanother de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dec97-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="dec97-155">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-156">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello toocopy vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="dec97-157">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="dec97-158">Partage de fichiers avec le bouton hello vous le souhaitez toocopy et - dans le menu contextuel de hello - sélectionnez **de partage de fichiers copie**.</span><span class="sxs-lookup"><span data-stu-id="dec97-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Copier le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="dec97-160">Cliquez sur le compte de stockage cible « hello souhaitée » dans lequel vous le souhaitez partage de fichiers toopaste hello et - dans le menu contextuel de hello - sélectionnez **coller un partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Coller le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="dec97-162">Obtenir hello SAS pour un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="dec97-163">A [signature d’accès partagé (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fournit tooresources accès délégué dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dec97-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="dec97-164">Cela signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu d’autorisations, spécifié sans avoir tooshare vos clés d’accès de compte.</span><span class="sxs-lookup"><span data-stu-id="dec97-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="dec97-165">Hello étapes suivantes illustrent comment toocreate partager un SAS pour un fichier : +</span><span class="sxs-lookup"><span data-stu-id="dec97-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="dec97-166">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-167">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello pour laquelle vous souhaitez tooget une SAP.</span><span class="sxs-lookup"><span data-stu-id="dec97-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="dec97-168">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="dec97-169">Avec le bouton droit de partage de fichier souhaité hello et - dans le menu contextuel de hello - sélectionnez **obtenir une Signature d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="dec97-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Obtenir une signature d’accès partagé](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="dec97-171">Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez la stratégie de hello, les dates de début et d’expiration, fuseau horaire et souhaité pour la ressource de hello des niveaux d’accès.</span><span class="sxs-lookup"><span data-stu-id="dec97-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="dec97-173">Lorsque vous avez terminé de spécifier les options de SAS hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="dec97-174">Une seconde **Signature d’accès partagé** boîte de dialogue affichera alors que les listes hello partage de fichiers, ainsi que les URL hello et requête que vous pouvez utiliser tooaccess hello ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="dec97-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="dec97-175">Sélectionnez **copie** suivant toohello URL toocopy toohello Presse-papiers vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Deuxième boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="dec97-177">Lorsque vous avez terminé, sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="dec97-178">Gérer les stratégies d’accès d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="dec97-179">Hello étapes suivantes illustrent comment toomanage (ajouter et supprimer) pour un partage de fichiers, les stratégies d’accès : +.</span><span class="sxs-lookup"><span data-stu-id="dec97-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="dec97-180">les stratégies d’accès Hello est utilisée pour créer des URL de SAP par le biais duquel les personnes peuvent utiliser tooaccess hello ressource du fichier de stockage pendant une période de temps définie.</span><span class="sxs-lookup"><span data-stu-id="dec97-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="dec97-181">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="dec97-182">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello dont vous souhaitez toomanage les stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="dec97-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="dec97-183">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="dec97-184">Sélectionnez le partage de fichier souhaité hello et - dans le menu contextuel de hello - sélectionnez **gérer les stratégies d’accès**.</span><span class="sxs-lookup"><span data-stu-id="dec97-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Gérer les stratégies d’accès - Menu contextuel](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="dec97-186">Hello **des stratégies d’accès** boîte de dialogue répertorie les stratégies d’accès déjà créés pour le partage de fichier sélectionné hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Stratégies d’accès](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="dec97-188">Suivez ces étapes en fonction de la tâche de gestion de stratégie hello accès :</span><span class="sxs-lookup"><span data-stu-id="dec97-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="dec97-189">**Ajouter une nouvelle stratégie d’accès** : sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dec97-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="dec97-190">Une fois généré, hello **des stratégies d’accès** boîte de dialogue affiche hello nouvellement ajouté accéder à la stratégie (avec les paramètres par défaut).</span><span class="sxs-lookup"><span data-stu-id="dec97-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="dec97-191">**Modifier une stratégie d’accès** : apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="dec97-192">**Supprimer une stratégie d’accès** : sélectionnez **supprimer** suivant toohello accès stratégie tooremove.</span><span class="sxs-lookup"><span data-stu-id="dec97-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="dec97-193">Créer une nouvelle URL de SAP à l’aide de hello la stratégie d’accès vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="dec97-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Obtenir une SAP](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Propriétés et nom de la SAP](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="dec97-196">Gestion des fichiers dans un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="dec97-196">Managing files in a file share</span></span>

<span data-ttu-id="dec97-197">Une fois que vous avez créé un partage de fichiers, vous pouvez télécharger un partage de fichiers toothat fichier, télécharger un ordinateur local tooyour de fichier, ouvrir un fichier sur votre ordinateur local et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="dec97-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="dec97-198">Hello étapes suivantes illustrent comment partagent des toomanage hello fichiers (et les dossiers) dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="dec97-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="dec97-199">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="dec97-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="dec97-200">Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello toomanage vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="dec97-201">Développez du compte de stockage hello **des partages de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="dec97-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="dec97-202">Double-cliquez sur le partage de fichiers hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dec97-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="dec97-203">volet principal de Hello affiche les contenu du partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-203">hello main pane will display hello file share's contents.</span></span>

    ![contenu du partage de Hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="dec97-205">volet principal de Hello affiche les contenu du partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="dec97-206">Suivez ces étapes en fonction de la tâche hello que vous souhaitez tooperform :</span><span class="sxs-lookup"><span data-stu-id="dec97-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="dec97-207">**Télécharger le partage de fichiers tooa de fichiers**</span><span class="sxs-lookup"><span data-stu-id="dec97-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="dec97-208">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-208">a.</span></span>  <span data-ttu-id="dec97-209">Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **télécharger des fichiers** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Charger des fichiers](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="dec97-211">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-211">b.</span></span> <span data-ttu-id="dec97-212">Bonjour **télécharger des fichiers** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **fichiers** hello tooselect fichier (s) vous souhaitez tooupload de zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dec97-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Ajout de fichiers](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="dec97-214">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-214">c.</span></span> <span data-ttu-id="dec97-215">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="dec97-215">Select **Upload**.</span></span>

    - <span data-ttu-id="dec97-216">**Télécharger un partage de fichiers tooa dossier**</span><span class="sxs-lookup"><span data-stu-id="dec97-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="dec97-217">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-217">a.</span></span> <span data-ttu-id="dec97-218">Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **dossier de téléchargement** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Télécharger un dossier - Menu](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="dec97-220">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-220">b.</span></span> <span data-ttu-id="dec97-221">Bonjour **dossier de téléchargement** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **dossier** dossier hello dont vous souhaitez tooupload le contenu de texte boîte tooselect.</span><span class="sxs-lookup"><span data-stu-id="dec97-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="dec97-222">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-222">c.</span></span> <span data-ttu-id="dec97-223">Si vous le souhaitez, spécifiez un dossier cible dans le hello contenu du dossier sélectionné sera téléchargé.</span><span class="sxs-lookup"><span data-stu-id="dec97-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="dec97-224">Si le dossier cible de hello n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="dec97-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="dec97-225">d.</span><span class="sxs-lookup"><span data-stu-id="dec97-225">d.</span></span> <span data-ttu-id="dec97-226">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="dec97-226">Select **Upload**.</span></span>

    - <span data-ttu-id="dec97-227">**Télécharger un ordinateur local tooyour de fichier**</span><span class="sxs-lookup"><span data-stu-id="dec97-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="dec97-228">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-228">a.</span></span> <span data-ttu-id="dec97-229">Sélectionnez le fichier hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="dec97-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="dec97-230">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-230">b.</span></span> <span data-ttu-id="dec97-231">Barre d’outils du volet hello principal, sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="dec97-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="dec97-232">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-232">c.</span></span> <span data-ttu-id="dec97-233">Bonjour **spécifier où toosave hello téléchargé le fichier** boîte de dialogue, spécifiez hello emplacement fichier hello téléchargé et hello nom que vous souhaitez toogive il.</span><span class="sxs-lookup"><span data-stu-id="dec97-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="dec97-234">d.</span><span class="sxs-lookup"><span data-stu-id="dec97-234">d.</span></span> <span data-ttu-id="dec97-235">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-235">Select **Save**.</span></span>

    - <span data-ttu-id="dec97-236">**Ouvrir un fichier sur votre ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="dec97-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="dec97-237">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-237">a.</span></span>  <span data-ttu-id="dec97-238">Sélectionnez le fichier hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="dec97-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="dec97-239">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-239">b.</span></span>  <span data-ttu-id="dec97-240">Barre d’outils du volet hello principal, sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="dec97-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="dec97-241">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-241">c.</span></span>  <span data-ttu-id="dec97-242">fichier de Hello est téléchargé et ouverts à l’aide d’application hello associée au type de fichier du fichier hello sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="dec97-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="dec97-243">**Copier un Presse-papiers toohello de fichier**</span><span class="sxs-lookup"><span data-stu-id="dec97-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="dec97-244">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-244">a.</span></span> <span data-ttu-id="dec97-245">Sélectionnez le fichier hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="dec97-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="dec97-246">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-246">b.</span></span> <span data-ttu-id="dec97-247">Barre d’outils du volet hello principal, sélectionnez **copie**.</span><span class="sxs-lookup"><span data-stu-id="dec97-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="dec97-248">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-248">c.</span></span> <span data-ttu-id="dec97-249">Dans le volet gauche de hello, accédez de partage de fichiers tooanother, puis double-cliquez dessus tooview dans le volet principal de hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="dec97-250">d.</span><span class="sxs-lookup"><span data-stu-id="dec97-250">d.</span></span> <span data-ttu-id="dec97-251">Barre d’outils du volet hello principal, sélectionnez **coller** toocreate une copie du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="dec97-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="dec97-252">**Supprimer un fichier**</span><span class="sxs-lookup"><span data-stu-id="dec97-252">**Delete a file**</span></span>

        <span data-ttu-id="dec97-253">a.</span><span class="sxs-lookup"><span data-stu-id="dec97-253">a.</span></span> <span data-ttu-id="dec97-254">Sélectionnez le fichier hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="dec97-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="dec97-255">b.</span><span class="sxs-lookup"><span data-stu-id="dec97-255">b.</span></span> <span data-ttu-id="dec97-256">Barre d’outils du volet hello principal, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dec97-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="dec97-257">c.</span><span class="sxs-lookup"><span data-stu-id="dec97-257">c.</span></span> <span data-ttu-id="dec97-258">Sélectionnez **Oui** boîte de dialogue de confirmation toohello.</span><span class="sxs-lookup"><span data-stu-id="dec97-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dec97-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dec97-259">Next steps</span></span>

- <span data-ttu-id="dec97-260">Hello de vue [dernières notes de version de l’Explorateur de stockage (version préliminaire) et les vidéos](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="dec97-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="dec97-261">Découvrez comment trop[créer des applications à l’aide d’objets BLOB Windows Azure, les tables, les files d’attente et les fichiers](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="dec97-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
