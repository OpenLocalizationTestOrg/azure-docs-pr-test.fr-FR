---
title: "AAA » interroger un index (portail - Azure Search) | Documents Microsoft »"
description: "Émettre une requête de recherche dans l’Explorateur de recherche du portail hello Azure."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="e792d-103">Interroger un index Azure Search à l’aide de l’Explorateur de recherche Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="e792d-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e792d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e792d-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="e792d-105">Portail</span><span class="sxs-lookup"><span data-stu-id="e792d-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="e792d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="e792d-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="e792d-107">REST</span><span class="sxs-lookup"><span data-stu-id="e792d-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="e792d-108">Cet article vous explique comment tooquery un indexeur Azure Search index à l’aide de **rechercher dans l’Explorateur** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e792d-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="e792d-109">Vous pouvez utiliser l’Explorateur de recherche toosubmit simple ou complète Lucene requête chaînes tooany existant index dans votre service.</span><span class="sxs-lookup"><span data-stu-id="e792d-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="e792d-110">Tableau de bord de service hello ouvert</span><span class="sxs-lookup"><span data-stu-id="e792d-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="e792d-111">Cliquez sur **toutes les ressources** dans la barre saut hello hello à gauche de hello [portail Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="e792d-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="e792d-112">Sélectionnez votre service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="e792d-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="e792d-113">Sélection d’un index</span><span class="sxs-lookup"><span data-stu-id="e792d-113">Select an index</span></span>

<span data-ttu-id="e792d-114">Index hello sélectionnez vous aimeriez toosearch de hello **index** vignette.</span><span class="sxs-lookup"><span data-stu-id="e792d-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="e792d-115">Ouverture de l’Explorateur de recherche</span><span class="sxs-lookup"><span data-stu-id="e792d-115">Open Search Explorer</span></span>

<span data-ttu-id="e792d-116">Cliquez sur hello barre de recherche de rechercher dans l’Explorateur vignette tooslide hello ouvert et le volet de résultats.</span><span class="sxs-lookup"><span data-stu-id="e792d-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="e792d-117">Commencez la recherche</span><span class="sxs-lookup"><span data-stu-id="e792d-117">Start searching</span></span>

<span data-ttu-id="e792d-118">Lorsque vous utilisez hello rechercher dans l’Explorateur, vous pouvez spécifier [des paramètres de requête](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) requête de hello tooformulate.</span><span class="sxs-lookup"><span data-stu-id="e792d-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="e792d-119">Saisissez une requête dans **Chaîne de requête** puis appuyez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="e792d-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="e792d-120">chaîne de requête Hello est automatiquement analysé dans la demande de bon de hello URL toosubmit une demande HTTP hello API REST Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e792d-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="e792d-121">Vous pouvez utiliser n’importe quel valide simple ou complète Lucene syntaxe toocreate hello demande de requête.</span><span class="sxs-lookup"><span data-stu-id="e792d-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="e792d-122">Hello `*` caractère est recherche vide ou non spécifiée tooan équivalente qui retourne tous les documents dans aucun ordre particulier.</span><span class="sxs-lookup"><span data-stu-id="e792d-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="e792d-123">Dans **résultats**, résultats de la requête sont présentés au format JSON brut, charge utile de toohello identiques sont retournées dans un corps de réponse HTTP lors de l’émission de demandes par programme.</span><span class="sxs-lookup"><span data-stu-id="e792d-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="e792d-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e792d-124">Next steps</span></span>

<span data-ttu-id="e792d-125">Hello suivant ressources fournit des exemples et des informations de syntaxe de requête supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e792d-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="e792d-126">Syntaxe de requête simple</span><span class="sxs-lookup"><span data-stu-id="e792d-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="e792d-127">Syntaxe de requête Lucene</span><span class="sxs-lookup"><span data-stu-id="e792d-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="e792d-128">Exemples de syntaxe de requête Lucene</span><span class="sxs-lookup"><span data-stu-id="e792d-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="e792d-129">Syntaxe d’expression de filtre OData</span><span class="sxs-lookup"><span data-stu-id="e792d-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 