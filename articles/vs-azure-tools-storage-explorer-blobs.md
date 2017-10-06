---
title: "aaaManage des ressources de stockage d’objets Blob Azure avec l’Explorateur de stockage (version préliminaire) | Documents Microsoft"
description: "Gérer les conteneurs d’objets blob et les blobs Azure avec l’Explorateur de stockage (version préliminaire)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="e8f0b-103">Gérer les ressources Azure Blob Storage avec l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="e8f0b-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="e8f0b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e8f0b-104">Overview</span></span>
<span data-ttu-id="e8f0b-105">[Stockage d’objets Blob Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) est un service destiné à stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="e8f0b-106">Vous pouvez utiliser les données de tooexpose de stockage Blob publiquement toohello world ou les données d’application toostore en privé.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="e8f0b-107">Dans cet article, vous allez apprendre comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec des conteneurs d’objets blob et les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8f0b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e8f0b-108">Prerequisites</span></span>
<span data-ttu-id="e8f0b-109">toocomplete hello étapes décrites dans cet article, vous allez hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="e8f0b-110">Télécharger et installer l’explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="e8f0b-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="e8f0b-111">Connexion de compte de stockage Azure tooa ou service</span><span class="sxs-lookup"><span data-stu-id="e8f0b-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="e8f0b-112">Création d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-112">Create a blob container</span></span>
<span data-ttu-id="e8f0b-113">Tous les objets blob doivent résider dans un conteneur d’objets blob, c’est-à-dire un simple regroupement logique d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="e8f0b-114">Un compte peut contenir un nombre illimité de conteneurs, et chaque conteneur peut stocker un nombre illimité d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="e8f0b-115">Hello étapes suivantes illustrent comment toocreate un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="e8f0b-116">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-117">Dans le volet gauche de hello, développez le compte de stockage hello dans lequel vous souhaitez le conteneur d’objets blob toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="e8f0b-118">Avec le bouton droit **conteneurs d’objets Blob**et - dans le menu contextuel de hello - sélectionnez **créer un conteneur d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Création de conteneurs d’objets blob - Menu contextuel][0]
4. <span data-ttu-id="e8f0b-120">Une zone de texte s’affichera sous hello **conteneurs d’objets Blob** dossier.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="e8f0b-121">Entrez le nom hello pour votre conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="e8f0b-122">Consultez hello [les règles d’affectation de noms de conteneur](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section pour obtenir la liste des règles et des restrictions sur les conteneurs d’objets blob d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Création de conteneurs d’objets blob - Zone de texte][1]
5. <span data-ttu-id="e8f0b-124">Appuyez sur **entrée** fois le conteneur d’objets blob toocreate hello, ou **ÉCHAP** toocancel.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="e8f0b-125">Une fois le conteneur d’objets blob hello a été créé avec succès, il sera affiché sous hello **conteneurs d’objets Blob** dossier pour hello sélectionné compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Conteneur d’objets blob créé][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="e8f0b-127">Affichage du contenu d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-127">View a blob container's contents</span></span>
<span data-ttu-id="e8f0b-128">Les conteneurs d’objets blob contiennent des objets blob et des dossiers (qui peuvent eux-mêmes contenir des objets blob).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="e8f0b-129">Hello étapes suivantes illustrent comment contenu de hello tooview d’un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire) :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="e8f0b-130">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-131">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="e8f0b-132">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-133">Conteneur d’objets blob avec le bouton hello vous le souhaitez tooview et - dans le menu contextuel de hello - sélectionnez **ouvrir l’éditeur de conteneur Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="e8f0b-134">Vous pouvez également double-cliquer sur le conteneur d’objets blob hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Ouvrir l’éditeur de conteneurs d’objets blob - Menu contextuel][19]
5. <span data-ttu-id="e8f0b-136">volet principal de Hello affiche le contenu du conteneur d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-136">hello main pane will display hello blob container's contents.</span></span>

   ![Éditeur de conteneurs d’objets blob][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="e8f0b-138">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-138">Delete a blob container</span></span>
<span data-ttu-id="e8f0b-139">Vous pouvez facilement créer et supprimer des conteneurs d’objets blob selon vos besoins</span><span class="sxs-lookup"><span data-stu-id="e8f0b-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="e8f0b-140">(toosee comment toodelete individuels des objets BLOB, consultez section toohello [gestion des objets BLOB dans un conteneur d’objets blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="e8f0b-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="e8f0b-141">Hello étapes suivantes illustrent comment toodelete un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire) :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="e8f0b-142">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-143">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="e8f0b-144">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-145">Conteneur d’objets blob avec le bouton hello vous le souhaitez toodelete et - dans le menu contextuel de hello - sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="e8f0b-146">Vous pouvez également appuyer sur **supprimer** conteneur de toodelete hello blob actuellement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Supprimer un conteneur d’objets blob - Menu contextuel][4]
5. <span data-ttu-id="e8f0b-148">Sélectionnez **Oui** boîte de dialogue de confirmation toohello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Supprimer un conteneur d’objets blob - Confirmation][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="e8f0b-150">Copie d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-150">Copy a blob container</span></span>
<span data-ttu-id="e8f0b-151">Explorateur de stockage (version préliminaire) vous permet de toocopy un Presse-papiers toohello du conteneur blob et collez ensuite que le conteneur d’objets blob dans un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="e8f0b-152">(toosee comment toocopy individuels des objets BLOB, consultez section toohello [gestion des objets BLOB dans un conteneur d’objets blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="e8f0b-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="e8f0b-153">Hello suit illustre comment toocopy un conteneur d’objets blob à partir du stockage d’un compte tooanother.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="e8f0b-154">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-155">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello toocopy vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="e8f0b-156">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-157">Conteneur d’objets blob avec le bouton hello vous le souhaitez toocopy et - dans le menu contextuel de hello - sélectionnez **conteneur d’objets Blob copie**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Copier un conteneur d’objets blob - Menu contextuel][6]
5. <span data-ttu-id="e8f0b-159">Cliquez sur le compte de stockage cible « hello souhaitée » dans lequel vous le souhaitez conteneur d’objets blob toopaste hello et - dans le menu contextuel de hello - sélectionnez **conteneur d’objets Blob coller**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Coller un conteneur d’objets blob - Menu contextuel][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="e8f0b-161">Obtenir hello SAS pour un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="e8f0b-162">A [signature d’accès partagé (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fournit tooresources accès délégué dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="e8f0b-163">Cela signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu spécifié d’autorisations, sans avoir à partager vos clés d’accès de compte.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="e8f0b-164">Hello étapes suivantes illustrent comment toocreate un SAS pour un conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="e8f0b-165">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-166">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello pour laquelle vous souhaitez tooget une SAP.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="e8f0b-167">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-168">Cliquez sur le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **obtenir une Signature d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Obtenir une signature d’accès partagé - Menu contextuel][8]
5. <span data-ttu-id="e8f0b-170">Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez la stratégie de hello, les dates de début et d’expiration, fuseau horaire et souhaité pour la ressource de hello des niveaux d’accès.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Obtenir une signature d’accès partagé - Options][9]
6. <span data-ttu-id="e8f0b-172">Lorsque vous avez terminé de spécifier les options de SAS hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="e8f0b-173">Une seconde **Signature d’accès partagé** boîte de dialogue affichera alors que les listes hello conteneur d’objets blob, ainsi que les URL hello et requête que vous pouvez utiliser tooaccess hello ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="e8f0b-174">Sélectionnez **copie** suivant toohello URL toocopy toohello Presse-papiers vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Copier les URL de SAP][10]
8. <span data-ttu-id="e8f0b-176">Lorsque vous avez terminé, sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="e8f0b-177">Gestion des stratégies d’accès d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="e8f0b-178">Hello étapes suivantes illustrent comment toomanage (ajouter et supprimer) pour un conteneur d’objets blob, les stratégies d’accès :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="e8f0b-179">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-180">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello dont vous souhaitez toomanage les stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="e8f0b-181">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-182">Sélectionnez le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **gérer les stratégies d’accès**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Gérer les stratégies d’accès - Menu contextuel][11]
5. <span data-ttu-id="e8f0b-184">Hello **des stratégies d’accès** boîte de dialogue répertorie les stratégies d’accès déjà créés pour le conteneur d’objet blob sélectionnés hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Options de stratégie d’accès][12]        
6. <span data-ttu-id="e8f0b-186">Suivez ces étapes en fonction de la tâche de gestion de stratégie hello accès :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="e8f0b-187">**Ajouter une nouvelle stratégie d’accès** : sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="e8f0b-188">Une fois généré, hello **des stratégies d’accès** boîte de dialogue affiche hello nouvellement ajouté accéder à la stratégie (avec les paramètres par défaut).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="e8f0b-189">**Modifier une stratégie d’accès** : apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="e8f0b-190">**Supprimer une stratégie d’accès** : sélectionnez **supprimer** suivant toohello accès stratégie tooremove.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="e8f0b-191">Ensemble hello niveau d’accès Public pour un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="e8f0b-192">Par défaut, chaque conteneur d’objets blob est défini trop « Aucun accès public ».</span><span class="sxs-lookup"><span data-stu-id="e8f0b-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="e8f0b-193">Hello étapes suivantes illustrent comment toospecify accès public au niveau d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="e8f0b-194">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-195">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello dont vous souhaitez toomanage les stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="e8f0b-196">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-197">Sélectionnez le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **définie au niveau de l’accès Public**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Définir le niveau d’accès public - Menu contextuel][13]
5. <span data-ttu-id="e8f0b-199">Bonjour **définir le niveau de l’accès Public du conteneur** boîte de dialogue, spécifiez le niveau d’accès hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Définir le niveau d’accès public - Options][14]
6. <span data-ttu-id="e8f0b-201">Sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="e8f0b-202">Gestion des objets blob dans un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="e8f0b-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="e8f0b-203">Une fois que vous avez créé un conteneur d’objets blob, vous pouvez télécharger un conteneur d’objets blob toothat blob, télécharger un ordinateur local de blob tooyour, ouvrir un objet blob sur votre ordinateur local et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="e8f0b-204">Hello suit illustre comment toomanage hello des objets BLOB (et les dossiers) dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="e8f0b-205">Ouvrez l’Explorateur de stockage (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="e8f0b-206">Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello toomanage vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="e8f0b-207">Développez du compte de stockage hello **conteneurs d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="e8f0b-208">Double-cliquez sur le conteneur d’objets blob hello tooview vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="e8f0b-209">volet principal de Hello affiche le contenu du conteneur d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-209">hello main pane will display hello blob container's contents.</span></span>

   ![Afficher le conteneur d’objets blob][3]
