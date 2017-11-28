---
title: "Enregistrer des recherches et épingler des ressources de données dans Azure Data Catalog | Microsoft Docs"
description: "Article de procédure abordant les fonctionnalités d’Azure Data Catalog permettant d’enregistrer des sources de données et des ressources de données en vue d’une utilisation ultérieure."
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
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="d097a-103">Enregistrer des recherches et épingler des ressources de données dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="d097a-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="d097a-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d097a-104">Introduction</span></span>
<span data-ttu-id="d097a-105">Azure Data Catalog fournit des fonctionnalités de détection des sources de données.</span><span class="sxs-lookup"><span data-stu-id="d097a-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="d097a-106">Vous pouvez rapidement rechercher et filtrer le catalogue pour localiser des sources de données et comprendre leur rôle respectif. Vous pouvez ainsi trouver plus facilement les données dont vous avez besoin pour le travail en cours.</span><span class="sxs-lookup"><span data-stu-id="d097a-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="d097a-107">Mais qu’en est-il lorsque vous devez utiliser régulièrement les mêmes données ?</span><span class="sxs-lookup"><span data-stu-id="d097a-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="d097a-108">Ou lorsque les utilisateurs mettent régulièrement à jour une même source de données du catalogue ?</span><span class="sxs-lookup"><span data-stu-id="d097a-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="d097a-109">Dans de telles situations, le fait d’effectuer toujours les mêmes recherches peut représenter une perte de temps.</span><span class="sxs-lookup"><span data-stu-id="d097a-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="d097a-110">C’est là que l’enregistrement des recherches et l’épinglage des ressources de données peuvent vous aider.</span><span class="sxs-lookup"><span data-stu-id="d097a-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="d097a-111">Recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="d097a-111">Saved searches</span></span>
<span data-ttu-id="d097a-112">Dans Data Catalog, une recherche enregistrée est une définition de recherche réutilisable spécifique à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d097a-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="d097a-113">Vous pouvez définir une recherche (termes, balises et autres filtres), puis l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="d097a-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="d097a-114">Ainsi, vous pourrez la réexécuter plus tard pour retourner les ressources de données qui correspondent aux critères de recherche.</span><span class="sxs-lookup"><span data-stu-id="d097a-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="d097a-115">Créer une recherche enregistrée</span><span class="sxs-lookup"><span data-stu-id="d097a-115">Create a saved search</span></span>
<span data-ttu-id="d097a-116">Pour créer une recherche enregistrée, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d097a-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="d097a-117">Dans le portail Azure Data Catalog, dans la fenêtre **Recherche actuelle**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d097a-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Bouton Enregistrer dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="d097a-119">Entrez les critères de recherche que vous souhaitez réutiliser, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d097a-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Attribution d’un nom à la recherche enregistrée dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="d097a-121">Lorsque vous y êtes invité, donnez un nom à la recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="d097a-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="d097a-122">Choisissez un nom significatif décrivant bien les ressources de données qui seront retournées par la recherche.</span><span class="sxs-lookup"><span data-stu-id="d097a-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="d097a-123">Gérer les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="d097a-123">Manage saved searches</span></span>
<span data-ttu-id="d097a-124">Lorsque vous enregistrez une recherche, l’option **Recherches enregistrées** s’affiche sous la zone de texte **Recherche actuelle**.</span><span class="sxs-lookup"><span data-stu-id="d097a-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="d097a-125">Lorsque la liste est développée, toutes les recherches enregistrées sont affichées.</span><span class="sxs-lookup"><span data-stu-id="d097a-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Liste des recherches enregistrées](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="d097a-127">Faites ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d097a-127">Do any of the following:</span></span>

* <span data-ttu-id="d097a-128">Pour exécuter une recherche, sélectionnez une recherche enregistrée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d097a-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="d097a-129">Pour afficher la liste des options de gestion d’une recherche enregistrée, cliquez sur la flèche bas en regard du nom de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d097a-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Options de gestion des recherches enregistrées](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="d097a-131">Pour attribuer un nouveau nom à une recherche enregistrée, sélectionnez **Renommer**.</span><span class="sxs-lookup"><span data-stu-id="d097a-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="d097a-132">La définition de la recherche reste inchangée.</span><span class="sxs-lookup"><span data-stu-id="d097a-132">The search definition is not changed.</span></span>

* <span data-ttu-id="d097a-133">Pour supprimer la recherche enregistrée de votre liste, sélectionnez **Supprimer**, puis confirmez la suppression.</span><span class="sxs-lookup"><span data-stu-id="d097a-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="d097a-134">Pour marquer la recherche enregistrée comme recherche par défaut, sélectionnez **Enregistrer par défaut**.</span><span class="sxs-lookup"><span data-stu-id="d097a-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="d097a-135">Si l’utilisateur effectue une recherche « vide » dans la page d’accueil Azure Data Catalog, la recherche par défaut est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d097a-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="d097a-136">En outre, la recherche marquée comme recherche par défaut s’affiche en haut de la liste **Recherches enregistrées**.</span><span class="sxs-lookup"><span data-stu-id="d097a-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="d097a-137">Recherches enregistrées organisationnelles</span><span class="sxs-lookup"><span data-stu-id="d097a-137">Organizational saved searches</span></span>
<span data-ttu-id="d097a-138">Tous les utilisateurs de votre organisation peuvent enregistrer des recherches pour leur propre usage.</span><span class="sxs-lookup"><span data-stu-id="d097a-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="d097a-139">Les administrateurs de Data Catalog peuvent également enregistrer des recherches à destination de tous les utilisateurs de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="d097a-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="d097a-140">Lorsque les administrateurs enregistrent une recherche, l’option **Partager au sein de l’entreprise** leur est proposée.</span><span class="sxs-lookup"><span data-stu-id="d097a-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="d097a-141">Cette option permet de partager la recherche enregistrée avec tous les utilisateurs de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="d097a-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Recherches enregistrées organisationnelles](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="d097a-143">Ressources de données épinglées</span><span class="sxs-lookup"><span data-stu-id="d097a-143">Pinned data assets</span></span>
<span data-ttu-id="d097a-144">Les recherches enregistrées vous permettent d’enregistrer et de réutiliser les définitions de recherche.</span><span class="sxs-lookup"><span data-stu-id="d097a-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="d097a-145">Les ressources de données qui sont retournées par la recherche changent en fonction des modifications apportées au catalogue.</span><span class="sxs-lookup"><span data-stu-id="d097a-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="d097a-146">L’épinglage des ressources de données vous permet d’identifier de manière explicite certaines ressources de données afin de faciliter leur accès, sans avoir besoin d’utiliser une recherche.</span><span class="sxs-lookup"><span data-stu-id="d097a-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="d097a-147">L’épinglage d’une ressource de données est simple.</span><span class="sxs-lookup"><span data-stu-id="d097a-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="d097a-148">Pour ajouter une ressource de données à votre liste de ressources épinglées, il vous suffit de cliquer sur l’icône représentant une **épingle**.</span><span class="sxs-lookup"><span data-stu-id="d097a-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="d097a-149">Cette icône s’affiche dans l’angle de la vignette de la ressource, dans l’affichage en mosaïque, ainsi que dans la colonne la plus à gauche de la liste, dans le portail Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d097a-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Icône permettant d’épingler une ressource de données](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="d097a-151">Le désépinglage d’une ressource de données est tout aussi simple.</span><span class="sxs-lookup"><span data-stu-id="d097a-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="d097a-152">Il vous suffit de recliquer sur l’icône représentant une **épingle** pour désépingler la ressource.</span><span class="sxs-lookup"><span data-stu-id="d097a-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![Icône permettant de désépingler une ressource de données](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="d097a-154">Section Mes ressources</span><span class="sxs-lookup"><span data-stu-id="d097a-154">The My Assets section</span></span>
<span data-ttu-id="d097a-155">La page d’accueil du portail Data Catalog comprend une section intitulée **Mes ressources** qui affiche les actifs d’intérêt pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="d097a-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="d097a-156">Cette section inclut à la fois les ressources épinglées et les recherches enregistrées.</span><span class="sxs-lookup"><span data-stu-id="d097a-156">This section includes both pinned assets and saved searches.</span></span>

![Section Mes actifs dans la page d’accueil](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="d097a-158">Résumé</span><span class="sxs-lookup"><span data-stu-id="d097a-158">Summary</span></span>
<span data-ttu-id="d097a-159">Azure Data Catalog offre aux utilisateurs des fonctionnalités qui leur permettent de mieux détecter les sources de données dont ils ont besoin, et ainsi de passer moins de temps à rechercher les données et plus de temps à les utiliser.</span><span class="sxs-lookup"><span data-stu-id="d097a-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="d097a-160">Les recherches enregistrées et l’épinglage des ressources de données viennent s’ajouter à ces fonctionnalités pour que les utilisateurs puissent identifier facilement les sources de données qu’ils utilisent le plus souvent.</span><span class="sxs-lookup"><span data-stu-id="d097a-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
