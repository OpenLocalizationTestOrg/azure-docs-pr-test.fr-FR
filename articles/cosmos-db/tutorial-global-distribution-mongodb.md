---
title: "Didacticiel de diffusion mondiale d’Azure Cosmos DB pour l’API MongoDB | Documents Microsoft"
description: "Découvrez comment configurer la diffusion mondiale d’Azure Cosmos DB à l’aide de l’API MongoDB."
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="765b1-104">Comment configurer la diffusion mondiale d’Azure Cosmos DB à l’aide de l’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="765b1-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="765b1-105">Dans cet article, nous vous montrons comment utiliser le portail Azure pour configurer la diffusion mondiale d’Azure Cosmos DB, puis établir une connexion à l’aide de l’API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="765b1-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="765b1-106">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="765b1-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="765b1-107">Configurer la diffusion mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="765b1-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="765b1-108">Configurer la diffusion mondiale à l’aide de [l’API MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="765b1-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="765b1-109">Vérification de votre configuration régionale avec l’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="765b1-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="765b1-110">La façon la plus simple de vérifier votre configuration globale au sein de l’API pour MongoDB consiste à exécuter la commande *isMaster()* à partir de l’interpréteur de commandes Mongo.</span><span class="sxs-lookup"><span data-stu-id="765b1-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="765b1-111">À partir de votre interpréteur de commandes Mongo :</span><span class="sxs-lookup"><span data-stu-id="765b1-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="765b1-112">Résultats de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="765b1-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="765b1-113">Connexion à une région de prédilection avec l’API MongoDB</span><span class="sxs-lookup"><span data-stu-id="765b1-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="765b1-114">L’API MongoDB vous permet de spécifier les préférences de lecture de votre collection pour une base de données mondialement diffusée.</span><span class="sxs-lookup"><span data-stu-id="765b1-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="765b1-115">Pour les lectures à faible latence et la haute disponibilité globale, nous vous recommandons de définir les préférences de lecture de votre collection sur *La plus proche*.</span><span class="sxs-lookup"><span data-stu-id="765b1-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="765b1-116">Une préférence de lecture définie sur *La plus proche* est configurée pour lire à partir de la région la plus proche.</span><span class="sxs-lookup"><span data-stu-id="765b1-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="765b1-117">Pour les applications avec une région primaire en lecture/écriture et une région secondaire pour les scénarios de récupération d’urgence, nous vous recommandons de définir les préférences de lecture de votre collection sur *Secondary preferred* (Secondaire par défaut).</span><span class="sxs-lookup"><span data-stu-id="765b1-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="765b1-118">Une préférence de lecture définie sur *Secondary preferred* (Secondaire par défaut) est configurée pour lire à partir de la région secondaire lorsque la région primaire n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="765b1-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="765b1-119">Enfin, si vous souhaitez spécifier manuellement vos régions de lecture,</span><span class="sxs-lookup"><span data-stu-id="765b1-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="765b1-120">vous pouvez définir la balise de la région dans vos préférences de lecture.</span><span class="sxs-lookup"><span data-stu-id="765b1-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="765b1-121">C’est ici que s’achève ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="765b1-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="765b1-122">Découvrez comment gérer la cohérence de votre compte répliqué à l’échelle mondiale en lisant l’article [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="765b1-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="765b1-123">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="765b1-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="765b1-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="765b1-124">Next steps</span></span>

<span data-ttu-id="765b1-125">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="765b1-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="765b1-126">Configurer la distribution mondiale à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="765b1-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="765b1-127">Configurer la distribution mondiale à l’aide des API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="765b1-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="765b1-128">Vous pouvez maintenant passer au didacticiel suivant pour apprendre à développer en local à l’aide de l’émulateur local Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="765b1-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="765b1-129">Développer en local avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="765b1-129">Develop locally with the emulator</span></span>](local-emulator.md)