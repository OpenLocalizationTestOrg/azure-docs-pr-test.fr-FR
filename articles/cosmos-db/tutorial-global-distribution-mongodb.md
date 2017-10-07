---
title: didacticiel de distribution globale Cosmos DB aaaAzure pour MongoDB API | Documents Microsoft
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API de MongoDB."
services: cosmos-db
keywords: diffusion mondiale, MongoDB
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="b4f50-104">Comment l’à l’aide de distribution globale de base de données Azure Cosmos toosetup hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="b4f50-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="b4f50-105">Dans cet article, nous montrons comment toouse hello toosetup portail Azure distribution globale de base de données Azure Cosmos et connectez-vous à l’aide de hello MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="b4f50-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="b4f50-106">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="b4f50-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b4f50-107">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b4f50-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="b4f50-108">Configurer la distribution globale à l’aide de hello [MongoDB API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b4f50-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="b4f50-109">Vérification de votre configuration régionale à l’aide de hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="b4f50-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="b4f50-110">moyen le plus simple de vérifier votre configuration globale dans l’API de MongoDB est toorun hello de double Hello *isMaster()* commande hello de commande Mongo.</span><span class="sxs-lookup"><span data-stu-id="b4f50-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="b4f50-111">À partir de votre interpréteur de commandes Mongo :</span><span class="sxs-lookup"><span data-stu-id="b4f50-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="b4f50-112">Résultats de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="b4f50-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="b4f50-113">Connexion à l’aide de hello MongoDB API la région préférée tooa</span><span class="sxs-lookup"><span data-stu-id="b4f50-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="b4f50-114">Hello MongoDB API permet de vous toospecify préférence de lecture de votre collection pour une base de données distribué internationalement.</span><span class="sxs-lookup"><span data-stu-id="b4f50-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="b4f50-115">Pour les deux faible latence lectures et globale haute disponibilité, nous vous recommandons de définir les préférences de lecture de votre collection trop*le plus proche*.</span><span class="sxs-lookup"><span data-stu-id="b4f50-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="b4f50-116">Une préférence de lecture de *le plus proche* est tooread configuré à partir de la région de hello le plus proche.</span><span class="sxs-lookup"><span data-stu-id="b4f50-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="b4f50-117">Pour les applications avec un serveur principal en lecture/écriture région, une région secondaire pour la récupération d’urgence (DR) scénarios, nous vous recommandons de définir les préférences de lecture de votre collection trop*secondaire préféré*.</span><span class="sxs-lookup"><span data-stu-id="b4f50-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="b4f50-118">Une préférence de lecture de *secondaire préféré* est tooread configuré à partir de la région secondaire hello lors de la région principale de hello n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="b4f50-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="b4f50-119">Enfin, si vous devez spécifier comme toomanually vos zones de lecture.</span><span class="sxs-lookup"><span data-stu-id="b4f50-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="b4f50-120">Vous pouvez définir la région de hello balise au sein de vos préférences de lecture.</span><span class="sxs-lookup"><span data-stu-id="b4f50-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="b4f50-121">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b4f50-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="b4f50-122">Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b4f50-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="b4f50-123">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b4f50-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4f50-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4f50-124">Next steps</span></span>

<span data-ttu-id="b4f50-125">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="b4f50-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4f50-126">Configurer la distribution globale à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b4f50-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="b4f50-127">Configurer la distribution globale à l’aide de hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b4f50-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="b4f50-128">Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b4f50-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4f50-129">Développer localement avec l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="b4f50-129">Develop locally with hello emulator</span></span>](local-emulator.md)
