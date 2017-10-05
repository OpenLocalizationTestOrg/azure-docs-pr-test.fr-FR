---
title: "API Azure Cosmos DB Node.js, kit de développement logiciel (SDK) et Ressources | Microsoft Docs"
description: "Tout savoir sur l’API Node.js et le kit de développement logiciel (SDK), y compris les dates de sortie, les dates de déclassement et les modifications effectuées entre chaque version du kit de développement logiciel (SDK) Azure Cosmos DB Node.js."
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="1b11f-103">Kit de développement logiciel (SDK) Azure Cosmos DB Node.js : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="1b11f-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b11f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1b11f-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="1b11f-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="1b11f-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="1b11f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1b11f-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="1b11f-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1b11f-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="1b11f-108">Java</span><span class="sxs-lookup"><span data-stu-id="1b11f-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="1b11f-109">Python</span><span class="sxs-lookup"><span data-stu-id="1b11f-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="1b11f-110">REST</span><span class="sxs-lookup"><span data-stu-id="1b11f-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="1b11f-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="1b11f-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="1b11f-112">SQL</span><span class="sxs-lookup"><span data-stu-id="1b11f-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="1b11f-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="1b11f-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="1b11f-114">NPM</span><span class="sxs-lookup"><span data-stu-id="1b11f-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="1b11f-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="1b11f-115">**API documentation**</span></span></td><td>[<span data-ttu-id="1b11f-116">Documentation de référence de l’API Node.js</span><span class="sxs-lookup"><span data-stu-id="1b11f-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="1b11f-117">**Instructions d’installation du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="1b11f-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="1b11f-118">Instructions d’installation</span><span class="sxs-lookup"><span data-stu-id="1b11f-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="1b11f-119">**Contribution au Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="1b11f-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="1b11f-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="1b11f-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="1b11f-121">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="1b11f-121">**Samples**</span></span></td><td>[<span data-ttu-id="1b11f-122">Exemples de code Node.js</span><span class="sxs-lookup"><span data-stu-id="1b11f-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="1b11f-123">**Didacticiel de prise en main**</span><span class="sxs-lookup"><span data-stu-id="1b11f-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="1b11f-124">Prise en main du Kit de développement logiciel (SDK) Node.js</span><span class="sxs-lookup"><span data-stu-id="1b11f-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="1b11f-125">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="1b11f-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="1b11f-126">Générer une application web Node.js à l’aide d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1b11f-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="1b11f-127">**Plateforme actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="1b11f-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="1b11f-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="1b11f-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="1b11f-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="1b11f-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="1b11f-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="1b11f-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="1b11f-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="1b11f-132">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="1b11f-132">Release notes</span></span>

### <span data-ttu-id="1b11f-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="1b11f-134">Documentation npm mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1b11f-134">npm documentation fixed.</span></span>

### <span data-ttu-id="1b11f-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="1b11f-136">Correction d’un bogue dans executeStoredProcedure où les documents impliqués disposaient de caractères Unicode spéciaux (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="1b11f-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="1b11f-137">Correction d’un bogue lors de la gestion de documents contenant des caractères Unicode dans la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="1b11f-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="1b11f-138">Prise en charge rétablie de la création de collections avec le support de nom.</span><span class="sxs-lookup"><span data-stu-id="1b11f-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="1b11f-139">Problème GitHub n° 114.</span><span class="sxs-lookup"><span data-stu-id="1b11f-139">Github issue #114.</span></span>
* <span data-ttu-id="1b11f-140">Prise en charge rétablie du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="1b11f-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="1b11f-141">Problème GitHub n° 178.</span><span class="sxs-lookup"><span data-stu-id="1b11f-141">Github issue #178.</span></span>

### <span data-ttu-id="1b11f-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="1b11f-143">Ajout de la prise en charge d’un nouveau [niveau de cohérence](consistency-levels.md) nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="1b11f-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="1b11f-144">Ajout de la prise en charge de UriFactory.</span><span class="sxs-lookup"><span data-stu-id="1b11f-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="1b11f-145">Correction d’un bogue de prise en charge des caractères Unicode.</span><span class="sxs-lookup"><span data-stu-id="1b11f-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="1b11f-146">Problème GitHub n° 171.</span><span class="sxs-lookup"><span data-stu-id="1b11f-146">GitHub issue #171.</span></span>

### <span data-ttu-id="1b11f-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="1b11f-148">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="1b11f-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="1b11f-149">Ajout de l’option permettant de contrôler le degré de parallélisme des requêtes entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="1b11f-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="1b11f-150">Ajout de l’option permettant de désactiver la vérification SSL en cas d’exécution sur l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b11f-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="1b11f-151">Débit minimal réduit sur les collections partitionnées de 10 100 unités de demande/s à 2 500 unités de demande/s.</span><span class="sxs-lookup"><span data-stu-id="1b11f-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="1b11f-152">Correction du bogue de jeton de continuation pour la collection à partition unique.</span><span class="sxs-lookup"><span data-stu-id="1b11f-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="1b11f-153">Problème GitHub n° 107.</span><span class="sxs-lookup"><span data-stu-id="1b11f-153">Github issue #107.</span></span>
* <span data-ttu-id="1b11f-154">Correction du bogue executeStoredProcedure lors de la gestion du 0 comme paramètre unique.</span><span class="sxs-lookup"><span data-stu-id="1b11f-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="1b11f-155">Problème GitHub n° 155.</span><span class="sxs-lookup"><span data-stu-id="1b11f-155">Github issue #155.</span></span>