6. <span data-ttu-id="e8f0b-211">volet principal de Hello affiche le contenu du conteneur d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="e8f0b-212">Suivez ces étapes en fonction de la tâche hello que vous souhaitez tooperform :</span><span class="sxs-lookup"><span data-stu-id="e8f0b-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="e8f0b-213">**Télécharger le conteneur d’objets blob tooa fichiers**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="e8f0b-214">Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **télécharger des fichiers** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Télécharger des fichiers - Menu][15]
     2. <span data-ttu-id="e8f0b-216">Bonjour **télécharger des fichiers** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **fichiers** hello tooselect fichier (s) vous souhaitez tooupload de zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Télécharger des fichiers - Options][16]
     3. <span data-ttu-id="e8f0b-218">Spécifiez le type hello de **type d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="e8f0b-219">article de Hello [prise en main le stockage Blob Azure à l’aide de .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explique les différences de hello hello entre les différents types d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="e8f0b-220">Si vous le souhaitez, spécifiez un dossier cible dans lequel les fichiers sélectionnés hello seront téléchargés.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="e8f0b-221">Si le dossier cible de hello n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="e8f0b-222">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-222">Select **Upload**.</span></span>
   * <span data-ttu-id="e8f0b-223">**Télécharger un conteneur d’objets blob tooa dossier**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="e8f0b-224">Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **dossier de téléchargement** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Télécharger un dossier - Menu][17]
     2. <span data-ttu-id="e8f0b-226">Bonjour **dossier de téléchargement** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **dossier** dossier hello dont vous souhaitez tooupload le contenu de texte boîte tooselect.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Télécharger un dossier - Options][18]
     3. <span data-ttu-id="e8f0b-228">Spécifiez le type hello de **type d’objets Blob**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="e8f0b-229">article de Hello [prise en main le stockage Blob Azure à l’aide de .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explique les différences de hello hello entre les différents types d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="e8f0b-230">Si vous le souhaitez, spécifiez un dossier cible dans le hello contenu du dossier sélectionné sera téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="e8f0b-231">Si le dossier cible de hello n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="e8f0b-232">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-232">Select **Upload**.</span></span>
   * <span data-ttu-id="e8f0b-233">**Télécharger un ordinateur local de blob tooyour**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="e8f0b-234">Sélectionnez blob hello toodownload vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="e8f0b-235">Barre d’outils du volet hello principal, sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="e8f0b-236">Bonjour **spécifier où toosave hello téléchargé blob** boîte de dialogue, spécifiez hello emplacement blob hello téléchargé et hello nom que vous souhaitez toogive il.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="e8f0b-237">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-237">Select **Save**.</span></span>
   * <span data-ttu-id="e8f0b-238">**Ouvrir un objet blob sur votre ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="e8f0b-239">Sélectionnez blob hello tooopen vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="e8f0b-240">Barre d’outils du volet hello principal, sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="e8f0b-241">objet blob de Hello sera téléchargé et ouvert à l’aide d’application hello associée au type de fichier sous-jacent de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="e8f0b-242">**Copier un Presse-papiers toohello de blob**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="e8f0b-243">Sélectionnez blob hello toocopy vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="e8f0b-244">Barre d’outils du volet hello principal, sélectionnez **copie**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="e8f0b-245">Dans le volet gauche de hello, accédez tooanother conteneur d’objets blob, puis double-cliquez dessus tooview dans le volet principal de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="e8f0b-246">Barre d’outils du volet hello principal, sélectionnez **coller** toocreate une copie de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="e8f0b-247">**Supprimer un blob.**</span><span class="sxs-lookup"><span data-stu-id="e8f0b-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="e8f0b-248">Sélectionnez blob hello toodelete vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="e8f0b-249">Barre d’outils du volet hello principal, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="e8f0b-250">Sélectionnez **Oui** boîte de dialogue de confirmation toohello.</span><span class="sxs-lookup"><span data-stu-id="e8f0b-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8f0b-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8f0b-251">Next steps</span></span>
* <span data-ttu-id="e8f0b-252">Hello de vue [dernières notes de version de l’Explorateur de stockage (version préliminaire) et les vidéos](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="e8f0b-253">Découvrez comment trop[créer des applications à l’aide d’objets BLOB Windows Azure, les tables, les files d’attente et les fichiers](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e8f0b-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
