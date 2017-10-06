---
title: "aaaAzure Cosmos DB .NET Core API, Kit de développement logiciel et les ressources | Documents Microsoft"
description: "Découvrez les hello .NET Core API et Kit de développement logiciel, y compris les dates de publication, les dates de retrait et les modifications apportées entre chaque version de hello Kit de développement logiciel Azure Cosmos DB .NET Core."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="5a6d7-103">Kit de développement logiciel (SDK) .NET Core Azure Cosmos DB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="5a6d7-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a6d7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5a6d7-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="5a6d7-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="5a6d7-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="5a6d7-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5a6d7-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="5a6d7-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5a6d7-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="5a6d7-108">Java</span><span class="sxs-lookup"><span data-stu-id="5a6d7-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="5a6d7-109">Python</span><span class="sxs-lookup"><span data-stu-id="5a6d7-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="5a6d7-110">REST</span><span class="sxs-lookup"><span data-stu-id="5a6d7-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="5a6d7-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="5a6d7-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="5a6d7-112">SQL</span><span class="sxs-lookup"><span data-stu-id="5a6d7-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="5a6d7-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-113">**SDK download**</span></span></td><td>[<span data-ttu-id="5a6d7-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="5a6d7-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="5a6d7-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-115">**API documentation**</span></span></td><td>[<span data-ttu-id="5a6d7-116">Documentation de référence sur l’API .NET</span><span class="sxs-lookup"><span data-stu-id="5a6d7-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="5a6d7-117">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-117">**Samples**</span></span></td><td>[<span data-ttu-id="5a6d7-118">Exemples de code .NET</span><span class="sxs-lookup"><span data-stu-id="5a6d7-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="5a6d7-119">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-119">**Get started**</span></span></td><td>[<span data-ttu-id="5a6d7-120">Prise en main hello Kit de développement logiciel Azure Cosmos DB .NET Core</span><span class="sxs-lookup"><span data-stu-id="5a6d7-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="5a6d7-121">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="5a6d7-122">Développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5a6d7-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="5a6d7-123">**Infrastructure actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="5a6d7-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="5a6d7-124">.NET Standard 1.6 et .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="5a6d7-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="5a6d7-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5a6d7-125">Release Notes</span></span>