### <span data-ttu-id="1b11f-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="1b11f-157">En-tête agent utilisateur fixe pour inclure la version du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="1b11f-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="1b11f-158">Nettoyage de code mineur.</span><span class="sxs-lookup"><span data-stu-id="1b11f-158">Minor code cleanup.</span></span>

### <span data-ttu-id="1b11f-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="1b11f-160">Désactiver la vérification SSL lors de l’utilisation du Kit de développement logiciel (SDK) pour cibler l’émulateur (hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="1b11f-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="1b11f-161">Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="1b11f-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="1b11f-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="1b11f-163">Ajout de la prise en charge des requêtes parallèles sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="1b11f-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="1b11f-164">Ajout de la prise en charge des requêtes TOP/ORDER BY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="1b11f-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="1b11f-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="1b11f-166">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées.</span><span class="sxs-lookup"><span data-stu-id="1b11f-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="1b11f-167">(Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, Azure Cosmos DB accepte neuf nouvelles tentatives pour chaque requête lorsque le code d’erreur 429 est renvoyé, conformément à l’heure de retryAfter spécifiée dans l’en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="1b11f-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="1b11f-168">Il est désormais possible de définir un intervalle fixe de nouvelle tentative dans la propriété RetryOptions sur l’objet ConnectionPolicy, si vous souhaitez ignorer le temps retryAfter retourné par le serveur entre chaque nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="1b11f-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="1b11f-169">Azure Cosmos DB attend maintenant au maximum 30 secondes pour chaque requête limitée (quel que soit le nombre de nouvelles tentatives) et renvoie la réponse avec un code d’erreur 429.</span><span class="sxs-lookup"><span data-stu-id="1b11f-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="1b11f-170">Cette durée peut également être remplacée dans la propriété RetryOptions sur l’objet ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="1b11f-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="1b11f-171">Cosmos DB renvoie maintenant x-ms-throttle-retry-count et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse dans chaque requête pour signaler le nombre limite de nouvelles tentatives et le cumul de temps d’attente observé par la requête entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="1b11f-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="1b11f-172">La classe RetryOptions a été ajoutée pour exposer la propriété RetryOptions sur la classe ConnectionPolicy, qui peut être utilisée pour substituer certaines des options de nouvelle tentative par défaut.</span><span class="sxs-lookup"><span data-stu-id="1b11f-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="1b11f-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="1b11f-174">Ajout de la prise en charge des comptes de base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="1b11f-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="1b11f-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="1b11f-176">Ajout de la fonctionnalité de durée de vie (TTL) pour les documents.</span><span class="sxs-lookup"><span data-stu-id="1b11f-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="1b11f-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="1b11f-178">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="1b11f-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="1b11f-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="1b11f-180">Résolution du bogue RangePartitionResolver.resolveForRead là où les liens n’étaient pas renvoyés en raison d’une concaténation incorrecte des résultats.</span><span class="sxs-lookup"><span data-stu-id="1b11f-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="1b11f-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="1b11f-182">Résout hashParitionResolver resolveForRead() : levait une exception si aucune clé de partition n’était fournie, au lieu de renvoyer une liste de tous les liens enregistrés.</span><span class="sxs-lookup"><span data-stu-id="1b11f-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="1b11f-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="1b11f-184">Résolution du problème [n° 100](https://github.com/Azure/azure-documentdb-node/issues/100) : Agent HTTPS dédié : éviter de modifier l’agent global pour les besoins d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b11f-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="1b11f-185">Utilisez un agent dédié pour toutes les demandes de la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="1b11f-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="1b11f-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="1b11f-187">Résolution du problème [n° 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestion correcte des tirets dans les ID de média.</span><span class="sxs-lookup"><span data-stu-id="1b11f-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="1b11f-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="1b11f-189">Résolution du problème [n° 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avertissement de fuite de l’écouteur EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="1b11f-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="1b11f-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="1b11f-191">Résolution du problème [n° 92](https://github.com/Azure/azure-documentdb-node/issues/90) : dossier Hash renommé en hash pour les systèmes respectant la casse.</span><span class="sxs-lookup"><span data-stu-id="1b11f-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="1b11f-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="1b11f-193">Implémentation de la prise en charge du partitionnement via l’ajout de programmes de résolution de partitions de hachage et de plage.</span><span class="sxs-lookup"><span data-stu-id="1b11f-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="1b11f-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="1b11f-195">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="1b11f-195">Implement Upsert.</span></span> <span data-ttu-id="1b11f-196">Nouvelles méthodes upsertXXX sur documentClient.</span><span class="sxs-lookup"><span data-stu-id="1b11f-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="1b11f-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="1b11f-198">Ignorée pour aligner le numéro de version avec les autres Kits de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="1b11f-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="1b11f-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="1b11f-200">Fractionnement du wrapper des promesses Q dans un nouveau dépôt.</span><span class="sxs-lookup"><span data-stu-id="1b11f-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="1b11f-201">Mise à jour du fichier de package pour le Registre npm.</span><span class="sxs-lookup"><span data-stu-id="1b11f-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="1b11f-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="1b11f-203">Implémentation du routage basé sur l’ID.</span><span class="sxs-lookup"><span data-stu-id="1b11f-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="1b11f-204">Résolution du problème [n° 49](https://github.com/Azure/azure-documentdb-node/issues/49) - propriété actuelle en conflit avec la méthode current().</span><span class="sxs-lookup"><span data-stu-id="1b11f-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="1b11f-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="1b11f-206">Ajout de la prise en charge de l’index géospatial.</span><span class="sxs-lookup"><span data-stu-id="1b11f-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="1b11f-207">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="1b11f-207">Validates id property for all resources.</span></span> <span data-ttu-id="1b11f-208">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, &#47;&#47; ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="1b11f-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="1b11f-209">Ajout du nouvel en-tête « progression de la transformation de l’index » à ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="1b11f-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="1b11f-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="1b11f-211">Implémente la stratégie d’indexation V2.</span><span class="sxs-lookup"><span data-stu-id="1b11f-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="1b11f-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="1b11f-213">Problème [n° 40](https://github.com/Azure/azure-documentdb-node/issues/40) : implémentation des configurations eslint et grunt dans le Kit de développement logiciel (SDK) principal et de promesse.</span><span class="sxs-lookup"><span data-stu-id="1b11f-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="1b11f-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="1b11f-215">Problème [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Le wrapper de promesses n’inclut pas d’en-tête avec erreur.</span><span class="sxs-lookup"><span data-stu-id="1b11f-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="1b11f-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="1b11f-217">Implémentation de la possibilité de créer une requête pour les conflits en ajoutant readConflicts, readConflictAsync et queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="1b11f-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="1b11f-218">Mise à jour de la documentation de l’API.</span><span class="sxs-lookup"><span data-stu-id="1b11f-218">Updated API documentation.</span></span>
* <span data-ttu-id="1b11f-219">Problème [n° 41](https://github.com/Azure/azure-documentdb-node/issues/41) : Erreur client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="1b11f-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="1b11f-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="1b11f-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="1b11f-221">Kit de développement logiciel (SDK) GA</span><span class="sxs-lookup"><span data-stu-id="1b11f-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="1b11f-222">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="1b11f-222">Release & Retirement Dates</span></span>
<span data-ttu-id="1b11f-223">Microsoft envoie une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1b11f-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="1b11f-224">Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit SDK actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du SDK dès que possible.</span><span class="sxs-lookup"><span data-stu-id="1b11f-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="1b11f-225">Le service rejette toute requête envoyée à Cosmos DB à l’aide d’un Kit de développement logiciel (SDK) supprimé.</span><span class="sxs-lookup"><span data-stu-id="1b11f-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="1b11f-226">Version</span><span class="sxs-lookup"><span data-stu-id="1b11f-226">Version</span></span> | <span data-ttu-id="1b11f-227">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="1b11f-227">Release Date</span></span> | <span data-ttu-id="1b11f-228">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="1b11f-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="1b11f-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="1b11f-230">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="1b11f-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="1b11f-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="1b11f-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="1b11f-232">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="1b11f-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="1b11f-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="1b11f-234">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="1b11f-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="1b11f-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="1b11f-236">16 mars 2017</span><span class="sxs-lookup"><span data-stu-id="1b11f-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="1b11f-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="1b11f-238">27 janvier 2017</span><span class="sxs-lookup"><span data-stu-id="1b11f-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="1b11f-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="1b11f-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="1b11f-240">22 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="1b11f-242">3 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="1b11f-244">7 juillet 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="1b11f-246">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="1b11f-248">26 avril 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="1b11f-250">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="1b11f-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="1b11f-252">8 mars 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="1b11f-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="1b11f-254">2 février 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="1b11f-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="1b11f-256">1er février 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="1b11f-258">26 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="1b11f-260">22 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="1b11f-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="1b11f-262">4 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="1b11f-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="1b11f-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="1b11f-264">31 décembre 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="1b11f-266">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="1b11f-268">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="1b11f-270">10 septembre 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="1b11f-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="1b11f-272">15 août 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="1b11f-274">5 août 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="1b11f-276">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="1b11f-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="1b11f-278">4 juin 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="1b11f-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="1b11f-280">23 mai 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="1b11f-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="1b11f-282">15 mai 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="1b11f-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1b11f-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="1b11f-284">8 avril 2015</span><span class="sxs-lookup"><span data-stu-id="1b11f-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="1b11f-285">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1b11f-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="1b11f-286">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1b11f-286">See also</span></span>
<span data-ttu-id="1b11f-287">Pour en savoir plus sur Cosmos DB, consultez la page du service [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1b11f-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

