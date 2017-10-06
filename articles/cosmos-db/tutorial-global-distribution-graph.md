---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API Graph | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API Graph."
services: cosmos-db
keywords: distribution globale, graph, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API Graph

Dans cet article, nous montrons comment toouse hello distribution globale de base de données Azure Cosmos toosetup portail Azure et connectez-vous à l’aide de hello l’API Graph (version préliminaire).

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello [API graphiques](graph-introduction.md) (version préliminaire)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Connexion à l’aide de l’API Graph hello hello .NET SDK à l’aide de la région préférée tooa

Hello API Graph est exposée comme une bibliothèque d’extension par-dessus hello DocumentDB SDK.

Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document. Pour ce faire, vous pouvez définir la stratégie de connexion hello. Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale en cours et la liste de préférence hello spécifié, hello la plupart des point de terminaison optimale sera choisi par l’écriture de tooperform hello SDK et les opérations de lecture.

Cette liste de préférence est spécifiée lors de l’initialisation d’une connexion à l’aide de kits de développement logiciel hello. Hello kits de développement logiciel accepte un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.

* **Écrit**: hello Kit de développement logiciel enverra automatiquement toutes les écrit la zone d’écriture en cours toohello.
* **Lit**: toutes les lectures seront envoyés toohello de première région disponibles dans la liste de PreferredLocations hello. En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite. Hello kits de développement logiciel tente uniquement tooread de régions hello spécifié dans PreferredLocations. Ainsi, par exemple, si hello Cosmos DB compte n’est disponible dans trois régions, mais le client de hello spécifie uniquement deux des régions de non-écriture hello pour PreferredLocations, puis aucune lecture ne sera utilisée en dehors de la région d’écriture hello, même dans les cas de hello de basculement.

application Hello peut vérifier le point de terminaison hello actuel écriture et lecture de point de terminaison choisi par hello SDK par la vérification deux propriétés, WriteEndpoint et ReadEndpoint, disponible dans la version du Kit de développement logiciel 1.8 et versions ultérieures. Si hello PreferredLocations propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.

### <a name="using-hello-sdk"></a>À l’aide du Kit de développement logiciel de hello

Par exemple, Bonjour .NET SDK, hello `ConnectionPolicy` paramètre hello `DocumentClient` constructeur a une propriété appelée `PreferredLocations`. Cette propriété peut être définie tooa la liste des noms de région. noms d’affichage de Hello pour [régions Azure] [ regions] peut être spécifié dans le cadre de `PreferredLocations`.

> [!NOTE]
> URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées. service de Hello peut mettre à jour à tout moment. Hello SDK gère cette modification automatiquement.
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
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

[regions]: https://azure.microsoft.com/regions/

