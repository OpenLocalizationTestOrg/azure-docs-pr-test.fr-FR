---
title: "aaaHow tooquery graphique des données dans la base de données Azure Cosmos ? | Microsoft Docs"
description: "En savoir plus tooquery un graphique des données dans la base de données Azure Cosmos"
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
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="09a95-104">Azure Cosmos DB : Comment tooquery avec hello l’API Graph (aperçu) ?</span><span class="sxs-lookup"><span data-stu-id="09a95-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="09a95-105">Bonjour Azure Cosmos DB [API Graph](graph-introduction.md) (version préliminaire) prend en charge [GREMLINE](https://docs.mongodb.com/manual/tutorial/query-documents/) requêtes.</span><span class="sxs-lookup"><span data-stu-id="09a95-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="09a95-106">Cet article fournit des exemples de documents et des requêtes tooget que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="09a95-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="09a95-107">Informations de référence détaillées GREMLINE sont fournie dans hello [prise en charge GREMLINE](gremlin-support.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="09a95-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="09a95-108">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="09a95-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="09a95-109">Interrogation des données avec Gremlin</span><span class="sxs-lookup"><span data-stu-id="09a95-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09a95-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09a95-110">Prerequisites</span></span>

<span data-ttu-id="09a95-111">Pour ces requêtes toowork, vous devez disposer d’un compte de base de données Azure Cosmos et un graphique des données dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="09a95-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="09a95-112">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="09a95-112">Don't have any of those?</span></span> <span data-ttu-id="09a95-113">Hello complète [démarrage rapide de 5 minutes](create-graph-dotnet.md) ou hello [didacticiel pour développeur](tutorial-query-graph.md) toocreate un compte et le remplir votre base de données.</span><span class="sxs-lookup"><span data-stu-id="09a95-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="09a95-114">Vous pouvez exécuter hello suivant des requêtes à l’aide de hello [bibliothèque graph de Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console de GREMLINE](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), ou votre pilote GREMLINE favori.</span><span class="sxs-lookup"><span data-stu-id="09a95-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="09a95-115">Nombre des sommets dans le graphique de hello</span><span class="sxs-lookup"><span data-stu-id="09a95-115">Count vertices in hello graph</span></span>

<span data-ttu-id="09a95-116">Hello suivant extrait de code montre comment toocount hello nombre de sommets dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="09a95-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="09a95-117">Filtres</span><span class="sxs-lookup"><span data-stu-id="09a95-117">Filters</span></span>

<span data-ttu-id="09a95-118">Vous pouvez effectuer des filtres à l’aide de GREMLINE `has` et `hasLabel` les étapes et les associer à l’aide de `and`, `or`, et `not` toobuild les filtres plus complexe.</span><span class="sxs-lookup"><span data-stu-id="09a95-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="09a95-119">Azure Cosmos DB propose une indexation sans schéma de toutes les propriétés au sein de vos vertex et degrés pour les requêtes rapides :</span><span class="sxs-lookup"><span data-stu-id="09a95-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="09a95-120">Projection</span><span class="sxs-lookup"><span data-stu-id="09a95-120">Projection</span></span>

<span data-ttu-id="09a95-121">Vous pouvez projeter certaines propriétés dans les résultats de la requête hello à l’aide de hello `values` étape :</span><span class="sxs-lookup"><span data-stu-id="09a95-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="09a95-122">Rechercher des vertex et des bords associés</span><span class="sxs-lookup"><span data-stu-id="09a95-122">Find related edges and vertices</span></span>

<span data-ttu-id="09a95-123">Jusqu’ici, nous avons seulement abordé les opérateurs de requête fonctionnant dans n’importe quelle base de données.</span><span class="sxs-lookup"><span data-stu-id="09a95-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="09a95-124">Graphiques sont rapides et efficaces pour les opérations de parcours lorsque vous avez besoin toonavigate toorelated arêtes et les sommets.</span><span class="sxs-lookup"><span data-stu-id="09a95-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="09a95-125">Recherchons à présent tous les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="09a95-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="09a95-126">Pour ce faire, nous à l’aide de GREMLINE `outE` toofind hello tous les out-bords Thomas à partir de l’étape, puis parcourir les sommets dans toohello entre les bords à l’aide de GREMLINE `inV` étape :</span><span class="sxs-lookup"><span data-stu-id="09a95-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="09a95-127">éditeur de requête suivant de Hello effectue deux sauts toofind tous « Amis de vos amis » de Thomas, en appelant `outE` et `inV` deux fois.</span><span class="sxs-lookup"><span data-stu-id="09a95-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="09a95-128">Vous pouvez générer des requêtes plus complexes et implémenter la logique de parcours puissant de graphique à l’aide de GREMLINE, y compris filtre mélange des expressions, exécution à l’aide de bouclage hello `loop` étape et la navigation conditionnelle implémentation à l’aide de hello `choose` étape.</span><span class="sxs-lookup"><span data-stu-id="09a95-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="09a95-129">En savoir plus sur ce que la [prise en charge de Gremlin](gremlin-support.md) vous permet de faire !</span><span class="sxs-lookup"><span data-stu-id="09a95-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="09a95-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09a95-130">Next steps</span></span>

<span data-ttu-id="09a95-131">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="09a95-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09a95-132">Appris comment tooquery à l’aide du graphique</span><span class="sxs-lookup"><span data-stu-id="09a95-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="09a95-133">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="09a95-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09a95-134">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="09a95-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)