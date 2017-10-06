---
title: "Azure Cosmos DB : API Java DocumentDB, Kit de développement logiciel (SDK) et ressources | Microsoft Docs"
description: "Découvrez les hello API Java et le Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version du Kit de développement logiciel Azure Cosmos DB DocumentDB Java de hello."
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
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="848af-103">Azure Cosmos DB - Kit de développement logiciel (SDK) Java DocumentDB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="848af-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="848af-104">.NET</span><span class="sxs-lookup"><span data-stu-id="848af-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="848af-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="848af-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="848af-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="848af-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="848af-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="848af-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="848af-108">Java</span><span class="sxs-lookup"><span data-stu-id="848af-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="848af-109">Python</span><span class="sxs-lookup"><span data-stu-id="848af-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="848af-110">REST</span><span class="sxs-lookup"><span data-stu-id="848af-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="848af-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="848af-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="848af-112">SQL</span><span class="sxs-lookup"><span data-stu-id="848af-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="848af-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="848af-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="848af-114">Maven</span><span class="sxs-lookup"><span data-stu-id="848af-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="848af-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="848af-115">**API documentation**</span></span></td><td>[<span data-ttu-id="848af-116">Documentation de référence sur l’API Java</span><span class="sxs-lookup"><span data-stu-id="848af-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="848af-117">**Contribuent tooSDK**</span><span class="sxs-lookup"><span data-stu-id="848af-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="848af-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="848af-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="848af-119">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="848af-119">**Get started**</span></span></td><td>[<span data-ttu-id="848af-120">Prise en main hello Kit de développement logiciel Java</span><span class="sxs-lookup"><span data-stu-id="848af-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="848af-121">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="848af-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="848af-122">Développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="848af-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="848af-123">**Runtime actuellement pris en charge**</span><span class="sxs-lookup"><span data-stu-id="848af-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="848af-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="848af-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="848af-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="848af-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="848af-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="848af-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="848af-127">Fractionnements de pages toorequest de correctifs critiques du traitement au cours de la partition.</span><span class="sxs-lookup"><span data-stu-id="848af-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="848af-128">Résolution du problème de hello fort et niveaux de cohérence BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="848af-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="848af-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="848af-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="848af-130">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="848af-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="848af-131">Correction d’un bogue de lecture de collection en mode de session.</span><span class="sxs-lookup"><span data-stu-id="848af-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="848af-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="848af-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="848af-133">Activation de la prise en charge de la collection partitionnée avec au minimum 2 500 RU/seconde et des incréments d’évolution de 100 RU/seconde.</span><span class="sxs-lookup"><span data-stu-id="848af-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="848af-134">Correction d’un bogue dans l’assembly natif de hello qui peut provoquer des NullRef exception de certaines requêtes.</span><span class="sxs-lookup"><span data-stu-id="848af-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="848af-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="848af-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="848af-136">Correction d’un bogue dans la configuration du moteur de requête hello qui peut provoquer des exceptions pour les requêtes en mode de passerelle.</span><span class="sxs-lookup"><span data-stu-id="848af-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="848af-137">Résolu quelques bogues dans le conteneur de session hello qui peut provoquer une exception « Ressource propriétaire introuvable » pour les demandes immédiatement après la création de la collection.</span><span class="sxs-lookup"><span data-stu-id="848af-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="848af-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="848af-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="848af-139">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="848af-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="848af-140">Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="848af-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="848af-141">Ajout de la prise en charge de la modification de flux.</span><span class="sxs-lookup"><span data-stu-id="848af-141">Added support for change feed.</span></span>
* <span data-ttu-id="848af-142">Ajout de la prise en charge des informations relatives aux quotas de collections via RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="848af-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="848af-143">Ajout de la prise en charge de l’enregistrement de script de procédure stockée via RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="848af-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="848af-144">Correction d’un bogue dans lequel la requête en mode DirectHttps peut se bloquer lorsqu’elle rencontre des échecs de limitation.</span><span class="sxs-lookup"><span data-stu-id="848af-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="848af-145">Correction d’un bogue dans le mode de cohérence de session.</span><span class="sxs-lookup"><span data-stu-id="848af-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="848af-146">Correction d’un bogue susceptible d’entraîner l’exception NullReferenceException dans HttpContext lorsque le taux de demandes est élevé.</span><span class="sxs-lookup"><span data-stu-id="848af-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="848af-147">Amélioration des performances du mode DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="848af-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="848af-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="848af-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="848af-149">Ajout de la prise en charge simple d’un proxy basé sur les instances d’un client avec l’API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="848af-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="848af-150">Ajouté DocumentClient.close() API tooproperly arrêter DocumentClient l’instance.</span><span class="sxs-lookup"><span data-stu-id="848af-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="848af-151">Meilleures performances des requêtes en mode de connectivité directe en dérivant de plan de requête hello assembly natif hello au lieu de hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="848af-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="848af-152">Définissez FAIL_ON_UNKNOWN_PROPERTIES = false, les utilisateurs n’avez pas besoin toodefine JsonIgnoreProperties dans leur POJO.</span><span class="sxs-lookup"><span data-stu-id="848af-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="848af-153">Journalisation refactorisé toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="848af-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="848af-154">Correction de quelques autres bogues dans un lecteur de cohérence.</span><span class="sxs-lookup"><span data-stu-id="848af-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="848af-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="848af-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="848af-156">Correction d’un bogue dans les pertes de connexion tooprevent hello connexion gestion en mode de connexion directe.</span><span class="sxs-lookup"><span data-stu-id="848af-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="848af-157">Correction d’un bogue dans la requête TOP de hello où il peut lever NullReferenece exception.</span><span class="sxs-lookup"><span data-stu-id="848af-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="848af-158">Amélioration des performances en réduisant le nombre de hello d’appel de réseau pour les caches internes hello.</span><span class="sxs-lookup"><span data-stu-id="848af-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="848af-159">Ajout d’un code d’état, d’un ID d’activité et d’un URI de requête dans DocumentClientException pour une meilleure résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="848af-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="848af-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="848af-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="848af-161">Correction d’un problème dans la gestion des connexions hello de stabilité.</span><span class="sxs-lookup"><span data-stu-id="848af-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="848af-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="848af-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="848af-163">Ajout de la prise en charge du niveau de cohérence BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="848af-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="848af-164">Ajout de la prise en charge de la connectivité directe pour les opérations CRUD pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="848af-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="848af-165">Correction d’un bogue dans l’interrogation d’une base de données avec SQL.</span><span class="sxs-lookup"><span data-stu-id="848af-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="848af-166">Correction d’un bogue dans le cache de session hello où le jeton de session peut-être être défini de façon incorrecte.</span><span class="sxs-lookup"><span data-stu-id="848af-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="848af-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="848af-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="848af-168">Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="848af-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="848af-169">Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="848af-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="848af-170">Ajout de la prise en charge de la cohérence forte.</span><span class="sxs-lookup"><span data-stu-id="848af-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="848af-171">Ajout de la prise en charge des requêtes en fonction du nom lors de l’utilisation de la connectivité directe.</span><span class="sxs-lookup"><span data-stu-id="848af-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="848af-172">Toomake fixe ActivityId maintenir une cohérence entre toutes les nouvelles tentatives de requête.</span><span class="sxs-lookup"><span data-stu-id="848af-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="848af-173">Correction d’un bogue lié cache de session toohello lors de la recréation d’une collection de hello même nom.</span><span class="sxs-lookup"><span data-stu-id="848af-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="848af-174">Ajout des types de données Polygone et LineString lors de la spécification de la stratégie d’indexation de collection pour les requêtes spatiales à délimitation géographique.</span><span class="sxs-lookup"><span data-stu-id="848af-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="848af-175">Résolution des problèmes liés à Java Doc pour Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="848af-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="848af-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="848af-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="848af-177">Correction d’un bogue dans PartitionKeyDefinitionMap toocache les collections de partitions uniques afin de pas supplémentaire fetch partition principales demandes.</span><span class="sxs-lookup"><span data-stu-id="848af-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="848af-178">Correction d’une nouvelle tentative de bogue toonot lorsqu’une valeur de clé de partition incorrecte est fournie.</span><span class="sxs-lookup"><span data-stu-id="848af-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="848af-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="848af-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="848af-180">Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="848af-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="848af-181">Prise en charge pour la nouvelle tentative automatique sur les demandes limitées par hello de toocustomize options max nouvelles tentatives et recommencez max de délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="848af-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="848af-182">Voir RetryOptions et ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="848af-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="848af-183">Propriété IPartitionResolver déconseillée basée sur un code de partitionnement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="848af-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="848af-184">Utilisez des collections partitionnées pour bénéficier d’un niveau de stockage et de débit supérieur.</span><span class="sxs-lookup"><span data-stu-id="848af-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="848af-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="848af-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="848af-186">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour la limitation.</span><span class="sxs-lookup"><span data-stu-id="848af-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="848af-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="848af-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="848af-188">Durée toolive (TTL) prise en charge pour les documents.</span><span class="sxs-lookup"><span data-stu-id="848af-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="848af-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="848af-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="848af-190">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="848af-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="848af-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="848af-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="848af-192">Correction d’un bogue dans les valeurs de hachage HashPartitionResolver toogenerate dans toobe little-endian cohérent avec les autres kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="848af-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="848af-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="848af-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="848af-194">Ajouter & age de hachage tooassist de programmes de résolution de partition avec des applications de partitionnement sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="848af-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="848af-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="848af-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="848af-196">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="848af-196">Implement Upsert.</span></span> <span data-ttu-id="848af-197">Nouvelles méthodes upsertXXX a ajouté une fonctionnalité de Upsert toosupport.</span><span class="sxs-lookup"><span data-stu-id="848af-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="848af-198">Implémenter l'ID en fonction du routage.</span><span class="sxs-lookup"><span data-stu-id="848af-198">Implement ID Based Routing.</span></span> <span data-ttu-id="848af-199">Aucune modification d'API publique, toutes les modifications en interne.</span><span class="sxs-lookup"><span data-stu-id="848af-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="848af-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="848af-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="848af-201">Version a ignoré le numéro de version toobring d’alignement avec les autres kits de développement logiciel</span><span class="sxs-lookup"><span data-stu-id="848af-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="848af-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="848af-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="848af-203">Prise en charge de l'index géospatial</span><span class="sxs-lookup"><span data-stu-id="848af-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="848af-204">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="848af-204">Validates id property for all resources.</span></span> <span data-ttu-id="848af-205">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="848af-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="848af-206">Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.</span><span class="sxs-lookup"><span data-stu-id="848af-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="848af-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="848af-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="848af-208">Implémente la stratégie d'indexation V2</span><span class="sxs-lookup"><span data-stu-id="848af-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="848af-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="848af-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="848af-210">Kit SDK GA</span><span class="sxs-lookup"><span data-stu-id="848af-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="848af-211">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="848af-211">Release & Retirement Dates</span></span>
<span data-ttu-id="848af-212">Microsoft enverra une notification au moins **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.</span><span class="sxs-lookup"><span data-stu-id="848af-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="848af-213">Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel kit de développement logiciel, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.</span><span class="sxs-lookup"><span data-stu-id="848af-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="848af-214">N’importe quel tooCosmos demande à l’aide d’un kit de développement logiciel mis hors service de base de données seront rejetées par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="848af-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="848af-215">Toutes les versions de hello DocumentDB SDK pour tooversion préalable de Java **1.0.0** sera retiré le **29 février 2016**.</span><span class="sxs-lookup"><span data-stu-id="848af-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="848af-216">Version</span><span class="sxs-lookup"><span data-stu-id="848af-216">Version</span></span> | <span data-ttu-id="848af-217">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="848af-217">Release Date</span></span> | <span data-ttu-id="848af-218">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="848af-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="848af-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="848af-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="848af-220">11 juillet 2017</span><span class="sxs-lookup"><span data-stu-id="848af-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="848af-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="848af-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="848af-222">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="848af-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="848af-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="848af-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="848af-224">11 mars 2017</span><span class="sxs-lookup"><span data-stu-id="848af-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="848af-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="848af-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="848af-226">21 février 2017</span><span class="sxs-lookup"><span data-stu-id="848af-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="848af-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="848af-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="848af-228">31 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="848af-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="848af-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="848af-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="848af-230">24 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="848af-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="848af-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="848af-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="848af-232">30 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="848af-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="848af-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="848af-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="848af-234">28 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="848af-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="848af-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="848af-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="848af-236">26 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="848af-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="848af-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="848af-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="848af-238">3 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="848af-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="848af-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="848af-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="848af-240">30 juin 2016</span><span class="sxs-lookup"><span data-stu-id="848af-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="848af-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="848af-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="848af-242">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="848af-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="848af-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="848af-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="848af-244">30 avril 2016</span><span class="sxs-lookup"><span data-stu-id="848af-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="848af-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="848af-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="848af-246">27 avril 2016</span><span class="sxs-lookup"><span data-stu-id="848af-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="848af-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="848af-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="848af-248">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="848af-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="848af-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="848af-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="848af-250">31 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="848af-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="848af-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="848af-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="848af-252">4 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="848af-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="848af-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="848af-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="848af-254">5 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="848af-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="848af-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="848af-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="848af-256">5 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="848af-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="848af-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="848af-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="848af-258">5 août 2015</span><span class="sxs-lookup"><span data-stu-id="848af-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="848af-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="848af-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="848af-260">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="848af-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="848af-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="848af-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="848af-262">12 mai 2015</span><span class="sxs-lookup"><span data-stu-id="848af-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="848af-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="848af-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="848af-264">7 avril 2015</span><span class="sxs-lookup"><span data-stu-id="848af-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="848af-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-265">0.9.5-prelease</span></span> |<span data-ttu-id="848af-266">9 mars 2015</span><span class="sxs-lookup"><span data-stu-id="848af-266">Mar 09, 2015</span></span> |<span data-ttu-id="848af-267">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-267">February 29, 2016</span></span> |
| <span data-ttu-id="848af-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-268">0.9.4-prelease</span></span> |<span data-ttu-id="848af-269">17 février 2015</span><span class="sxs-lookup"><span data-stu-id="848af-269">February 17, 2015</span></span> |<span data-ttu-id="848af-270">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-270">February 29, 2016</span></span> |
| <span data-ttu-id="848af-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-271">0.9.3-prelease</span></span> |<span data-ttu-id="848af-272">13 janvier 2015</span><span class="sxs-lookup"><span data-stu-id="848af-272">January 13, 2015</span></span> |<span data-ttu-id="848af-273">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-273">February 29, 2016</span></span> |
| <span data-ttu-id="848af-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-274">0.9.2-prelease</span></span> |<span data-ttu-id="848af-275">19 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="848af-275">December 19, 2014</span></span> |<span data-ttu-id="848af-276">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-276">February 29, 2016</span></span> |
| <span data-ttu-id="848af-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-277">0.9.1-prelease</span></span> |<span data-ttu-id="848af-278">19 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="848af-278">December 19, 2014</span></span> |<span data-ttu-id="848af-279">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-279">February 29, 2016</span></span> |
| <span data-ttu-id="848af-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="848af-280">0.9.0-prelease</span></span> |<span data-ttu-id="848af-281">10 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="848af-281">December 10, 2014</span></span> |<span data-ttu-id="848af-282">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="848af-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="848af-283">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="848af-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="848af-284">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="848af-284">See Also</span></span>
<span data-ttu-id="848af-285">toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.</span><span class="sxs-lookup"><span data-stu-id="848af-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

