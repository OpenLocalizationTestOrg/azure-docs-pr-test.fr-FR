---
title: "aaaHow toouse Azure Search à partir d’une Application .NET | Documents Microsoft"
description: "Comment effectuer une recherche toouse Azure à partir d’une Application .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="f55b1-103">Comment effectuer une recherche toouse Azure à partir d’une Application .NET</span><span class="sxs-lookup"><span data-stu-id="f55b1-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="f55b1-104">Cet article est un tooget de procédure pas à pas vous opérationnel avec hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="f55b1-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="f55b1-105">Vous pouvez utiliser hello .NET SDK tooimplement une riche expérience de recherche dans votre application à l’aide d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="f55b1-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="f55b1-106">Nouveautés dans hello recherche Azure SDK</span><span class="sxs-lookup"><span data-stu-id="f55b1-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="f55b1-107">Hello SDK se compose d’une bibliothèque cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="f55b1-108">Il vous toomanage votre index, les sources de données et les indexeurs, ainsi que télécharger et gérer des documents et exécuter des requêtes, le tout sans avoir toodeal avec les détails de hello de HTTP et JSON.</span><span class="sxs-lookup"><span data-stu-id="f55b1-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="f55b1-109">bibliothèque cliente de Hello définit des classes telles que `Index`, `Field`, et `Document`, ainsi que des opérations telles que `Indexes.Create` et `Documents.Search` sur hello `SearchServiceClient` et `SearchIndexClient` classes.</span><span class="sxs-lookup"><span data-stu-id="f55b1-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="f55b1-110">Ces classes sont organisés en hello suivant des espaces de noms :</span><span class="sxs-lookup"><span data-stu-id="f55b1-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="f55b1-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="f55b1-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="f55b1-112">Microsoft.Azure.Search.Models.</span><span class="sxs-lookup"><span data-stu-id="f55b1-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="f55b1-113">version actuelle de Hello Hello Azure Search .NET SDK est désormais disponible.</span><span class="sxs-lookup"><span data-stu-id="f55b1-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="f55b1-114">Si vous souhaitez que les commentaires tooprovide pour nous tooincorporate dans la version suivante de hello, visitez notre [page de commentaires](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="f55b1-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="f55b1-115">Hello .NET SDK prend en charge la version `2016-09-01` Hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f55b1-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="f55b1-116">Cette version inclut désormais la prise en charge des analyseurs personnalisés et de l’indexeur de table Azure et des objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f55b1-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="f55b1-117">Afficher un aperçu des fonctionnalités qui sont *pas* dans le cadre de cette version, telles que la prise en charge pour l’indexation de fichiers JSON et les volumes partagés de cluster, sont dans [aperçu](search-api-2015-02-28-preview.md) et disponibles via hello plus anciens [2.0 préversion de hello .NET SDK ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="f55b1-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="f55b1-118">Ce Kit de développement logiciel (SDK) ne prend pas en charge les [opérations de gestion](https://docs.microsoft.com/rest/api/searchmanagement/) telles que la création et la mise à l’échelle des services de recherche, ainsi que la gestion des clés API.</span><span class="sxs-lookup"><span data-stu-id="f55b1-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="f55b1-119">Si vous devez toomanage vos ressources de recherche à partir d’une application .NET, vous pouvez utiliser hello [SDK de gestion Azure Search .NET](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="f55b1-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="f55b1-120">Mise à niveau de la version la plus récente du Kit de développement logiciel de hello toohello</span><span class="sxs-lookup"><span data-stu-id="f55b1-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="f55b1-121">Si vous utilisez déjà une version antérieure de hello Azure Search .NET SDK et que vous souhaitez tooupgrade toohello version nouvelle disponible de manière générale, [cet article](search-dotnet-sdk-migration.md) explique comment.</span><span class="sxs-lookup"><span data-stu-id="f55b1-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="f55b1-122">Configuration requise pour le Kit de développement logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="f55b1-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="f55b1-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f55b1-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="f55b1-124">Votre propre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="f55b1-124">Your own Azure Search service.</span></span> <span data-ttu-id="f55b1-125">Bonjour toouse de l’ordre SDK, vous devez nom hello de votre service et une ou plusieurs clés API.</span><span class="sxs-lookup"><span data-stu-id="f55b1-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="f55b1-126">[Créer un service dans le portail de hello](search-create-service-portal.md) vous aidera tout au long de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="f55b1-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="f55b1-127">Télécharger hello Azure Search .NET SDK [package NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) à l’aide de « Gérer les Packages NuGet » dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f55b1-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="f55b1-128">Nom du package hello simplement rechercher `Microsoft.Azure.Search` sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f55b1-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="f55b1-129">Bonjour Azure Search .NET SDK prend en charge les applications qui ciblent hello .NET Framework 4.6 et .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f55b1-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="f55b1-130">Principaux scénarios</span><span class="sxs-lookup"><span data-stu-id="f55b1-130">Core scenarios</span></span>
<span data-ttu-id="f55b1-131">Il existe plusieurs choses que vous aurez besoin de toodo dans votre application de recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="f55b1-132">Dans ce didacticiel, nous aborderons ces principaux scénarios :</span><span class="sxs-lookup"><span data-stu-id="f55b1-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="f55b1-133">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="f55b1-133">Creating an index</span></span>
* <span data-ttu-id="f55b1-134">Remplissage d’index hello avec des documents</span><span class="sxs-lookup"><span data-stu-id="f55b1-134">Populating hello index with documents</span></span>
* <span data-ttu-id="f55b1-135">Recherche de documents à l'aide de filtres et de la recherche en texte intégral</span><span class="sxs-lookup"><span data-stu-id="f55b1-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="f55b1-136">exemple de code Hello qui suit illustre chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="f55b1-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="f55b1-137">Vous pouvez toouse libre des extraits de code hello dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="f55b1-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="f55b1-138">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f55b1-138">Overview</span></span>
<span data-ttu-id="f55b1-139">Hello exemple d’application nous allons nous intéresser à crée un index nommé « hôtels », le remplit avec des documents, puis exécute des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="f55b1-140">Voici le programme principal hello, montrant hello flux global :</span><span class="sxs-lookup"><span data-stu-id="f55b1-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="f55b1-141">Vous pouvez trouver le code source complet de l’exemple d’application hello utilisé dans cette procédure pas à pas sur hello [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f55b1-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="f55b1-142">Nous allons le détailler, étape par étape.</span><span class="sxs-lookup"><span data-stu-id="f55b1-142">We'll walk through this step by step.</span></span> <span data-ttu-id="f55b1-143">Tout d’abord, nous devons toocreate un nouveau `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="f55b1-144">Cet objet vous permet de toomanage index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="f55b1-145">Dans l’ordre tooconstruct une, vous devez tooprovide le nom de votre service Azure Search ainsi que d’une clé d’API d’administration.</span><span class="sxs-lookup"><span data-stu-id="f55b1-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="f55b1-146">Vous pouvez entrer ces informations dans hello `appsettings.json` fichier Hello [exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f55b1-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="f55b1-147">Si vous fournissez une clé incorrecte (par exemple, une clé de requête où une clé d’administration a été requise), hello `SearchServiceClient` lèvera une `CloudException` avec hello « Interdit » du message erreur hello première fois que vous appelez une méthode d’opération, tel que `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="f55b1-148">Si cela produit tooyou, vérifiez la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="f55b1-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="f55b1-149">Hello quelques lignes appellent méthodes toocreate un index nommé « hôtels », suppression de tout d’abord s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="f55b1-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="f55b1-150">Nous étudierons ces méthodes un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="f55b1-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="f55b1-151">Ensuite, les index hello doit toobe rempli.</span><span class="sxs-lookup"><span data-stu-id="f55b1-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="f55b1-152">toodo, nous devons un `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="f55b1-153">Il existe deux tooobtain manières une : en construction, ou en appelant `Indexes.GetClient` sur hello `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="f55b1-154">Nous utilisons hello ce dernier pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="f55b1-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="f55b1-155">Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="f55b1-156">`Indexes.GetClient`est pratique pour remplir un index, car vous épargne hello des difficultés à fournir un autre `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="f55b1-157">Pour ce faire, il en passant la clé d’administration hello que hello utilisé toocreate vous `SearchServiceClient` toohello nouveau `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="f55b1-158">Toutefois, dans la partie hello de votre application qui exécute des requêtes, il est mieux toocreate hello `SearchIndexClient` directement afin que vous pouvez passer d’une clé de requête au lieu d’une clé d’administration.</span><span class="sxs-lookup"><span data-stu-id="f55b1-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="f55b1-159">Cela est conforme au principe hello du privilège minimum et permettra de toomake votre application plus sécurisée.</span><span class="sxs-lookup"><span data-stu-id="f55b1-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="f55b1-160">Pour en savoir plus sur les clés d’administration et les clés de requête, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="f55b1-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="f55b1-161">Maintenant que nous avons un `SearchIndexClient`, nous pouvons remplir des index de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="f55b1-162">Cette opération est exécutée par une autre méthode que nous étudierons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f55b1-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="f55b1-163">Enfin, nous exécuter des requêtes de recherche et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="f55b1-164">Cette fois-ci, nous utilisons un `SearchIndexClient` différent :</span><span class="sxs-lookup"><span data-stu-id="f55b1-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="f55b1-165">Nous allons étudier hello `RunQueries` méthode ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f55b1-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="f55b1-166">Voici hello de toocreate code hello nouveau `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="f55b1-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="f55b1-167">Cette fois, nous utilisons une clé de requête, car nous n’avez pas besoin d’un accès en écriture toohello index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="f55b1-168">Vous pouvez entrer ces informations dans hello `appsettings.json` fichier Hello [exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f55b1-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="f55b1-169">Si vous exécutez cette application avec un nom de service valide et les clés API, la sortie de hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="f55b1-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="f55b1-170">le code source complet de l’application hello Hello est fourni à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="f55b1-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="f55b1-171">Ensuite, nous allons étudier chacune des méthodes hello appelées par `Main`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="f55b1-172">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="f55b1-172">Creating an index</span></span>
<span data-ttu-id="f55b1-173">Après avoir créé un `SearchServiceClient`, présent hello `Main` est est index des hôtels « delete hello » s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="f55b1-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="f55b1-174">Qui est effectuée par hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="f55b1-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="f55b1-175">Cette méthode utilise hello donné `SearchServiceClient` toocheck s’il existe des index de hello et si tel est le cas, supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="f55b1-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-176">exemple de code Hello dans cet article utilise des méthodes synchrones de hello Hello Azure Search .NET SDK pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="f55b1-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="f55b1-177">Nous vous recommandons d’utiliser les méthodes asynchrones hello dans vos propres applications tookeep les évolutives et réactives.</span><span class="sxs-lookup"><span data-stu-id="f55b1-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="f55b1-178">Par exemple, Bonjour méthode ci-dessus, vous pouvez utiliser `ExistsAsync` et `DeleteAsync` au lieu de `Exists` et `Delete`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="f55b1-179">Ensuite, `Main` crée un index « hotels » en appelant cette méthode :</span><span class="sxs-lookup"><span data-stu-id="f55b1-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="f55b1-180">Cette méthode crée un nouveau `Index` objet avec une liste de `Field` objets qui définit le schéma de hello du nouvel index de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="f55b1-181">Chaque champ a un nom, un type de données et plusieurs attributs qui définissent son comportement de recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="f55b1-182">Hello `FieldBuilder` classe utilise réflexion toocreate une liste de `Field` objets pour les index hello en examinant hello propriétés publiques et les attributs de hello donné `Hotel` classe de modèle.</span><span class="sxs-lookup"><span data-stu-id="f55b1-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="f55b1-183">Nous allons étudier hello `Hotel` classe ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f55b1-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-184">Vous pouvez toujours créer la liste des hello `Field` objets directement au lieu d’utiliser `FieldBuilder` si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f55b1-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="f55b1-185">Par exemple, vous ne souhaitez pas toouse une classe de modèle ou vous devrez peut-être toouse une classe de modèle existante que vous ne souhaitez pas toomodify en ajoutant des attributs.</span><span class="sxs-lookup"><span data-stu-id="f55b1-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="f55b1-186">En outre toofields, vous pouvez également ajouter les profils de calcul de score, générateurs de suggestions ou CORS options toohello Index (omis à partir de l’exemple hello par souci de concision).</span><span class="sxs-lookup"><span data-stu-id="f55b1-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="f55b1-187">Vous trouverez plus d’informations sur l’objet d’Index hello et ses parties constituantes Bonjour [référence SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), ainsi que dans hello [référence d’API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f55b1-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="f55b1-188">Remplissage d’index de hello</span><span class="sxs-lookup"><span data-stu-id="f55b1-188">Populating hello index</span></span>
<span data-ttu-id="f55b1-189">étape suivante Hello `Main` est toopopulate hello nouvellement créés par index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="f55b1-190">Cette opération est effectuée dans hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="f55b1-190">This is done in hello following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="f55b1-191">Cette méthode présente quatre parties.</span><span class="sxs-lookup"><span data-stu-id="f55b1-191">This method has four parts.</span></span> <span data-ttu-id="f55b1-192">Hello crée d’abord un tableau de `Hotel` les objets qui serviront de notre index toohello de tooupload des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f55b1-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="f55b1-193">Ces données sont codées en dur pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="f55b1-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="f55b1-194">Dans votre application, vos données seront probablement issues d'une source de données externe, comme une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f55b1-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="f55b1-195">deuxième partie de Hello crée un `IndexBatch` contenant des documents de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="f55b1-196">Vous spécifiez hello opération tooapply toohello lot au moment de sa création, dans ce cas en appelant l’hello `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="f55b1-197">Hello lot est alors téléchargé toohello Azure Search index par hello `Documents.Index` (méthode).</span><span class="sxs-lookup"><span data-stu-id="f55b1-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-198">Dans cet exemple, nous allons simplement charger les documents.</span><span class="sxs-lookup"><span data-stu-id="f55b1-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="f55b1-199">Si vous souhaitiez toomerge change dans des documents existants ou supprimer les documents, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, ou `IndexBatch.Delete` à la place.</span><span class="sxs-lookup"><span data-stu-id="f55b1-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="f55b1-200">Vous pouvez également combiner plusieurs opérations dans un lot unique en appelant `IndexBatch.New`, qui accepte une collection de `IndexAction` objets, chacun d’eux indique une opération spécifique sur un document à Azure Search tooperform.</span><span class="sxs-lookup"><span data-stu-id="f55b1-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="f55b1-201">Vous pouvez créer chaque `IndexAction` avec son propre opération en appelant méthode correspondante hello comme `IndexAction.Merge`, `IndexAction.Upload`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f55b1-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="f55b1-202">Hello troisième partie de cette méthode est un bloc catch qui gère un cas d’erreur importants pour l’indexation.</span><span class="sxs-lookup"><span data-stu-id="f55b1-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="f55b1-203">Si votre service Azure Search échoue tooindex hello certains documents dans un lot de hello, un `IndexBatchException` est levée par `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="f55b1-204">Cela peut se produire si vous indexez des documents lorsque votre service est surchargé.</span><span class="sxs-lookup"><span data-stu-id="f55b1-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="f55b1-205">**Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.**</span><span class="sxs-lookup"><span data-stu-id="f55b1-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="f55b1-206">Vous pouvez retarder et réessayez d’indexation des documents hello ayant échoué, ou vous pouvez ouvrir une session et continuer comme l’exemple hello réalise, ou vous pouvez faire quelque chose d’autre selon les exigences de cohérence de données de votre application.</span><span class="sxs-lookup"><span data-stu-id="f55b1-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-207">Vous pouvez utiliser hello `FindFailedActionsToRetry` tooconstruct méthode un nouveau lot contenant hello uniquement les actions qui ont échoué dans un appel précédent trop`Index`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="f55b1-208">méthode Hello est documenté [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) et qu’il existe une présentation de la façon dont le tooproperly utilisent [sur StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="f55b1-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="f55b1-209">Enfin, hello `UploadDocuments` des délais de méthode pour les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="f55b1-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="f55b1-210">L’indexation se produit à l’en mode asynchrone dans votre service Azure Search, par conséquent, exemple d’application hello doit toowait un tooensure peu de temps que les documents hello sont disponibles pour la recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="f55b1-211">Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.</span><span class="sxs-lookup"><span data-stu-id="f55b1-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="f55b1-212">Comment hello .NET SDK traite les documents</span><span class="sxs-lookup"><span data-stu-id="f55b1-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="f55b1-213">Vous vous demandez peut-être comment hello Azure Search .NET SDK est instances tooupload en mesure d’une classe définie par l’utilisateur comme `Hotel` toohello index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="f55b1-214">toohelp répondre à cette question, examinons hello `Hotel` classe :</span><span class="sxs-lookup"><span data-stu-id="f55b1-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="f55b1-215">Hello première toonotice est que chaque propriété publique `Hotel` correspond tooa champ dans la définition de l’index hello, mais avec une différence essentielle : hello le nom de chaque champ commence par une lettre minuscule (« casse mixte »), tandis que nom hello chaque public propriété de `Hotel` commence par une lettre majuscule (« casse Pascal »).</span><span class="sxs-lookup"><span data-stu-id="f55b1-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="f55b1-216">Il s’agit d’un scénario courant dans les applications .NET d’effectuer une liaison de données où le schéma cible hello est contrôle hello en dehors du développeur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="f55b1-217">Au lieu de .NET de hello tooviolate affectation de noms en rendant la propriété noms casse mixte, vous pouvez indiquer à hello SDK toomap hello noms toocamel en cas de propriété automatiquement avec hello `[SerializePropertyNamesAsCamelCase]` attribut.</span><span class="sxs-lookup"><span data-stu-id="f55b1-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-218">Bonjour Azure Search .NET SDK utilise hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de bibliothèque et de désérialiser vos tooand d’objets de modèle personnalisé à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="f55b1-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="f55b1-219">Vous pouvez personnaliser cette sérialisation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f55b1-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="f55b1-220">Pour plus d’informations, consultez [Sérialisation personnalisée avec JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="f55b1-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="f55b1-221">Hello deuxième chose toonotice sont les attributs hello comme `IsFilterable`, `IsSearchable`, `Key`, et `Analyzer` qui décorent chaque propriété publique.</span><span class="sxs-lookup"><span data-stu-id="f55b1-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="f55b1-222">Ces attributs sont mappés directement toohello [des attributs correspondants de l’index de recherche de Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="f55b1-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="f55b1-223">Hello `FieldBuilder` classe utilise ces définitions de champ tooconstruct pour les index hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="f55b1-224">Hello tiers le plus important de hello `Hotel` classe sont les types de données hello des propriétés publiques de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="f55b1-225">les types .NET Hello de ces propriétés mappent les types de champ équivalent tootheir dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="f55b1-226">Par exemple, hello `Category` propriété de chaîne mappe toohello `category` champ, ce qui est de type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="f55b1-227">Il existe des mappages de type similaire entre `bool?` et `Edm.Boolean`, `DateTimeOffset?` et `Edm.DateTimeOffset`, etc. hello des règles spécifiques pour le mappage de type hello sont documentées par hello `Documents.Get` méthode Bonjour [Azure Search .NET SDK référence](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="f55b1-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="f55b1-228">Hello `FieldBuilder` classe prend en charge ce mappage pour vous, mais il peut toujours être toounderstand utile en cas de besoin tootroubleshoot les problèmes de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="f55b1-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="f55b1-229">Cette possibilité toouse vos propres classes en tant que documents fonctionne dans les deux directions ; Vous pouvez également récupérer les résultats de la recherche et hello SDK automatiquement désérialiser les tooa type de votre choix, comme nous le verrons dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-230">Bonjour Azure Search .NET SDK prend également en charge les documents typées dynamiquement à l’aide de hello `Document` (classe), qui est un mappage de clé/valeur noms toofield des valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="f55b1-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="f55b1-231">Cela est utile dans les scénarios où vous ne connaissez pas schéma d’index hello au moment du design ou dans lesquelles il serait pas pratique toobind toospecific de classes de modèle.</span><span class="sxs-lookup"><span data-stu-id="f55b1-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="f55b1-232">Toutes les méthodes hello hello SDK qui traitent des documents ont des surcharges qui fonctionnent avec hello `Document` classe, ainsi que les surcharges fortement typée qui prennent un paramètre de type générique.</span><span class="sxs-lookup"><span data-stu-id="f55b1-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="f55b1-233">Uniquement les hello ce dernier sont utilisées dans l’exemple de code hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f55b1-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="f55b1-234">Hello `Document` hérite de la classe `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="f55b1-235">Vous trouverez plus d’informations [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="f55b1-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="f55b1-236">**Pourquoi utiliser des types de données Nullable**</span><span class="sxs-lookup"><span data-stu-id="f55b1-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="f55b1-237">Lorsque vous créez votre propre index Azure Search de modèle classes toomap tooan, nous vous recommandons de déclarer des propriétés de types valeur tels que `bool` et `int` toobe nullable (par exemple, `bool?` au lieu de `bool`).</span><span class="sxs-lookup"><span data-stu-id="f55b1-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="f55b1-238">Si vous utilisez une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="f55b1-239">Hello SDK, ni hello service Azure Search aidera à vous tooenforce cela.</span><span class="sxs-lookup"><span data-stu-id="f55b1-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="f55b1-240">Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="f55b1-241">Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search).</span><span class="sxs-lookup"><span data-stu-id="f55b1-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="f55b1-242">Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :</span><span class="sxs-lookup"><span data-stu-id="f55b1-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="f55b1-243">Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.</span><span class="sxs-lookup"><span data-stu-id="f55b1-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="f55b1-244">Sérialisation personnalisée avec JSON.NET</span><span class="sxs-lookup"><span data-stu-id="f55b1-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="f55b1-245">Hello SDK utilise JSON.NET pour sérialiser et désérialiser des documents.</span><span class="sxs-lookup"><span data-stu-id="f55b1-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="f55b1-246">Vous pouvez personnaliser la sérialisation et la désérialisation si nécessaire en définissant votre propre `JsonConverter` ou `IContractResolver` (voir hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="f55b1-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="f55b1-247">Cela peut être utile lorsque vous souhaitez tooadapt une classe de modèle existante à partir de votre application pour une utilisation avec Azure Search et d’autres scénarios plus avancés.</span><span class="sxs-lookup"><span data-stu-id="f55b1-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="f55b1-248">Par exemple, avec la sérialisation personnalisée, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="f55b1-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="f55b1-249">Incluez ou exclure certaines propriétés de votre classe de modèle dans le stockage en tant que champs de document.</span><span class="sxs-lookup"><span data-stu-id="f55b1-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="f55b1-250">Mappez des noms de propriété dans le code et des noms de champ de votre index.</span><span class="sxs-lookup"><span data-stu-id="f55b1-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="f55b1-251">Créer des attributs personnalisés qui peuvent être utilisés pour le mappage des champs de propriétés toodocument.</span><span class="sxs-lookup"><span data-stu-id="f55b1-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="f55b1-252">Vous trouverez des exemples d’implémentation de sérialisation personnalisée dans les tests unitaires de hello pour hello Azure Search .NET SDK sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f55b1-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="f55b1-253">[Ce dossier](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="f55b1-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="f55b1-254">Il contient des classes qui sont utilisées par les tests de sérialisation personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="f55b1-255">Recherche de documents dans l’index de hello</span><span class="sxs-lookup"><span data-stu-id="f55b1-255">Searching for documents in hello index</span></span>
<span data-ttu-id="f55b1-256">dernière étape de Hello dans l’exemple d’application hello est toosearch pour certains documents dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="f55b1-257">Hello méthode effectue cette opération :</span><span class="sxs-lookup"><span data-stu-id="f55b1-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="f55b1-258">Chaque fois qu’elle exécute une requête, cette méthode crée tout d’abord un objet `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="f55b1-259">Il s’agit de toospecify utilisé des options supplémentaires pour la requête hello telles que le tri, le filtrage, la pagination et des facettes.</span><span class="sxs-lookup"><span data-stu-id="f55b1-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="f55b1-260">Dans cette méthode, nous allons définir hello `Filter`, `Select`, `OrderBy`, et `Top` propriété pour des requêtes différentes.</span><span class="sxs-lookup"><span data-stu-id="f55b1-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="f55b1-261">Tous les hello `SearchParameters` propriétés sont documentées [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="f55b1-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="f55b1-262">étape suivante de Hello est tooactually exécuter la requête de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="f55b1-263">Cette opération est effectuée à l’aide de hello `Documents.Search` (méthode).</span><span class="sxs-lookup"><span data-stu-id="f55b1-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="f55b1-264">Pour chaque requête, nous passons hello recherche texte toouse sous forme de chaîne (ou `"*"` si aucun texte de recherche), ainsi que hello créés précédemment des paramètres de recherche.</span><span class="sxs-lookup"><span data-stu-id="f55b1-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="f55b1-265">Nous avons également de spécifier `Hotel` en tant que paramètre de type hello `Documents.Search`, ce qui indique à des documents toodeserialize hello SDK dans les résultats de recherche hello dans des objets de type `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b1-266">Vous trouverez plus d’informations sur la syntaxe d’expression de requête recherche hello [ici](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="f55b1-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="f55b1-267">Enfin, après chaque requête cette méthode effectue une itération dans toutes les correspondances hello dans les résultats de recherche hello, l’impression de chaque console toohello de document :</span><span class="sxs-lookup"><span data-stu-id="f55b1-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="f55b1-268">Jetons un œil plus proche à chacune des requêtes de hello à son tour.</span><span class="sxs-lookup"><span data-stu-id="f55b1-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="f55b1-269">Voici la première requête hello code tooexecute hello :</span><span class="sxs-lookup"><span data-stu-id="f55b1-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f55b1-270">Dans ce cas, nous recherchons hôtels qui hello mot « budget », et nous souhaitons tooget uniquement hello hôtel noms, tel que spécifié par hello `Select` paramètre.</span><span class="sxs-lookup"><span data-stu-id="f55b1-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="f55b1-271">Voici les résultats hello :</span><span class="sxs-lookup"><span data-stu-id="f55b1-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="f55b1-272">Ensuite, nous souhaitez hôtels de hello toofind avec un taux nocturne de moins de 150 $ et retourne uniquement l’ID d’hôtel hello et description :</span><span class="sxs-lookup"><span data-stu-id="f55b1-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f55b1-273">Cette requête utilise un OData `$filter` expression, `baseRate lt 150`, documents de hello toofilter dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="f55b1-274">Vous trouverez plus d’informations sur hello syntaxe OData prenant en charge Azure Search [ici](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="f55b1-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="f55b1-275">Voici des résultats de requête de hello hello :</span><span class="sxs-lookup"><span data-stu-id="f55b1-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="f55b1-276">Ensuite, nous souhaitons toofind hello supérieur deux hôtels qui ont été rénovés plus récemment et affichent le nom de l’hôtel hello et de la dernière date de rénovation.</span><span class="sxs-lookup"><span data-stu-id="f55b1-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="f55b1-277">Voici le code de hello :</span><span class="sxs-lookup"><span data-stu-id="f55b1-277">Here is hello code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f55b1-278">Dans ce cas, nous utilisons à nouveau hello de toospecify syntaxe OData `OrderBy` paramètre en tant que `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="f55b1-279">Nous définissons également `Top` too2 tooensure nous obtenir uniquement des documents des deux premiers hello.</span><span class="sxs-lookup"><span data-stu-id="f55b1-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="f55b1-280">Comme précédemment, nous avons défini `Select` toospecify les champs qui doivent être retournés.</span><span class="sxs-lookup"><span data-stu-id="f55b1-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="f55b1-281">Voici les résultats hello :</span><span class="sxs-lookup"><span data-stu-id="f55b1-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="f55b1-282">Enfin, nous souhaitons toofind tous les hôtels qui hello mot « motel » :</span><span class="sxs-lookup"><span data-stu-id="f55b1-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f55b1-283">Voici les résultats de hello, qui incluent tous les champs dans la mesure où nous ne spécifiait pas hello `Select` propriété :</span><span class="sxs-lookup"><span data-stu-id="f55b1-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="f55b1-284">Cette étape achève le didacticiel de hello, mais ne pas vous arrêter là.</span><span class="sxs-lookup"><span data-stu-id="f55b1-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="f55b1-285">**Étapes suivantes** fournit des ressources supplémentaires pour en apprendre davantage sur Azure Search.</span><span class="sxs-lookup"><span data-stu-id="f55b1-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55b1-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f55b1-286">Next steps</span></span>
* <span data-ttu-id="f55b1-287">Parcourir les références hello pour hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f55b1-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="f55b1-288">Approfondissez vos connaissances grâce aux [vidéos et autres exemples et didacticiels](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="f55b1-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="f55b1-289">Révision [conventions de dénomination](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello modalités d’affectation de noms différents objets.</span><span class="sxs-lookup"><span data-stu-id="f55b1-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="f55b1-290">Faites connaissance avec les [types de données pris en charge](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) par Azure Search.</span><span class="sxs-lookup"><span data-stu-id="f55b1-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
