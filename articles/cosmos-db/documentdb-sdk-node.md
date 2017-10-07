---
title: "aaaAzure Cosmos DB Node.js API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello Node.js API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello Azure Cosmos DB Node.js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="96245-103">Kit de développement logiciel (SDK) Azure Cosmos DB Node.js : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="96245-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96245-104">.NET</span><span class="sxs-lookup"><span data-stu-id="96245-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="96245-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="96245-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="96245-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="96245-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="96245-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="96245-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="96245-108">Java</span><span class="sxs-lookup"><span data-stu-id="96245-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="96245-109">Python</span><span class="sxs-lookup"><span data-stu-id="96245-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="96245-110">REST</span><span class="sxs-lookup"><span data-stu-id="96245-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="96245-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="96245-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="96245-112">SQL</span><span class="sxs-lookup"><span data-stu-id="96245-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="96245-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="96245-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="96245-114">NPM</span><span class="sxs-lookup"><span data-stu-id="96245-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="96245-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="96245-115">**API documentation**</span></span></td><td>[<span data-ttu-id="96245-116">Documentation de référence de l’API Node.js</span><span class="sxs-lookup"><span data-stu-id="96245-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="96245-117">**Instructions d’installation du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="96245-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="96245-118">Instructions d’installation</span><span class="sxs-lookup"><span data-stu-id="96245-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="96245-119">**Contribuent tooSDK**</span><span class="sxs-lookup"><span data-stu-id="96245-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="96245-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="96245-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="96245-121">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="96245-121">**Samples**</span></span></td><td>[<span data-ttu-id="96245-122">Exemples de code Node.js</span><span class="sxs-lookup"><span data-stu-id="96245-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="96245-123">**Didacticiel de prise en main**</span><span class="sxs-lookup"><span data-stu-id="96245-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="96245-124">Prise en main hello Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="96245-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="96245-125">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="96245-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="96245-126">Générer une application web Node.js à l’aide d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="96245-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="96245-127">**Plateforme actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="96245-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="96245-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="96245-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="96245-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="96245-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="96245-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="96245-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="96245-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="96245-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="96245-132">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="96245-132">Release notes</span></span>

### <span data-ttu-id="96245-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="96245-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="96245-134">Documentation npm mise à jour.</span><span class="sxs-lookup"><span data-stu-id="96245-134">npm documentation fixed.</span></span>

### <span data-ttu-id="96245-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="96245-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="96245-136">Correction d’un bogue dans executeStoredProcedure où les documents impliqués disposaient de caractères Unicode spéciaux (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="96245-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="96245-137">Correction d’un bogue dans la gestion des documents avec des caractères Unicode dans la clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="96245-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="96245-138">Prise en charge fixe pour la création de regroupements avec un support nom hello.</span><span class="sxs-lookup"><span data-stu-id="96245-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="96245-139">Problème GitHub n° 114.</span><span class="sxs-lookup"><span data-stu-id="96245-139">Github issue #114.</span></span>
* <span data-ttu-id="96245-140">Prise en charge rétablie du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="96245-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="96245-141">Problème GitHub n° 178.</span><span class="sxs-lookup"><span data-stu-id="96245-141">Github issue #178.</span></span>

### <span data-ttu-id="96245-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="96245-143">Ajout de la prise en charge d’un nouveau [niveau de cohérence](consistency-levels.md) nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="96245-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="96245-144">Ajout de la prise en charge de UriFactory.</span><span class="sxs-lookup"><span data-stu-id="96245-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="96245-145">Correction d’un bogue de prise en charge des caractères Unicode.</span><span class="sxs-lookup"><span data-stu-id="96245-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="96245-146">Problème GitHub n° 171.</span><span class="sxs-lookup"><span data-stu-id="96245-146">GitHub issue #171.</span></span>

### <span data-ttu-id="96245-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="96245-148">Prise en charge de hello ajouté pour les requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="96245-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="96245-149">Option hello ajoutée pour contrôler le degré de parallélisme pour entre les requêtes de partition.</span><span class="sxs-lookup"><span data-stu-id="96245-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="96245-150">Option hello ajouté pour désactiver la vérification SSL lors de l’exécution par rapport à l’émulateur de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="96245-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="96245-151">Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.</span><span class="sxs-lookup"><span data-stu-id="96245-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="96245-152">Bogue de jeton continuation hello fixe pour une collection de partition unique.</span><span class="sxs-lookup"><span data-stu-id="96245-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="96245-153">Problème GitHub n° 107.</span><span class="sxs-lookup"><span data-stu-id="96245-153">Github issue #107.</span></span>
* <span data-ttu-id="96245-154">Bogue d’executeStoredProcedure hello fixe de gestion de 0 en tant que param unique.</span><span class="sxs-lookup"><span data-stu-id="96245-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="96245-155">Problème GitHub n° 155.</span><span class="sxs-lookup"><span data-stu-id="96245-155">Github issue #155.</span></span>

### <span data-ttu-id="96245-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="96245-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="96245-157">Agent utilisateur fixe en-tête tooinclude hello SDK version.</span><span class="sxs-lookup"><span data-stu-id="96245-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="96245-158">Nettoyage de code mineur.</span><span class="sxs-lookup"><span data-stu-id="96245-158">Minor code cleanup.</span></span>

### <span data-ttu-id="96245-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="96245-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="96245-160">La désactivation de vérification SSL lors de l’utilisation de hello SDK tootarget hello emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="96245-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="96245-161">Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="96245-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="96245-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="96245-163">Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="96245-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="96245-164">Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="96245-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="96245-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="96245-166">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées.</span><span class="sxs-lookup"><span data-stu-id="96245-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="96245-167">(Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, base de données Azure Cosmos tentatives de neuf pour chaque demande lorsque le code d’erreur 429 est rencontrée, en respectant le temps de retryAfter hello dans l’en-tête de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="96245-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="96245-168">Un intervalle fixe peut désormais être défini en tant que partie de hello RetryOptions propriété sur l’objet de ConnectionPolicy hello si vous souhaitez que tooignore hello retryAfter retourné par serveur entre les tentatives de hello.</span><span class="sxs-lookup"><span data-stu-id="96245-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="96245-169">Base de données Azure Cosmos attend maintenant un maximum de 30 secondes pour chaque demande qui est limitée (quel que soit le nombre de tentatives) et retourne la réponse hello avec le code d’erreur 429.</span><span class="sxs-lookup"><span data-stu-id="96245-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="96245-170">Cette durée peut également être substituée dans hello propriété RetryOptions sur ConnectionPolicy objet.</span><span class="sxs-lookup"><span data-stu-id="96245-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="96245-171">COSMOS DB retourne x-ms-limitation de bande passante--nombre de tentatives et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse hello dans chaque limitation hello toodenote des demandes délai entre deux tentatives nombre et hello cumulative hello demander d’attente entre les tentatives de hello.</span><span class="sxs-lookup"><span data-stu-id="96245-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="96245-172">Hello RetryOptions classe a été ajouté, exposant hello RetryOptions propriété sur une classe ConnectionPolicy hello qui peut être utilisé toooverride certains de valeur par défaut hello options de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="96245-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="96245-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="96245-174">Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="96245-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="96245-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="96245-176">Hello ajouté prend en charge pour la fonctionnalité tooLive(TTL) de temps pour les documents.</span><span class="sxs-lookup"><span data-stu-id="96245-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="96245-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="96245-178">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="96245-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="96245-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="96245-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="96245-180">Bogue RangePartitionResolver.resolveForRead où il a été ne retourne pas des liens en raison de concat incorrecte de tooa des résultats.</span><span class="sxs-lookup"><span data-stu-id="96245-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="96245-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="96245-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="96245-182">Résout hashParitionResolver resolveForRead() : levait une exception si aucune clé de partition n’était fournie, au lieu de renvoyer une liste de tous les liens enregistrés.</span><span class="sxs-lookup"><span data-stu-id="96245-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="96245-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="96245-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="96245-184">Résout le problème [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -dédié de l’Agent HTTPS : la modification de l’agent global de hello pour des raisons de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="96245-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="96245-185">Utiliser un agent dédié pour toutes les demandes de lib hello.</span><span class="sxs-lookup"><span data-stu-id="96245-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="96245-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="96245-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="96245-187">Résolution du problème [n° 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestion correcte des tirets dans les ID de média.</span><span class="sxs-lookup"><span data-stu-id="96245-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="96245-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="96245-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="96245-189">Résolution du problème [n° 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avertissement de fuite de l’écouteur EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="96245-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="96245-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="96245-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="96245-191">Résout le problème [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -renommer toohash de hachage de dossier pour les systèmes qui respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="96245-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="96245-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="96245-193">Implémentation de la prise en charge du partitionnement via l’ajout de programmes de résolution de partitions de hachage et de plage.</span><span class="sxs-lookup"><span data-stu-id="96245-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="96245-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="96245-195">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="96245-195">Implement Upsert.</span></span> <span data-ttu-id="96245-196">Nouvelles méthodes upsertXXX sur documentClient.</span><span class="sxs-lookup"><span data-stu-id="96245-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="96245-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="96245-198">Numéros de version ignorée toobring en alignement avec les autres kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="96245-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="96245-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="96245-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="96245-200">Fractionnement Q promet référentiel toonew de wrapper.</span><span class="sxs-lookup"><span data-stu-id="96245-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="96245-201">Fichier toopackage de mise à jour pour le Registre npm.</span><span class="sxs-lookup"><span data-stu-id="96245-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="96245-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="96245-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="96245-203">Implémentation du routage basé sur l’ID.</span><span class="sxs-lookup"><span data-stu-id="96245-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="96245-204">Résolution du problème [n° 49](https://github.com/Azure/azure-documentdb-node/issues/49) - propriété actuelle en conflit avec la méthode current().</span><span class="sxs-lookup"><span data-stu-id="96245-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="96245-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="96245-206">Ajout de la prise en charge de l’index géospatial.</span><span class="sxs-lookup"><span data-stu-id="96245-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="96245-207">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="96245-207">Validates id property for all resources.</span></span> <span data-ttu-id="96245-208">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, &#47;&#47; ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="96245-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="96245-209">Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.</span><span class="sxs-lookup"><span data-stu-id="96245-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="96245-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="96245-211">Implémente la stratégie d’indexation V2.</span><span class="sxs-lookup"><span data-stu-id="96245-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="96245-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="96245-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="96245-213">Problème [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - implémentée eslint des grunt des configurations de base de hello et assurons le Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="96245-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="96245-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="96245-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="96245-215">Problème [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Le wrapper de promesses n’inclut pas d’en-tête avec erreur.</span><span class="sxs-lookup"><span data-stu-id="96245-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="96245-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="96245-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="96245-217">Implémenté tooquery possibilité de conflits en ajoutant readConflicts, readConflictAsync et queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="96245-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="96245-218">Mise à jour de la documentation de l’API.</span><span class="sxs-lookup"><span data-stu-id="96245-218">Updated API documentation.</span></span>
* <span data-ttu-id="96245-219">Problème [n° 41](https://github.com/Azure/azure-documentdb-node/issues/41) : Erreur client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="96245-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="96245-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="96245-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="96245-221">Kit de développement logiciel (SDK) GA</span><span class="sxs-lookup"><span data-stu-id="96245-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="96245-222">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="96245-222">Release & Retirement Dates</span></span>
<span data-ttu-id="96245-223">Microsoft fournit au moins une notification **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.</span><span class="sxs-lookup"><span data-stu-id="96245-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="96245-224">Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel SDK, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.</span><span class="sxs-lookup"><span data-stu-id="96245-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="96245-225">Toute demande tooCosmos DB à l’aide d’un kit de développement logiciel mis hors service est rejetée par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="96245-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="96245-226">Version</span><span class="sxs-lookup"><span data-stu-id="96245-226">Version</span></span> | <span data-ttu-id="96245-227">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="96245-227">Release Date</span></span> | <span data-ttu-id="96245-228">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="96245-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="96245-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="96245-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="96245-230">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="96245-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="96245-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="96245-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="96245-232">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="96245-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="96245-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="96245-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="96245-234">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="96245-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="96245-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="96245-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="96245-236">16 mars 2017</span><span class="sxs-lookup"><span data-stu-id="96245-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="96245-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="96245-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="96245-238">27 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="96245-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="96245-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="96245-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="96245-240">22 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="96245-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="96245-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="96245-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="96245-242">3 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="96245-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="96245-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="96245-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="96245-244">7 juillet 2016</span><span class="sxs-lookup"><span data-stu-id="96245-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="96245-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="96245-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="96245-246">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="96245-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="96245-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="96245-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="96245-248">26 avril 2016</span><span class="sxs-lookup"><span data-stu-id="96245-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="96245-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="96245-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="96245-250">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="96245-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="96245-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="96245-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="96245-252">8 mars 2016</span><span class="sxs-lookup"><span data-stu-id="96245-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="96245-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="96245-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="96245-254">2 février 2016</span><span class="sxs-lookup"><span data-stu-id="96245-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="96245-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="96245-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="96245-256">1er février 2016</span><span class="sxs-lookup"><span data-stu-id="96245-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="96245-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="96245-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="96245-258">26 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="96245-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="96245-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="96245-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="96245-260">22 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="96245-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="96245-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="96245-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="96245-262">4 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="96245-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="96245-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="96245-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="96245-264">31 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="96245-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="96245-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="96245-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="96245-266">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="96245-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="96245-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="96245-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="96245-268">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="96245-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="96245-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="96245-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="96245-270">10 septembre 2015</span><span class="sxs-lookup"><span data-stu-id="96245-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="96245-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="96245-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="96245-272">15 août 2015</span><span class="sxs-lookup"><span data-stu-id="96245-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="96245-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="96245-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="96245-274">5 août 2015</span><span class="sxs-lookup"><span data-stu-id="96245-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="96245-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="96245-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="96245-276">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="96245-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="96245-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="96245-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="96245-278">4 juin 2015</span><span class="sxs-lookup"><span data-stu-id="96245-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="96245-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="96245-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="96245-280">23 mai 2015</span><span class="sxs-lookup"><span data-stu-id="96245-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="96245-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="96245-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="96245-282">15 mai 2015</span><span class="sxs-lookup"><span data-stu-id="96245-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="96245-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="96245-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="96245-284">8 avril 2015</span><span class="sxs-lookup"><span data-stu-id="96245-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="96245-285">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="96245-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="96245-286">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96245-286">See also</span></span>
<span data-ttu-id="96245-287">toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.</span><span class="sxs-lookup"><span data-stu-id="96245-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

