---
title: "aaaSave recherches et code confidentiel des ressources de données dans Azure Data Catalog | Documents Microsoft"
description: "Tooarticle de façon à des fonctionnalités mise en surbrillance dans Azure Data Catalog pour enregistrer les sources de données et des ressources de données pour une utilisation ultérieure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="30c00-103">Enregistrer des recherches et épingler des ressources de données dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="30c00-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="30c00-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="30c00-104">Introduction</span></span>
<span data-ttu-id="30c00-105">Azure Data Catalog fournit des fonctionnalités de détection des sources de données.</span><span class="sxs-lookup"><span data-stu-id="30c00-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="30c00-106">Vous pouvez rapidement rechercher et filtrer les sources de données toolocate hello catalogue et comprendre leur rôle respectif, rend plus facile toofind hello bonnes données pour la tâche hello à portée de main.</span><span class="sxs-lookup"><span data-stu-id="30c00-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="30c00-107">Mais que se passe-t-il si vous devez tooregularly fonctionnent avec hello même données ?</span><span class="sxs-lookup"><span data-stu-id="30c00-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="30c00-108">Et que se passe-t-il si d’autres utilisateurs contribuent régulièrement votre toohello de la base de connaissances mêmes sources de données dans le catalogue de hello ?</span><span class="sxs-lookup"><span data-stu-id="30c00-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="30c00-109">Dans ces situations, ayant toorepeatedly problème hello même recherche peut être inefficace.</span><span class="sxs-lookup"><span data-stu-id="30c00-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="30c00-110">C’est là que l’enregistrement des recherches et l’épinglage des ressources de données peuvent vous aider.</span><span class="sxs-lookup"><span data-stu-id="30c00-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="30c00-111">Recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="30c00-111">Saved searches</span></span>
<span data-ttu-id="30c00-112">Dans Data Catalog, une recherche enregistrée est une définition de recherche réutilisable spécifique à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30c00-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="30c00-113">Vous pouvez définir une recherche (termes, balises et autres filtres), puis l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="30c00-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="30c00-114">Vous pouvez réexécuter définition de recherche hello enregistré ultérieure tooreturn toutes les ressources de données qui correspondent aux critères de recherche.</span><span class="sxs-lookup"><span data-stu-id="30c00-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="30c00-115">Créer une recherche enregistrée</span><span class="sxs-lookup"><span data-stu-id="30c00-115">Create a saved search</span></span>
<span data-ttu-id="30c00-116">toocreate une recherche enregistrée, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="30c00-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="30c00-117">Dans le portail Azure Data Catalog hello, Bonjour **recherche actuelle** fenêtre, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="30c00-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Bouton Enregistrer dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="30c00-119">Entrez les critères de recherche hello que vous souhaitez tooreuse, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="30c00-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Attribution d’un nom à la recherche enregistrée dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="30c00-121">Lorsque vous êtes invité, entrez un nom pour hello recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="30c00-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="30c00-122">Choisissez un nom qui est significatif et qui décrit les ressources de données hello qui seront retournées par la recherche de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="30c00-123">Gérer les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="30c00-123">Manage saved searches</span></span>
<span data-ttu-id="30c00-124">Après avoir enregistré une ou plusieurs des recherches, une **recherches enregistrées** option s’affiche sous hello **recherche actuelle** boîte.</span><span class="sxs-lookup"><span data-stu-id="30c00-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="30c00-125">Lors de la liste de hello est développée, toutes les recherches enregistrées sont affichées.</span><span class="sxs-lookup"><span data-stu-id="30c00-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Liste des recherches enregistrées](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="30c00-127">Effectuez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="30c00-127">Do any of hello following:</span></span>

* <span data-ttu-id="30c00-128">tooexecute une recherche, sélectionnez une recherche enregistrée dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="30c00-129">tooview une liste d’options de gestion d’une recherche enregistrée, cliquez sur hello nom recherche toohello suivant de flèche vers le bas.</span><span class="sxs-lookup"><span data-stu-id="30c00-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Options de gestion des recherches enregistrées](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="30c00-131">tooenter un nouveau nom pour la recherche de hello enregistré, sélectionnez **renommer**.</span><span class="sxs-lookup"><span data-stu-id="30c00-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="30c00-132">définition de recherche Hello n’est pas modifiée.</span><span class="sxs-lookup"><span data-stu-id="30c00-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="30c00-133">recherche de hello enregistré tooremove dans votre liste, sélectionnez **supprimer**, puis confirmez la suppression de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="30c00-134">recherche de hello enregistré toomark en tant que la recherche par défaut, sélectionnez **enregistrer en tant que valeur par défaut**.</span><span class="sxs-lookup"><span data-stu-id="30c00-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="30c00-135">Si vous effectuez une recherche « vide » à partir de la page d’accueil Azure Data Catalog hello, votre recherche par défaut est exécutée.</span><span class="sxs-lookup"><span data-stu-id="30c00-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="30c00-136">En outre, hello recherche qui est marqué comme la recherche par défaut de hello est affiché en haut de hello de hello **recherches enregistrées** liste.</span><span class="sxs-lookup"><span data-stu-id="30c00-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="30c00-137">Recherches enregistrées organisationnelles</span><span class="sxs-lookup"><span data-stu-id="30c00-137">Organizational saved searches</span></span>
<span data-ttu-id="30c00-138">Tous les utilisateurs de votre organisation peuvent enregistrer des recherches pour leur propre usage.</span><span class="sxs-lookup"><span data-stu-id="30c00-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="30c00-139">Les administrateurs de catalogue de données peuvent également enregistrer des recherches pour tous les utilisateurs au sein de l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="30c00-140">Lorsque les administrateurs enregistrement une recherche, elles apparaissent avec un **partage au sein de la société de hello** option.</span><span class="sxs-lookup"><span data-stu-id="30c00-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="30c00-141">En sélectionnant cette hello de partages option enregistré de recherche pour tous les utilisateurs dans l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Recherches enregistrées organisationnelles](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="30c00-143">Ressources de données épinglées</span><span class="sxs-lookup"><span data-stu-id="30c00-143">Pinned data assets</span></span>
<span data-ttu-id="30c00-144">Les recherches enregistrées vous permettent d’enregistrer et de réutiliser les définitions de recherche.</span><span class="sxs-lookup"><span data-stu-id="30c00-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="30c00-145">ressources de données Hello qui sont retournées par les recherches de hello peuvent changer au fil du temps en tant que contenu hello de modification de catalogue hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="30c00-146">Quand vous épinglez des ressources de données, vous pouvez identifier de manière explicite toomake actifs de données spécifique les tooaccess plus facilement sans avoir besoin de toouse une recherche.</span><span class="sxs-lookup"><span data-stu-id="30c00-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="30c00-147">L’épinglage d’une ressource de données est simple.</span><span class="sxs-lookup"><span data-stu-id="30c00-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="30c00-148">tooadd hello données asset tooyour épinglé la liste, cliquez simplement sur hello **code confidentiel** icône.</span><span class="sxs-lookup"><span data-stu-id="30c00-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="30c00-149">icône de Hello s’affiche dans hello de vignette d’élément multimédia hello dans l’affichage en mosaïque hello et dans la colonne la plus à gauche de hello dans la vue de liste de hello dans le portail d’Azure Data Catalog hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![icône d’épingle Hello ressource de données](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="30c00-151">Le désépinglage d’une ressource de données est tout aussi simple.</span><span class="sxs-lookup"><span data-stu-id="30c00-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="30c00-152">Cliquez simplement sur hello **désépingler** paramètre de hello tootoggle icône pour un composant sélectionné de hello.</span><span class="sxs-lookup"><span data-stu-id="30c00-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![icône de ressource de données Hello détacher](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="30c00-154">Hello section de mes ressources</span><span class="sxs-lookup"><span data-stu-id="30c00-154">hello My Assets section</span></span>
<span data-ttu-id="30c00-155">Hello Data Catalog, page d’accueil du portail inclut un **mes ressources** section qui affiche les ressources de l’utilisateur actuel de toohello qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="30c00-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="30c00-156">Cette section inclut à la fois les ressources épinglées et les recherches enregistrées.</span><span class="sxs-lookup"><span data-stu-id="30c00-156">This section includes both pinned assets and saved searches.</span></span>

![Hello section Mes actifs sur la page d’accueil hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="30c00-158">Résumé</span><span class="sxs-lookup"><span data-stu-id="30c00-158">Summary</span></span>
<span data-ttu-id="30c00-159">Azure Data Catalog offre des fonctionnalités qui le rendent plus facile toodiscover hello des sources de données que vous avez besoin, que vous et autres membres de l’organisation peuvent consacrer moins de temps et en plus de temps avec lui.</span><span class="sxs-lookup"><span data-stu-id="30c00-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="30c00-160">Les recherches enregistrées et l’épinglage des ressources de données viennent s’ajouter à ces fonctionnalités pour que les utilisateurs puissent identifier facilement les sources de données qu’ils utilisent le plus souvent.</span><span class="sxs-lookup"><span data-stu-id="30c00-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