<span data-ttu-id="5a6d7-126">Hello Kit de développement logiciel Azure Cosmos DB .NET Core a parité de fonctionnalités avec la version la plus récente de hello hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="5a6d7-127">Bonjour Azure Cosmos DB .NET Core SDK n’est pas encore compatible avec les applications de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="5a6d7-128">Si vous êtes intéressé par hello Kit de développement .NET Core qui ne prend pas en charge les applications UWP, envoyer un courrier électronique trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="5a6d7-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="5a6d7-130">Prise en charge supplémentaire pour PartitionKeyRangeId comme une FeedOption pour étendre la valeur de plage de clés de requête résultats tooa partition spécifique.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="5a6d7-131">Prise en charge supplémentaire pour StartTime comme un toostart ChangeFeedOption recherche de modifications de hello après cette heure.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="5a6d7-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="5a6d7-133">Correction d’un problème dans hello classe JsonSerializable qui peut provoquer une exception de dépassement de capacité de pile.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="5a6d7-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="5a6d7-135">Ajout de la prise en charge de la spécification des JsonSerializerSettings personnalisés lors de l’instanciation d’une instance [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="5a6d7-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="5a6d7-137">Prise en charge 1,5 Standard de .NET en tant qu’une des infrastructures de cible hello.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="5a6d7-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="5a6d7-139">Correction d’un problème concernant les ordinateurs x64 qui ne prennent pas en charge l’instruction SSE4 et génèrent une SEHException lors de l’exécution de requêtes Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="5a6d7-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="5a6d7-141">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="5a6d7-142">Prise en charge ajoutée pour les mesures de requête liées aux partitions individuelles.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="5a6d7-143">Prise en charge supplémentaire pour limiter la taille de hello hello du jeton de continuation pour les requêtes.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="5a6d7-144">Prise en charge ajoutée pour un suivi plus détaillé des demandes ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="5a6d7-145">Apporté des améliorations de performances dans le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="5a6d7-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="5a6d7-147">Correction d’un problème qui a ignoré la valeur de PartitionKey hello fournie dans FeedOptions pour les requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="5a6d7-148">Résolution du problème de gestion transparente des partitions pendant l’exécution d’une requête Order By (Trier par) entre partitions intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="5a6d7-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="5a6d7-150">Correction d’un problème qui a provoqué des blocages dans certains hello async API lorsqu’il est utilisé à l’intérieur du contexte ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="5a6d7-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="5a6d7-152">Résout toomake SDK plus basculement tooautomatic résilient sous certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="5a6d7-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="5a6d7-154">Corriger un problème qui provoque parfois une WebException : nom de hello distant n’a pas pu être résolu.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="5a6d7-155">Hello ajouté prend en charge pour la lecture directe d’un document typé en ajoutant la nouvelle API tooReadDocumentAsync de surcharges.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="5a6d7-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="5a6d7-157">Ajout de la prise en charge LINQ des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="5a6d7-158">Correctif pour un problème de fuite de mémoire pour l’objet de ConnectionPolicy hello dû à l’aide de hello de gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="5a6d7-159">Correction d’un problème de fonctionnement d’UpsertAttachmentAsync avec l’utilisation d’ETag.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="5a6d7-160">Correction d’un problème de fonctionnement de la liaison des requêtes ORDER BY entre les partitions lors d’un tri sur un champ de chaîne.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="5a6d7-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="5a6d7-162">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="5a6d7-163">Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="5a6d7-164">Réduisez le débit minimal sur les collections partitionnées de 10,100 ur/s too2500 ur/s.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="5a6d7-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="5a6d7-166">Hello Kit de développement logiciel Azure Cosmos DB .NET Core vous permet de toobuild rapide, inter-plateformes [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) toorun d’applications sur Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="5a6d7-167">Bonjour dernière version de hello Kit de développement logiciel Azure Cosmos DB .NET Core est entièrement [Xamarin](https://www.xamarin.com) compatible et être utilisés toobuild les applications qui ciblent iOS, Android et Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="5a6d7-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="5a6d7-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="5a6d7-169">Bonjour Azure Cosmos DB .NET Core aperçu SDK vous permet de toobuild rapide, inter-plateformes [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) toorun d’applications sur Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="5a6d7-170">Bonjour Azure Cosmos DB .NET Core aperçu SDK a parité de fonctionnalités avec la version la plus récente de hello hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) et prend en charge hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="5a6d7-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="5a6d7-171">Tous les [modes de connexion](performance-tips.md#networking) : mode passerelle, TCP Direct et HTTPs Direct.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="5a6d7-172">Tous les [niveaux de cohérence](consistency-levels.md): Forte, Session, Obsolescence limitée et Éventuelle.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="5a6d7-173">[Collections partitionnées](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="5a6d7-174">[Comptes de base de données multirégions et géoréplication](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="5a6d7-175">Si vous avez des questions, toothis connexes SDK, validez trop[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), fichier ou un problème dans hello [référentiel github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="5a6d7-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="5a6d7-176">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="5a6d7-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="5a6d7-177">Version</span><span class="sxs-lookup"><span data-stu-id="5a6d7-177">Version</span></span> | <span data-ttu-id="5a6d7-178">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="5a6d7-178">Release Date</span></span> | <span data-ttu-id="5a6d7-179">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="5a6d7-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="5a6d7-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="5a6d7-181">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="5a6d7-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="5a6d7-183">7 août 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="5a6d7-185">2 août 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="5a6d7-187">12 juin 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="5a6d7-189">23 mai 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="5a6d7-191">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="5a6d7-193">19 avril 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="5a6d7-195">29 mars 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="5a6d7-197">25 mars 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="5a6d7-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="5a6d7-199">20 mars 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="5a6d7-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="5a6d7-201">14 mars 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="5a6d7-203">16 février 2017</span><span class="sxs-lookup"><span data-stu-id="5a6d7-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="5a6d7-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="5a6d7-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="5a6d7-205">21 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="5a6d7-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="5a6d7-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="5a6d7-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="5a6d7-207">15 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="5a6d7-207">November 15, 2016</span></span> |<span data-ttu-id="5a6d7-208">31 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="5a6d7-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="5a6d7-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5a6d7-209">See Also</span></span>
<span data-ttu-id="5a6d7-210">toolearn savoir plus sur Cosmos DB, consultez [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) page du service.</span><span class="sxs-lookup"><span data-stu-id="5a6d7-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

