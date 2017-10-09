---
title: "prise en charge de flux aaaWorking avec modification de hello dans la base de données Azure Cosmos | Documents Microsoft"
description: "Utilisez Azure Cosmos DB modifier les modifications tootrack de prise en charge des flux dans les documents et exécuter basés sur les événements de traitement tout comme les déclencheurs et la maintenance des systèmes de caches et analytique à."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="61419-104">Utilisation de la prise en charge flux hello modification dans la base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="61419-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="61419-105">[Azure Cosmos DB](../cosmos-db/introduction.md) est un service de base de données répliqué mondialement, rapide et flexible utilisé pour le stockage d’importants volumes de données transactionnelles et opérationnelles avec une latence prévisible en quelques millisecondes pour les lectures et les écritures.</span><span class="sxs-lookup"><span data-stu-id="61419-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="61419-106">Il est ainsi parfait pour les applications d’IoT, de jeux, de vente au détail et de journalisation des compteurs.</span><span class="sxs-lookup"><span data-stu-id="61419-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="61419-107">Un modèle de conception courants dans ces applications est tootrack modifications apportées tooAzure la Cosmos base de données et mettre à jour les vues matérialisées, effectuer l’analytique en temps réel, archive toocold stockage des données et des notifications de déclenchement de certains événements en fonction de ces modifications.</span><span class="sxs-lookup"><span data-stu-id="61419-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="61419-108">Hello **prise en charge de flux de changement** dans la base de données Azure Cosmos vous permet de toobuild efficace et évolutive des solutions pour chacun de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="61419-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="61419-109">Modification de flux de prise en charge, base de données Azure Cosmos fournit une liste triée de documents dans une collection de base de données Azure Cosmos dans l’ordre de hello dans lequel ils ont été modifiés.</span><span class="sxs-lookup"><span data-stu-id="61419-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="61419-110">Ce flux peut être toolisten utilisé pour toodata des modifications au sein de la collection de hello et effectuer des actions telles que :</span><span class="sxs-lookup"><span data-stu-id="61419-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="61419-111">Déclencher une tooan appel API lorsqu’un document est inséré ou modifié</span><span class="sxs-lookup"><span data-stu-id="61419-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="61419-112">effectuer un traitement en temps réel (flux) sur les mises à jour ;</span><span class="sxs-lookup"><span data-stu-id="61419-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="61419-113">synchroniser les données avec un cache, le moteur de recherche ou l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="61419-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="61419-114">Les modifications dans Azure Cosmos DB sont conservées et peuvent être traitées de manière asynchrone et réparties sur un ou plusieurs consommateurs pour un traitement en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61419-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="61419-115">Examinons hello API pour les flux de modification et comment vous pouvez les utiliser toobuild hautement évolutives en temps réel.</span><span class="sxs-lookup"><span data-stu-id="61419-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="61419-116">Cet article explique comment toowork avec la base de données Azure Cosmos modifier le flux et hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="61419-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![À l’aide de la modification de la base de données Azure Cosmos flux analytique en temps réel de toopower et des scénarios de traitement pilotée par événements](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="61419-118">Modification de flux de prise en charge est disponible que pour hello API DocumentDB pour l’instant ; Hello API Graph et API de Table ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="61419-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="61419-119">Cas d'utilisation et scénarios</span><span class="sxs-lookup"><span data-stu-id="61419-119">Use cases and scenarios</span></span>
<span data-ttu-id="61419-120">Flux de modification permet un traitement efficace de grands jeux de données avec un grand nombre d’écritures et offre une tooidentify de jeux de données entière tooquerying autre ce qui a changé.</span><span class="sxs-lookup"><span data-stu-id="61419-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="61419-121">Par exemple, vous pouvez effectuer hello efficacement des tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="61419-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="61419-122">Mettre à jour un cache, l’index de recherche ou un entrepôt de données avec les données stockées dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61419-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="61419-123">Implémenter hiérarchisation et d’archivage de données de niveau application, autrement dit, stocker des données « chaudes » dans la base de données Azure Cosmos et expire trop de « données à froid »[stockage d’objets Blob Azure](../storage/common/storage-introduction.md) ou [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61419-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="61419-124">Implémenter une analyse en mode batch sur les données à l’aide [d’Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="61419-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="61419-125">Implémenter des [pipelines lambda sur Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61419-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="61419-126">Azure Cosmos DB fournit une solution de base de données évolutive qui peut gérer l’ingestion et l’interrogation, et implémenter des architectures lambda avec un faible coût total de possession.</span><span class="sxs-lookup"><span data-stu-id="61419-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="61419-127">Effectuer un zéro tooanother migrations d’inactivité du compte de base de données Azure Cosmos avec un schéma de partitionnement différent.</span><span class="sxs-lookup"><span data-stu-id="61419-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="61419-128">**Pipelines lambda avec Azure Cosmos DB pour l’ingestion et l’interrogation :**</span><span class="sxs-lookup"><span data-stu-id="61419-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda Azure Cosmos DB pour l’ingestion et l’interrogation](./media/change-feed/lambda.png)

<span data-ttu-id="61419-130">Vous pouvez utiliser tooreceive de la base de données Azure Cosmos et stocker les données d’événement à partir d’appareils, capteurs, l’infrastructure et les applications et traiter ces événements en temps réel avec [Analytique de flux de données Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61419-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="61419-131">Au sein de votre [sans](http://azure.com/serverless) web et des applications mobiles, vous pouvez suivre les événements tels que tootrigger de profil, préférences ou l’emplacement du client de modifications tooyour certaines actions, telles que l’envoi push appareils tootheir de notifications à l’aide de [Fonctions azure](../azure-functions/functions-bindings-documentdb.md) ou [des Services d’application](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="61419-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="61419-132">Si vous utilisez une base de données Azure Cosmos toobuild un jeu, vous pouvez, par exemple, utiliser ajouterons en temps réel de modification tooimplement de flux basé sur des scores à partir de jeux terminées.</span><span class="sxs-lookup"><span data-stu-id="61419-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="61419-133">Fonctionnement du flux de modification dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61419-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="61419-134">Base de données Azure Cosmos fournit hello capacité tooincrementally lire tooan de mises à jour la collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="61419-135">Ce flux du changement a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="61419-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="61419-136">Les modifications sont persistantes dans Azure Cosmos DB et peuvent être traitées de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="61419-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="61419-137">Toodocuments de modifications dans une collection de sont disponibles immédiatement dans le flux de changement de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="61419-138">Chaque modification tooa document apparaît une seule fois dans le flux du changement hello et clients de gérer leur logique de points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="61419-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="61419-139">bibliothèque de flux de processeur Hello modification fournit des points de contrôle automatiques et « au moins une fois » sémantique.</span><span class="sxs-lookup"><span data-stu-id="61419-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="61419-140">Modification la plus récente hello uniquement pour un document donné est incluse dans le journal des modifications hello.</span><span class="sxs-lookup"><span data-stu-id="61419-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="61419-141">Les modifications intermédiaires peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="61419-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="61419-142">flux de modification Hello est triée par ordre de modification au sein de chaque valeur de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="61419-143">Il n’existe aucun ordre garanti entre les valeurs de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="61419-144">Les modifications peuvent être synchronisées à partir de n’importe quel moment donné ; autrement dit, il n’existe aucune période de rétention de données fixes pendant laquelle les modifications sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="61419-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="61419-145">Les modifications sont disponibles dans des blocs de plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="61419-146">Cette fonctionnalité permet des modifications à partir de toobe de grandes collections traités en parallèle par plusieurs consommateurs/serveurs.</span><span class="sxs-lookup"><span data-stu-id="61419-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="61419-147">Les applications peuvent demander pour modifier plusieurs flux simultanément sur hello même collection.</span><span class="sxs-lookup"><span data-stu-id="61419-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="61419-148">Le flux de modification d’Azure Cosmos DB est activé par défaut pour tous les comptes.</span><span class="sxs-lookup"><span data-stu-id="61419-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="61419-149">Vous pouvez utiliser votre [débit approvisionné](request-units.md) dans votre région d’écriture ou les [lire zone](distribute-data-globally.md) tooread de hello modifier le flux, comme toute autre opération de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="61419-150">flux de changement de Hello inclut les insertions et les opérations de mise à jour apportées toodocuments au sein de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="61419-151">Vous pouvez capturer des suppressions en définissant un indicateur de « suppression réversible » dans vos documents à la place des suppressions.</span><span class="sxs-lookup"><span data-stu-id="61419-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="61419-152">Vous pouvez également définir une période d’expiration de vos documents via hello [fonctionnalité de la durée de vie](time-to-live.md), pour l’exemple, 24 heures et utilisation hello la valeur de cette propriété toocapture supprime.</span><span class="sxs-lookup"><span data-stu-id="61419-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="61419-153">Avec cette solution, vous avez tooprocess modifications dans un intervalle de temps inférieur à la période d’expiration de durée de vie hello.</span><span class="sxs-lookup"><span data-stu-id="61419-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="61419-154">Hello modification flux n’est disponible pour chaque plage de clés de partition dans la collection de documents hello et par conséquent, peut être distribué sur un ou plusieurs consommateurs pour un traitement parallèle.</span><span class="sxs-lookup"><span data-stu-id="61419-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Traitement distribué du flux de modification d’Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="61419-156">Vous avez plusieurs options pour implémenter une modification de flux dans votre code client.</span><span class="sxs-lookup"><span data-stu-id="61419-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="61419-157">Hello sections qui est immédiatement suivi décrivent comment les tooimplement hello du flux de modification à l’aide de hello API REST de Azure Cosmos DB et hello kits de développement logiciel DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="61419-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="61419-158">Toutefois, pour les applications .NET, nous vous recommandons d’utiliser hello nouvelle [processeur bibliothèque de flux de modification](#change-feed-processor) pour le traitement des événements à partir de hello modifient le flux lorsqu’il simplifie les modifications de la lecture sur plusieurs partitions et permet à plusieurs threads en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61419-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="61419-159"><a id="rest-apis"></a>Utilisation de hello API REST et les kits de développement logiciel DocumentDB</span><span class="sxs-lookup"><span data-stu-id="61419-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="61419-160">Azure Cosmos DB fournit des conteneurs élastiques de stockage et de débit appelés **collections**.</span><span class="sxs-lookup"><span data-stu-id="61419-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="61419-161">Les données contenues dans les collections sont regroupées logiquement à l’aide de [clés de partition](partition-data.md) à des fins d’évolutivité et de performance.</span><span class="sxs-lookup"><span data-stu-id="61419-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="61419-162">Azure Cosmos DB fournit diverses API pour accéder à ces données, y compris la recherche par ID (Read/Get), les requêtes et les flux de lecture (analyses).</span><span class="sxs-lookup"><span data-stu-id="61419-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="61419-163">Hello modification flux peut être obtenu en remplissant les deux toohello d’en-têtes demande nouvelle DocumentDB `ReadDocumentFeed` API et peuvent être traités en parallèle sur des plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="61419-164">API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="61419-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="61419-165">Examinons brièvement comment ReadDocumentFeed fonctionne.</span><span class="sxs-lookup"><span data-stu-id="61419-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="61419-166">Base de données Azure Cosmos prend en charge la lecture d’un flux de documents dans une collection via hello `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="61419-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="61419-167">Par exemple, hello de demande suivant retourne une page de documents à l’intérieur de hello `serverlogs` collection.</span><span class="sxs-lookup"><span data-stu-id="61419-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="61419-168">Résultats peuvent être limitées à l’aide de hello `x-ms-max-item-count` en-tête et les lectures peuvent être reprise par le renvoi de la demande de hello avec un `x-ms-continuation` en-tête est retourné dans la réponse précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="61419-169">Lors de l’opération à partir d’un seul client, `ReadDocumentFeed` itère dans les résultats sur les différentes partitions en série.</span><span class="sxs-lookup"><span data-stu-id="61419-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="61419-170">**Flux de lecture de documents en série**</span><span class="sxs-lookup"><span data-stu-id="61419-170">**Serial read document feed**</span></span>

<span data-ttu-id="61419-171">Vous pouvez également récupérer des flux hello de documents à l’aide d’une des hello pris en charge [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="61419-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="61419-172">Par exemple, les hello suivant extrait de code montre comment toouse hello [ReadDocumentFeedAsync méthode](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) dans .NET.</span><span class="sxs-lookup"><span data-stu-id="61419-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="61419-173">Exécution distribuée de ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="61419-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="61419-174">Pour les collections qui contiennent des téraoctets de données ou plus, ou qui reçoivent un grand nombre de mises à jour, l’exécution en série de flux de lecture à partir d’un seul ordinateur client n’est pas forcément pratique.</span><span class="sxs-lookup"><span data-stu-id="61419-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="61419-175">Dans l’ordre toosupport ces scénarios de données volumineuses, Azure Cosmos DB fournit les API toodistribute `ReadDocumentFeed` appels en toute transparence sur plusieurs lecteurs de client/consommateurs.</span><span class="sxs-lookup"><span data-stu-id="61419-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="61419-176">**Flux de lecture de documents distribué**</span><span class="sxs-lookup"><span data-stu-id="61419-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="61419-177">tooprovide de traitement évolutif des modifications incrémentielles, Azure Cosmos DB prend en charge un modèle de montée en puissance parallèle pour les modifications de hello flux API basée sur des plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="61419-178">Vous pouvez obtenir une liste des plages de clés de partition d’une collection effectuant un appel `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="61419-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="61419-179">Pour chaque plage de clés de partition, vous pouvez effectuer une `ReadDocumentFeed` tooread des documents avec les clés de partition dans la plage.</span><span class="sxs-lookup"><span data-stu-id="61419-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="61419-180">Récupération des plages de clés de partition d’une collection</span><span class="sxs-lookup"><span data-stu-id="61419-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="61419-181">Vous pouvez récupérer des plages de clés de partition hello en hello demande `pkranges` ressource au sein d’une collection.</span><span class="sxs-lookup"><span data-stu-id="61419-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="61419-182">Par exemple hello de demande suivant récupère hello liste de plages de clés de partition pour hello `serverlogs` collection :</span><span class="sxs-lookup"><span data-stu-id="61419-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="61419-183">Cette requête renvoie hello suivant de réponse contenant les métadonnées sur les plages de clés de partition hello :</span><span class="sxs-lookup"><span data-stu-id="61419-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="61419-184">**Propriétés de la plage de clé de partition**: chaque plage de clés de partition inclut des propriétés de métadonnées hello Bonjour tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="61419-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="61419-185">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61419-185">Header name</span></span></th>
        <th><span data-ttu-id="61419-186">Description</span><span class="sxs-lookup"><span data-stu-id="61419-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-187">id</span><span class="sxs-lookup"><span data-stu-id="61419-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="61419-188">ID de Hello pour la plage de clés de partition hello.</span><span class="sxs-lookup"><span data-stu-id="61419-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="61419-189">Il s’agit d’un ID stable et unique dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="61419-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="61419-190">Doit être utilisé par la plage de clé de partition Bonjour appel tooread modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="61419-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="61419-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="61419-192">Hello partition maximale clé valeur de hachage pour la plage de clés de partition hello.</span><span class="sxs-lookup"><span data-stu-id="61419-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="61419-193">À usage interne.</span><span class="sxs-lookup"><span data-stu-id="61419-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="61419-194">minInclusive</span></span></td>
        <td><span data-ttu-id="61419-195">Hello minimum de partition clé valeur de hachage pour la plage de clés de partition hello.</span><span class="sxs-lookup"><span data-stu-id="61419-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="61419-196">À usage interne.</span><span class="sxs-lookup"><span data-stu-id="61419-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="61419-197">Cela à l’aide de hello pris en charge [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="61419-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="61419-198">Par exemple, hello extrait de code suivant montre comment la clé de partition tooretrieve plages dans .NET à l’aide de hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) (méthode).</span><span class="sxs-lookup"><span data-stu-id="61419-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="61419-199">Base de données Azure Cosmos prend en charge la récupération de documents par plage de clés de partition par hello de paramètre facultatif `x-ms-documentdb-partitionkeyrangeid` en-tête.</span><span class="sxs-lookup"><span data-stu-id="61419-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="61419-200">Exécution d’un ReadDocumentFeed incrémentiel</span><span class="sxs-lookup"><span data-stu-id="61419-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="61419-201">ReadDocumentFeed prend en charge hello scénarios/tâches pour le traitement incrémentiel de modifications apportées aux collections de base de données Azure Cosmos suivantes :</span><span class="sxs-lookup"><span data-stu-id="61419-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="61419-202">Lire tous les modifie toodocuments à partir du début de hello, autrement dit, à partir de la création de la collection.</span><span class="sxs-lookup"><span data-stu-id="61419-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="61419-203">Lire tous les modifie toofuture mises à jour toodocuments de l’heure actuelle, ou les modifications apportées depuis une durée spécifiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="61419-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="61419-204">Lire toutes les modifications toodocuments à partir d’une version de logique de collection de hello (ETag).</span><span class="sxs-lookup"><span data-stu-id="61419-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="61419-205">Vous pouvez le point de contrôle vos consommateurs selon hello retourné ETag à partir des demandes de flux de lecture incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="61419-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="61419-206">les changements de Hello incluent toodocuments insertions et mises à jour.</span><span class="sxs-lookup"><span data-stu-id="61419-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="61419-207">Supprime de toocapture, vous devez utiliser une propriété « suppression réversible » au sein de vos documents, ou utilisez hello [propriété TTL intégrée](time-to-live.md) toosignal une suppression en attente Bonjour modifier le flux.</span><span class="sxs-lookup"><span data-stu-id="61419-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="61419-208">Hello suivants table listes hello [demande](/rest/api/documentdb/common-documentdb-rest-request-headers.md) et [les en-têtes de réponse](/rest/api/documentdb/common-documentdb-rest-response-headers.md) pour les opérations de ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="61419-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="61419-209">**En-têtes de demande pour les opérations ReadDocumentFeed incrémentielles** :</span><span class="sxs-lookup"><span data-stu-id="61419-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="61419-210">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61419-210">Header name</span></span></th>
        <th><span data-ttu-id="61419-211">Description</span><span class="sxs-lookup"><span data-stu-id="61419-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="61419-212">A-IM</span></span></td>
        <td><span data-ttu-id="61419-213">Doit avoir la valeur trop « Incrémentiel flux », ou est omis dans le cas contraire</span><span class="sxs-lookup"><span data-stu-id="61419-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="61419-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="61419-215">Aucun en-tête : retourne toutes les modifications à partir de hello depuis (création de la collection)</span><span class="sxs-lookup"><span data-stu-id="61419-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="61419-216">« * » : retourne toutes les nouvelles modifications toodata, au sein de la collection de hello</span><span class="sxs-lookup"><span data-stu-id="61419-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="61419-217">&lt;eTag&gt;: si jeu tooa collection ETag, retourne toutes les modifications apportées depuis cette date logique</span><span class="sxs-lookup"><span data-stu-id="61419-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="61419-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="61419-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="61419-219">Format d’heure RFC 1123 ; ignoré si If-None-Match est spécifié.</span><span class="sxs-lookup"><span data-stu-id="61419-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="61419-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="61419-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="61419-221">ID de plage de clés Hello partition pour la lecture des données.</span><span class="sxs-lookup"><span data-stu-id="61419-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="61419-222">**En-têtes de réponse pour les opérations ReadDocumentFeed incrémentielles** :</span><span class="sxs-lookup"><span data-stu-id="61419-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="61419-223">Nom de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="61419-223">Header name</span></span></th>
        <th><span data-ttu-id="61419-224">Description</span><span class="sxs-lookup"><span data-stu-id="61419-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-225">etag</span><span class="sxs-lookup"><span data-stu-id="61419-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="61419-226">numéro de séquence logique Hello (LSN) du dernier document renvoyé dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="61419-227">L’opération ReadDocumentFeed incrémentielle peut être reprise en resoumettant cette valeur dans If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="61419-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="61419-228">Voici un tooreturn de demande exemple toutes les modifications incrémentielles dans la collection à partir de la logique de hello version/ETag `28535` et de la plage de clés de partition = `16`:</span><span class="sxs-lookup"><span data-stu-id="61419-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="61419-229">Modifications sont classées par temps au sein de chaque valeur de clé de partition dans la plage de clés de partition hello.</span><span class="sxs-lookup"><span data-stu-id="61419-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="61419-230">Il n’existe aucun ordre garanti entre les valeurs de clé de partition.</span><span class="sxs-lookup"><span data-stu-id="61419-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="61419-231">S’il y a plus de résultats peut être contenue dans une seule page, vous pouvez lire la page de résultats suivante hello à soumettre à nouveau la demande hello avec hello `If-None-Match` en-tête avec la valeur des toohello égal `etag` à partir de la réponse précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="61419-232">Si plusieurs documents ont été insérées ou mises à jour au niveau transactionnel au sein d’une procédure stockée ou un déclencheur, ils seront tous renvoyés dans hello même page de réponse.</span><span class="sxs-lookup"><span data-stu-id="61419-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="61419-233">Avec la modification de l’alimentation, vous pouvez obtenir plus d’éléments retournés dans une page à celle spécifiée dans `x-ms-max-item-count` dans les cas de hello de plusieurs documents insérées ou mises à jour à l’intérieur des procédures stockées ou des déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="61419-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="61419-234">Lorsque vous utilisez hello .NET SDK (1.17.0), définir le champ de hello `StartTime` dans `ChangeFeedOptions` documents toodirectly retour modifié depuis `StartTime` lors de l’appel `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="61419-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="61419-235">En spécifiant `If-Modified-Since` à l’aide des API REST de hello, votre requête retourne pas les documents hello, mais plutôt le jeton de continuation hello ou `etag` dans l’en-tête de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="61419-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="61419-236">documents de hello tooreturn hello modifié spécifié, jeton de continuation hello `etag` doit ensuite être utilisée dans la demande suivante de hello avec `If-None-Match` tooreturn hello documents réels.</span><span class="sxs-lookup"><span data-stu-id="61419-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="61419-237">Hello .NET SDK fournit hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) et [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess les modifications apportées tooa collection de classes d’assistance.</span><span class="sxs-lookup"><span data-stu-id="61419-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="61419-238">Hello extrait de code suivant montre les tooretrieve toutes les modifications à partir du début hello à l’aide de hello .NET SDK à partir d’un seul client.</span><span class="sxs-lookup"><span data-stu-id="61419-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="61419-239">Et hello extrait de code suivant montre comment tooprocess change en temps réel avec la base de données Azure Cosmos à l’aide des modifications de hello flux prise en charge et hello précédant la fonction.</span><span class="sxs-lookup"><span data-stu-id="61419-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="61419-240">Hello premier appel retourne tous les documents hello dans la collection de hello et hello ensuite uniquement retourne hello deux documents créés qui ont été créés depuis le dernier point de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="61419-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="61419-241">Vous pouvez également filtrer les flux de changement de hello à l’aide d’événements de processus de tooselectively logique côté client.</span><span class="sxs-lookup"><span data-stu-id="61419-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="61419-242">Par exemple, Voici un extrait de code qui utilise tooprocess LINQ côté client uniquement les événements de modification de température de capteurs de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="61419-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="61419-243"><a id="change-feed-processor"></a>Bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61419-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="61419-244">Une autre option consiste à toouse hello [bibliothèque d’Azure Cosmos DB modifier flux processeur](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), qui peut vous aider à distribuer facilement à partir d’une modification sur plusieurs consommateurs de flux de traitement des événements.</span><span class="sxs-lookup"><span data-stu-id="61419-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="61419-245">bibliothèque de Hello est idéal pour la création de lecteurs de flux sur la plateforme .NET de hello de modification.</span><span class="sxs-lookup"><span data-stu-id="61419-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="61419-246">Certains flux de travail est simplifiée à l’aide de la bibliothèque du processeur de modification de flux hello sur méthodes hello inclus dans hello autres kits de développement de base de données Cosmos sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="61419-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="61419-247">Extraction de mises à jour à partir du flux de modification quand les données sont stockées sur plusieurs partitions</span><span class="sxs-lookup"><span data-stu-id="61419-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="61419-248">Déplacement ou la réplication de données à partir d’une collection tooanother</span><span class="sxs-lookup"><span data-stu-id="61419-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="61419-249">Exécution parallèle des actions déclenchées par les mises à jour toodata et modification de flux</span><span class="sxs-lookup"><span data-stu-id="61419-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="61419-250">À l’aide des API de hello Bonjour Cosmos kits de développement logiciel fournit un accès précis toochange flux mises à jour dans chaque partition, à l’aide de la bibliothèque de processeur de modification de flux hello simplifie les modifications de lecture entre plusieurs threads en parallèle et les partitions.</span><span class="sxs-lookup"><span data-stu-id="61419-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="61419-251">Au lieu de lire manuellement des modifications à partir de chaque conteneur et l’enregistrement d’un jeton de liaison pour chaque partition, hello processeur de modification de flux gère automatiquement les modifications de la lecture sur plusieurs partitions à l’aide d’un mécanisme de bail.</span><span class="sxs-lookup"><span data-stu-id="61419-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="61419-252">bibliothèque de Hello est disponible sous forme de NuGet Package : [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) et à partir de code source en tant qu’un Github [exemple](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="61419-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="61419-253">Présentation de la bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61419-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="61419-254">Il existe quatre composants principaux de l’implémentation hello processeur de flux de modification : hello analysés collection, collection de bail hello, hello processeur hôte et les consommateurs hello.</span><span class="sxs-lookup"><span data-stu-id="61419-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="61419-255">**Collecte analysé :** collection de hello analysé est données hello à partir de quels hello flux de modification est généré.</span><span class="sxs-lookup"><span data-stu-id="61419-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="61419-256">N’importe quelle collection toohello analysé insertions et les modifications sont répercutées dans le flux du changement hello de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="61419-257">**Collection de bail :** hello coordonnées de collection de bail modification hello flux entre plusieurs threads de travail de traitement.</span><span class="sxs-lookup"><span data-stu-id="61419-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="61419-258">Une collection distincte est baux de hello toostore utilisé avec un bail par partition.</span><span class="sxs-lookup"><span data-stu-id="61419-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="61419-259">Il est avantageux toostore cette collection de bail sur un autre compte avec hello écrire hello toowhere plus proche de la région, processeur de flux de modification est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="61419-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="61419-260">Un objet de bail contient hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="61419-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="61419-261">Propriétaire : Spécifie l’hôte hello qui détient le bail de hello</span><span class="sxs-lookup"><span data-stu-id="61419-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="61419-262">Continuation : Spécifie la position d’hello (jeton de continuation) modification hello pour une partition particulière de flux</span><span class="sxs-lookup"><span data-stu-id="61419-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="61419-263">Date et heure : Dernière bail a été mis à jour ; Hello timestamp peut être utilisé toocheck si le bail de hello est considéré comme expiré</span><span class="sxs-lookup"><span data-stu-id="61419-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="61419-264">**Processeur hôte :** chaque hôte détermine combien tooprocess de partitions basé sur le nombre d’autres instances d’hôtes ont des baux actifs.</span><span class="sxs-lookup"><span data-stu-id="61419-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="61419-265">Lorsqu’un ordinateur hôte démarre, il acquiert la charge de travail de baux toobalance hello sur tous les hôtes.</span><span class="sxs-lookup"><span data-stu-id="61419-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="61419-266">Un hôte renouvelle périodiquement les baux afin que ceux-ci restent actifs.</span><span class="sxs-lookup"><span data-stu-id="61419-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="61419-267">Un hôte des points de contrôle hello dernière continuation jeton tooits bail pour chaque lecture.</span><span class="sxs-lookup"><span data-stu-id="61419-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="61419-268">la sécurité d’accès concurrentiel tooensure, un hôte vérifie hello ETag pour chaque mise à jour de bail.</span><span class="sxs-lookup"><span data-stu-id="61419-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="61419-269">D’autres stratégies de point de contrôle sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="61419-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="61419-270">En cas d’arrêt, un hôte libère tous les baux mais conserve hello les informations de liaison, afin de pouvoir reprendre la lecture à partir du point de contrôle stockée hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="61419-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="61419-271">À ce stade, nombre hello d’hôtes ne peut pas être supérieur au nombre de hello de partitions (Location).</span><span class="sxs-lookup"><span data-stu-id="61419-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="61419-272">**Consommateurs :** des traitements, ou des consommateurs sont des threads qui effectuent des modifications hello processus initié par chaque hôte de flux.</span><span class="sxs-lookup"><span data-stu-id="61419-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="61419-273">Chaque hôte de processeur peut avoir plusieurs consommateurs.</span><span class="sxs-lookup"><span data-stu-id="61419-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="61419-274">Chaque consommateur lit les flux de modification hello de hello partition, elle est assignée tooand informe son hôte de modifications et expiration des baux.</span><span class="sxs-lookup"><span data-stu-id="61419-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="61419-275">toofurther comprendre comment ces quatre éléments de processeur de modification de flux fonctionnent ensemble, examinons un exemple Bonjour suivant schéma.</span><span class="sxs-lookup"><span data-stu-id="61419-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="61419-276">Hello analysés collection stocke les documents et utilise hello « city » en tant que clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="61419-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="61419-277">Nous constatons que les partitions hello bleu contient des documents avec le champ « Ville » de hello à partir de « A-E » et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="61419-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="61419-278">Il existe deux hôtes, chacun avec deux consommateurs lors de la lecture à partir de partitions hello quatre en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61419-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="61419-279">les flèches de Hello indiquent les consommateurs hello lors de la lecture à partir d’un point spécifique dans hello modifier le flux.</span><span class="sxs-lookup"><span data-stu-id="61419-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="61419-280">Dans la première partition de hello, bleu foncé de hello représente les modifications non lues tandis que bleu clair de hello représente hello déjà lu les modifications dans le flux du changement hello.</span><span class="sxs-lookup"><span data-stu-id="61419-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="61419-281">les hôtes de Hello utilisent hello bail collection toostore une piste de tookeep de valeur « continuation » de hello en cours de la lecture de position pour chaque consommateur.</span><span class="sxs-lookup"><span data-stu-id="61419-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![À l’aide de la modification de base de données Azure Cosmos hello flux processeur hôte](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="61419-283">Utilisation de la bibliothèque du processeur de flux de modification</span><span class="sxs-lookup"><span data-stu-id="61419-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="61419-284">Hello suivant la section explique comment toouse hello bibliothèque processeur de modification de flux dans le contexte de hello de réplication des modifications à partir d’une collection de destination tooa collection source.</span><span class="sxs-lookup"><span data-stu-id="61419-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="61419-285">Ici, hello source collection est hello analysé dans le processeur de modification de flux.</span><span class="sxs-lookup"><span data-stu-id="61419-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="61419-286">**Installer et inclure le package NuGet de processeur de flux de changement de hello**</span><span class="sxs-lookup"><span data-stu-id="61419-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="61419-287">Avant d’installer le package NuGet du processeur de flux de modification, vous devez d’abord installer :</span><span class="sxs-lookup"><span data-stu-id="61419-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="61419-288">Microsoft.Azure.DocumentDB, version 1.13.1 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="61419-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="61419-289">Newtonsoft.Json, version 9.0.1 ou ultérieure. Installez `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` et incluez-le comme référence.</span><span class="sxs-lookup"><span data-stu-id="61419-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="61419-290">**Créer une collection analysée, une collection de baux et une collection de destination**</span><span class="sxs-lookup"><span data-stu-id="61419-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="61419-291">Collection de bail hello hello toouse de commande processeur bibliothèque de flux de modification, doit toobe créé avant l’exécution des hôtes de processeur hello.</span><span class="sxs-lookup"><span data-stu-id="61419-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="61419-292">Là encore, nous vous recommandons de stocker une collection de bail sur un autre compte avec un hello toowhere écriture le plus proche de la région que processeur de flux de modification est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="61419-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="61419-293">Dans cet exemple de déplacement des données, nous devons la collection de destination hello toocreate avant d’exécuter l’hôte du processeur de modification de flux hello.</span><span class="sxs-lookup"><span data-stu-id="61419-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="61419-294">Dans l’exemple de code hello, nous appelons un Bonjour toocreate de méthode d’assistance surveillé, loué et des regroupements de destination s’ils n’existent pas déjà.</span><span class="sxs-lookup"><span data-stu-id="61419-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="61419-295">Création d’une collection a tarification implications, que vous réservez un débit de toocommunicate d’application hello avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="61419-296">Pour plus d’informations, visitez hello [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="61419-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="61419-297">*Création d’un hôte de processeur*</span><span class="sxs-lookup"><span data-stu-id="61419-297">*Creating a processor host*</span></span>

<span data-ttu-id="61419-298">Hello `ChangeFeedProcessorHost` classe fournit un environnement d’exécution de thread-safe, plusieurs processus sécurisé pour les implémentations de processeur d’événements qui permet également la gestion de bail de points de contrôle et de la partition.</span><span class="sxs-lookup"><span data-stu-id="61419-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="61419-299">toouse hello `ChangeFeedProcessorHost` (classe), vous pouvez implémenter `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="61419-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="61419-300">Cette interface contient trois méthodes :</span><span class="sxs-lookup"><span data-stu-id="61419-300">This interface contains three methods:</span></span>

* <span data-ttu-id="61419-301">`OpenAsync` : cette fonction est appelée quand l’observateur de flux de modification est ouvert.</span><span class="sxs-lookup"><span data-stu-id="61419-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="61419-302">Il peut être modifié tooperform une action spécifique lorsque le consommateur/observateur est ouvert.</span><span class="sxs-lookup"><span data-stu-id="61419-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="61419-303">`CloseAsync` : cette fonction est appelée quand l’observateur de flux de modification est arrêté.</span><span class="sxs-lookup"><span data-stu-id="61419-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="61419-304">Il peut être modifié tooperform une action spécifique lorsque le consommateur/observateur est fermé.</span><span class="sxs-lookup"><span data-stu-id="61419-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="61419-305">`ProcessChangesAsync` : cette fonction est appelée quand de nouvelles modifications de document sont disponibles sur le flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61419-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="61419-306">Il peut être modifié tooperform une action spécifique sur chaque mise à jour de la modification de flux.</span><span class="sxs-lookup"><span data-stu-id="61419-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="61419-307">Dans notre exemple, nous implémentons interface de hello `IChangeFeedObserver` via hello `DocumentFeedObserver` classe.</span><span class="sxs-lookup"><span data-stu-id="61419-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="61419-308">Ici, hello `ProcessChangesAsync` upserts (mises à jour), un document à partir de la modification de flux dans la collection de destination hello de fonction.</span><span class="sxs-lookup"><span data-stu-id="61419-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="61419-309">Cet exemple est utile pour le déplacement des données à partir d’une collection des tooanother dans la clé de partition toochange hello ordre d’un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="61419-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="61419-310">*Hello processeur hôte en cours d’exécution*</span><span class="sxs-lookup"><span data-stu-id="61419-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="61419-311">Avant de commencer le traitement des événements, vous pouvez personnaliser les options de flux de modification et les options d’hôte de flux de modification.</span><span class="sxs-lookup"><span data-stu-id="61419-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="61419-312">champs Hello spécifiques qui peuvent être personnalisés sont résumées dans hello les tableaux suivants.</span><span class="sxs-lookup"><span data-stu-id="61419-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="61419-313">**Options de flux de modification** :</span><span class="sxs-lookup"><span data-stu-id="61419-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="61419-314">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="61419-314">Property Name</span></span></th>
        <th><span data-ttu-id="61419-315">Description</span><span class="sxs-lookup"><span data-stu-id="61419-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="61419-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="61419-317">Obtient ou définit le nombre maximal de hello de toobe d’éléments retourné dans l’opération d’énumération hello Bonjour service de base de données de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="61419-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="61419-319">Obtient ou définit l’id de plage de clés de partition hello pour la demande en cours de hello dans le service de base de données de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="61419-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="61419-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="61419-321">Obtient ou définit le jeton de continuation de requête hello dans le service de base de données de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="61419-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="61419-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="61419-322">SessionToken</span></span></td>
        <td><span data-ttu-id="61419-323">Obtient ou définit le jeton de session hello pour une utilisation avec la cohérence de session dans hello service de base de données de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="61419-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="61419-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="61419-325">Obtient ou définit si la modification de flux dans le service de base de données de base de données Azure Cosmos hello doit démarrer à partir de hello depuis (true) ou en cours (false).</span><span class="sxs-lookup"><span data-stu-id="61419-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="61419-326">Par défaut, il démarre de la position actuelle (false).</span><span class="sxs-lookup"><span data-stu-id="61419-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="61419-327">**Options de l’hôte de flux de modification** :</span><span class="sxs-lookup"><span data-stu-id="61419-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="61419-328">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="61419-328">Property Name</span></span></th>
        <th><span data-ttu-id="61419-329">Type</span><span class="sxs-lookup"><span data-stu-id="61419-329">Type</span></span></th>
        <th><span data-ttu-id="61419-330">Description</span><span class="sxs-lookup"><span data-stu-id="61419-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="61419-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="61419-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61419-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="61419-333">intervalle de salutation pour tous les baux pour les partitions actuellement détenu par l’instance de ChangeFeedEventHost hello.</span><span class="sxs-lookup"><span data-stu-id="61419-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="61419-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="61419-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61419-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="61419-336">Bonjour tookick intervalle désactiver une tâche de toocompute si les partitions sont réparties uniformément entre les instances d’hôte connus.</span><span class="sxs-lookup"><span data-stu-id="61419-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="61419-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="61419-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61419-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="61419-339">Intervalle Hello pour le hello bail est effectuée sur un bail qui représente une partition.</span><span class="sxs-lookup"><span data-stu-id="61419-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="61419-340">Si le bail de hello n’est pas renouvelé dans cet intervalle, elle a expiré et la propriété de partition de hello passe tooanother ChangeFeedEventHost instance.</span><span class="sxs-lookup"><span data-stu-id="61419-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="61419-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="61419-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61419-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="61419-343">délai de Hello entre l’interrogation d’une partition de nouvelles modifications sur hello flux, une fois que toutes les modifications actuelles sont purgées.</span><span class="sxs-lookup"><span data-stu-id="61419-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="61419-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="61419-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="61419-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="61419-346">baux de fréquence toocheckpoint Hello.</span><span class="sxs-lookup"><span data-stu-id="61419-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="61419-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="61419-348">Int</span><span class="sxs-lookup"><span data-stu-id="61419-348">Int</span></span></td>
        <td><span data-ttu-id="61419-349">nombre minimal de partitions de Hello pour l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="61419-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="61419-351">Int</span><span class="sxs-lookup"><span data-stu-id="61419-351">Int</span></span></td>
        <td><span data-ttu-id="61419-352">nombre maximal de Hello d’hôte hello de partitions peut traiter.</span><span class="sxs-lookup"><span data-stu-id="61419-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="61419-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="61419-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="61419-354">Bool</span><span class="sxs-lookup"><span data-stu-id="61419-354">Bool</span></span></td>
        <td><span data-ttu-id="61419-355">Si sur hello début de l’hôte de hello, tous les baux existants doit être supprimé et l’hôte de hello doit démarrer à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="61419-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="61419-356">traitement des événements toostart instancier `ChangeFeedProcessorHost`, en fournissant les paramètres appropriés hello pour votre collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="61419-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="61419-357">Ensuite, appelez `RegisterObserverAsync` tooregister votre `IChangeFeedObserver` implémentation (DocumentFeedObserver dans cet exemple) avec le runtime de hello.</span><span class="sxs-lookup"><span data-stu-id="61419-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="61419-358">À ce stade, les hôtes hello tentatives tooacquire un bail sur chaque plage de clés de partition dans la collection de base de données Azure Cosmos hello à l’aide d’un algorithme « greedy ».</span><span class="sxs-lookup"><span data-stu-id="61419-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="61419-359">Ces baux sont valables pour une période donnée et doivent ensuite être renouvelés.</span><span class="sxs-lookup"><span data-stu-id="61419-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="61419-360">Comme les nouveaux nœuds dans ce cas, les instances de travail en ligne, ils placent des réservations de baux et au fil du temps chargement de hello déplace entre les nœuds que chaque hôte tentatives tooacquire baux supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="61419-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="61419-361">Dans l’exemple de code hello, nous utilisons un toocreate (DocumentFeedObserverFactory.cs) de classe de fabrique un observateur et le hello `RegistObserverFactoryAsync` Observateur de hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="61419-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="61419-362">Au fil du temps, un équilibre est établi.</span><span class="sxs-lookup"><span data-stu-id="61419-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="61419-363">Cette capacité dynamique permet de processeur mise à l’échelle toobe appliqué tooconsumers pour la montée en puissance parallèle et l’échelle vers le bas.</span><span class="sxs-lookup"><span data-stu-id="61419-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="61419-364">Si les modifications sont disponibles dans la base de données Azure Cosmos à un rythme plus rapide que les consommateurs peuvent en traiter, augmentation du processeur hello consommateurs peut être utilisé toocause une à l’échelle automatique sur le nombre d’instances de processus de travail.</span><span class="sxs-lookup"><span data-stu-id="61419-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61419-365">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61419-365">Next steps</span></span>
* <span data-ttu-id="61419-366">Essayez de hello [changement de base de données Azure Cosmos flux des exemples de code sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="61419-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="61419-367">Commencer le codage par hello [kits de développement de base de données Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="61419-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
