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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="4949c-103">Partitionnement de base de données Azure Cosmos à l’aide de hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4949c-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="4949c-104">[Base de données Microsoft Azure Cosmos](../cosmos-db/introduction.md) est un toohelp de service conçu global de base de données distribuées, comportant plusieurs modèles vous atteindre des performances rapides et prévisibles et une échelle en toute transparence avec votre application qu’elle se développe.</span><span class="sxs-lookup"><span data-stu-id="4949c-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="4949c-105">Cet article fournit une vue d’ensemble de la toowork avec le partitionnement de conteneurs Cosmos DB avec hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4949c-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4949c-106">Consultez [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) afin de découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4949c-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="4949c-107">tooget a démarré avec le code, de télécharger le projet à partir de hello [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4949c-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="4949c-108">Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="4949c-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="4949c-109">Comment le partitionnement dans Azure Cosmos DB fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="4949c-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="4949c-110">Comment configurer le partitionnement dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="4949c-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="4949c-111">Quelles sont les clés de partition, et comment choisir hello bonne clé de partition pour mon application ?</span><span class="sxs-lookup"><span data-stu-id="4949c-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="4949c-112">tooget a démarré avec le code, de télécharger le projet à partir de hello [Azure Cosmos DB performances test pilote, exemple](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4949c-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="4949c-113">Clés de partition</span><span class="sxs-lookup"><span data-stu-id="4949c-113">Partition keys</span></span>

<span data-ttu-id="4949c-114">Bonjour API DocumentDB, vous spécifiez la définition de clé de partition hello sous forme de hello d’un chemin d’accès JSON.</span><span class="sxs-lookup"><span data-stu-id="4949c-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="4949c-115">Hello tableau suivant présente des exemples de définitions de clé de partition et les valeurs hello correspondant tooeach.</span><span class="sxs-lookup"><span data-stu-id="4949c-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="4949c-116">clé de partition Hello est spécifié comme un chemin d’accès, par exemple, `/department` représente hello département de propriété.</span><span class="sxs-lookup"><span data-stu-id="4949c-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="4949c-117"><strong>Clé de partition</strong></span><span class="sxs-lookup"><span data-stu-id="4949c-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4949c-118"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="4949c-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4949c-119">/department</span><span class="sxs-lookup"><span data-stu-id="4949c-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4949c-120">Correspond à valeur toohello doc.department où doc est élément de hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4949c-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="4949c-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4949c-122">Correspond à valeur toohello doc.properties.name où le document est l’élément hello (propriété imbriquée).</span><span class="sxs-lookup"><span data-stu-id="4949c-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4949c-123">/id</span><span class="sxs-lookup"><span data-stu-id="4949c-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4949c-124">Correspond valeur toohello doc.id (clé de partition et les id sont hello même propriété).</span><span class="sxs-lookup"><span data-stu-id="4949c-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4949c-125">/"nom de service"</span><span class="sxs-lookup"><span data-stu-id="4949c-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4949c-126">Correspond à valeur toohello document [« nom de service »] où doc est élément de hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="4949c-127">syntaxe de Hello pour la clé de partition est la spécification de chemin d’accès toohello similaire pour l’indexation de chemins d’accès de la stratégie à hello différence près que hello du chemin d’accès correspond propriété toohello au lieu de la valeur de hello, il n’y a aucun caractère générique à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="4949c-128">Par exemple, vous devez spécifier /department/?</span><span class="sxs-lookup"><span data-stu-id="4949c-128">For example, you would specify /department/?</span></span> <span data-ttu-id="4949c-129">tooindex hello valeurs sous service, mais spécifier /department en tant que définition de clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="4949c-130">clé de partition Hello implicitement indexé et ne peut pas être exclu de l’indexation à l’aide des remplacements de la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="4949c-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="4949c-131">Examinons à présent l’impact des performances hello de votre application par choix hello de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="4949c-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="4949c-132">Utilisation de hello kits de développement de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="4949c-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="4949c-133">Avec l’[API REST version 2015-12-16](/rest/api/documentdb/), Azure Cosmos DB a ajouté la prise en charge du partitionnement automatique.</span><span class="sxs-lookup"><span data-stu-id="4949c-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="4949c-134">Dans des conteneurs toocreate partitionnée de commande, vous devez télécharger les versions du Kit de développement logiciel 1.6.0 ou plus récente dans un des hello la prise en charge des plateformes de kit de développement logiciel (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="4949c-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="4949c-135">Création de conteneurs</span><span class="sxs-lookup"><span data-stu-id="4949c-135">Creating containers</span></span>
<span data-ttu-id="4949c-136">Hello exemple suivant illustre un toocreate d’extrait de code .NET un données de télémétrie conteneur toostore appareil 20 000 d’unités de demande par seconde de débit.</span><span class="sxs-lookup"><span data-stu-id="4949c-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="4949c-137">Hello SDK définit la valeur de OfferThroughput hello (qui définit à son tour hello `x-ms-offer-throughput` en-tête de demande dans l’API REST de hello).</span><span class="sxs-lookup"><span data-stu-id="4949c-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="4949c-138">Ici, nous avons défini hello `/deviceId` en tant que clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="4949c-139">choix de Hello de clé de partition est enregistré avec reste hello de métadonnées du conteneur hello comme nom et la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="4949c-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="4949c-140">Pour cet exemple, nous avons choisi `deviceId` étant donné que nous savons que (a), car il existe un grand nombre de périphériques, écritures peuvent être distribués uniformément sur plusieurs partitions et nous autorisez tooscale hello de base de données tooingest massive des volumes de données et (b) plus de demandes de hello comme l’extraction de la lecture de la plus récente de hello pour un périphérique sont tooa étendue unique ID de périphérique et peuvent être récupérés à partir d’une seule partition.</span><span class="sxs-lookup"><span data-stu-id="4949c-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

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

<span data-ttu-id="4949c-141">Cette méthode appelle une API REST tooCosmos DB et service de hello configurera un nombre de partitions basé sur le débit hello demandée.</span><span class="sxs-lookup"><span data-stu-id="4949c-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4949c-142">Vous pouvez modifier le débit de hello d’un conteneur de besoins évoluent.</span><span class="sxs-lookup"><span data-stu-id="4949c-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="4949c-143">Lecture et écriture d’éléments</span><span class="sxs-lookup"><span data-stu-id="4949c-143">Reading and writing items</span></span>
<span data-ttu-id="4949c-144">À présent, nous allons insérer des données dans Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4949c-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="4949c-145">Voici un exemple de classe contenant la lecture d’une unité et un tooinsert de tooCreateDocumentAsync appel un nouveau périphérique de lecture dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="4949c-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="4949c-146">Il s’agit d’un exemple en exploitant hello API DocumentDB :</span><span class="sxs-lookup"><span data-stu-id="4949c-146">This is an example leveraging hello DocumentDB API:</span></span>

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

<span data-ttu-id="4949c-147">Nous allons élément hello par sa clé de partition et l’id de lire, mettre à jour et le supprimer puis dans la dernière étape, par id et clé de partition. Notez que les lectures hello incluent une valeur de PartitionKey (correspondante toohello `x-ms-documentdb-partitionkey` en-tête de demande dans l’API REST de hello).</span><span class="sxs-lookup"><span data-stu-id="4949c-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="4949c-148">Interrogation de conteneurs partitionnés</span><span class="sxs-lookup"><span data-stu-id="4949c-148">Querying partitioned containers</span></span>
<span data-ttu-id="4949c-149">Lorsque vous interrogez des données dans les conteneurs partitionnées, Cosmos DB automatiquement les itinéraires hello partitions toohello de requête correspondant des valeurs de clé de partition toohello spécifiées dans le filtre de hello (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="4949c-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4949c-150">Par exemple, cette requête est routé toojust hello partition contenant hello clé de partition « XMS-0001 ».</span><span class="sxs-lookup"><span data-stu-id="4949c-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4949c-151">Bonjour requête suivante n’a pas de filtre sur la clé de partition hello (DeviceId) et les partitions tooall où elle est exécutée sur les index de la partition hello est déployée.</span><span class="sxs-lookup"><span data-stu-id="4949c-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4949c-152">Notez que vous avez toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Bonjour API REST) toohave hello SDK tooexecute une requête sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="4949c-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="4949c-153">Cosmos DB prend en charge les [fonctions d’agrégation](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` et `AVG` sur des conteneurs partitionnés à l’aide de SQL à partir des Kits de développement logiciel (SDK) 1.12.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4949c-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="4949c-154">Les requêtes doivent inclure un opérateur d’agrégation unique et doivent inclure une valeur unique dans la projection de hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="4949c-155">Exécution de requêtes parallèles</span><span class="sxs-lookup"><span data-stu-id="4949c-155">Parallel query execution</span></span>
<span data-ttu-id="4949c-156">Hello kits de développement logiciel DB Cosmos à 1.9.0 et supérieur prennent en charge les options d’exécution de requête parallèle, qui vous permettront d’une latence faible tooperform de requêtes sur les collections partitionnées, même lorsqu’ils ont besoin tootouch un grand nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="4949c-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4949c-157">Par exemple, hello suivant la requête est configuré toorun en parallèle sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="4949c-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4949c-158">Vous pouvez gérer l’exécution des requêtes parallèles en réglant hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="4949c-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4949c-159">En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler hello degré de parallélisme c'est-à-dire hello maximal de partitions du conteneur de toohello connexions réseau simultanées.</span><span class="sxs-lookup"><span data-stu-id="4949c-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="4949c-160">Si vous affectez ce trop-1, degré hello de parallélisme est géré par hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4949c-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4949c-161">Si hello `MaxDegreeOfParallelism` n’est pas spécifié ou la valeur de too0, qui est la valeur par défaut de hello, il y aura des partitions d’un réseau unique connexion toohello du conteneur.</span><span class="sxs-lookup"><span data-stu-id="4949c-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="4949c-162">En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête.</span><span class="sxs-lookup"><span data-stu-id="4949c-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4949c-163">Si vous omettez ce paramètre ou cette trop-1, nombre de hello d’éléments mis en mémoire tampon lors de l’exécution de requête parallèle est géré par hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4949c-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4949c-164">Fonction hello même d’état de la collection de hello, une requête parallèle renvoie des résultats dans le même ordre que dans l’exécution séquentielle de hello.</span><span class="sxs-lookup"><span data-stu-id="4949c-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4949c-165">Lorsque vous effectuez une requête de partitions croisées qui inclut le tri (ORDER BY et/ou haut), problèmes de kit de développement de base de données Azure Cosmos hello hello requête en parallèle sur les partitions et les fusions partiellement trié entraîne hello client côté tooproduce globalement les résultats classés.</span><span class="sxs-lookup"><span data-stu-id="4949c-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="4949c-166">Exécution de procédures stockées</span><span class="sxs-lookup"><span data-stu-id="4949c-166">Executing stored procedures</span></span>
<span data-ttu-id="4949c-167">Vous pouvez également exécuter des transactions atomiques par rapport à des documents avec hello même ID de périphérique, par exemple, si vous gérez des agrégats ou hello dernier état d’un périphérique dans un seul élément.</span><span class="sxs-lookup"><span data-stu-id="4949c-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="4949c-168">Dans la section suivante de hello, nous examiner comment vous pouvez déplacer les conteneurs toopartitioned à partir des conteneurs de partition unique.</span><span class="sxs-lookup"><span data-stu-id="4949c-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4949c-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4949c-169">Next steps</span></span>
<span data-ttu-id="4949c-170">Dans cet article, nous avons fourni une vue d’ensemble de la toowork avec le partitionnement de base de données Azure Cosmos des conteneurs avec hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4949c-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4949c-171">Consultez également [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) pour découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4949c-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="4949c-172">Effectuez un test des performances et de la mise à l’échelle avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4949c-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="4949c-173">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md) pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="4949c-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="4949c-174">Commencer le codage par hello [kits de développement logiciel](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="4949c-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="4949c-175">Apprenez-en davantage sur le [débit approvisionné dans Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="4949c-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

