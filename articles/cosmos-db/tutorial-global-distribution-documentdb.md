---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API DocumentDB | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API DocumentDB."
services: cosmos-db
keywords: distribution mondiale, documentdb
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
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API DocumentDB

Dans cet article, nous montrons comment toouse hello toosetup portail Azure distribution globale de base de données Azure Cosmos et connectez-vous à l’aide de hello API DocumentDB.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello [APIs DocumentDB](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Connexion tooa la région préférée à l’aide de hello API DocumentDB

Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document. Pour ce faire, vous pouvez définir la stratégie de connexion hello. Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale en cours et la liste de préférence hello spécifié, hello la plupart des point de terminaison optimale est sélectionnée par hello DocumentDB SDK tooperform écrire et lire des opérations.

Cette liste de préférence est spécifiée lors de l’initialisation d’une connexion à l’aide de kits de développement logiciel hello DocumentDB. Hello kits de développement logiciel accepte un paramètre facultatif « PreferredLocations » qui est une liste ordonnée des régions Azure.

Hello Kit de développement logiciel enverra automatiquement région pour l’écriture de toutes les écritures toohello actuelle.

Toutes les lectures seront envoyés toohello de première région disponibles dans la liste de PreferredLocations hello. En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite.

Hello kits de développement logiciel tente uniquement tooread de régions hello spécifié dans PreferredLocations. Ainsi, par exemple, si hello compte de base de données est disponible dans trois régions, mais le client de hello spécifie uniquement deux des régions de non-écriture hello pour PreferredLocations, puis aucune lecture ne sera utilisée en dehors de la région d’écriture hello, même dans les cas de hello de basculement.

application Hello peut vérifier le point de terminaison hello actuel écriture et lecture de point de terminaison choisi par hello SDK par la vérification deux propriétés, WriteEndpoint et ReadEndpoint, disponible dans la version du Kit de développement logiciel 1.8 et versions ultérieures.

Si hello PreferredLocations propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.

## <a name="net-sdk"></a>Kit de développement logiciel (SDK) .NET
Hello SDK peut servir sans aucune modification du code. Dans ce cas, hello SDK dirige les opérations de lecture automatiquement et écrit la zone d’écriture en cours toohello.

Dans la version 1.8 de hello .NET SDK, hello ConnectionPolicy paramètre de constructeur de DocumentClient hello est une propriété appelée Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Cette propriété est de type Collection `<string>` et doit contenir une liste des noms de région. les valeurs de chaîne Hello sont mis en forme par colonne de nom de la région de hello sur hello [régions Azure] [ regions] page, sans espaces avant ou après hello premier et dernier caractère respectivement.

écriture en cours de Hello et lecture des points de terminaison sont disponibles dans DocumentClient.WriteEndpoint et DocumentClient.ReadEndpoint respectivement.

> [!NOTE]
> URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées. service de Hello peut mettre à jour à tout moment. Hello SDK gère cette modification automatiquement.
>
>

```csharp
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

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>SDK Node.js, JavaScript et Python
Hello SDK peut servir sans aucune modification du code. Dans ce cas, hello que SDK dirigera automatiquement à la fois lit et écrit la zone d’écriture en cours toohello.

Dans la version 1.8 et version ultérieure de chaque SDK, hello ConnectionPolicy paramètre hello DocumentClient constructeur une nouvelle propriété nommée DocumentClient.ConnectionPolicy.PreferredLocations. Ce paramètre est un tableau de chaînes qui prend une liste de noms de régions. les noms de Hello sont mis en forme par colonne de nom de la région de hello Bonjour [régions Azure] [ regions] page. Vous pouvez également utiliser des constantes de hello prédéfini dans l’objet de commodité hello AzureDocuments.Regions

écriture en cours de Hello et lecture des points de terminaison sont disponibles dans DocumentClient.getWriteEndpoint et DocumentClient.getReadEndpoint respectivement.

> [!NOTE]
> URL de Hello pour les points de terminaison hello ne doivent pas être considérés comme des constantes de longue durées. service de Hello peut mettre à jour à tout moment. Hello SDK gère automatiquement ce changement.
>
>

Voici un exemple de code pour NodeJS/Javascript. Python et Java suivront hello même modèle.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Une fois qu’un compte de base de données a mis à disposition dans plusieurs régions, les clients peuvent interroger sa disponibilité en effectuant une requête GET sur hello suivant l’URI.

    https://{databaseaccount}.documents.azure.com/

service de Hello renvoie la liste des régions et de leur base de données Azure Cosmos point de terminaison correspondant URI pour les réplicas de hello. zone d’écriture en cours Hello est indiqué dans la réponse de hello. client de Hello peut ensuite sélectionner point de terminaison approprié hello pour toutes les autres demandes d’API REST comme suit.

Exemple de réponse

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* PUT, POST et DELETE de toutes les demandes doivent passer toohello indiqué écrire URI
* Obtient tous les et les autres demandes en lecture seule (par exemple les requêtes) peuvent être tooany de point de terminaison de choix du client hello

Écriture des régions tooread uniquement les demandes échouent avec le code d’erreur HTTP 403 (« interdit »).

Si la zone d’écriture hello change après phase de la découverte initiale du client hello, ultérieur écrit toohello précédente région d’écriture échoue avec le code d’erreur HTTP 403 (« interdit »). client de Hello doit ensuite obtenir la liste des régions hello nouveau tooget hello écriture mis à jour la région.

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

