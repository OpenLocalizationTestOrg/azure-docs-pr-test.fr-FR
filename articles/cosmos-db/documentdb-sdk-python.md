---
title: API, SDK et ressources Python Azure Cosmos DB | Microsoft Docs
description: "Découvrez l’API et le Kit de développement logiciel (SDK) Python, y compris les dates de publication, les dates de suppression et les modifications apportées entre chaque version du Kit de développement logiciel (SDK) Python Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="86710-103">Kit de développement logiciel (SDK) Python Azure Cosmos DB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="86710-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86710-104">.NET</span><span class="sxs-lookup"><span data-stu-id="86710-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="86710-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="86710-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="86710-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="86710-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="86710-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="86710-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="86710-108">Java</span><span class="sxs-lookup"><span data-stu-id="86710-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="86710-109">Python</span><span class="sxs-lookup"><span data-stu-id="86710-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="86710-110">REST</span><span class="sxs-lookup"><span data-stu-id="86710-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="86710-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="86710-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="86710-112">SQL</span><span class="sxs-lookup"><span data-stu-id="86710-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="86710-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="86710-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="86710-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="86710-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="86710-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="86710-115">**API documentation**</span></span></td><td>[<span data-ttu-id="86710-116">Documentation de référence sur l’API Python</span><span class="sxs-lookup"><span data-stu-id="86710-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="86710-117">**Instructions d’installation du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="86710-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="86710-118">Instructions d’installation du Kit de développement logiciel (SDK) Python</span><span class="sxs-lookup"><span data-stu-id="86710-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="86710-119">**Contribution au Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="86710-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="86710-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="86710-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="86710-121">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="86710-121">**Get started**</span></span></td><td>[<span data-ttu-id="86710-122">Bien démarrer avec le Kit de développement logiciel (SDK) Python</span><span class="sxs-lookup"><span data-stu-id="86710-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="86710-123">**Plateforme actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="86710-123">**Current supported platform**</span></span></td><td><span data-ttu-id="86710-124">[Python 2.7](https://www.python.org/downloads/) et [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="86710-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="86710-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="86710-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="86710-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="86710-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="86710-127">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="86710-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="86710-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="86710-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="86710-129">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="86710-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="86710-130">Ajout d’une option permettant de désactiver la vérification SSL pendant son exécution sur l’émulateur Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86710-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="86710-131">Suppression de la restriction du module de demandes dépendantes qui devait correspondre exactement à la version 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="86710-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="86710-132">Débit minimal réduit sur les collections partitionnées de 10 100 unités de demande/s à 2 500 unités de demande/s.</span><span class="sxs-lookup"><span data-stu-id="86710-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="86710-133">Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="86710-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="86710-134">Version de l’API REST passée à « 2017-01-19 » à l’occasion de cette publication.</span><span class="sxs-lookup"><span data-stu-id="86710-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="86710-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="86710-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="86710-136">Modifications éditoriales apportées aux commentaires de documentation.</span><span class="sxs-lookup"><span data-stu-id="86710-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="86710-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="86710-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="86710-138">Ajout de la prise en charge de Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="86710-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="86710-139">Ajout de la prise en charge du regroupement de connexions à l’aide d’un module de demandes.</span><span class="sxs-lookup"><span data-stu-id="86710-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="86710-140">Ajout de la prise en charge de la cohérence de session.</span><span class="sxs-lookup"><span data-stu-id="86710-140">Added support for session consistency.</span></span>
* <span data-ttu-id="86710-141">Ajout de la prise en charge des requêtes TOP/ORDERBY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="86710-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="86710-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="86710-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="86710-143">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées.</span><span class="sxs-lookup"><span data-stu-id="86710-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="86710-144">(Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, Azure Cosmos DB accepte neuf nouvelles tentatives pour chaque requête lorsque le code d’erreur 429 est renvoyé, conformément à l’heure de retryAfter spécifiée dans l’en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="86710-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="86710-145">Il est désormais possible de définir un intervalle fixe de nouvelle tentative dans la propriété RetryOptions sur l’objet ConnectionPolicy, si vous souhaitez ignorer le temps retryAfter retourné par le serveur entre chaque nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="86710-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="86710-146">Azure Cosmos DB attend maintenant au maximum 30 secondes pour chaque requête limitée (quel que soit le nombre de nouvelles tentatives) et renvoie la réponse avec un code d’erreur 429.</span><span class="sxs-lookup"><span data-stu-id="86710-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="86710-147">Cette durée peut également être remplacée dans la propriété RetryOptions sur l’objet ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="86710-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="86710-148">Cosmos DB renvoie maintenant x-ms-throttle-retry-count et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse dans chaque requête pour signaler le nombre limite de nouvelles tentatives et le cumul de temps d’attente observé par la requête entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="86710-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="86710-149">Suppression de la classe RetryPolicy et de la propriété correspondante (retry_policy) exposées sur la classe document_client, et introduction d’une classe RetryOptions qui expose la propriété RetryOptions sur la classe ConnectionPolicy pouvant être utilisée pour substituer certaines des options de nouvelle tentative par défaut.</span><span class="sxs-lookup"><span data-stu-id="86710-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="86710-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="86710-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="86710-151">Ajout de la prise en charge des comptes de base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="86710-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="86710-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="86710-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="86710-153">Ajout de la fonctionnalité de durée de vie (TTL) pour les documents.</span><span class="sxs-lookup"><span data-stu-id="86710-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="86710-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="86710-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="86710-155">Résolution des bogues liés au partitionnement côté serveur pour autoriser des caractères spéciaux dans le chemin d’accès à la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="86710-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="86710-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="86710-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="86710-157">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="86710-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="86710-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="86710-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="86710-159">Ajoutez des programmes de résolution de partitions par hachage et par spécification de plages de valeurs pour vous aider lors du partitionnement des applications sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="86710-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="86710-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="86710-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="86710-161">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="86710-161">Implement Upsert.</span></span> <span data-ttu-id="86710-162">Nouvelles méthodes UpsertXXX ajoutées pour prendre en charge la fonctionnalité Upsert.</span><span class="sxs-lookup"><span data-stu-id="86710-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="86710-163">Implémenter l'ID en fonction du routage.</span><span class="sxs-lookup"><span data-stu-id="86710-163">Implement ID Based Routing.</span></span> <span data-ttu-id="86710-164">Aucune modification d'API publique, toutes les modifications en interne.</span><span class="sxs-lookup"><span data-stu-id="86710-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="86710-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="86710-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="86710-166">Prise en charge de l'index géospatial.</span><span class="sxs-lookup"><span data-stu-id="86710-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="86710-167">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="86710-167">Validates id property for all resources.</span></span> <span data-ttu-id="86710-168">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="86710-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="86710-169">Ajoute le nouvel en-tête « progression de la transformation de l'index » à ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="86710-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="86710-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="86710-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="86710-171">Implémente la stratégie d’indexation V2.</span><span class="sxs-lookup"><span data-stu-id="86710-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="86710-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="86710-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="86710-173">Prend en charge la connexion proxy.</span><span class="sxs-lookup"><span data-stu-id="86710-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="86710-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="86710-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="86710-175">Kit de développement logiciel (SDK) GA</span><span class="sxs-lookup"><span data-stu-id="86710-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="86710-176">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="86710-176">Release & retirement dates</span></span>
<span data-ttu-id="86710-177">Microsoft fournira une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.</span><span class="sxs-lookup"><span data-stu-id="86710-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="86710-178">Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit de développement logiciel (SDK) actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du Kit de développement logiciel (SDK) dès que possible.</span><span class="sxs-lookup"><span data-stu-id="86710-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="86710-179">Le service rejette toute requête envoyée à Cosmos DB à l’aide d’un Kit de développement logiciel (SDK) supprimé.</span><span class="sxs-lookup"><span data-stu-id="86710-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="86710-180">Toutes les versions du Kit de développement logiciel (SDK) Azure DocumentDB pour Python antérieures à la version **1.0.0** seront supprimées le **29 février 2016**.</span><span class="sxs-lookup"><span data-stu-id="86710-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="86710-181">Version</span><span class="sxs-lookup"><span data-stu-id="86710-181">Version</span></span> | <span data-ttu-id="86710-182">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="86710-182">Release Date</span></span> | <span data-ttu-id="86710-183">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="86710-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="86710-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="86710-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="86710-185">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="86710-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="86710-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="86710-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="86710-187">1er mai 2017</span><span class="sxs-lookup"><span data-stu-id="86710-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="86710-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="86710-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="86710-189">30 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="86710-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="86710-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="86710-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="86710-191">29 septembre 2016</span><span class="sxs-lookup"><span data-stu-id="86710-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="86710-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="86710-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="86710-193">7 juillet 2016</span><span class="sxs-lookup"><span data-stu-id="86710-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="86710-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="86710-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="86710-195">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="86710-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="86710-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="86710-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="86710-197">26 avril 2016</span><span class="sxs-lookup"><span data-stu-id="86710-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="86710-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="86710-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="86710-199">8 avril 2016</span><span class="sxs-lookup"><span data-stu-id="86710-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="86710-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="86710-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="86710-201">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="86710-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="86710-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="86710-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="86710-203">3 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="86710-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="86710-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="86710-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="86710-205">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="86710-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="86710-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="86710-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="86710-207">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="86710-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="86710-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="86710-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="86710-209">6 août 2015</span><span class="sxs-lookup"><span data-stu-id="86710-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="86710-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="86710-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="86710-211">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="86710-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="86710-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="86710-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="86710-213">25 mai 2015</span><span class="sxs-lookup"><span data-stu-id="86710-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="86710-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="86710-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="86710-215">7 avril 2015</span><span class="sxs-lookup"><span data-stu-id="86710-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="86710-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="86710-216">0.9.4-prelease</span></span> |<span data-ttu-id="86710-217">14 janvier 2015</span><span class="sxs-lookup"><span data-stu-id="86710-217">January 14, 2015</span></span> |<span data-ttu-id="86710-218">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="86710-218">February 29, 2016</span></span> |
| <span data-ttu-id="86710-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="86710-219">0.9.3-prelease</span></span> |<span data-ttu-id="86710-220">9 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="86710-220">December 09, 2014</span></span> |<span data-ttu-id="86710-221">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="86710-221">February 29, 2016</span></span> |
| <span data-ttu-id="86710-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="86710-222">0.9.2-prelease</span></span> |<span data-ttu-id="86710-223">25 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="86710-223">November 25, 2014</span></span> |<span data-ttu-id="86710-224">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="86710-224">February 29, 2016</span></span> |
| <span data-ttu-id="86710-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="86710-225">0.9.1-prelease</span></span> |<span data-ttu-id="86710-226">23 septembre 2014</span><span class="sxs-lookup"><span data-stu-id="86710-226">September 23, 2014</span></span> |<span data-ttu-id="86710-227">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="86710-227">February 29, 2016</span></span> |
| <span data-ttu-id="86710-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="86710-228">0.9.0-prelease</span></span> |<span data-ttu-id="86710-229">21.08.14</span><span class="sxs-lookup"><span data-stu-id="86710-229">August 21, 2014</span></span> |<span data-ttu-id="86710-230">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="86710-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="86710-231">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="86710-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="86710-232">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="86710-232">See also</span></span>
<span data-ttu-id="86710-233">Pour en savoir plus sur Cosmos DB, consultez la page du service [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="86710-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

