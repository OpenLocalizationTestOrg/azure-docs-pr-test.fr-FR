---
title: "Comment effectuer des interrogation avec le langage SQL dans Azure Cosmos DB ? | Microsoft Docs"
description: "Apprendre à interroger à l’aide de données DocumentDB avec le langage SQL dans Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="6d703-104">Azure Cosmos DB : Comment effectuer des interrogations avec le langage .SQL ?</span><span class="sxs-lookup"><span data-stu-id="6d703-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="6d703-105">L’[API DocumentDB](documentdb-introduction.md) Azure Cosmos DB prend en charge l’interrogation de documents à l’aide de SQL.</span><span class="sxs-lookup"><span data-stu-id="6d703-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="6d703-106">Cet article fournit un exemple de document et deux exemples de requêtes SQL et de résultats.</span><span class="sxs-lookup"><span data-stu-id="6d703-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="6d703-107">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d703-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6d703-108">Interrogation des données avec SQL</span><span class="sxs-lookup"><span data-stu-id="6d703-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="6d703-109">Exemple de document</span><span class="sxs-lookup"><span data-stu-id="6d703-109">Sample document</span></span>

<span data-ttu-id="6d703-110">L’exemple de document suivant est utilisé pour les interrogations SQL de cet article.</span><span class="sxs-lookup"><span data-stu-id="6d703-110">The SQL queries in this article use the following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="6d703-111">Où puis-je exécuter des requêtes SQL ?</span><span class="sxs-lookup"><span data-stu-id="6d703-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="6d703-112">Vous pouvez exécuter des requêtes à l’aide de l’Explorateur de données dans le portail Azure, via l’[API REST et Kits de développement logiciel (SDK) ](documentdb-sdk-dotnet.md)et même l’[interface de requête](https://www.documentdb.com/sql/demo), qui exécute des requêtes sur un ensemble d’exemples de données existant.</span><span class="sxs-lookup"><span data-stu-id="6d703-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="6d703-113">Pour plus d’informations sur les requêtes SQL, consultez :</span><span class="sxs-lookup"><span data-stu-id="6d703-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="6d703-114">Requête SQL et syntaxe SQL</span><span class="sxs-lookup"><span data-stu-id="6d703-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="6d703-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6d703-115">Prerequisites</span></span>

<span data-ttu-id="6d703-116">Ce didacticiel suppose que vous ayez un compte et une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6d703-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="6d703-117">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="6d703-117">Don't have any of those?</span></span> <span data-ttu-id="6d703-118">Lancez le [démarrage rapide de 5 minutes](create-mongodb-nodejs.md) ou le [didacticiel destiné aux développeurs](tutorial-develop-mongodb.md) pour créer un compte et une collection.</span><span class="sxs-lookup"><span data-stu-id="6d703-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="6d703-119">Exemple de requête 1</span><span class="sxs-lookup"><span data-stu-id="6d703-119">Example query 1</span></span>

<span data-ttu-id="6d703-120">Étant donné l’exemple de document de famille ci-dessus, la requête SQL suivante renvoie les documents où le champ id correspond à `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="6d703-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="6d703-121">Comme il s’agit d’une instruction `SELECT *`, le résultat de la requête est le document JSON complet :</span><span class="sxs-lookup"><span data-stu-id="6d703-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="6d703-122">**Requête**</span><span class="sxs-lookup"><span data-stu-id="6d703-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="6d703-123">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="6d703-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="6d703-124">Exemple de requête 2</span><span class="sxs-lookup"><span data-stu-id="6d703-124">Example query 2</span></span>

<span data-ttu-id="6d703-125">La requête suivante renvoie tous les noms donnés des enfants de la famille dont l’ID correspond à `WakefieldFamily` classés par classe.</span><span class="sxs-lookup"><span data-stu-id="6d703-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="6d703-126">**Requête**</span><span class="sxs-lookup"><span data-stu-id="6d703-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="6d703-127">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="6d703-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="6d703-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d703-128">Next steps</span></span>

<span data-ttu-id="6d703-129">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="6d703-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d703-130">Effectuer des interrogations à l’aide de SQL</span><span class="sxs-lookup"><span data-stu-id="6d703-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="6d703-131">Vous pouvez maintenant poursuivre avec le didacticiel suivant montrant comment distribuer vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="6d703-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d703-132">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="6d703-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

