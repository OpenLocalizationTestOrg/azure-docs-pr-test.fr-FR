---
title: "API .NET Core Azure Cosmos DB, kit de développement logiciel (SDK) et Ressources | Microsoft Docs"
description: "Tout savoir sur l’API .NET Core et le kit de développement logiciel (SDK), y compris les dates de sortie, les dates de déclassement et les modifications effectuées entre chaque version du kit de développement logiciel (SDK) .NET Core Azure Cosmos DB."
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
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="de1a1-103">Kit de développement logiciel (SDK) .NET Core Azure Cosmos DB : notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="de1a1-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de1a1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="de1a1-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="de1a1-105">Flux de modification .NET</span><span class="sxs-lookup"><span data-stu-id="de1a1-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="de1a1-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="de1a1-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="de1a1-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="de1a1-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="de1a1-108">Java</span><span class="sxs-lookup"><span data-stu-id="de1a1-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="de1a1-109">Python</span><span class="sxs-lookup"><span data-stu-id="de1a1-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="de1a1-110">REST</span><span class="sxs-lookup"><span data-stu-id="de1a1-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="de1a1-111">API REST Resource Provider</span><span class="sxs-lookup"><span data-stu-id="de1a1-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="de1a1-112">SQL</span><span class="sxs-lookup"><span data-stu-id="de1a1-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="de1a1-113">**Téléchargement du Kit de développement logiciel (SDK)**</span><span class="sxs-lookup"><span data-stu-id="de1a1-113">**SDK download**</span></span></td><td>[<span data-ttu-id="de1a1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="de1a1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="de1a1-115">**Documentation de l’API**</span><span class="sxs-lookup"><span data-stu-id="de1a1-115">**API documentation**</span></span></td><td>[<span data-ttu-id="de1a1-116">Documentation de référence sur l’API .NET</span><span class="sxs-lookup"><span data-stu-id="de1a1-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="de1a1-117">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="de1a1-117">**Samples**</span></span></td><td>[<span data-ttu-id="de1a1-118">Exemples de code .NET</span><span class="sxs-lookup"><span data-stu-id="de1a1-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="de1a1-119">**Prise en main**</span><span class="sxs-lookup"><span data-stu-id="de1a1-119">**Get started**</span></span></td><td>[<span data-ttu-id="de1a1-120">Prise en main du kit de développement logiciel (SDK) .NET Core Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de1a1-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="de1a1-121">**Didacticiel d’application web**</span><span class="sxs-lookup"><span data-stu-id="de1a1-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="de1a1-122">Développement d’applications web avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de1a1-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="de1a1-123">**Infrastructure actuellement prise en charge**</span><span class="sxs-lookup"><span data-stu-id="de1a1-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="de1a1-124">.NET Standard 1.6 et .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="de1a1-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="de1a1-125">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="de1a1-125">Release Notes</span></span>

<span data-ttu-id="de1a1-126">Le kit de développement logiciel (SDK) .NET Core Azure Cosmos DB assure la parité des fonctions avec la dernière version du [kit de développement logiciel (SDK) .NET Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="de1a1-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="de1a1-127">Le kit de développement logiciel (SDK) .NET Core Azure Cosmos DB n’est pas encore compatible avec les applications de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="de1a1-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="de1a1-128">Si un Kit de développement logiciel (SDK) .NET Core qui prend en charge les applications UWP vous intéresse, envoyez un e-mail à l’adresse [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="de1a1-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="de1a1-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="de1a1-130">Ajout de la prise en charge du paramètre PartitionKeyRangeId en tant qu’option FeedOption pour la définition de l’étendue des résultats des requêtes sur une valeur de plage de clés de partition spécifique.</span><span class="sxs-lookup"><span data-stu-id="de1a1-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="de1a1-131">Ajout de la prise en charge du paramètre StartTime en tant qu’option ChangeFeedOption pour le démarrage de la recherche de modifications après cette heure.</span><span class="sxs-lookup"><span data-stu-id="de1a1-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="de1a1-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="de1a1-133">Correction d’un problème dans la classe JsonSerializable qui peut provoquer une exception de dépassement de la capacité de la pile.</span><span class="sxs-lookup"><span data-stu-id="de1a1-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="de1a1-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="de1a1-135">Ajout de la prise en charge de la spécification des JsonSerializerSettings personnalisés lors de l’instanciation d’une instance [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="de1a1-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="de1a1-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="de1a1-137">Prise en charge de .NET Standard 1.5 en tant que version cible de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="de1a1-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="de1a1-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="de1a1-139">Correction d’un problème concernant les ordinateurs x64 qui ne prennent pas en charge l’instruction SSE4 et génèrent une SEHException lors de l’exécution de requêtes Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de1a1-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="de1a1-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="de1a1-141">Prise en charge ajoutée pour un nouveau niveau de cohérence nommé ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="de1a1-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="de1a1-142">Prise en charge ajoutée pour les mesures de requête liées aux partitions individuelles.</span><span class="sxs-lookup"><span data-stu-id="de1a1-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="de1a1-143">Prise en charge ajoutée pour la limitation de la taille du jeton de continuation concernant les requêtes.</span><span class="sxs-lookup"><span data-stu-id="de1a1-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="de1a1-144">Prise en charge ajoutée pour un suivi plus détaillé des demandes ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="de1a1-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="de1a1-145">Améliorations de certaines performances du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="de1a1-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="de1a1-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="de1a1-147">Résolution du problème qui ignorait la valeur PartitionKey fournie dans FeedOptions pour les requêtes d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="de1a1-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="de1a1-148">Résolution du problème de gestion transparente des partitions pendant l’exécution d’une requête Order By (Trier par) entre partitions intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="de1a1-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="de1a1-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="de1a1-150">Résolution du problème qui provoquait des blocages parmi certaines API asynchrones lorsqu’elles sont utilisées dans le contexte ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="de1a1-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="de1a1-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="de1a1-152">Correctifs pour augmenter la résistance du Kit de développement logiciel (SDK) au basculement automatique dans certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="de1a1-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="de1a1-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="de1a1-154">Résolution du problème qui provoque parfois une exception WebException : Le nom distant n’a pas pu être résolu.</span><span class="sxs-lookup"><span data-stu-id="de1a1-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="de1a1-155">Ajout de la prise en charge permettant de lire directement un document tapé en ajoutant de nouvelles surcharges à l’API ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="de1a1-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="de1a1-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="de1a1-157">Ajout de la prise en charge LINQ des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="de1a1-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="de1a1-158">Correction d’un problème de fuite de mémoire pour l’objet ConnectionPolicy dû à l’utilisation du Gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="de1a1-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="de1a1-159">Correction d’un problème de fonctionnement d’UpsertAttachmentAsync avec l’utilisation d’ETag.</span><span class="sxs-lookup"><span data-stu-id="de1a1-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="de1a1-160">Correction d’un problème de fonctionnement de la liaison des requêtes ORDER BY entre les partitions lors d’un tri sur un champ de chaîne.</span><span class="sxs-lookup"><span data-stu-id="de1a1-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="de1a1-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="de1a1-162">Ajout de la prise en charge des requêtes d’agrégation (COUNT, MIN, MAX, SUM et AVG).</span><span class="sxs-lookup"><span data-stu-id="de1a1-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="de1a1-163">Consultez l’article [Aggregation support (Prise en charge de l’agrégation)](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="de1a1-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="de1a1-164">Débit minimal réduit sur les collections partitionnées de 10 100 unités de demande/s à 2 500 unités de demande/s.</span><span class="sxs-lookup"><span data-stu-id="de1a1-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="de1a1-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="de1a1-166">Le kit de développement logiciel (SDK) .NET Core Azure Cosmos DB permet de générer des applications [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) rapides et multiplateformes à exécuter sous Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="de1a1-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="de1a1-167">La dernière version du kit de développement logiciel (SDK) .NET Core Azure Cosmos DB est entièrement compatible avec [Xamarin](https://www.xamarin.com) et est utilisée pour générer des applications qui ciblent iOS, Android et Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="de1a1-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="de1a1-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="de1a1-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="de1a1-169">La version préliminaire du kit de développement logiciel (SDK) .NET Core Azure Cosmos DB permet de générer des applications [ASP.NET Core](https://www.asp.net/core) et [.NET Core](https://www.microsoft.com/net/core#windows) rapides et multiplateformes à exécuter sous Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="de1a1-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="de1a1-170">La version préliminaire du kit de développement logiciel (SDK) .NET Core Azure Cosmos DB assure la parité des fonctions avec la dernière version du [kit de développement logiciel (SDK) .NET Azure Cosmos DB](documentdb-sdk-dotnet.md) et prend en charge les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="de1a1-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="de1a1-171">Tous les [modes de connexion](performance-tips.md#networking) : mode passerelle, TCP Direct et HTTPs Direct.</span><span class="sxs-lookup"><span data-stu-id="de1a1-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="de1a1-172">Tous les [niveaux de cohérence](consistency-levels.md): Forte, Session, Obsolescence limitée et Éventuelle.</span><span class="sxs-lookup"><span data-stu-id="de1a1-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="de1a1-173">[Collections partitionnées](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="de1a1-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="de1a1-174">[Comptes de base de données multirégions et géoréplication](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="de1a1-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="de1a1-175">Si vous avez des questions liées à ce SDK, publiez sur [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) ou envoyez une demande sur le [référentiel GitHub](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="de1a1-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="de1a1-176">Dates de lancement et de suppression</span><span class="sxs-lookup"><span data-stu-id="de1a1-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="de1a1-177">Version</span><span class="sxs-lookup"><span data-stu-id="de1a1-177">Version</span></span> | <span data-ttu-id="de1a1-178">Date de lancement</span><span class="sxs-lookup"><span data-stu-id="de1a1-178">Release Date</span></span> | <span data-ttu-id="de1a1-179">Date de suppression</span><span class="sxs-lookup"><span data-stu-id="de1a1-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="de1a1-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="de1a1-181">10 août 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="de1a1-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="de1a1-183">7 août 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="de1a1-185">2 août 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="de1a1-187">12 juin 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="de1a1-189">23 mai 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="de1a1-191">10 mai 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="de1a1-193">19 avril 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="de1a1-195">29 mars 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="de1a1-197">25 mars 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="de1a1-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="de1a1-199">20 mars 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="de1a1-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="de1a1-201">14 mars 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="de1a1-203">16 février 2017</span><span class="sxs-lookup"><span data-stu-id="de1a1-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="de1a1-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="de1a1-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="de1a1-205">21 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="de1a1-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="de1a1-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="de1a1-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="de1a1-207">15 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="de1a1-207">November 15, 2016</span></span> |<span data-ttu-id="de1a1-208">31 décembre 2016</span><span class="sxs-lookup"><span data-stu-id="de1a1-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="de1a1-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="de1a1-209">See Also</span></span>
<span data-ttu-id="de1a1-210">Pour en savoir plus sur Cosmos DB, consultez la page du service [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="de1a1-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

