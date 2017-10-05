---
title: "Azure Cosmos DB : API Java DocumentDB, Kit de développement logiciel (SDK) et ressources | Microsoft Docs"
description: "Découvrez l'API et le Kit de développement logiciel (SDK) Java, y compris les dates de lancement, les dates de suppression et les modifications apportées entre chaque version du Kit de développement logiciel (SDK) Java DocumentDB d’Azure Cosmos DB."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="dad22-103">Azure Cosmos DB - Kit de développement logiciel (SDK) Java DocumentDB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="dad22-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dad22-104">.NET</span><span class="sxs-lookup"><span data-stu-id="dad22-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="dad22-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="dad22-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="dad22-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dad22-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="dad22-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="dad22-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="dad22-108">Java</span><span class="sxs-lookup"><span data-stu-id="dad22-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="dad22-109">Python</span><span class="sxs-lookup"><span data-stu-id="dad22-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="dad22-110">REST</span><span class="sxs-lookup"><span data-stu-id="dad22-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="dad22-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="dad22-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="dad22-112">SQL</span><span class="sxs-lookup"><span data-stu-id="dad22-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="dad22-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="dad22-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="dad22-114">Maven</span><span class="sxs-lookup"><span data-stu-id="dad22-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="dad22-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="dad22-115">**API documentation**</span></span></td><td>[<span data-ttu-id="dad22-116">Documentation de référence sur l’API Java</span><span class="sxs-lookup"><span data-stu-id="dad22-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="dad22-117">**Contribution au Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="dad22-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="dad22-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="dad22-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="dad22-119">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="dad22-119">**Get started**</span></span></td><td>[<span data-ttu-id="dad22-120">Bien démarrer avec le Kit de développement logiciel (SDK) Java</span><span class="sxs-lookup"><span data-stu-id="dad22-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="dad22-121">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="dad22-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="dad22-122">Développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dad22-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="dad22-123">**Runtime actuellement pris en charge**</span><span class="sxs-lookup"><span data-stu-id="dad22-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="dad22-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="dad22-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="dad22-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="dad22-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="dad22-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="dad22-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="dad22-127">Correctifs de bogues critiques pour demander le traitement lors de fractionnements de partition.</span><span class="sxs-lookup"><span data-stu-id="dad22-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="dad22-128">Correction d’un problème avec les niveaux de cohérence Strong et BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="dad22-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="dad22-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="dad22-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="dad22-130">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="dad22-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="dad22-131">Correction d’un bogue de lecture de collection en mode de session.</span><span class="sxs-lookup"><span data-stu-id="dad22-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="dad22-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="dad22-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="dad22-133">Activation de la prise en charge de la collection partitionnée avec au minimum 2 500 RU/seconde et des incréments d’évolution de 100 RU/seconde.</span><span class="sxs-lookup"><span data-stu-id="dad22-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="dad22-134">Correction d’un bogue dans l’assembly natif, qui pouvait entraîner des exceptions NullRef pour certaines requêtes.</span><span class="sxs-lookup"><span data-stu-id="dad22-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="dad22-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="dad22-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="dad22-136">Correction d’un bogue dans la configuration du moteur de requête qui peut provoquer des exceptions pour les requêtes en mode de passerelle.</span><span class="sxs-lookup"><span data-stu-id="dad22-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="dad22-137">Correction de quelques bogues dans le conteneur de session qui peut provoquer une exception « Ressource propriétaire introuvable » pour les demandes dès la création de la collection.</span><span class="sxs-lookup"><span data-stu-id="dad22-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="dad22-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="dad22-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="dad22-139">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="dad22-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="dad22-140">Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="dad22-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="dad22-141">Ajout de la prise en charge de la modification de flux.</span><span class="sxs-lookup"><span data-stu-id="dad22-141">Added support for change feed.</span></span>
* <span data-ttu-id="dad22-142">Ajout de la prise en charge des informations relatives aux quotas de collections via RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="dad22-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="dad22-143">Ajout de la prise en charge de l’enregistrement de script de procédure stockée via RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="dad22-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="dad22-144">Correction d’un bogue dans lequel la requête en mode DirectHttps peut se bloquer lorsqu’elle rencontre des échecs de limitation.</span><span class="sxs-lookup"><span data-stu-id="dad22-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="dad22-145">Correction d’un bogue dans le mode de cohérence de session.</span><span class="sxs-lookup"><span data-stu-id="dad22-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="dad22-146">Correction d’un bogue susceptible d’entraîner l’exception NullReferenceException dans HttpContext lorsque le taux de demandes est élevé.</span><span class="sxs-lookup"><span data-stu-id="dad22-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="dad22-147">Amélioration des performances du mode DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="dad22-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="dad22-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="dad22-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="dad22-149">Ajout de la prise en charge simple d’un proxy basé sur les instances d’un client avec l’API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="dad22-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="dad22-150">Ajout de l’API DocumentClient.close() permettant de fermer correctement l’instance DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="dad22-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="dad22-151">Amélioration des performances de requête en mode de connectivité directe en dérivant le plan de requête à partir de l’assembly natif au lieu de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="dad22-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="dad22-152">Définissez FAIL_ON_UNKNOWN_PROPERTIES = false, de sorte que les utilisateurs n’aient pas besoin de définir JsonIgnoreProperties dans leur POJO.</span><span class="sxs-lookup"><span data-stu-id="dad22-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="dad22-153">Journalisation refactorisée pour utiliser SLF4J.</span><span class="sxs-lookup"><span data-stu-id="dad22-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="dad22-154">Correction de quelques autres bogues dans un lecteur de cohérence.</span><span class="sxs-lookup"><span data-stu-id="dad22-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="dad22-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="dad22-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="dad22-156">Correction d’un bogue dans la gestion des connexions pour éviter les fuites de connexion en mode de connectivité directe.</span><span class="sxs-lookup"><span data-stu-id="dad22-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="dad22-157">Correction d’un bogue dans la requête TOP des exceptions NullReference peuvent être levées.</span><span class="sxs-lookup"><span data-stu-id="dad22-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="dad22-158">Amélioration des performances avec la réduction du nombre d’appels réseau pour les caches internes.</span><span class="sxs-lookup"><span data-stu-id="dad22-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="dad22-159">Ajout d’un code d’état, d’un ID d’activité et d’un URI de requête dans DocumentClientException pour une meilleure résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="dad22-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="dad22-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="dad22-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="dad22-161">Résolution d’un problème de gestion des connexions pour plus de stabilité.</span><span class="sxs-lookup"><span data-stu-id="dad22-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="dad22-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="dad22-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="dad22-163">Ajout de la prise en charge du niveau de cohérence BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="dad22-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="dad22-164">Ajout de la prise en charge de la connectivité directe pour les opérations CRUD pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="dad22-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="dad22-165">Correction d’un bogue dans l’interrogation d’une base de données avec SQL.</span><span class="sxs-lookup"><span data-stu-id="dad22-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="dad22-166">Correction d’un bogue dans le cache de session où le jeton de session peut être défini de manière incorrecte.</span><span class="sxs-lookup"><span data-stu-id="dad22-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="dad22-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="dad22-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="dad22-168">Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="dad22-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="dad22-169">Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="dad22-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="dad22-170">Ajout de la prise en charge de la cohérence forte.</span><span class="sxs-lookup"><span data-stu-id="dad22-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="dad22-171">Ajout de la prise en charge des requêtes en fonction du nom lors de l’utilisation de la connectivité directe.</span><span class="sxs-lookup"><span data-stu-id="dad22-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="dad22-172">Correction visant à rendre ActivityId cohérent entre toutes les nouvelles tentatives de requête.</span><span class="sxs-lookup"><span data-stu-id="dad22-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="dad22-173">Correction d’un bogue lié au cache de session lors de la nouvelle création d’une collection avec le même nom.</span><span class="sxs-lookup"><span data-stu-id="dad22-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="dad22-174">Ajout des types de données Polygone et LineString lors de la spécification de la stratégie d’indexation de collection pour les requêtes spatiales à délimitation géographique.</span><span class="sxs-lookup"><span data-stu-id="dad22-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="dad22-175">Résolution des problèmes liés à Java Doc pour Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="dad22-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="dad22-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="dad22-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="dad22-177">Correction d’un bogue dans PartitionKeyDefinitionMap pour la mise en cache de collections de partitions uniques, sans aucune extraction supplémentaire des demandes de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="dad22-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="dad22-178">Correction d’un bogue pour l’absence de nouvelle tentative en cas de valeur de clé de partition incorrecte.</span><span class="sxs-lookup"><span data-stu-id="dad22-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="dad22-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="dad22-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="dad22-180">Ajout de la prise en charge des comptes de base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="dad22-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="dad22-181">Ajout de la prise en charge d’une nouvelle tentative automatique sur les requêtes limitées avec options de personnalisation du nombre maximum de tentatives et du délai d’attente maximum entre deux tentatives.</span><span class="sxs-lookup"><span data-stu-id="dad22-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="dad22-182">Voir RetryOptions et ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="dad22-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="dad22-183">Propriété IPartitionResolver déconseillée basée sur un code de partitionnement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="dad22-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="dad22-184">Utilisez des collections partitionnées pour bénéficier d’un niveau de stockage et de débit supérieur.</span><span class="sxs-lookup"><span data-stu-id="dad22-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="dad22-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="dad22-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="dad22-186">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour la limitation.</span><span class="sxs-lookup"><span data-stu-id="dad22-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="dad22-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="dad22-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="dad22-188">Ajout de la prise en charge de la durée de vie (TTL) pour les documents.</span><span class="sxs-lookup"><span data-stu-id="dad22-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="dad22-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="dad22-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="dad22-190">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dad22-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="dad22-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="dad22-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="dad22-192">Correction d’un bogue dans HashPartitionResolver pour générer des valeurs de hachage en little-endian dans un souci de cohérence avec les autres kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="dad22-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="dad22-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="dad22-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="dad22-194">Ajoutez des programmes de résolution de partitions par hachage et par spécification de plages de valeurs pour vous aider lors du partitionnement des applications sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="dad22-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="dad22-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="dad22-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="dad22-196">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="dad22-196">Implement Upsert.</span></span> <span data-ttu-id="dad22-197">Nouvelles méthodes upsertXXX ajoutées pour prendre en charge la fonctionnalité Upsert.</span><span class="sxs-lookup"><span data-stu-id="dad22-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="dad22-198">Implémenter l'ID en fonction du routage.</span><span class="sxs-lookup"><span data-stu-id="dad22-198">Implement ID Based Routing.</span></span> <span data-ttu-id="dad22-199">Aucune modification d'API publique, toutes les modifications en interne.</span><span class="sxs-lookup"><span data-stu-id="dad22-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="dad22-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="dad22-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="dad22-201">Version ignorée pour aligner le numéro de version avec les autres Kits de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="dad22-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="dad22-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="dad22-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="dad22-203">Prise en charge de l'index géospatial</span><span class="sxs-lookup"><span data-stu-id="dad22-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="dad22-204">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="dad22-204">Validates id property for all resources.</span></span> <span data-ttu-id="dad22-205">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="dad22-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="dad22-206">Ajoute le nouvel en-tête « progression de la transformation de l'index » à ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="dad22-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="dad22-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="dad22-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="dad22-208">Implémente la stratégie d'indexation V2</span><span class="sxs-lookup"><span data-stu-id="dad22-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="dad22-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="dad22-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="dad22-210">Kit SDK GA</span><span class="sxs-lookup"><span data-stu-id="dad22-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="dad22-211">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="dad22-211">Release & Retirement Dates</span></span>
<span data-ttu-id="dad22-212">Microsoft fournira une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.</span><span class="sxs-lookup"><span data-stu-id="dad22-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="dad22-213">Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit de développement logiciel (SDK) actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du Kit de développement logiciel (SDK) dès que possible.</span><span class="sxs-lookup"><span data-stu-id="dad22-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="dad22-214">Le service rejette toute requête envoyée à Cosmos DB à l’aide d’un Kit de développement logiciel (SDK) supprimé.</span><span class="sxs-lookup"><span data-stu-id="dad22-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="dad22-215">Toutes les versions du Kit de développement logiciel (SDK) DocumentDB pour Java antérieures à la version **1.0.0** seront supprimées le **29 février 2016**.</span><span class="sxs-lookup"><span data-stu-id="dad22-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="dad22-216">Version</span><span class="sxs-lookup"><span data-stu-id="dad22-216">Version</span></span> | <span data-ttu-id="dad22-217">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="dad22-217">Release Date</span></span> | <span data-ttu-id="dad22-218">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="dad22-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="dad22-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="dad22-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="dad22-220">11 juillet 2017</span><span class="sxs-lookup"><span data-stu-id="dad22-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="dad22-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="dad22-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="dad22-222">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="dad22-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="dad22-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="dad22-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="dad22-224">11 mars 2017</span><span class="sxs-lookup"><span data-stu-id="dad22-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="dad22-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="dad22-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="dad22-226">21 février 2017</span><span class="sxs-lookup"><span data-stu-id="dad22-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="dad22-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="dad22-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="dad22-228">31 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="dad22-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="dad22-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="dad22-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="dad22-230">24 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="dad22-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="dad22-232">30 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="dad22-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="dad22-234">28 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="dad22-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="dad22-236">26 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="dad22-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="dad22-238">3 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="dad22-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="dad22-240">30 juin 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="dad22-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="dad22-242">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="dad22-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="dad22-244">30 avril 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="dad22-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="dad22-246">27 avril 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="dad22-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="dad22-248">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="dad22-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="dad22-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="dad22-250">31 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="dad22-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="dad22-252">4 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="dad22-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="dad22-254">5 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="dad22-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="dad22-256">5 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="dad22-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="dad22-258">5 août 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dad22-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="dad22-260">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="dad22-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="dad22-262">12 mai 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="dad22-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="dad22-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="dad22-264">7 avril 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="dad22-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-265">0.9.5-prelease</span></span> |<span data-ttu-id="dad22-266">9 mars 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-266">Mar 09, 2015</span></span> |<span data-ttu-id="dad22-267">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-267">February 29, 2016</span></span> |
| <span data-ttu-id="dad22-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-268">0.9.4-prelease</span></span> |<span data-ttu-id="dad22-269">17 février 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-269">February 17, 2015</span></span> |<span data-ttu-id="dad22-270">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-270">February 29, 2016</span></span> |
| <span data-ttu-id="dad22-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-271">0.9.3-prelease</span></span> |<span data-ttu-id="dad22-272">13 janvier 2015</span><span class="sxs-lookup"><span data-stu-id="dad22-272">January 13, 2015</span></span> |<span data-ttu-id="dad22-273">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-273">February 29, 2016</span></span> |
| <span data-ttu-id="dad22-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-274">0.9.2-prelease</span></span> |<span data-ttu-id="dad22-275">19 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="dad22-275">December 19, 2014</span></span> |<span data-ttu-id="dad22-276">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-276">February 29, 2016</span></span> |
| <span data-ttu-id="dad22-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-277">0.9.1-prelease</span></span> |<span data-ttu-id="dad22-278">19 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="dad22-278">December 19, 2014</span></span> |<span data-ttu-id="dad22-279">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-279">February 29, 2016</span></span> |
| <span data-ttu-id="dad22-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="dad22-280">0.9.0-prelease</span></span> |<span data-ttu-id="dad22-281">10 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="dad22-281">December 10, 2014</span></span> |<span data-ttu-id="dad22-282">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="dad22-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="dad22-283">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="dad22-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="dad22-284">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dad22-284">See Also</span></span>
<span data-ttu-id="dad22-285">Pour en savoir plus sur Cosmos DB, consultez la page du service [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="dad22-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

