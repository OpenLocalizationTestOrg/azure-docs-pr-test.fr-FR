---
title: "Azure Cosmos DB : Comment à l’aide de tooquery hello des API DocumentDB ? | Microsoft Docs"
description: "En savoir plus tooquery avec hello API DocumentDB de base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="89b5f-104">Azure Cosmos DB : Comment tooquery avec l’API pour MongoDB ?</span><span class="sxs-lookup"><span data-stu-id="89b5f-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="89b5f-105">Bonjour Azure Cosmos DB [API pour MongoDB](mongodb-introduction.md) prend en charge [requêtes de shell MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="89b5f-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="89b5f-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="89b5f-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="89b5f-107">Interrogation des données avec MongoDB</span><span class="sxs-lookup"><span data-stu-id="89b5f-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="89b5f-108">Exemple de document</span><span class="sxs-lookup"><span data-stu-id="89b5f-108">Sample document</span></span>

<span data-ttu-id="89b5f-109">les requêtes de Hello dans cet article utilisent hello suivant l’exemple de document.</span><span class="sxs-lookup"><span data-stu-id="89b5f-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="89b5f-110"><a id="examplequery1"></a> Exemple de requête 1</span><span class="sxs-lookup"><span data-stu-id="89b5f-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="89b5f-111">Étant donné hello famille document d’exemple ci-dessus, renvoie des documents hello où correspond au champ de code hello de requête suivante de hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="89b5f-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="89b5f-112">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="89b5f-113">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="89b5f-114"><a id="examplequery2"></a>Exemple de requête 2</span><span class="sxs-lookup"><span data-stu-id="89b5f-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="89b5f-115">les requêtes suivant Hello retourne tous les enfants de hello dans la famille de hello.</span><span class="sxs-lookup"><span data-stu-id="89b5f-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="89b5f-116">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="89b5f-117">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="89b5f-118"><a id="examplequery3"></a>Exemple de requête 3</span><span class="sxs-lookup"><span data-stu-id="89b5f-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="89b5f-119">les requêtes suivant Hello retourne toutes les familles de hello qui sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="89b5f-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="89b5f-120">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="89b5f-121">**Résultats** aucun document ne sera renvoyé.</span><span class="sxs-lookup"><span data-stu-id="89b5f-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="89b5f-122"><a id="examplequery4"></a>Exemple de requête 4</span><span class="sxs-lookup"><span data-stu-id="89b5f-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="89b5f-123">les requêtes suivant Hello retourne toutes les familles de hello qui ne sont pas enregistrés.</span><span class="sxs-lookup"><span data-stu-id="89b5f-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="89b5f-124">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="89b5f-125">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="89b5f-126">}</span><span class="sxs-lookup"><span data-stu-id="89b5f-126">}</span></span>

## <span data-ttu-id="89b5f-127"><a id="examplequery5"></a>Exemple de requête 5</span><span class="sxs-lookup"><span data-stu-id="89b5f-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="89b5f-128">les requêtes suivant Hello retourne toutes les familles de hello qui ne sont pas enregistrés et l’état est NY.</span><span class="sxs-lookup"><span data-stu-id="89b5f-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="89b5f-129">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="89b5f-130">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="89b5f-131">}</span><span class="sxs-lookup"><span data-stu-id="89b5f-131">}</span></span>


## <span data-ttu-id="89b5f-132"><a id="examplequery6"></a>Exemple de requête 6</span><span class="sxs-lookup"><span data-stu-id="89b5f-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="89b5f-133">les requêtes suivant Hello retourne toutes les familles de hello où les classes enfants sont 8.</span><span class="sxs-lookup"><span data-stu-id="89b5f-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="89b5f-134">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="89b5f-135">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="89b5f-136">}</span><span class="sxs-lookup"><span data-stu-id="89b5f-136">}</span></span>

## <span data-ttu-id="89b5f-137"><a id="examplequery7"></a>Exemple de requête 7</span><span class="sxs-lookup"><span data-stu-id="89b5f-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="89b5f-138">les requêtes suivant Hello retourne toutes les familles de hello où la taille du tableau des enfants est 3.</span><span class="sxs-lookup"><span data-stu-id="89b5f-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="89b5f-139">**Requête**</span><span class="sxs-lookup"><span data-stu-id="89b5f-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="89b5f-140">**Résultats**</span><span class="sxs-lookup"><span data-stu-id="89b5f-140">**Results**</span></span>

<span data-ttu-id="89b5f-141">Aucun résultat n’est renvoyé car aucune n’a plus de 2 enfants.</span><span class="sxs-lookup"><span data-stu-id="89b5f-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="89b5f-142">Uniquement lorsque le paramètre est 2 cette requête se réussissent et complète pour le document hello.</span><span class="sxs-lookup"><span data-stu-id="89b5f-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89b5f-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89b5f-143">Next steps</span></span>

<span data-ttu-id="89b5f-144">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="89b5f-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89b5f-145">Appris comment tooquery à l’aide de MongoDB</span><span class="sxs-lookup"><span data-stu-id="89b5f-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="89b5f-146">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.</span><span class="sxs-lookup"><span data-stu-id="89b5f-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89b5f-147">Distribuer vos données globalement</span><span class="sxs-lookup"><span data-stu-id="89b5f-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

