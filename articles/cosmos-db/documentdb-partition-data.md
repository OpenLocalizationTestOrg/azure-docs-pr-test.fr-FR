---
title: "aaaPartitioning et mise à l’échelle dans la base de données Azure Cosmos | Documents Microsoft"
description: "En savoir plus sur le partitionnement de base de données Azure Cosmos, comment tooconfigure partitionnement et les clés de partition, et comment toopick hello droite clé de partition pour votre application."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Partitionnement de base de données Azure Cosmos à l’aide de hello API DocumentDB

[Base de données Microsoft Azure Cosmos](../cosmos-db/introduction.md) est un toohelp de service conçu global de base de données distribuées, comportant plusieurs modèles vous atteindre des performances rapides et prévisibles et une échelle en toute transparence avec votre application qu’elle se développe. 

Cet article fournit une vue d’ensemble de la toowork avec le partitionnement de conteneurs Cosmos DB avec hello API DocumentDB. Consultez [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) afin de découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB. 

tooget a démarré avec le code, de télécharger le projet à partir de hello [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :   

* Comment le partitionnement dans Azure Cosmos DB fonctionne-t-il ?
* Comment configurer le partitionnement dans Azure Cosmos DB ?
* Quelles sont les clés de partition, et comment choisir hello bonne clé de partition pour mon application ?

tooget a démarré avec le code, de télécharger le projet à partir de hello [Azure Cosmos DB performances test pilote, exemple](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Clés de partition

Bonjour API DocumentDB, vous spécifiez la définition de clé de partition hello sous forme de hello d’un chemin d’accès JSON. Hello tableau suivant présente des exemples de définitions de clé de partition et les valeurs hello correspondant tooeach. clé de partition Hello est spécifié comme un chemin d’accès, par exemple, `/department` représente hello département de propriété. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Clé de partition</strong></p></td>
            <td valign="top"><p><strong>Description</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Correspond à valeur toohello doc.department où doc est élément de hello.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Correspond à valeur toohello doc.properties.name où le document est l’élément hello (propriété imbriquée).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Correspond valeur toohello doc.id (clé de partition et les id sont hello même propriété).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"nom de service"</p></td>
            <td valign="top"><p>Correspond à valeur toohello document [« nom de service »] où doc est élément de hello.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> syntaxe de Hello pour la clé de partition est la spécification de chemin d’accès toohello similaire pour l’indexation de chemins d’accès de la stratégie à hello différence près que hello du chemin d’accès correspond propriété toohello au lieu de la valeur de hello, il n’y a aucun caractère générique à la fin de hello. Par exemple, vous devez spécifier /department/? tooindex hello valeurs sous service, mais spécifier /department en tant que définition de clé de partition hello. clé de partition Hello implicitement indexé et ne peut pas être exclu de l’indexation à l’aide des remplacements de la stratégie d’indexation.
> 
> 

Examinons à présent l’impact des performances hello de votre application par choix hello de clé de partition.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Utilisation de hello kits de développement de base de données Azure Cosmos
Avec l’[API REST version 2015-12-16](/rest/api/documentdb/), Azure Cosmos DB a ajouté la prise en charge du partitionnement automatique. Dans des conteneurs toocreate partitionnée de commande, vous devez télécharger les versions du Kit de développement logiciel 1.6.0 ou plus récente dans un des hello la prise en charge des plateformes de kit de développement logiciel (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Création de conteneurs
Hello exemple suivant illustre un toocreate d’extrait de code .NET un données de télémétrie conteneur toostore appareil 20 000 d’unités de demande par seconde de débit. Hello SDK définit la valeur de OfferThroughput hello (qui définit à son tour hello `x-ms-offer-throughput` en-tête de demande dans l’API REST de hello). Ici, nous avons défini hello `/deviceId` en tant que clé de partition hello. choix de Hello de clé de partition est enregistré avec reste hello de métadonnées du conteneur hello comme nom et la stratégie d’indexation.

Pour cet exemple, nous avons choisi `deviceId` étant donné que nous savons que (a), car il existe un grand nombre de périphériques, écritures peuvent être distribués uniformément sur plusieurs partitions et nous autorisez tooscale hello de base de données tooingest massive des volumes de données et (b) plus de demandes de hello comme l’extraction de la lecture de la plus récente de hello pour un périphérique sont tooa étendue unique ID de périphérique et peuvent être récupérés à partir d’une seule partition.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Cette méthode appelle une API REST tooCosmos DB et service de hello configurera un nombre de partitions basé sur le débit hello demandée. Vous pouvez modifier le débit de hello d’un conteneur de besoins évoluent. 

### <a name="reading-and-writing-items"></a>Lecture et écriture d’éléments
À présent, nous allons insérer des données dans Cosmos DB. Voici un exemple de classe contenant la lecture d’une unité et un tooinsert de tooCreateDocumentAsync appel un nouveau périphérique de lecture dans un conteneur. Il s’agit d’un exemple en exploitant hello API DocumentDB :

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

Nous allons élément hello par sa clé de partition et l’id de lire, mettre à jour et le supprimer puis dans la dernière étape, par id et clé de partition. Notez que les lectures hello incluent une valeur de PartitionKey (correspondante toohello `x-ms-documentdb-partitionkey` en-tête de demande dans l’API REST de hello).

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a>Interrogation de conteneurs partitionnés
Lorsque vous interrogez des données dans les conteneurs partitionnées, Cosmos DB automatiquement les itinéraires hello partitions toohello de requête correspondant des valeurs de clé de partition toohello spécifiées dans le filtre de hello (le cas échéant). Par exemple, cette requête est routé toojust hello partition contenant hello clé de partition « XMS-0001 ».

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

Cosmos DB prend en charge les [fonctions d’agrégation](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` et `AVG` sur des conteneurs partitionnés à l’aide de SQL à partir des Kits de développement logiciel (SDK) 1.12.0 et versions ultérieures. Les requêtes doivent inclure un opérateur d’agrégation unique et doivent inclure une valeur unique dans la projection de hello.

### <a name="parallel-query-execution"></a>Exécution de requêtes parallèles
Hello kits de développement logiciel DB Cosmos à 1.9.0 et supérieur prennent en charge les options d’exécution de requête parallèle, qui vous permettront d’une latence faible tooperform de requêtes sur les collections partitionnées, même lorsqu’ils ont besoin tootouch un grand nombre de partitions. Par exemple, hello suivant la requête est configuré toorun en parallèle sur plusieurs partitions.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Vous pouvez gérer l’exécution des requêtes parallèles en réglant hello paramètres suivants :

* En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler hello degré de parallélisme c'est-à-dire hello maximal de partitions du conteneur de toohello connexions réseau simultanées. Si vous affectez ce trop-1, degré hello de parallélisme est géré par hello SDK. Si hello `MaxDegreeOfParallelism` n’est pas spécifié ou la valeur de too0, qui est la valeur par défaut de hello, il y aura des partitions d’un réseau unique connexion toohello du conteneur.
* En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête. Si vous omettez ce paramètre ou cette trop-1, nombre de hello d’éléments mis en mémoire tampon lors de l’exécution de requête parallèle est géré par hello SDK.

Fonction hello même d’état de la collection de hello, une requête parallèle renvoie des résultats dans le même ordre que dans l’exécution séquentielle de hello. Lorsque vous effectuez une requête de partitions croisées qui inclut le tri (ORDER BY et/ou haut), problèmes de kit de développement de base de données Azure Cosmos hello hello requête en parallèle sur les partitions et les fusions partiellement trié entraîne hello client côté tooproduce globalement les résultats classés.

### <a name="executing-stored-procedures"></a>Exécution de procédures stockées
Vous pouvez également exécuter des transactions atomiques par rapport à des documents avec hello même ID de périphérique, par exemple, si vous gérez des agrégats ou hello dernier état d’un périphérique dans un seul élément. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
Dans la section suivante de hello, nous examiner comment vous pouvez déplacer les conteneurs toopartitioned à partir des conteneurs de partition unique.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, nous avons fourni une vue d’ensemble de la toowork avec le partitionnement de base de données Azure Cosmos des conteneurs avec hello API DocumentDB. Consultez également [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) pour découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB. 

* Effectuez un test des performances et de la mise à l’échelle avec Azure Cosmos DB. Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md) pour obtenir un exemple.
* Commencer le codage par hello [kits de développement logiciel](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/)
* Apprenez-en davantage sur le [débit approvisionné dans Azure Cosmos DB](request-units.md)

