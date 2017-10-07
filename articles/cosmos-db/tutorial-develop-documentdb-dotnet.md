---
title: "Azure Cosmos DB : Développer avec hello API DocumentDB dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API DocumentDB Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB : Développer avec hello API DocumentDB dans .NET

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce didacticiel montre comment toocreate un compte de base de données Azure Cosmos à l’aide de hello portail Azure et ensuite créer une base de données du document et de la collection avec une [clé de partition](documentdb-partition-data.md#partition-keys) à l’aide de hello [DocumentDB .NET API](documentdb-introduction.md). En définissant une clé de partition lorsque vous créez une collection, votre application est prête tooscale aptitude à mesure que vos données augmentent. 

Les tâches suivantes hello didacticiel couvre à l’aide de hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Création d’un compte Azure Cosmos DB
> * Créer une base de données et une collection avec une clé de partition
> * Créer des documents JSON
> * Mettre à jour un document
> * Interroger des collections partitionnées
> * Exécuter des procédures stockées
> * Supprimer un document
> * Supprimer une base de données

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/). 
    * Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel, si vous souhaitez que toouse un environnement local qui émule les services d’Azure DocumentDB hello à des fins de développement.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Création d’un compte Azure Cosmos DB

Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.

> [!TIP]
> * Possédez-vous un compte Azure Cosmos DB ? Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)
> * Possédiez-vous un compte Azure DocumentDB ? Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).  
> * Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Configurer votre solution Visual Studio
1. Ouvrez **Visual Studio** sur votre ordinateur.
2. Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.
3. Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **l’application Console (.NET Framework)**, nommez votre projet, puis cliquez sur **OK**.
   ![Capture d’écran de la fenêtre de nouveau projet hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**
    
    ![Capture d’écran de hello droite Menu Clicked hello projet](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. Bonjour **NuGet** , cliquez sur **Parcourir**et le type **documentdb** dans la zone de recherche hello.
<!---stopped here--->
6. Dans les résultats de hello, recherchez **Microsoft.Azure.DocumentDB** et cliquez sur **installer**.
   ID de package Hello pour hello Azure Cosmos DB Client Library est [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Capture d’écran de hello Menu de NuGet pour la recherche de base de données Client SDK Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**. Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.

## <a id="Connect"></a>Ajoutez les références tooyour projet
les étapes restantes de Hello dans ce didacticiel fournir hello API DocumentDB code des extraits de code requis toocreate et mise à jour de base de données Azure Cosmos ressources dans votre projet.

Ajoutez d’abord ces applications tooyour de références.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Connecter votre application

Ajoutez ces deux constantes et votre variable *client* à votre application.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Ensuite, head sauvegarde toohello [portail Azure](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire. URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application.

Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**.

Copiez hello URI à partir du portail de hello et collez-la sur `<your endpoint URL>` dans le fichier program.cs de hello. Copie hello clé primaire à partir du portail de hello et collez-la sur `<your primary key>`. Être vraiment tooremove hello `<` et `>` à partir de vos valeurs.

![Capture d’écran de hello portail Azure utilisée par toocreate de didacticiel hello NoSQL une application console c#. Indique un compte de base de données Azure Cosmos, hello mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello, les clés et hello URI et les valeurs de clé primaire mise en surbrillance dans le panneau de clés hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Instancier hello DocumentClient

À présent, créez une nouvelle instance de hello **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Créer une base de données

Ensuite, créez une base de données Azure Cosmos [base de données](documentdb-resources.md#databases) à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello  **DocumentClient** classe à partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md). Une base de données est un conteneur logique de hello JSON de stockage de documents partitionné entre des collections.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Choisir une clé de partition 

Les collections sont des conteneurs servant au stockage des documents. Ce sont des ressources logiques. [Elles peuvent s’étendre sur une ou plusieurs partitions physiques](partition-data.md). A [clé de partition](documentdb-partition-data.md) est une propriété (ou le chemin d’accès) dans vos documents est utilisée toodistribute vos données entre les serveurs de hello ou les partitions. Tous les documents dont la même clé de partition sont stockées dans des hello hello même partition. 

Détermination d’une clé de partition d’est une décision importante de toomake avant de créer une collection. Les clés de partition sont une propriété (ou le chemin d’accès) dans vos documents qui peuvent être utilisées par la base de données Azure Cosmos toodistribute vos données entre plusieurs serveurs ou des partitions. COSMOS DB hache la valeur de clé de partition hello et utilise la partition de hello toodetermine hello haché résultat dans le document de hello toostore. Tous les documents dont la même clé de partition sont stockées dans des hello hello même partition, et les clés de partition ne peut pas être modifiés après la création d’une collection. 

Pour ce didacticiel, nous allons clé de partition tooset hello trop`/deviceId` ainsi que hello toutes les données hello pour un seul périphérique est stocké dans une partition unique. Vous souhaitez toochoose une clé de partition qui a un grand nombre de valeurs, chacune d’elles servent à hello sur la même fréquence tooensure Cosmos DB peut équilibrer la charge que vos données augmente et obtenir un débit complet de la collection de hello hello. 

Pour plus d’informations sur le partitionnement, consultez [comment toopartition et l’échelle dans la base de données Azure Cosmos ?](partition-data.md) 

## <a id="CreateColl"></a>Créer une collection 

Maintenant que nous savons notre clé de partition, `/deviceId`, permet de créer un [collection](documentdb-resources.md#collections) à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode ou [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient** classe. Une collection est un conteneur de documents JSON. Elle est associée à une logique d’application JavaScript. 

> [!WARNING]
> Création d’une collection a tarification implications, que vous réservez un débit de toocommunicate d’application hello avec la base de données Azure Cosmos. Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Méthode donc une API REST appeler tooAzure Cosmos DB et hello dispositions de service à un nombre de partitions basé sur le débit hello demandée. Vous pouvez modifier le débit d’une collection hello besoins évoluent à l’aide de hello SDK ou hello [portail Azure](set-throughput.md).

## <a id="CreateDoc"></a>Créer des documents JSON
Insérons maintenant des documents JSON dans Azure Cosmos DB. A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) méthode Hello **DocumentClient** classe. Les documents sont du contenu JSON (arbitraire) défini par l'utilisateur. Cet exemple de classe contient une lecture de l’appareil et un tooinsert de tooCreateDocumentAsync appel un nouveau périphérique de lecture dans une collection.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>Lire les données

Nous allons lire document hello par sa clé de partition et un Id à l’aide de la méthode de ReadDocumentAsync hello. Notez que les lectures hello incluent une valeur de PartitionKey (correspondante toohello `x-ms-documentdb-partitionkey` en-tête de demande dans l’API REST de hello).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Mettre à jour des données

Maintenant nous allons mettre à jour des données à l’aide de la méthode de ReplaceDocumentAsync hello.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Suppression de données

Vous permet de supprimer un document par clé de partition et l’id en utilisant la méthode de DeleteDocumentAsync hello.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Interroger des collections partitionnées

Lorsque vous interrogez des données dans des collections partitionnées, la base de données Azure Cosmos automatiquement les itinéraires hello partitions toohello de requête correspondant des valeurs de clé de partition toohello spécifiées dans le filtre de hello (le cas échéant). Par exemple, cette requête est routé toojust hello partition contenant hello clé de partition « XMS-0001 ».

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Bonjour requête suivante n’a pas de filtre sur la clé de partition hello (DeviceId) et les partitions tooall où elle est exécutée sur les index de la partition hello est déployée. Notez que vous avez toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Bonjour API REST) toohave hello SDK tooexecute une requête sur plusieurs partitions.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>Exécution de requêtes parallèles
Hello kits de développement Azure Cosmos DB DocumentDB à 1.9.0 et supérieur prennent en charge les options d’exécution de requête parallèle, qui vous permettront d’une latence faible tooperform de requêtes sur les collections partitionnées, même lorsqu’ils ont besoin tootouch un grand nombre de partitions. Par exemple, hello suivant la requête est configuré toorun en parallèle sur plusieurs partitions.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Vous pouvez gérer l’exécution des requêtes parallèles en réglant hello paramètres suivants :

* En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler le degré de hello de parallélisme c'est-à-dire hello nombre maximal de partitions de la collection de toohello connexions réseau simultanées. Si vous affectez ce trop-1, degré hello de parallélisme est géré par hello SDK. Si hello `MaxDegreeOfParallelism` n’est pas spécifié ou la valeur de too0, qui est la valeur par défaut de hello, il y aura des partitions d’un réseau unique connexion toohello la collection.
* En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête. Si vous omettez ce paramètre ou cette trop-1, nombre de hello d’éléments mis en mémoire tampon lors de l’exécution de requête parallèle est géré par hello SDK.

Fonction hello même d’état de la collection de hello, une requête parallèle renvoie des résultats dans le même ordre que dans l’exécution séquentielle de hello. Lorsque vous effectuez une requête de partitions croisées qui inclut le tri (ORDER BY et/ou haut), hello DocumentDB SDK émet des requêtes hello en parallèle sur plusieurs partitions et fusionne les résultats partiellement triés dans hello client côté tooproduce globalement les résultats classés.

## <a name="execute-stored-procedures"></a>Exécuter des procédures stockées
Enfin, vous pouvez exécuter des transactions atomiques par rapport à des documents avec hello même ID de périphérique, par exemple, si vous gérez des agrégats ou hello du dernier état d’un périphérique dans un document unique en ajoutant hello suivant du projet de code tooyour.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

Et le tour est joué ! Il s’hello principaux composants d’une application de base de données Azure Cosmos qui utilise une distribution de données de l’échelle de clé tooefficiently partition sur plusieurs partitions.  

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce didacticiel dans hello portail Azure par hello comme suit :

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur le nom unique de hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello : 

> [!div class="checklist"]
> * Créé un compte Azure Cosmos DB
> * Créé une base de données et une collection avec une clé de partition
> * Créé des documents JSON
> * Mis à jour un document
> * Interrogé des collections partitionnées
> * Exécuté une procédure stockée
> * Supprimé un document
> * Supprimé une base de données

Vous pouvez maintenant continuer le didacticiel suivant de toohello et importer des données supplémentaires tooyour Cosmos DB compte. 

> [!div class="nextstepaction"]
> [Importer des données dans Azure Cosmos DB](import-data.md)
