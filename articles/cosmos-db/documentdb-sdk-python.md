---
title: "aaaAzure Cosmos DB Python API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello Python API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version du Kit de développement logiciel Azure Cosmos DB Python de hello."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="75e93-103">Kit de développement logiciel (SDK) Python Azure Cosmos DB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="75e93-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75e93-104">.NET</span><span class="sxs-lookup"><span data-stu-id="75e93-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="75e93-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="75e93-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="75e93-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="75e93-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="75e93-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="75e93-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="75e93-108">Java</span><span class="sxs-lookup"><span data-stu-id="75e93-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="75e93-109">Python</span><span class="sxs-lookup"><span data-stu-id="75e93-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="75e93-110">REST</span><span class="sxs-lookup"><span data-stu-id="75e93-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="75e93-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="75e93-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="75e93-112">SQL</span><span class="sxs-lookup"><span data-stu-id="75e93-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="75e93-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="75e93-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="75e93-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="75e93-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="75e93-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="75e93-115">**API documentation**</span></span></td><td>[<span data-ttu-id="75e93-116">Documentation de référence sur l’API Python</span><span class="sxs-lookup"><span data-stu-id="75e93-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="75e93-117">**Instructions d’installation du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="75e93-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="75e93-118">Instructions d’installation du Kit de développement logiciel (SDK) Python</span><span class="sxs-lookup"><span data-stu-id="75e93-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="75e93-119">**Contribuent tooSDK**</span><span class="sxs-lookup"><span data-stu-id="75e93-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="75e93-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="75e93-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="75e93-121">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="75e93-121">**Get started**</span></span></td><td>[<span data-ttu-id="75e93-122">Prise en main hello Python SDK</span><span class="sxs-lookup"><span data-stu-id="75e93-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="75e93-123">**Plateforme actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="75e93-123">**Current supported platform**</span></span></td><td><span data-ttu-id="75e93-124">[Python 2.7](https://www.python.org/downloads/) et [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="75e93-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="75e93-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="75e93-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="75e93-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="75e93-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="75e93-127">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="75e93-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="75e93-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="75e93-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="75e93-129">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="75e93-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="75e93-130">Ajout d’une option permettant de désactiver la vérification SSL pendant son exécution sur l’émulateur Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="75e93-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="75e93-131">Supprimé la restriction hello de demandes dépendantes module toobe 2.10.0 exactement.</span><span class="sxs-lookup"><span data-stu-id="75e93-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="75e93-132">Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.</span><span class="sxs-lookup"><span data-stu-id="75e93-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="75e93-133">Ajout de la prise en charge de l’activation de la journalisation de script pendant l’exécution de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="75e93-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="75e93-134">Version de l’API REST pour agrandir trop ' 2017-01-19 » avec cette version.</span><span class="sxs-lookup"><span data-stu-id="75e93-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="75e93-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="75e93-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="75e93-136">Apportées les modifications rédactionnelles toodocumentation commentaires.</span><span class="sxs-lookup"><span data-stu-id="75e93-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="75e93-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="75e93-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="75e93-138">Ajout de la prise en charge de Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="75e93-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="75e93-139">Ajout de la prise en charge du regroupement de connexions à l’aide d’un module de demandes.</span><span class="sxs-lookup"><span data-stu-id="75e93-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="75e93-140">Ajout de la prise en charge de la cohérence de session.</span><span class="sxs-lookup"><span data-stu-id="75e93-140">Added support for session consistency.</span></span>
* <span data-ttu-id="75e93-141">Ajout de la prise en charge des requêtes TOP/ORDERBY pour les collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="75e93-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="75e93-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="75e93-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="75e93-143">Ajout de la prise en charge d’une stratégie de nouvelle tentative pour les requêtes limitées.</span><span class="sxs-lookup"><span data-stu-id="75e93-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="75e93-144">(Les requêtes limitées reçoivent une exception de taux de requête excessif, code d’erreur 429.) Par défaut, base de données Azure Cosmos tentatives de neuf pour chaque demande lorsque le code d’erreur 429 est rencontrée, en respectant le temps de retryAfter hello dans l’en-tête de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="75e93-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="75e93-145">Un intervalle fixe peut désormais être défini en tant que partie de hello RetryOptions propriété sur l’objet de ConnectionPolicy hello si vous souhaitez que tooignore hello retryAfter retourné par serveur entre les tentatives de hello.</span><span class="sxs-lookup"><span data-stu-id="75e93-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="75e93-146">Base de données Azure Cosmos attend maintenant un maximum de 30 secondes pour chaque demande qui est limitée (quel que soit le nombre de tentatives) et retourne la réponse hello avec le code d’erreur 429.</span><span class="sxs-lookup"><span data-stu-id="75e93-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="75e93-147">Cette durée peut également être remplacées Bonjour propriété RetryOptions sur ConnectionPolicy objet.</span><span class="sxs-lookup"><span data-stu-id="75e93-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="75e93-148">COSMOS DB retourne x-ms-limitation de bande passante--nombre de tentatives et x-ms-throttle-retry-wait-time-ms comme en-têtes de réponse hello dans chaque limitation hello toodenote des demandes délai entre deux tentatives nombre et hello cummulative hello demander d’attente entre les tentatives de hello.</span><span class="sxs-lookup"><span data-stu-id="75e93-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="75e93-149">Classe de RetryPolicy hello supprimé et la propriété correspondante, hello (retry_policy) exposées sur la classe de document_client hello et au lieu de cela introduit une classe RetryOptions exposition propriété RetryOptions hello classe ConnectionPolicy qui peut être utilisé toooverride options des par défaut de hello de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="75e93-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="75e93-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="75e93-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="75e93-151">Prise en charge de hello ajouté pour les comptes de la base de données de plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="75e93-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="75e93-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="75e93-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="75e93-153">Hello ajouté prend en charge pour la fonctionnalité tooLive(TTL) de temps pour les documents.</span><span class="sxs-lookup"><span data-stu-id="75e93-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="75e93-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="75e93-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="75e93-155">Correctifs de bogues liés côté tooserver partitionnement tooallow des caractères spéciaux dans le chemin d’accès de partitionkey.</span><span class="sxs-lookup"><span data-stu-id="75e93-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="75e93-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="75e93-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="75e93-157">Implémentation des [collections partitionnées](partition-data.md) et des [niveaux de performances définis par l’utilisateur](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="75e93-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="75e93-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="75e93-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="75e93-159">Ajouter & age de hachage tooassist de programmes de résolution de partition avec des applications de partitionnement sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="75e93-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="75e93-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="75e93-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="75e93-161">Implémentation de l’opération Upsert.</span><span class="sxs-lookup"><span data-stu-id="75e93-161">Implement Upsert.</span></span> <span data-ttu-id="75e93-162">Nouvelles méthodes UpsertXXX a ajouté une fonctionnalité de Upsert toosupport.</span><span class="sxs-lookup"><span data-stu-id="75e93-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="75e93-163">Implémenter l'ID en fonction du routage.</span><span class="sxs-lookup"><span data-stu-id="75e93-163">Implement ID Based Routing.</span></span> <span data-ttu-id="75e93-164">Aucune modification d'API publique, toutes les modifications en interne.</span><span class="sxs-lookup"><span data-stu-id="75e93-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="75e93-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="75e93-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="75e93-166">Prise en charge de l'index géospatial.</span><span class="sxs-lookup"><span data-stu-id="75e93-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="75e93-167">Validation de la propriété ID pour toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="75e93-167">Validates id property for all resources.</span></span> <span data-ttu-id="75e93-168">Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \, ou se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="75e93-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="75e93-169">Ajoute un nouveau tooResourceResponse de « cours de transformation d’index » en-tête.</span><span class="sxs-lookup"><span data-stu-id="75e93-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="75e93-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="75e93-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="75e93-171">Implémente la stratégie d’indexation V2.</span><span class="sxs-lookup"><span data-stu-id="75e93-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="75e93-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="75e93-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="75e93-173">Prend en charge la connexion proxy.</span><span class="sxs-lookup"><span data-stu-id="75e93-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="75e93-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="75e93-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="75e93-175">Kit de développement logiciel (SDK) GA</span><span class="sxs-lookup"><span data-stu-id="75e93-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="75e93-176">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="75e93-176">Release & retirement dates</span></span>
<span data-ttu-id="75e93-177">Microsoft enverra une notification au moins **12 mois** avant la mise hors service d’un kit de développement dans la version plus récente/prise en charge ordre toosmooth hello transition tooa.</span><span class="sxs-lookup"><span data-stu-id="75e93-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="75e93-178">Nouvelles fonctionnalités et les fonctionnalités et les optimisations sont ajoutées uniquement toohello actuel kit de développement logiciel, par conséquent il est recommandé que vous toohello mise à niveau toujours la dernière SDK version dès que possible.</span><span class="sxs-lookup"><span data-stu-id="75e93-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="75e93-179">N’importe quel tooCosmos demande à l’aide d’un kit de développement logiciel mis hors service de base de données seront rejetées par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="75e93-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="75e93-180">Toutes les versions de hello Kit de développement logiciel Azure DocumentDB pour tooversion préalable de Python **1.0.0** sera retiré le **29 février 2016**.</span><span class="sxs-lookup"><span data-stu-id="75e93-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="75e93-181">Version</span><span class="sxs-lookup"><span data-stu-id="75e93-181">Version</span></span> | <span data-ttu-id="75e93-182">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="75e93-182">Release Date</span></span> | <span data-ttu-id="75e93-183">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="75e93-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="75e93-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="75e93-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="75e93-185">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="75e93-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="75e93-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="75e93-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="75e93-187">1er mai 2017</span><span class="sxs-lookup"><span data-stu-id="75e93-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="75e93-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="75e93-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="75e93-189">30 octobre 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="75e93-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="75e93-191">29 septembre 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="75e93-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="75e93-193">7 juillet 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="75e93-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="75e93-195">14 juin 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="75e93-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="75e93-197">26 avril 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="75e93-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="75e93-199">8 avril 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="75e93-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="75e93-201">29 mars 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="75e93-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="75e93-203">3 janvier 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="75e93-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="75e93-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="75e93-205">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="75e93-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="75e93-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="75e93-207">6 octobre 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="75e93-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="75e93-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="75e93-209">6 août 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="75e93-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="75e93-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="75e93-211">9 juillet 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="75e93-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="75e93-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="75e93-213">25 mai 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="75e93-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="75e93-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="75e93-215">7 avril 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="75e93-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="75e93-216">0.9.4-prelease</span></span> |<span data-ttu-id="75e93-217">14 janvier 2015</span><span class="sxs-lookup"><span data-stu-id="75e93-217">January 14, 2015</span></span> |<span data-ttu-id="75e93-218">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-218">February 29, 2016</span></span> |
| <span data-ttu-id="75e93-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="75e93-219">0.9.3-prelease</span></span> |<span data-ttu-id="75e93-220">9 décembre 2014</span><span class="sxs-lookup"><span data-stu-id="75e93-220">December 09, 2014</span></span> |<span data-ttu-id="75e93-221">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-221">February 29, 2016</span></span> |
| <span data-ttu-id="75e93-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="75e93-222">0.9.2-prelease</span></span> |<span data-ttu-id="75e93-223">25 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="75e93-223">November 25, 2014</span></span> |<span data-ttu-id="75e93-224">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-224">February 29, 2016</span></span> |
| <span data-ttu-id="75e93-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="75e93-225">0.9.1-prelease</span></span> |<span data-ttu-id="75e93-226">23 septembre 2014</span><span class="sxs-lookup"><span data-stu-id="75e93-226">September 23, 2014</span></span> |<span data-ttu-id="75e93-227">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-227">February 29, 2016</span></span> |
| <span data-ttu-id="75e93-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="75e93-228">0.9.0-prelease</span></span> |<span data-ttu-id="75e93-229">21.08.14</span><span class="sxs-lookup"><span data-stu-id="75e93-229">August 21, 2014</span></span> |<span data-ttu-id="75e93-230">29 février 2016</span><span class="sxs-lookup"><span data-stu-id="75e93-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="75e93-231">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="75e93-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="75e93-232">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="75e93-232">See also</span></span>
<span data-ttu-id="75e93-233">toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.</span><span class="sxs-lookup"><span data-stu-id="75e93-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

