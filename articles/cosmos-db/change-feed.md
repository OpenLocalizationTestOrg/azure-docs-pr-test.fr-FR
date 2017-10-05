---
title: Utilisation du support de flux de modification dans Azure Cosmos DB | Microsoft Docs
description: "Utilisez le support de flux de modification d’Azure Cosmos DB pour suivre les modifications dans les documents et effectuer des opérations de traitement basées sur les événements tels que des déclencheurs et la mise à jour des systèmes de cache et d’analyse."
keywords: change feed
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="61b43-104">Utilisation du support de flux de modification dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61b43-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="61b43-105">[Azure Cosmos DB](../cosmos-db/introduction.md) est un service de base de données répliqué mondialement, rapide et flexible utilisé pour le stockage d’importants volumes de données transactionnelles et opérationnelles avec une latence prévisible en quelques millisecondes pour les lectures et les écritures.</span><span class="sxs-lookup"><span data-stu-id="61b43-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="61b43-106">Il est ainsi parfait pour les applications d’IoT, de jeux, de vente au détail et de journalisation des compteurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="61b43-107">Un modèle de conception courant dans ces applications consiste à suivre les modifications apportées aux données Azure Cosmos DB et mettre à jour les vues matérialisées, effectuer des analyses en temps réel, archiver les données vers le stockage à froid et déclencher des notifications pour certains événements en fonction de ces modifications.</span><span class="sxs-lookup"><span data-stu-id="61b43-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="61b43-108">Le **support de flux de modification** d’Azure Cosmos DB vous permet de créer des solutions efficaces et évolutives pour chacun de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="61b43-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="61b43-109">Avec le support de flux de modification, Azure Cosmos DB fournit une liste triée de documents d’une collection Azure Cosmos DB affichés dans l’ordre dans lequel ils ont été modifiés.</span><span class="sxs-lookup"><span data-stu-id="61b43-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="61b43-110">Ce flux peut être utilisé pour écouter les modifications apportées aux données dans la collection et effectuer des actions telles que :</span><span class="sxs-lookup"><span data-stu-id="61b43-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="61b43-111">déclencher un appel à une API quand un document est inséré ou modifié ;</span><span class="sxs-lookup"><span data-stu-id="61b43-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="61b43-112">effectuer un traitement en temps réel (flux) sur les mises à jour ;</span><span class="sxs-lookup"><span data-stu-id="61b43-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="61b43-113">synchroniser les données avec un cache, le moteur de recherche ou l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="61b43-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="61b43-114">Les modifications dans Azure Cosmos DB sont conservées et peuvent être traitées de manière asynchrone et réparties sur un ou plusieurs consommateurs pour un traitement en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61b43-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="61b43-115">Examinons les API pour le flux de modification et voyons comment vous pouvez les utiliser pour créer des applications évolutives en temps réel.</span><span class="sxs-lookup"><span data-stu-id="61b43-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="61b43-116">Cet article montre comment utiliser le flux de modification dans Azure Cosmos DB et l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="61b43-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Utilisation du flux de modification d’Azure Cosmos DB pour alimenter les analyses en temps réel et les scénarios de calcul pilotés par les événements](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="61b43-118">À l’heure actuelle, le support de flux de modification est fourni uniquement pour l’API DocumentDB ; l’API Graph et l’API Table ne sont pas encore prises en charge.</span><span class="sxs-lookup"><span data-stu-id="61b43-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="61b43-119">Cas d'utilisation et scénarios</span><span class="sxs-lookup"><span data-stu-id="61b43-119">Use cases and scenarios</span></span>
<span data-ttu-id="61b43-120">Le flux de modification permet un traitement efficace des jeux de données importants avec un volume d’écritures élevé et offre une alternative à l’interrogation des jeux de données pour identifier les changements apportés.</span><span class="sxs-lookup"><span data-stu-id="61b43-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="61b43-121">Par exemple, vous pouvez effectuer efficacement les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="61b43-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="61b43-122">Mettre à jour un cache, l’index de recherche ou un entrepôt de données avec les données stockées dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="61b43-123">Implémenter la hiérarchisation et l’archivage des données de niveau application, autrement dit, stocker les « données à chaud » dans Azure Cosmos DB et archiver les « données à froid » dans [Stockage Blob Azure](../storage/common/storage-introduction.md) ou [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61b43-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="61b43-124">Implémenter une analyse en mode batch sur les données à l’aide [d’Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="61b43-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="61b43-125">Implémenter des [pipelines lambda sur Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="61b43-126">Azure Cosmos DB fournit une solution de base de données évolutive qui peut gérer l’ingestion et l’interrogation, et implémenter des architectures lambda avec un faible coût total de possession.</span><span class="sxs-lookup"><span data-stu-id="61b43-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="61b43-127">Effectuer des migrations sans aucun temps d’arrêt vers un autre compte Azure Cosmos DB avec un schéma de partitionnement différent.</span><span class="sxs-lookup"><span data-stu-id="61b43-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="61b43-128">**Pipelines lambda avec Azure Cosmos DB pour l’ingestion et l’interrogation :**</span><span class="sxs-lookup"><span data-stu-id="61b43-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda Azure Cosmos DB pour l’ingestion et l’interrogation](./media/change-feed/lambda.png)

<span data-ttu-id="61b43-130">Vous pouvez utiliser Azure Cosmos DB pour recevoir et stocker des données d’événement d’appareils, de capteurs, de l’infrastructure et des applications, et traiter ces événements en temps réel avec [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61b43-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="61b43-131">Dans les applications web et mobiles [sans serveur](http://azure.com/serverless), vous pouvez suivre les événements tels que les modifications apportées au profil, aux préférences ou à l’emplacement de votre client pour déclencher certaines actions, comme l’envoi de notifications Push à leurs appareils avec [Azure Functions](../azure-functions/functions-bindings-documentdb.md) ou [App Services](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="61b43-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="61b43-132">Si vous utilisez Azure Cosmos DB pour créer un jeu, vous pouvez, par exemple, utiliser le flux de modification pour implémenter des classements en temps réel basés sur des scores de jeux terminés.</span><span class="sxs-lookup"><span data-stu-id="61b43-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="61b43-133">Fonctionnement du flux de modification dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61b43-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="61b43-134">Azure Cosmos DB offre la possibilité de lire de façon incrémentielle les mises à jour apportées à une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="61b43-135">Ce flux de modification a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="61b43-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="61b43-136">Les modifications sont persistantes dans Azure Cosmos DB et peuvent être traitées de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="61b43-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="61b43-137">Les modifications apportées aux documents d’une collection sont disponibles immédiatement dans le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="61b43-138">Chaque modification apportée à un document n’apparaît qu’une seule fois dans le flux des modifications. En outre, les clients gèrent leur logique de points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="61b43-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="61b43-139">La bibliothèque du processeur de flux des modifications fournit des points de contrôle automatiques, ainsi qu’une sémantique de type « au moins une fois ».</span><span class="sxs-lookup"><span data-stu-id="61b43-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="61b43-140">Seule la dernière modification d’un document donné est incluse dans le journal des modifications.</span><span class="sxs-lookup"><span data-stu-id="61b43-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="61b43-141">Les modifications intermédiaires peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="61b43-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="61b43-142">Le flux de modification est trié par ordre de modification au sein de chaque valeur de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="61b43-143">Il n’existe aucun ordre garanti entre les valeurs de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="61b43-144">Les modifications peuvent être synchronisées à partir de n’importe quel moment donné ; autrement dit, il n’existe aucune période de rétention de données fixes pendant laquelle les modifications sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="61b43-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="61b43-145">Les modifications sont disponibles dans des blocs de plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="61b43-146">Cette fonctionnalité permet le traitement en parallèle de modifications de grandes collections par plusieurs consommateurs/serveurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="61b43-147">Les applications peuvent demander plusieurs flux de modification simultanément sur la même collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="61b43-148">Le flux de modification d’Azure Cosmos DB est activé par défaut pour tous les comptes.</span><span class="sxs-lookup"><span data-stu-id="61b43-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="61b43-149">Vous pouvez utiliser votre [débit configuré](request-units.md) dans votre région d’écriture ou toute [région de lecture](distribute-data-globally.md) pour lire à partir du flux de modification comme toute autre opération effectuée à partir d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="61b43-150">Le flux de modification inclut les insertions et les opérations de mise à jour apportées aux documents de la collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="61b43-151">Vous pouvez capturer des suppressions en définissant un indicateur de « suppression réversible » dans vos documents à la place des suppressions.</span><span class="sxs-lookup"><span data-stu-id="61b43-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="61b43-152">Vous pouvez également définir un délai d’expiration limité pour vos documents via la [fonctionnalité de durée de vie (TTL)](time-to-live.md), par exemple 24 heures, et utiliser la valeur de cette propriété pour capturer les suppressions.</span><span class="sxs-lookup"><span data-stu-id="61b43-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="61b43-153">Avec cette solution, vous devez traiter les modifications dans un intervalle de temps inférieur à la période d’expiration de durée de vie.</span><span class="sxs-lookup"><span data-stu-id="61b43-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="61b43-154">Le flux de modification est disponible pour chaque plage de clés de partition dans la collection de documents et peut ainsi être distribué vers un ou plusieurs consommateurs pour un traitement en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61b43-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Traitement distribué du flux de modification d’Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="61b43-156">Vous avez plusieurs options pour implémenter une modification de flux dans votre code client.</span><span class="sxs-lookup"><span data-stu-id="61b43-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="61b43-157">Les sections qui suivent immédiatement décrivent comment implémenter la modification de flux à l’aide de l’API REST Azure Cosmos DB et des SDK DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="61b43-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="61b43-158">Toutefois, pour les applications .NET, nous recommandons d’utiliser la nouvelle [Bibliothèque du processeur de flux de modification](#change-feed-processor) pour le traitement des événements à partir du flux de modification, car elle simplifie la lecture des modifications parmi les partitions et autorise l’exécution de plusieurs threads en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61b43-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="61b43-159"><a id="rest-apis"></a>Utilisation de l’API REST et des SDK DocumentDB</span><span class="sxs-lookup"><span data-stu-id="61b43-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="61b43-160">Azure Cosmos DB fournit des conteneurs élastiques de stockage et de débit appelés **collections**.</span><span class="sxs-lookup"><span data-stu-id="61b43-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="61b43-161">Les données contenues dans les collections sont regroupées logiquement à l’aide de [clés de partition](partition-data.md) à des fins d’évolutivité et de performance.</span><span class="sxs-lookup"><span data-stu-id="61b43-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="61b43-162">Azure Cosmos DB fournit diverses API pour accéder à ces données, y compris la recherche par ID (Read/Get), les requêtes et les flux de lecture (analyses).</span><span class="sxs-lookup"><span data-stu-id="61b43-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="61b43-163">Le flux de modification peut être obtenu en remplissant deux nouveaux en-têtes de demande de l’API `ReadDocumentFeed` de DocumentDB et peut être traité en parallèle sur différentes plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="61b43-164">API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="61b43-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="61b43-165">Examinons brièvement comment ReadDocumentFeed fonctionne.</span><span class="sxs-lookup"><span data-stu-id="61b43-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="61b43-166">Azure Cosmos DB prend en charge la lecture d’un flux de documents dans une collection via l’API `ReadDocumentFeed`.</span><span class="sxs-lookup"><span data-stu-id="61b43-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="61b43-167">Par exemple, la demande suivante retourne une page de documents à l’intérieur de la collection `serverlogs`.</span><span class="sxs-lookup"><span data-stu-id="61b43-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="61b43-168">Les résultats peuvent être limités à l’aide de l’en-tête `x-ms-max-item-count`, et les lectures peuvent être reprises en soumettant à nouveau la demande avec un en-tête `x-ms-continuation` retourné dans la réponse précédente.</span><span class="sxs-lookup"><span data-stu-id="61b43-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="61b43-169">Lors de l’opération à partir d’un seul client, `ReadDocumentFeed` itère dans les résultats sur les différentes partitions en série.</span><span class="sxs-lookup"><span data-stu-id="61b43-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="61b43-170">**Flux de lecture de documents en série**</span><span class="sxs-lookup"><span data-stu-id="61b43-170">**Serial read document feed**</span></span>

<span data-ttu-id="61b43-171">Vous pouvez également récupérer le flux de documents à l’aide d’un des [kits de développement logiciel (SDK) d’Azure Cosmos DB ](documentdb-sdk-dotnet.md) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="61b43-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="61b43-172">Par exemple, l’extrait de code suivant montre comment utiliser la méthode [ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) dans .NET.</span><span class="sxs-lookup"><span data-stu-id="61b43-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="61b43-173">Exécution distribuée de ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="61b43-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="61b43-174">Pour les collections qui contiennent des téraoctets de données ou plus, ou qui reçoivent un grand nombre de mises à jour, l’exécution en série de flux de lecture à partir d’un seul ordinateur client n’est pas forcément pratique.</span><span class="sxs-lookup"><span data-stu-id="61b43-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="61b43-175">Pour prendre en charge ces scénarios Big Data, Azure Cosmos DB propose des API pour distribuer les appels `ReadDocumentFeed` de façon transparente sur plusieurs lecteurs/consommateurs clients.</span><span class="sxs-lookup"><span data-stu-id="61b43-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="61b43-176">**Flux de lecture de documents distribué**</span><span class="sxs-lookup"><span data-stu-id="61b43-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="61b43-177">Pour fournir un traitement évolutif des modifications incrémentielles, Azure Cosmos DB prend en charge un modèle d’augmentation de la taille des instances pour l’API de flux de modification en fonction des plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="61b43-178">Vous pouvez obtenir une liste des plages de clés de partition d’une collection effectuant un appel `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="61b43-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="61b43-179">Pour chaque plage de clés de partition, vous pouvez exécuter `ReadDocumentFeed` pour la lecture des documents avec des clés de partition dans cette plage.</span><span class="sxs-lookup"><span data-stu-id="61b43-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="61b43-180">Récupération des plages de clés de partition d’une collection</span><span class="sxs-lookup"><span data-stu-id="61b43-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="61b43-181">Vous pouvez récupérer les plages de clés de partition en demandant la ressource `pkranges` au sein d’une collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="61b43-182">Par exemple, la demande suivante récupère la liste des plages de clés de partition de la collection `serverlogs` :</span><span class="sxs-lookup"><span data-stu-id="61b43-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="61b43-183">Cette demande renvoie la réponse suivante contenant les métadonnées des plages de clés de partition :</span><span class="sxs-lookup"><span data-stu-id="61b43-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="61b43-184">**Propriétés des plages de clés de partition** : chaque plage de clés de partition inclut les propriétés de métadonnées indiquées dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="61b43-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="61b43-185">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61b43-185">Header name</span></span></th>
        <th><span data-ttu-id="61b43-186">Description</span><span class="sxs-lookup"><span data-stu-id="61b43-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-187">id</span><span class="sxs-lookup"><span data-stu-id="61b43-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="61b43-188">ID de la plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-188">The ID for the partition key range.</span></span> <span data-ttu-id="61b43-189">Il s’agit d’un ID stable et unique dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="61b43-190">Il doit être utilisé dans l’appel suivant pour lire les modifications par plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="61b43-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="61b43-192">Valeur de hachage de la clé de partition maximale pour la plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="61b43-193">À usage interne.</span><span class="sxs-lookup"><span data-stu-id="61b43-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="61b43-194">minInclusive</span></span></td>
        <td><span data-ttu-id="61b43-195">Valeur de hachage de la clé de partition minimale pour la plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="61b43-196">À usage interne.</span><span class="sxs-lookup"><span data-stu-id="61b43-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="61b43-197">Vous pouvez effectuer cette opération à l’aide d’un des [kits de développement logiciel (SDK) d’Azure Cosmos DB](documentdb-sdk-dotnet.md) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="61b43-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="61b43-198">Par exemple, l’extrait de code suivant montre comment récupérer des plages de clés de partition dans .NET à l’aide de la méthode [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="61b43-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="61b43-199">Azure Cosmos DB prend en charge la récupération de documents par plage de clés de partition en définissant l’en-tête `x-ms-documentdb-partitionkeyrangeid` facultatif.</span><span class="sxs-lookup"><span data-stu-id="61b43-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="61b43-200">Exécution d’un ReadDocumentFeed incrémentiel</span><span class="sxs-lookup"><span data-stu-id="61b43-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="61b43-201">ReadDocumentFeed prend en charge les scénarios/tâches suivants pour le traitement incrémentiel des modifications dans les collections Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="61b43-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="61b43-202">Lecture de toutes les modifications apportées aux documents depuis le début, autrement dit, depuis la création de la collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="61b43-203">Lecture de toutes les modifications ou futures mises à jour qui seront apportées aux documents à partir de maintenant ou d’une date définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="61b43-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="61b43-204">Lecture de toutes les modifications apportées aux documents à partir d’une version logique de la collection (ETag).</span><span class="sxs-lookup"><span data-stu-id="61b43-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="61b43-205">Vous pouvez contrôler vos consommateurs en fonction de l’ETag retourné à partir des demandes de flux de lecture incrémentiels.</span><span class="sxs-lookup"><span data-stu-id="61b43-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="61b43-206">Les modifications incluent les insertions et les mises à jour apportées aux documents.</span><span class="sxs-lookup"><span data-stu-id="61b43-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="61b43-207">Pour capturer les suppressions, vous devez utiliser une propriété de « suppression réversible » dans vos documents, ou utiliser la [propriété TTL intégrée](time-to-live.md) pour signaler une suppression en attente dans le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="61b43-208">Le tableau suivant répertorie les en-têtes de [demande](/rest/api/documentdb/common-documentdb-rest-request-headers.md) et de [réponse](/rest/api/documentdb/common-documentdb-rest-response-headers.md) pour les opérations ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="61b43-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="61b43-209">**En-têtes de demande pour les opérations ReadDocumentFeed incrémentielles** :</span><span class="sxs-lookup"><span data-stu-id="61b43-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="61b43-210">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61b43-210">Header name</span></span></th>
        <th><span data-ttu-id="61b43-211">Description</span><span class="sxs-lookup"><span data-stu-id="61b43-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="61b43-212">A-IM</span></span></td>
        <td><span data-ttu-id="61b43-213">Doit être défini sur « Incremental feed » (Flux incrémentiel), ou omis.</span><span class="sxs-lookup"><span data-stu-id="61b43-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="61b43-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="61b43-215">Aucun en-tête : retourne toutes les modifications depuis le début (création de la collection).</span><span class="sxs-lookup"><span data-stu-id="61b43-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="61b43-216">« * » : retourne toutes les nouvelles modifications apportées aux données dans la collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="61b43-217">&lt;etag&gt; : s’il est défini sur un ETag de la collection, retourne toutes les modifications effectuées depuis cet horodatage logique.</span><span class="sxs-lookup"><span data-stu-id="61b43-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="61b43-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="61b43-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="61b43-219">Format d’heure RFC 1123 ; ignoré si If-None-Match est spécifié.</span><span class="sxs-lookup"><span data-stu-id="61b43-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="61b43-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="61b43-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="61b43-221">ID de la plage de clés de partition pour la lecture des données.</span><span class="sxs-lookup"><span data-stu-id="61b43-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="61b43-222">**En-têtes de réponse pour les opérations ReadDocumentFeed incrémentielles** :</span><span class="sxs-lookup"><span data-stu-id="61b43-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="61b43-223">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61b43-223">Header name</span></span></th>
        <th><span data-ttu-id="61b43-224">Description</span><span class="sxs-lookup"><span data-stu-id="61b43-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-225">etag</span><span class="sxs-lookup"><span data-stu-id="61b43-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="61b43-226">Numéro de séquence logique (LSN) du dernier document renvoyé dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="61b43-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="61b43-227">L’opération ReadDocumentFeed incrémentielle peut être reprise en resoumettant cette valeur dans If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="61b43-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="61b43-228">Voici un exemple de demande pour retourner toutes les modifications incrémentielles de la collection à partir de la version logique/ETag `28535` et de la plage de clés de partition = `16` :</span><span class="sxs-lookup"><span data-stu-id="61b43-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="61b43-229">Les modifications sont classées par heure dans chaque valeur de clé de partition de la plage.</span><span class="sxs-lookup"><span data-stu-id="61b43-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="61b43-230">Il n’existe aucun ordre garanti entre les valeurs de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="61b43-231">Si les résultats sont trop nombreux pour figurer sur une seule page, vous pouvez lire la page de résultats suivante en soumettant à nouveau la demande avec l’en-tête `If-None-Match` et une valeur égale à l’`etag` de la réponse précédente.</span><span class="sxs-lookup"><span data-stu-id="61b43-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="61b43-232">Si plusieurs documents ont été insérés ou mis à jour via des transactions au sein d’une procédure stockée ou avec un déclencheur, ils seront tous renvoyés dans la même page de réponse.</span><span class="sxs-lookup"><span data-stu-id="61b43-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="61b43-233">Avec le flux de modification, plus d’éléments seront retournés dans une page spécifiée dans `x-ms-max-item-count` dans le cas de plusieurs documents insérés ou mis à jour à l’intérieur des procédures stockées ou des déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="61b43-234">Lorsque vous utilisez le SDK .NET (1.17.0), définissez le champ `StartTime` dans `ChangeFeedOptions` de manière à retourner directement les documents modifiés depuis `StartTime` lors de l’appel de `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="61b43-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="61b43-235">Quand vous spécifiez `If-Modified-Since` à l’aide de l’API REST, votre requête ne retourne pas les documents, mais le jeton de continuation ou `etag` dans l’en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="61b43-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="61b43-236">Pour retourner les documents modifiés depuis la date spécifiée, le jeton de continuation `etag` doit être utilisé dans la prochaine requête avec `If-None-Match`.</span><span class="sxs-lookup"><span data-stu-id="61b43-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="61b43-237">Le Kit de développement logiciel (SDK) .NET fournit les classes d’assistance [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) et [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) pour accéder aux modifications apportées à une collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="61b43-238">L’extrait de code suivant montre comment récupérer toutes les modifications apportées depuis le début à l’aide du SDK .NET à partir d’un seul client.</span><span class="sxs-lookup"><span data-stu-id="61b43-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="61b43-239">L’extrait de code suivant montre comment traiter les modifications en temps réel avec Azure Cosmos DB à l’aide du support de flux de modification et de la fonction qui précède.</span><span class="sxs-lookup"><span data-stu-id="61b43-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="61b43-240">Le premier appel retourne tous les documents de la collection, et le second retourne uniquement les deux documents créés depuis le dernier point de contrôle.</span><span class="sxs-lookup"><span data-stu-id="61b43-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="61b43-241">Vous pouvez également filtrer le flux de modification à l’aide de la logique côté client pour traiter les événements de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="61b43-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="61b43-242">Par exemple, voici un extrait de code qui utilise LINQ côté client pour traiter uniquement les événements de modification de température des capteurs de périphérique.</span><span class="sxs-lookup"><span data-stu-id="61b43-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="61b43-243"><a id="change-feed-processor"></a>Bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61b43-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="61b43-244">Une autre option consiste à utiliser la [bibliothèque du processeur de flux de modification Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), qui peut vous aider à distribuer facilement le traitement des événements d’un flux de modification parmi plusieurs consommateurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="61b43-245">La bibliothèque est idéale pour générer des lecteurs de flux de modification sur la plateforme .NET.</span><span class="sxs-lookup"><span data-stu-id="61b43-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="61b43-246">Voici quelques flux de travail qui seraient simplifiés par l’utilisation de la bibliothèque du processeur de flux de modification sur les méthodes incluses dans les autres SDK Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="61b43-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="61b43-247">Extraction de mises à jour à partir du flux de modification quand les données sont stockées sur plusieurs partitions</span><span class="sxs-lookup"><span data-stu-id="61b43-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="61b43-248">Déplacement ou réplication de données d’une collection vers une autre</span><span class="sxs-lookup"><span data-stu-id="61b43-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="61b43-249">Exécution en parallèle d’actions déclenchées par des mises à jour de données et de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61b43-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="61b43-250">Bien que l’utilisation des API dans les SDK Cosmos fournisse un accès précis aux mises à jour de flux de modification dans chaque partition, l’utilisation de la bibliothèque du processeur de flux de modification simplifie la lecture des modifications entre les partitions et l’exécution en parallèle des threads.</span><span class="sxs-lookup"><span data-stu-id="61b43-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="61b43-251">Au lieu de lire manuellement les modifications à partir de chaque conteneur et d’enregistrer un jeton de liaison pour chaque partition, le processeur de flux de modification gère automatiquement la lecture des modifications parmi les partitions à l’aide d’un mécanisme de bail.</span><span class="sxs-lookup"><span data-stu-id="61b43-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="61b43-252">La bibliothèque est disponible sous forme de package NuGet : [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) et à partir du code source en tant qu’[exemple](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor) Github.</span><span class="sxs-lookup"><span data-stu-id="61b43-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="61b43-253">Présentation de la bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61b43-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="61b43-254">L’implémentation du processeur de flux de modification fait appel à quatre composants principaux : la collection analysée, la collection de baux, l’hôte de processeur et les consommateurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="61b43-255">**Collecte analysé :** la collection analysée est constituée des données à partir desquelles le flux de modification est généré.</span><span class="sxs-lookup"><span data-stu-id="61b43-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="61b43-256">Toutes les insertions et les modifications apportées à la collection analysée sont répercutées dans le flux de modification de la collection.</span><span class="sxs-lookup"><span data-stu-id="61b43-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="61b43-257">**Collection de baux :** la collection de baux coordonne le traitement du flux de modification parmi les threads de travail.</span><span class="sxs-lookup"><span data-stu-id="61b43-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="61b43-258">Une collection distincte est utilisée pour stocker les baux avec un bail par partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="61b43-259">Il est préférable de stocker cette collection de baux sur un autre compte, avec une zone d’écriture plus proche de l’endroit où le processeur de flux de modification s’exécute.</span><span class="sxs-lookup"><span data-stu-id="61b43-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="61b43-260">Un objet de bail contient les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="61b43-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="61b43-261">Propriétaire : spécifie l’hôte détenteur du bail.</span><span class="sxs-lookup"><span data-stu-id="61b43-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="61b43-262">Continuation : spécifie la position (jeton de continuation) d’une partition particulière dans le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="61b43-263">Horodatage : heure de dernière mise à jour du bail. Vous pouvez utiliser l’horodatage pour vérifier si le bail est considéré comme ayant expiré.</span><span class="sxs-lookup"><span data-stu-id="61b43-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="61b43-264">**Hôte de processeur :** chaque hôte détermine le nombre de partitions à traiter en fonction de la quantité d’autres instances d’hôtes ayant des baux actifs.</span><span class="sxs-lookup"><span data-stu-id="61b43-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="61b43-265">Quand un hôte démarre, il acquiert des baux pour équilibrer la charge de travail parmi tous les hôtes.</span><span class="sxs-lookup"><span data-stu-id="61b43-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="61b43-266">Un hôte renouvelle périodiquement les baux afin que ceux-ci restent actifs.</span><span class="sxs-lookup"><span data-stu-id="61b43-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="61b43-267">Un hôte crée un point de contrôle pour le dernier jeton de continuation de son bail pour chaque lecture.</span><span class="sxs-lookup"><span data-stu-id="61b43-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="61b43-268">Pour garantir la sécurité de l’accès concurrentiel, un hôte vérifie l’ETag pour chaque mise à jour de bail.</span><span class="sxs-lookup"><span data-stu-id="61b43-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="61b43-269">D’autres stratégies de point de contrôle sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="61b43-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="61b43-270">En cas d’arrêt, un hôte libère tous les baux mais conserve les informations de continuation, afin de pouvoir reprendre ultérieurement la lecture à partir du point de contrôle stocké.</span><span class="sxs-lookup"><span data-stu-id="61b43-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="61b43-271">À ce stade, le nombre d’hôtes ne peut pas être supérieur au nombre de partitions (baux).</span><span class="sxs-lookup"><span data-stu-id="61b43-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="61b43-272">**Consommateurs :** les consommateurs, ou Workers, sont des threads qui exécutent le traitement du flux de modification initié par chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="61b43-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="61b43-273">Chaque hôte de processeur peut avoir plusieurs consommateurs.</span><span class="sxs-lookup"><span data-stu-id="61b43-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="61b43-274">Chaque consommateur lit le flux de modification à partir de la partition à laquelle il est assigné, et il informe son hôte des modifications et des baux expirés.</span><span class="sxs-lookup"><span data-stu-id="61b43-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="61b43-275">Pour mieux comprendre comment ces quatre éléments du processeur de flux de modification interagissent, examinons un exemple à l’aide du schéma suivant.</span><span class="sxs-lookup"><span data-stu-id="61b43-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="61b43-276">La collection analysée stocke des documents et utilise « city » comme clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="61b43-277">Nous constatons que la partition bleue contient des documents avec le champ « city » de « A-E », et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="61b43-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="61b43-278">Il existe deux hôtes, chacun avec deux consommateurs lisant à partir des quatre partitions en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61b43-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="61b43-279">Les flèches indiquent les consommateurs lisant à partir d’un point spécifique dans le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="61b43-280">Dans la première partition, le bleu foncé représente les modifications non lues, tandis que le bleu clair représente les modifications déjà lues sur le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="61b43-281">Les hôtes utilisent la collection de baux pour stocker une valeur de « continuation » afin d’assurer le suivi de la position de lecture actuelle pour chaque consommateur.</span><span class="sxs-lookup"><span data-stu-id="61b43-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Utilisation de l’hôte du processus de flux de modification Azure Cosmos DB](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="61b43-283">Utilisation de la bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61b43-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="61b43-284">La section suivante explique comment utiliser la bibliothèque du processeur de flux de modification dans le contexte de la réplication des modifications d’une collection source vers une collection de destination.</span><span class="sxs-lookup"><span data-stu-id="61b43-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="61b43-285">Ici, la collection source est la collection analysée dans le processeur de flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="61b43-286">**Installer et inclure le package NuGet du processeur de flux de modification**</span><span class="sxs-lookup"><span data-stu-id="61b43-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="61b43-287">Avant d’installer le package NuGet du processeur de flux de modification, vous devez d’abord installer :</span><span class="sxs-lookup"><span data-stu-id="61b43-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="61b43-288">Microsoft.Azure.DocumentDB, version 1.13.1 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="61b43-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="61b43-289">Newtonsoft.Json, version 9.0.1 ou ultérieure. Installez `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` et incluez-le comme référence.</span><span class="sxs-lookup"><span data-stu-id="61b43-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="61b43-290">**Créer une collection analysée, une collection de baux et une collection de destination**</span><span class="sxs-lookup"><span data-stu-id="61b43-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="61b43-291">Pour pouvoir utiliser la bibliothèque du processeur de flux de modification, vous devez créer la collection de baux avant d’exécuter les hôtes de processeur.</span><span class="sxs-lookup"><span data-stu-id="61b43-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="61b43-292">Là encore, nous vous recommandons de stocker une collection de baux sur un autre compte, avec une zone d’écriture plus proche de l’endroit où le processeur de flux de modification s’exécute.</span><span class="sxs-lookup"><span data-stu-id="61b43-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="61b43-293">Dans cet exemple de déplacement de données, nous devons créer la collection de destination avant d’exécuter l’hôte du processeur de flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="61b43-294">Dans l’exemple de code, nous appelons une méthode d’assistance pour créer la collection analysée, la collection de baux et la collection de destination, si elles n’existent pas encore.</span><span class="sxs-lookup"><span data-stu-id="61b43-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="61b43-295">La création d’une collection a des conséquences d’un point de vue tarifaire. En effet, vous réservez une part du débit pour que l’application puisse communiquer avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="61b43-296">Pour plus d’informations, consultez la [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="61b43-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="61b43-297">*Création d’un hôte de processeur*</span><span class="sxs-lookup"><span data-stu-id="61b43-297">*Creating a processor host*</span></span>

<span data-ttu-id="61b43-298">La classe `ChangeFeedProcessorHost` fournit un environnement d'exécution sécurisé, multiprocessus, thread-safe pour des implémentations d’événements qui fournissent également une gestion de contrôle et de location de partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="61b43-299">Pour utiliser la classe `ChangeFeedProcessorHost`, vous pouvez implémenter `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="61b43-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="61b43-300">Cette interface contient trois méthodes :</span><span class="sxs-lookup"><span data-stu-id="61b43-300">This interface contains three methods:</span></span>

* <span data-ttu-id="61b43-301">`OpenAsync` : cette fonction est appelée quand l’observateur de flux de modification est ouvert.</span><span class="sxs-lookup"><span data-stu-id="61b43-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="61b43-302">Elle peut être modifiée pour effectuer une action spécifique quand le consommateur/observateur est ouvert.</span><span class="sxs-lookup"><span data-stu-id="61b43-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="61b43-303">`CloseAsync` : cette fonction est appelée quand l’observateur de flux de modification est arrêté.</span><span class="sxs-lookup"><span data-stu-id="61b43-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="61b43-304">Elle peut être modifiée pour effectuer une action spécifique quand le consommateur/observateur est fermé.</span><span class="sxs-lookup"><span data-stu-id="61b43-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="61b43-305">`ProcessChangesAsync` : cette fonction est appelée quand de nouvelles modifications de document sont disponibles sur le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="61b43-306">Elle peut être modifiée pour effectuer une action spécifique à chaque mise à jour du flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="61b43-307">Dans notre exemple, nous implémentent l’interface `IChangeFeedObserver` par l’intermédiaire de la classe `DocumentFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="61b43-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="61b43-308">Ici, la fonction `ProcessChangesAsync` effectue une opération d’upsert (mise à jour) sur un document du flux de modification vers la collection de destination.</span><span class="sxs-lookup"><span data-stu-id="61b43-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="61b43-309">Cet exemple est utile pour le déplacement de données d’une collection vers une autre afin de changer la clé de partition d’un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="61b43-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="61b43-310">*Exécution de l’hôte de processeur*</span><span class="sxs-lookup"><span data-stu-id="61b43-310">*Running the Processor Host*</span></span>

<span data-ttu-id="61b43-311">Avant de commencer le traitement des événements, vous pouvez personnaliser les options de flux de modification et les options d’hôte de flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61b43-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="61b43-312">Les champs spécifiques pouvant être personnalisés sont résumés dans les tableaux suivants.</span><span class="sxs-lookup"><span data-stu-id="61b43-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="61b43-313">**Options de flux de modification** :</span><span class="sxs-lookup"><span data-stu-id="61b43-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="61b43-314">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="61b43-314">Property Name</span></span></th>
        <th><span data-ttu-id="61b43-315">Description</span><span class="sxs-lookup"><span data-stu-id="61b43-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="61b43-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="61b43-317">Obtient ou définit le nombre maximal d’éléments à retourner dans l’opération d’énumération dans le service de base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="61b43-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="61b43-319">Obtient ou définit l’ID de plage de clés de partition pour la demande actuelle dans le service de base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="61b43-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="61b43-321">Obtient ou définit le jeton de continuation de demande dans le service de base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="61b43-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="61b43-322">SessionToken</span></span></td>
        <td><span data-ttu-id="61b43-323">Obtient ou définit le jeton de session pour une utilisation avec la cohérence de session dans le service de base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="61b43-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="61b43-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="61b43-325">Obtient ou définit une valeur indiquant si le flux de modification dans le service de base de données Azure Cosmos DB doit démarrer à partir du début (true) ou de la position actuelle (false).</span><span class="sxs-lookup"><span data-stu-id="61b43-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="61b43-326">Par défaut, il démarre de la position actuelle (false).</span><span class="sxs-lookup"><span data-stu-id="61b43-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="61b43-327">**Options de l’hôte de flux de modification** :</span><span class="sxs-lookup"><span data-stu-id="61b43-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="61b43-328">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="61b43-328">Property Name</span></span></th>
        <th><span data-ttu-id="61b43-329">Type</span><span class="sxs-lookup"><span data-stu-id="61b43-329">Type</span></span></th>
        <th><span data-ttu-id="61b43-330">Description</span><span class="sxs-lookup"><span data-stu-id="61b43-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="61b43-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="61b43-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61b43-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="61b43-333">Intervalle pour tous les baux pour les partitions actuellement détenues par l’instance de ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="61b43-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="61b43-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="61b43-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61b43-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="61b43-336">Intervalle pour déclencher une tâche afin de calculer si les partitions sont réparties uniformément parmi les instances d’hôte connues.</span><span class="sxs-lookup"><span data-stu-id="61b43-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="61b43-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="61b43-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61b43-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="61b43-339">Intervalle pour lequel le bail est pris sur un bail représentant une partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="61b43-340">Si le bail n’est pas renouvelé dans cet intervalle, il expire et une autre instance de ChangeFeedEventHost devient propriétaire de la partition.</span><span class="sxs-lookup"><span data-stu-id="61b43-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="61b43-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="61b43-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61b43-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="61b43-343">Délai entre le moment où toutes les modifications sont purgées et le moment où une partition est interrogée afin d’identifier les nouvelles modifications.</span><span class="sxs-lookup"><span data-stu-id="61b43-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="61b43-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="61b43-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="61b43-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="61b43-346">Fréquence de création de points de contrôle pour les baux.</span><span class="sxs-lookup"><span data-stu-id="61b43-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="61b43-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="61b43-348">int</span><span class="sxs-lookup"><span data-stu-id="61b43-348">Int</span></span></td>
        <td><span data-ttu-id="61b43-349">Nombre minimal de partitions pour l’hôte.</span><span class="sxs-lookup"><span data-stu-id="61b43-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="61b43-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="61b43-351">int</span><span class="sxs-lookup"><span data-stu-id="61b43-351">Int</span></span></td>
        <td><span data-ttu-id="61b43-352">Nombre maximal de partitions que l’hôte peut gérer.</span><span class="sxs-lookup"><span data-stu-id="61b43-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61b43-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="61b43-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="61b43-354">Bool</span><span class="sxs-lookup"><span data-stu-id="61b43-354">Bool</span></span></td>
        <td><span data-ttu-id="61b43-355">Indique si, au démarrage de l’hôte, tous les baux existants doivent être supprimés et l’hôte doit redémarrer à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="61b43-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="61b43-356">Pour commencer le traitement des événements, instanciez `ChangeFeedProcessorHost` en fournissant les paramètres appropriés pour votre collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61b43-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="61b43-357">Ensuite, appelez `RegisterObserverAsync` pour inscrire votre implémentation de `IChangeFeedObserver` (DocumentFeedObserver dans cet exemple) auprès du runtime.</span><span class="sxs-lookup"><span data-stu-id="61b43-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="61b43-358">À ce stade, l’hôte tente d’acquérir un bail sur chaque plage de clés de partition dans la collection Azure Cosmos DB à l’aide d’un algorithme « gourmand ».</span><span class="sxs-lookup"><span data-stu-id="61b43-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="61b43-359">Ces baux sont valables pour une période donnée et doivent ensuite être renouvelés.</span><span class="sxs-lookup"><span data-stu-id="61b43-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="61b43-360">À mesure que de nouveaux nœuds (ici, des instances de Workers) basculent en ligne, ils placent des réservations de bail et, au fil du temps, la charge est déplacée entre les nœuds à mesure que chaque nœud tente d’acquérir davantage de baux.</span><span class="sxs-lookup"><span data-stu-id="61b43-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="61b43-361">Dans l’exemple de code, nous utilisons une classe de fabrique (DocumentFeedObserverFactory.cs) pour créer un observateur et `RegistObserverFactoryAsync` pour inscrire l’observateur.</span><span class="sxs-lookup"><span data-stu-id="61b43-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="61b43-362">Au fil du temps, un équilibre est établi.</span><span class="sxs-lookup"><span data-stu-id="61b43-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="61b43-363">Cette fonctionnalité dynamique permet d’appliquer aux consommateurs une mise à l’échelle automatique basée sur le processeur pour une augmentation et une diminution d’échelle.</span><span class="sxs-lookup"><span data-stu-id="61b43-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="61b43-364">Si Azure Cosmos DB affiche plus de modifications que ce que les consommateurs peuvent traiter, l’augmentation du processeur sur les consommateurs peut être utilisée pour effectuer une mise à l’échelle automatique sur le nombre d’instances de travail.</span><span class="sxs-lookup"><span data-stu-id="61b43-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b43-365">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61b43-365">Next steps</span></span>
* <span data-ttu-id="61b43-366">Essayez les [exemples de code de flux de modification Azure Cosmos DB sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed).</span><span class="sxs-lookup"><span data-stu-id="61b43-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="61b43-367">Commencez à coder avec les [SDK Azure Cosmos DB](documentdb-sdk-dotnet.md) ou l’[API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="61b43-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
