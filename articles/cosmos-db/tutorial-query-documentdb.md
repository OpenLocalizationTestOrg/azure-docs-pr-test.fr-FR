---
title: "tooquery aaaHow avec SQL dans la base de données Azure Cosmos ? | Microsoft Docs"
description: "En savoir plus tooquery avec des données avec SQL dans la base de données Azure Cosmos DocumentDB"
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
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="4cf99-104">Azure Cosmos DB : Comment tooquery à l’aide de SQL ?</span><span class="sxs-lookup"><span data-stu-id="4cf99-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="4cf99-105">Bonjour Azure Cosmos DB [API DocumentDB](documentdb-introduction.md) prend en charge l’interrogation de documents à l’aide de SQL.</span><span class="sxs-lookup"><span data-stu-id="4cf99-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="4cf99-106">Cet article fournit un exemple de document et deux exemples de requêtes SQL et de résultats.</span><span class="sxs-lookup"><span data-stu-id="4cf99-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="4cf99-107">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4cf99-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4cf99-108">Interrogation des données avec SQL</span><span class="sxs-lookup"><span data-stu-id="4cf99-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="4cf99-109">Exemple de document</span><span class="sxs-lookup"><span data-stu-id="4cf99-109">Sample document</span></span>

<span data-ttu-id="4cf99-110">les requêtes SQL Hello dans cet article utilisent hello suivant l’exemple de document.</span><span class="sxs-lookup"><span data-stu-id="4cf99-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="4cf99-111">Où puis-je exécuter des requêtes SQL ?</span><span class="sxs-lookup"><span data-stu-id="4cf99-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="4cf99-112">Vous pouvez exécuter des requêtes à l’aide de hello Explorateur de données Bonjour portail Azure, via hello [API REST et les kits de développement logiciel](documentdb-sdk-dotnet.md)et même hello [Query playground](https://www.documentdb.com/sql/demo), qui exécute des requêtes sur un jeu existant d’exemples de données.</span><span class="sxs-lookup"><span data-stu-id="4cf99-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="4cf99-113">Pour plus d’informations sur les requêtes SQL, consultez :</span><span class="sxs-lookup"><span data-stu-id="4cf99-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="4cf99-114">Requête SQL et syntaxe SQL</span><span class="sxs-lookup"><span data-stu-id="4cf99-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="4cf99-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4cf99-115">Prerequisites</span></span>

<span data-ttu-id="4cf99-116">Ce didacticiel suppose que vous ayez un compte et une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4cf99-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="4cf99-117">Cela n’est pas le cas ?</span><span class="sxs-lookup"><span data-stu-id="4cf99-117">Don't have any of those?</span></span> <span data-ttu-id="4cf99-118">Hello complète [démarrage rapide de 5 minutes](create-mongodb-nodejs.md) ou hello [didacticiel pour développeur](tutorial-develop-mongodb.md) toocreate un compte et la collection.</span><span class="sxs-lookup"><span data-stu-id="4cf99-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="4cf99-119">Exemple de requête 1</span><span class="sxs-lookup"><span data-stu-id="4cf99-119">Example query 1</span></span>

<span data-ttu-id="4cf99-120">Hello famille document d’exemple ci-dessus, suivant la requête SQL renvoie des documents hello où correspond au champ de code hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="4cf99-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="4cf99-121">Dans la mesure où il s’agit d’un `SELECT *` instruction, sortie hello de requête de hello est le document JSON complet hello :</span><span class="sxs-lookup"><span data-stu-id="4cf99-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="4cf99-122">**Requête**</span><span class="sxs-lookup"><span data-stu-id="4cf99-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="4cf99-123">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="4cf99-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="4cf99-124">Exemple de requête 2</span><span class="sxs-lookup"><span data-stu-id="4cf99-124">Example query 2</span></span>

<span data-ttu-id="4cf99-125">les requêtes suivant Hello retourne tous les noms de donné de hello d’enfants dans la famille hello dont l’id correspond à `WakefieldFamily` classés par leur qualité.</span><span class="sxs-lookup"><span data-stu-id="4cf99-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="4cf99-126">**Requête**</span><span class="sxs-lookup"><span data-stu-id="4cf99-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="4cf99-127">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="4cf99-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="4cf99-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4cf99-128">Next steps</span></span>

<span data-ttu-id="4cf99-129">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="4cf99-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4cf99-130">Appris comment tooquery à l’aide de SQL</span><span class="sxs-lookup"><span data-stu-id="4cf99-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="4cf99-131">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="4cf99-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cf99-132">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="4cf99-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

