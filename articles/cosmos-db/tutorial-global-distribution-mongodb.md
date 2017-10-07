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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Comment l’à l’aide de distribution globale de base de données Azure Cosmos toosetup hello MongoDB API

Dans cet article, nous montrons comment toouse hello toosetup portail Azure distribution globale de base de données Azure Cosmos et connectez-vous à l’aide de hello MongoDB API.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello [MongoDB API](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Vérification de votre configuration régionale à l’aide de hello MongoDB API
moyen le plus simple de vérifier votre configuration globale dans l’API de MongoDB est toorun hello de double Hello *isMaster()* commande hello de commande Mongo.

À partir de votre interpréteur de commandes Mongo :

   ```
      db.isMaster()
   ```
   
Résultats de l’exemple :

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Connexion à l’aide de hello MongoDB API la région préférée tooa

Hello MongoDB API permet de vous toospecify préférence de lecture de votre collection pour une base de données distribué internationalement. Pour les deux faible latence lectures et globale haute disponibilité, nous vous recommandons de définir les préférences de lecture de votre collection trop*le plus proche*. Une préférence de lecture de *le plus proche* est tooread configuré à partir de la région de hello le plus proche.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Pour les applications avec un serveur principal en lecture/écriture région, une région secondaire pour la récupération d’urgence (DR) scénarios, nous vous recommandons de définir les préférences de lecture de votre collection trop*secondaire préféré*. Une préférence de lecture de *secondaire préféré* est tooread configuré à partir de la région secondaire hello lors de la région principale de hello n’est pas disponible.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Enfin, si vous devez spécifier comme toomanually vos zones de lecture. Vous pouvez définir la région de hello balise au sein de vos préférences de lecture.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

C’est ici que s’achève ce didacticiel. Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md). Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello APIs DocumentDB

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.

> [!div class="nextstepaction"]
> [Développer localement avec l’émulateur de hello](local-emulator.md)
