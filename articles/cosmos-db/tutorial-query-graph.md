---
title: "Comment interroger des données de graphique dans Azure Cosmos DB ? | Microsoft Docs"
description: "Apprendre à interroger des données de graphique dans Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="7410f-104">Azure Cosmos DB : Comment interroger avec l’API Graph (version préliminaire) ?</span><span class="sxs-lookup"><span data-stu-id="7410f-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="7410f-105">L’[API Graph](graph-introduction.md) (version préliminaire) d’Azure Cosmos DB prend en charge les requêtes [GREMLINE](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="7410f-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="7410f-106">Cet article fournit des exemples de documents et de requêtes pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="7410f-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="7410f-107">L’article relatif à la [prise en charge de Gremlin](gremlin-support.md) comporte des informations de référence détaillées sur Gremlin.</span><span class="sxs-lookup"><span data-stu-id="7410f-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="7410f-108">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7410f-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7410f-109">Interrogation des données avec Gremlin</span><span class="sxs-lookup"><span data-stu-id="7410f-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7410f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7410f-110">Prerequisites</span></span>

<span data-ttu-id="7410f-111">Pour le bon fonctionnement de ces requêtes, vous devez disposer d’un compte Azure Cosmos DB et de données de graphique dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="7410f-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="7410f-112">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="7410f-112">Don't have any of those?</span></span> <span data-ttu-id="7410f-113">Lancez le [démarrage rapide de 5 minutes](create-graph-dotnet.md) ou le [didacticiel destiné aux développeurs](tutorial-query-graph.md) pour créer un compte et alimenter votre base de données.</span><span class="sxs-lookup"><span data-stu-id="7410f-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="7410f-114">Vous pouvez exécuter les requêtes suivantes à l’aide de la [bibliothèque de graphiques Azure Cosmos DB .NET](graph-sdk-dotnet.md), la [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), ou votre pilote Gremlin favori.</span><span class="sxs-lookup"><span data-stu-id="7410f-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="7410f-115">Compter le nombre de vertex du graphique</span><span class="sxs-lookup"><span data-stu-id="7410f-115">Count vertices in the graph</span></span>

<span data-ttu-id="7410f-116">L’extrait de code suivant montre comment compter le nombre de vertex du graphique :</span><span class="sxs-lookup"><span data-stu-id="7410f-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="7410f-117">Filtres</span><span class="sxs-lookup"><span data-stu-id="7410f-117">Filters</span></span>

<span data-ttu-id="7410f-118">Vous pouvez appliquer des filtres à l’aide des étapes `has` et `hasLabel` de Gremlin et les associer à l’aide de `and`, `or`, et `not` pour créer des filtres plus complexes.</span><span class="sxs-lookup"><span data-stu-id="7410f-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="7410f-119">Azure Cosmos DB propose une indexation sans schéma de toutes les propriétés au sein de vos vertex et degrés pour les requêtes rapides :</span><span class="sxs-lookup"><span data-stu-id="7410f-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="7410f-120">Projection</span><span class="sxs-lookup"><span data-stu-id="7410f-120">Projection</span></span>

<span data-ttu-id="7410f-121">Vous pouvez projeter certaines propriétés dans les résultats de requête à l’aide de l’étape `values` :</span><span class="sxs-lookup"><span data-stu-id="7410f-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="7410f-122">Rechercher des vertex et des bords associés</span><span class="sxs-lookup"><span data-stu-id="7410f-122">Find related edges and vertices</span></span>

<span data-ttu-id="7410f-123">Jusqu’ici, nous avons seulement abordé les opérateurs de requête fonctionnant dans n’importe quelle base de données.</span><span class="sxs-lookup"><span data-stu-id="7410f-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="7410f-124">Les graphiques sont rapides et efficaces pour les opérations de traversée lorsque vous avez besoin d’accéder aux vertex et bords associés.</span><span class="sxs-lookup"><span data-stu-id="7410f-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="7410f-125">Recherchons à présent tous les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="7410f-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="7410f-126">Nous suivons pour cela l’étape `outE` de Gremlin pour rechercher toutes les bords externes de Thomas afin de se diriger vers les vertex internes de ces bords en suivant l’étape `inV` de Gremlin :</span><span class="sxs-lookup"><span data-stu-id="7410f-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="7410f-127">La requête suivante effectue deux sauts pour rechercher tous les « amis des amis de Thomas », en appelant `outE` et `inV` deux fois.</span><span class="sxs-lookup"><span data-stu-id="7410f-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="7410f-128">Vous pouvez créer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante à l’aide de Gremlin, y compris en mixant des expressions de filtre, en exécutant des boucles à l’aide de l’étape `loop` et en mettant en œuvre la navigation conditionnelle à l’aide de l’étape `choose`.</span><span class="sxs-lookup"><span data-stu-id="7410f-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="7410f-129">En savoir plus sur ce que la [prise en charge de Gremlin](gremlin-support.md) vous permet de faire !</span><span class="sxs-lookup"><span data-stu-id="7410f-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7410f-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7410f-130">Next steps</span></span>

<span data-ttu-id="7410f-131">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="7410f-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7410f-132">Effectuer des interrogations à l’aide de Graph</span><span class="sxs-lookup"><span data-stu-id="7410f-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="7410f-133">Vous pouvez maintenant poursuivre avec le didacticiel suivant montrant comment distribuer vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="7410f-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7410f-134">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="7410f-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)