---
title: "Partitionnement et mise à l’échelle dans Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment le partitionnement fonctionne dans Azure Cosmos DB, comment configurer le partitionnement et les clés de partition, et comment choisir la clé de partition appropriée pour votre application."
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
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="ebb59-103">Partitionnement dans Azure Cosmos DB à l’aide de l’API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ebb59-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="ebb59-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) est un service de base de données multi-modèle, distribué globalement conçu pour vous aider à obtenir des performances rapides et prévisibles, et à monter en charge en toute transparence parallèlement à l’évolution de votre application.</span><span class="sxs-lookup"><span data-stu-id="ebb59-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="ebb59-105">Cet article fournit une vue d’ensemble de l’utilisation du partitionnement des conteneurs Cosmos DB avec l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ebb59-106">Consultez [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) afin de découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="ebb59-107">Pour commencer avec le code, téléchargez le projet à partir de [GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ebb59-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="ebb59-108">Après avoir lu cet article, vous serez en mesure de répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebb59-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="ebb59-109">Comment le partitionnement dans Azure Cosmos DB fonctionne-t-il ?</span><span class="sxs-lookup"><span data-stu-id="ebb59-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="ebb59-110">Comment configurer le partitionnement dans Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="ebb59-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="ebb59-111">Que sont les clés de partition et comment choisir la bonne clé de partition pour mon application ?</span><span class="sxs-lookup"><span data-stu-id="ebb59-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="ebb59-112">Pour commencer avec le code, téléchargez le projet à partir de l’[exemple de pilote de test des performances Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ebb59-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="ebb59-113">Clés de partition</span><span class="sxs-lookup"><span data-stu-id="ebb59-113">Partition keys</span></span>

<span data-ttu-id="ebb59-114">Dans l’API DocumentDB, vous spécifiez la définition de la clé de partition sous la forme d’un chemin d’accès JSON.</span><span class="sxs-lookup"><span data-stu-id="ebb59-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="ebb59-115">Le tableau suivant présente des exemples de définitions de clé de partition ainsi que les valeurs correspondantes.</span><span class="sxs-lookup"><span data-stu-id="ebb59-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="ebb59-116">La clé de partition est spécifiée en tant que chemin d’accès. Par exemple, `/department` représente le service de la propriété.</span><span class="sxs-lookup"><span data-stu-id="ebb59-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="ebb59-117"><strong>Clé de partition</strong></span><span class="sxs-lookup"><span data-stu-id="ebb59-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ebb59-118"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="ebb59-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ebb59-119">/department</span><span class="sxs-lookup"><span data-stu-id="ebb59-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ebb59-120">Correspond à la valeur de doc.department, où doc est l’élément.</span><span class="sxs-lookup"><span data-stu-id="ebb59-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ebb59-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="ebb59-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ebb59-122">Correspond à la valeur de doc.properties.name, où doc est l’élément (propriété imbriquée).</span><span class="sxs-lookup"><span data-stu-id="ebb59-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ebb59-123">/id</span><span class="sxs-lookup"><span data-stu-id="ebb59-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ebb59-124">Correspond à la valeur de doc.id (l’ID et la clé de partition sont la même propriété).</span><span class="sxs-lookup"><span data-stu-id="ebb59-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ebb59-125">/"nom de service"</span><span class="sxs-lookup"><span data-stu-id="ebb59-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ebb59-126">Correspond à la valeur de doc["nom de service"], où doc est l’élément.</span><span class="sxs-lookup"><span data-stu-id="ebb59-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="ebb59-127">La syntaxe de la clé de partition est semblable à la spécification de chemin d’accès pour l’indexation des chemins d’accès de stratégie, à la différence notable que le chemin d’accès correspond à la propriété plutôt qu’à la valeur, de sorte qu’il n’y a pas de caractère générique à la fin.</span><span class="sxs-lookup"><span data-stu-id="ebb59-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="ebb59-128">Par exemple, vous devez spécifier /department/?</span><span class="sxs-lookup"><span data-stu-id="ebb59-128">For example, you would specify /department/?</span></span> <span data-ttu-id="ebb59-129">pour indexer les valeurs sous le service, mais spécifier /department comme définition de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="ebb59-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="ebb59-130">La clé de partition est indexée de façon implicite et ne peut pas être exclue de l’indexation à l’aide de remplacements de la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="ebb59-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="ebb59-131">Observons comment le choix de la clé de partition a une incidence sur les performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="ebb59-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="ebb59-132">Utilisation des kits SDK Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ebb59-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="ebb59-133">Avec l’[API REST version 2015-12-16](/rest/api/documentdb/), Azure Cosmos DB a ajouté la prise en charge du partitionnement automatique.</span><span class="sxs-lookup"><span data-stu-id="ebb59-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="ebb59-134">Afin de créer des conteneurs partitionnés, vous devez télécharger le Kit de développement logiciel (SDK) version 1.6.0 ou une version plus récente sur l’une des plateformes SDK prises en charge (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="ebb59-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="ebb59-135">Création de conteneurs</span><span class="sxs-lookup"><span data-stu-id="ebb59-135">Creating containers</span></span>
<span data-ttu-id="ebb59-136">L’exemple suivant montre un extrait de code .NET permettant de créer un conteneur pour stocker les données de télémétrie d’appareil avec un débit de 20 000 unités de demande par seconde.</span><span class="sxs-lookup"><span data-stu-id="ebb59-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="ebb59-137">Le Kit de développement logiciel (SDK) définit la valeur OfferThroughput (qui définit à son tour l’en-tête de demande `x-ms-offer-throughput` dans l’API REST).</span><span class="sxs-lookup"><span data-stu-id="ebb59-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="ebb59-138">Ici, nous définissons `/deviceId` comme clé de partition.</span><span class="sxs-lookup"><span data-stu-id="ebb59-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="ebb59-139">Le choix de la clé de partition est enregistré avec le reste des métadonnées du conteneur, telles que le nom et la stratégie d’indexation.</span><span class="sxs-lookup"><span data-stu-id="ebb59-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="ebb59-140">Pour cet exemple, nous avons choisi `deviceId` , car nous savons que (a) dans la mesure où il existe un grand nombre d’appareils, les écritures peuvent être réparties uniformément entre les partitions, ce qui permet de mettre à l’échelle la base de données pour recevoir de très gros volumes de données et (b) plusieurs requêtes, comme l’extraction de la dernière lecture d’un appareil, sont limitées à un identificateur d’appareil unique et peuvent être récupérées à partir d’une seule partition.</span><span class="sxs-lookup"><span data-stu-id="ebb59-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="ebb59-141">Cette méthode passe un appel de l’API REST à Cosmos DB, et le service approvisionne plusieurs partitions en fonction du débit demandé.</span><span class="sxs-lookup"><span data-stu-id="ebb59-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="ebb59-142">Vous pouvez modifier le débit d’un conteneur à mesure que vos besoins en matière de performances évoluent.</span><span class="sxs-lookup"><span data-stu-id="ebb59-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="ebb59-143">Lecture et écriture d’éléments</span><span class="sxs-lookup"><span data-stu-id="ebb59-143">Reading and writing items</span></span>
<span data-ttu-id="ebb59-144">À présent, nous allons insérer des données dans Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="ebb59-145">Voici un exemple de classe qui contient la lecture d’un appareil et un appel à CreateDocumentAsync pour insérer une nouvelle lecture d’appareil dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ebb59-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="ebb59-146">Voici un exemple recourant à l’API DocumentDB :</span><span class="sxs-lookup"><span data-stu-id="ebb59-146">This is an example leveraging the DocumentDB API:</span></span>

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

<span data-ttu-id="ebb59-147">Nous allons lire l’élément avec sa clé de partition et son ID, le mettre à jour et, dans un dernier temps, nous allons le supprimer par clé de partition et ID. Notez que les lectures incluent une valeur PartitionKey (correspondant à l’en-tête de demande `x-ms-documentdb-partitionkey` dans l’API REST).</span><span class="sxs-lookup"><span data-stu-id="ebb59-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="ebb59-148">Interrogation de conteneurs partitionnés</span><span class="sxs-lookup"><span data-stu-id="ebb59-148">Querying partitioned containers</span></span>
<span data-ttu-id="ebb59-149">Lorsque vous interrogez des données dans des conteneurs partitionnés, Cosmos DB achemine automatiquement la requête vers les partitions correspondant aux valeurs de clé de partition spécifiées dans le filtre (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="ebb59-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="ebb59-150">Par exemple, cette requête est acheminée uniquement vers la partition contenant la clé de partition « XMS-0001 ».</span><span class="sxs-lookup"><span data-stu-id="ebb59-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="ebb59-151">Pour la requête suivante, la clé de partition (DeviceId) n’a pas de filtre. La requête est donc distribuée à toutes les partitions où elle est exécutée sur l’index de la partition.</span><span class="sxs-lookup"><span data-stu-id="ebb59-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="ebb59-152">Notez que vous devez spécifier la valeur EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` dans l’API REST) pour que le Kit de développement logiciel (SDK) exécute une requête sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="ebb59-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="ebb59-153">Cosmos DB prend en charge les [fonctions d’agrégation](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` et `AVG` sur des conteneurs partitionnés à l’aide de SQL à partir des Kits de développement logiciel (SDK) 1.12.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ebb59-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="ebb59-154">Les requêtes doivent comporter un opérateur d’agrégation unique et doivent inclure une valeur unique dans la projection.</span><span class="sxs-lookup"><span data-stu-id="ebb59-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="ebb59-155">Exécution de requêtes parallèles</span><span class="sxs-lookup"><span data-stu-id="ebb59-155">Parallel query execution</span></span>
<span data-ttu-id="ebb59-156">Les kits de développement logiciel (SDK) de Cosmos DB version 1.9.0 et versions ultérieures prennent en charge des options d’exécution de requêtes parallèles, ce qui vous permet d’effectuer des requêtes à faible latence sur les collections partitionnées, même lorsque ces requêtes concernent un grand nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="ebb59-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="ebb59-157">Par exemple, la requête suivante est configurée pour s’exécuter en parallèle sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="ebb59-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="ebb59-158">Vous pouvez gérer l’exécution de requêtes parallèles en réglant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ebb59-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="ebb59-159">En définissant `MaxDegreeOfParallelism`, vous pouvez contrôler le degré de parallélisme, c’est-à-dire le nombre maximal de connexions réseau simultanées aux partitions du conteneur.</span><span class="sxs-lookup"><span data-stu-id="ebb59-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="ebb59-160">Si vous définissez cette valeur sur -1, le degré de parallélisme est géré par le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="ebb59-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="ebb59-161">Si la valeur `MaxDegreeOfParallelism` n’est pas spécifiée ou définie sur 0, qui est la valeur par défaut, il n’y a qu’une seule connexion réseau aux partitions du conteneur.</span><span class="sxs-lookup"><span data-stu-id="ebb59-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="ebb59-162">En définissant `MaxBufferedItemCount`, vous pouvez compenser l’utilisation de la mémoire côté client et la latence de la requête.</span><span class="sxs-lookup"><span data-stu-id="ebb59-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="ebb59-163">Si vous omettez ce paramètre ou que vous lui affectez la valeur -1, le nombre d’éléments mis en mémoire tampon pendant l’exécution de requêtes parallèles est géré par le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="ebb59-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="ebb59-164">Avec un même état de collection, une requête parallèle retourne les résultats dans l’ordre d’exécution en série.</span><span class="sxs-lookup"><span data-stu-id="ebb59-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="ebb59-165">Lorsque vous effectuez une requête sur plusieurs partitions qui inclut le tri (ORDER BY et/ou TOP), le kit SDK d’Azure Cosmos DB émet la requête en parallèle sur plusieurs partitions et fusionne les résultats partiellement triés côté client pour produire des résultats classés globalement.</span><span class="sxs-lookup"><span data-stu-id="ebb59-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="ebb59-166">Exécution de procédures stockées</span><span class="sxs-lookup"><span data-stu-id="ebb59-166">Executing stored procedures</span></span>
<span data-ttu-id="ebb59-167">Vous pouvez également exécuter des transactions atomiques sur des documents avec le même ID d’appareil, par exemple, si vous conservez des agrégats ou le dernier état d’un appareil dans un élément unique.</span><span class="sxs-lookup"><span data-stu-id="ebb59-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="ebb59-168">Dans la section suivante, nous examinons la manière de passer des conteneurs à partition unique à des conteneurs partitionnés.</span><span class="sxs-lookup"><span data-stu-id="ebb59-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebb59-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebb59-169">Next steps</span></span>
<span data-ttu-id="ebb59-170">Dans cet article, nous avons fourni une vue d’ensemble de l’utilisation du partitionnement des conteneurs Azure Cosmos DB avec l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ebb59-171">Consultez également [Partitionnement et mise à l’échelle horizontale](../cosmos-db/partition-data.md) pour découvrir une vue d’ensemble des concepts et bonnes pratiques pour le partitionnement avec l’API Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="ebb59-172">Effectuez un test des performances et de la mise à l’échelle avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ebb59-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ebb59-173">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md) pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="ebb59-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ebb59-174">Commencez à coder avec les [Kits de développement logiciel (SDK)](documentdb-sdk-dotnet.md) ou [l’API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="ebb59-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="ebb59-175">Apprenez-en davantage sur le [débit approvisionné dans Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ebb59-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

