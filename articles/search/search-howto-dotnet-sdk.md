---
title: "Comment utiliser la Recherche Azure à partir d’une application .NET | Microsoft Docs"
description: "Comment utiliser Azure Search à partir d'une application .NET"
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="568b9-103">Comment utiliser Azure Search à partir d'une application .NET</span><span class="sxs-lookup"><span data-stu-id="568b9-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="568b9-104">Cet article est une procédure pas à pas dont le but est de vous aider à utiliser le [SDK .NET Azure Search](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="568b9-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="568b9-105">Vous pouvez utiliser le SDK .NET pour intégrer une expérience de recherche enrichie dans votre application à l'aide d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="568b9-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="568b9-106">Contenu du SDK Azure Search</span><span class="sxs-lookup"><span data-stu-id="568b9-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="568b9-107">Ce kit de développement se compose d'une bibliothèque cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="568b9-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="568b9-108">Il vous permet de gérer vos index, sources de données et indexeurs, ainsi que de télécharger et gérer des documents, et d'exécuter des requêtes, sans avoir à gérer les détails de HTTP et de JSON.</span><span class="sxs-lookup"><span data-stu-id="568b9-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="568b9-109">La bibliothèque cliente définit des classes comme `Index`, `Field` et `Document`, ainsi que des opérations telles que `Indexes.Create` et `Documents.Search` sur les classes `SearchServiceClient` et `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="568b9-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="568b9-110">Ces classes sont organisées dans les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="568b9-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="568b9-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="568b9-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="568b9-112">Microsoft.Azure.Search.Models.</span><span class="sxs-lookup"><span data-stu-id="568b9-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="568b9-113">La version actuelle du Kit de développement logiciel (SDK) .NET Azure Search est désormais mise à la disposition générale.</span><span class="sxs-lookup"><span data-stu-id="568b9-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="568b9-114">Si vous souhaitez fournir des commentaires que nous pourrons intégrer dans la prochaine version, consultez notre [page de commentaires](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="568b9-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="568b9-115">Le Kit de développement logiciel (SDK) .NET prend en charge la version `2016-09-01` de [l’API REST de la Recherche Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="568b9-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="568b9-116">Cette version inclut désormais la prise en charge des analyseurs personnalisés et de l’indexeur de table Azure et des objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="568b9-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="568b9-117">Les fonctionnalités d’évaluation qui ne font *pas* partie de cette version, par exemple la prise en charge de l’indexation des fichiers CSV et JSON, sont disponibles en [version d’évaluation](search-api-2015-02-28-preview.md) et accessibles par l’intermédiaire de la version [2.0-preview du Kit de développement logiciel (SDK) .NET](https://aka.ms/search-sdk-preview), plus ancienne.</span><span class="sxs-lookup"><span data-stu-id="568b9-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="568b9-118">Ce Kit de développement logiciel (SDK) ne prend pas en charge les [opérations de gestion](https://docs.microsoft.com/rest/api/searchmanagement/) telles que la création et la mise à l’échelle des services de recherche, ainsi que la gestion des clés API.</span><span class="sxs-lookup"><span data-stu-id="568b9-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="568b9-119">Si vous avez besoin de gérer vos ressources de recherche à partir d’une application .NET, vous pouvez utiliser le [Kit de développement logiciel (SDK) .NET de la Recherche Azure](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="568b9-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="568b9-120">Mise à niveau vers la dernière version du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="568b9-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="568b9-121">Si vous utilisez déjà une version antérieure du Kit de développement logiciel (SDK) .NET Azure Search et que vous souhaitez mettre à niveau vers la nouvelle version mise à la disposition générale, [cet article](search-dotnet-sdk-migration.md) vous explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="568b9-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="568b9-122">Configuration requise pour le SDK</span><span class="sxs-lookup"><span data-stu-id="568b9-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="568b9-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="568b9-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="568b9-124">Votre propre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="568b9-124">Your own Azure Search service.</span></span> <span data-ttu-id="568b9-125">Pour utiliser le SDK, vous devez connaître le nom de votre service et une ou plusieurs clés API.</span><span class="sxs-lookup"><span data-stu-id="568b9-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="568b9-126">[Créer un service dans le portail](search-create-service-portal.md) vous guidera à travers ces étapes.</span><span class="sxs-lookup"><span data-stu-id="568b9-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="568b9-127">Téléchargez le [package NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) du SDK .NET Azure Search en utilisant « Gérer les packages NuGet » dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="568b9-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="568b9-128">Recherchez le package nommé `Microsoft.Azure.Search` sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="568b9-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="568b9-129">Le Kit de développement logiciel (SDK) .NET Recherche Azure prend en charge les applications qui ciblent .NET Framework 4.6 et .NET Core.</span><span class="sxs-lookup"><span data-stu-id="568b9-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="568b9-130">Principaux scénarios</span><span class="sxs-lookup"><span data-stu-id="568b9-130">Core scenarios</span></span>
<span data-ttu-id="568b9-131">Vous devez faire plusieurs choses dans votre application de recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="568b9-132">Dans ce didacticiel, nous aborderons ces principaux scénarios :</span><span class="sxs-lookup"><span data-stu-id="568b9-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="568b9-133">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="568b9-133">Creating an index</span></span>
* <span data-ttu-id="568b9-134">Remplissage de l'index avec des documents</span><span class="sxs-lookup"><span data-stu-id="568b9-134">Populating the index with documents</span></span>
* <span data-ttu-id="568b9-135">Recherche de documents à l'aide de filtres et de la recherche en texte intégral</span><span class="sxs-lookup"><span data-stu-id="568b9-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="568b9-136">L'exemple de code suivant illustre chacun de ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="568b9-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="568b9-137">N'hésitez pas à utiliser les extraits de code dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="568b9-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="568b9-138">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="568b9-138">Overview</span></span>
<span data-ttu-id="568b9-139">L’application exemple que nous allons examiner crée un index nommé « hotels », le remplit avec des documents, puis exécute des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="568b9-140">Voici le programme principal, décrivant le flux global :</span><span class="sxs-lookup"><span data-stu-id="568b9-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="568b9-141">Vous trouverez le code source complet de l’exemple d’application utilisé dans cette procédure sur [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="568b9-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="568b9-142">Nous allons le détailler, étape par étape.</span><span class="sxs-lookup"><span data-stu-id="568b9-142">We'll walk through this step by step.</span></span> <span data-ttu-id="568b9-143">Tout d’abord, nous devons créer un objet `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="568b9-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="568b9-144">Cet objet vous permet de gérer les index.</span><span class="sxs-lookup"><span data-stu-id="568b9-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="568b9-145">Pour en construire un, vous devez indiquer le nom de votre service Azure Search, ainsi qu’une clé API d'administration.</span><span class="sxs-lookup"><span data-stu-id="568b9-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="568b9-146">Vous pouvez entrer ces informations dans le fichier `appsettings.json` de [l’exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="568b9-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="568b9-147">Si vous fournissez une clé incorrecte (par exemple, une clé de requête là où une clé d’administration était demandée), `SearchServiceClient` génère une `CloudException` avec le message d’erreur « Forbidden » la première fois que vous invoquez une méthode d'opération dessus, comme `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="568b9-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="568b9-148">Si cette situation se produit, vérifiez la clé API.</span><span class="sxs-lookup"><span data-stu-id="568b9-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="568b9-149">Les quelques lignes suivantes appellent des méthodes pour créer un index nommé « hotels », en le supprimant s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="568b9-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="568b9-150">Nous étudierons ces méthodes un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="568b9-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="568b9-151">Ensuite, l'index doit être rempli.</span><span class="sxs-lookup"><span data-stu-id="568b9-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="568b9-152">Pour ce faire, nous avons besoin de `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="568b9-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="568b9-153">Il existe deux façons d'en obtenir un : en le créant ou en appelant `Indexes.GetClient` sur `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="568b9-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="568b9-154">Pour des raisons pratiques, nous allons opter pour la deuxième solution.</span><span class="sxs-lookup"><span data-stu-id="568b9-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="568b9-155">Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="568b9-156">`Indexes.GetClient` est pratique pour remplir un index car il vous évite de fournir un autre `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="568b9-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="568b9-157">Pour ce faire, il transmet la clé d’administration que vous avez utilisée afin de créer le `SearchServiceClient` dans le nouveau `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="568b9-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="568b9-158">Toutefois, dans la partie de votre application qui exécute des requêtes, il vaut mieux créer le `SearchIndexClient` directement afin de transmettre une clé de requête au lieu d'une clé d'administration.</span><span class="sxs-lookup"><span data-stu-id="568b9-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="568b9-159">Cela est conforme au principe du moindre privilège et vous permet de mieux sécuriser votre application.</span><span class="sxs-lookup"><span data-stu-id="568b9-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="568b9-160">Pour en savoir plus sur les clés d’administration et les clés de requête, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="568b9-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="568b9-161">Maintenant que nous avons un `SearchIndexClient`, nous pouvons remplir l'index.</span><span class="sxs-lookup"><span data-stu-id="568b9-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="568b9-162">Cette opération est exécutée par une autre méthode que nous étudierons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="568b9-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="568b9-163">Enfin, nous exécutons quelques requêtes de recherche et affichons les résultats.</span><span class="sxs-lookup"><span data-stu-id="568b9-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="568b9-164">Cette fois-ci, nous utilisons un `SearchIndexClient` différent :</span><span class="sxs-lookup"><span data-stu-id="568b9-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="568b9-165">Nous examinerons la méthode `RunQueries` plus en détail un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="568b9-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="568b9-166">Voici le code permettant de créer le nouveau `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="568b9-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="568b9-167">Cette fois, nous utilisons une clé de requête, car nous n’avons pas besoin d’obtenir un accès en écriture à l’index.</span><span class="sxs-lookup"><span data-stu-id="568b9-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="568b9-168">Vous pouvez entrer ces informations dans le fichier `appsettings.json` de [l’exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="568b9-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="568b9-169">Si vous exécutez cette application avec un nom de service et une clé API valides, la sortie doit être similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="568b9-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="568b9-170">Le code source complet de l'application est fourni à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="568b9-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="568b9-171">Ensuite, nous allons étudier chacune des méthodes appelées par `Main`.</span><span class="sxs-lookup"><span data-stu-id="568b9-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="568b9-172">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="568b9-172">Creating an index</span></span>
<span data-ttu-id="568b9-173">Après la création d’un `SearchServiceClient`, la prochaine opération effectuée par `Main` est de supprimer l'index « hotels » s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="568b9-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="568b9-174">Cette opération est effectuée par la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="568b9-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="568b9-175">Cette méthode utilise `SearchServiceClient` pour vérifier si l'index existe et, dans l’affirmative, elle le supprime.</span><span class="sxs-lookup"><span data-stu-id="568b9-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-176">L'exemple de code dans cet article utilise les méthodes synchrones du SDK .NET Azure Search pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="568b9-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="568b9-177">Nous vous recommandons d'utiliser les méthodes asynchrones dans vos propres applications pour les rendre évolutives et réactives.</span><span class="sxs-lookup"><span data-stu-id="568b9-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="568b9-178">Par exemple, dans la méthode ci-dessus, vous pouvez utiliser `ExistsAsync` et `DeleteAsync` au lieu de `Exists` et `Delete`.</span><span class="sxs-lookup"><span data-stu-id="568b9-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="568b9-179">Ensuite, `Main` crée un index « hotels » en appelant cette méthode :</span><span class="sxs-lookup"><span data-stu-id="568b9-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="568b9-180">Cette méthode crée un objet `Index` avec une liste d’objets `Field` qui définit le schéma du nouvel index.</span><span class="sxs-lookup"><span data-stu-id="568b9-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="568b9-181">Chaque champ a un nom, un type de données et plusieurs attributs qui définissent son comportement de recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="568b9-182">La classe `FieldBuilder` utilise la réflexion pour créer une liste d’objets `Field` pour l’index en examinant les attributs et propriétés publics de la classe de modèle `Hotel` donnée.</span><span class="sxs-lookup"><span data-stu-id="568b9-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="568b9-183">Nous examinerons la classe `Hotel` plus en détail un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="568b9-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-184">Vous pouvez toujours créer directement la liste des objets `Field` au lieu d’utiliser la fonctionnalité `FieldBuilder`, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="568b9-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="568b9-185">Par exemple, vous ne souhaitez pas utiliser une classe de modèle, ou vous pouvez être amené à recourir à une classe de modèle existante, que vous ne souhaitez pas modifier en ajoutant des attributs.</span><span class="sxs-lookup"><span data-stu-id="568b9-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="568b9-186">En plus des champs, vous pouvez ajouter des profils de notation, des générateurs de suggestions ou des options CORS à l'index (éléments supprimés de l'exemple pour des raisons de concision).</span><span class="sxs-lookup"><span data-stu-id="568b9-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="568b9-187">Vous trouverez plus d’informations sur l’objet Index et ses composants dans la page de [référence sur le Kit de développement logiciel (SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), ainsi que dans la page de [référence sur l’API REST de la Recherche Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="568b9-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="568b9-188">Remplissage de l'index</span><span class="sxs-lookup"><span data-stu-id="568b9-188">Populating the index</span></span>
<span data-ttu-id="568b9-189">La prochaine étape dans `Main` consiste à remplir l'index créé.</span><span class="sxs-lookup"><span data-stu-id="568b9-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="568b9-190">Cette opération est effectuée par la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="568b9-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="568b9-191">Cette méthode présente quatre parties.</span><span class="sxs-lookup"><span data-stu-id="568b9-191">This method has four parts.</span></span> <span data-ttu-id="568b9-192">La première crée un tableau d’objets `Hotel` qui servent de données d'entrée à charger dans l'index.</span><span class="sxs-lookup"><span data-stu-id="568b9-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="568b9-193">Ces données sont codées en dur pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="568b9-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="568b9-194">Dans votre application, vos données seront probablement issues d'une source de données externe, comme une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="568b9-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="568b9-195">La deuxième partie crée un `IndexBatch` contenant les documents.</span><span class="sxs-lookup"><span data-stu-id="568b9-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="568b9-196">Vous spécifiez l’opération que vous souhaitez appliquer au lot au moment de sa création, dans ce cas en appelant `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="568b9-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="568b9-197">Le lot est ensuite chargé dans l'index Azure Search par la méthode `Documents.Index` .</span><span class="sxs-lookup"><span data-stu-id="568b9-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-198">Dans cet exemple, nous allons simplement charger les documents.</span><span class="sxs-lookup"><span data-stu-id="568b9-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="568b9-199">Si vous souhaitez fusionner les modifications dans les documents existants ou supprimer des documents, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete` à la place.</span><span class="sxs-lookup"><span data-stu-id="568b9-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="568b9-200">Vous pouvez aussi combiner plusieurs opérations dans un lot unique en appelant `IndexBatch.New`, qui accepte une collection d’objets `IndexAction`, dont chacun indique à Azure Search d’effectuer une opération spécifique sur un document.</span><span class="sxs-lookup"><span data-stu-id="568b9-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="568b9-201">Vous pouvez créer chaque `IndexAction` avec sa propre opération en appelant la méthode correspondante comme `IndexAction.Merge`, `IndexAction.Upload`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="568b9-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="568b9-202">La troisième partie de cette méthode est un bloc catch qui gère un cas d'erreur important pour l'indexation.</span><span class="sxs-lookup"><span data-stu-id="568b9-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="568b9-203">Si votre service Azure Search ne parvient pas à indexer certains documents du lot, `Documents.Index` génère un `IndexBatchException`.</span><span class="sxs-lookup"><span data-stu-id="568b9-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="568b9-204">Cela peut se produire si vous indexez des documents lorsque votre service est surchargé.</span><span class="sxs-lookup"><span data-stu-id="568b9-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="568b9-205">**Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.**</span><span class="sxs-lookup"><span data-stu-id="568b9-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="568b9-206">Vous pouvez retarder puis relancer l'indexation des documents qui ont échoué, ouvrir une session et continuer comme dans l’exemple, ou faire autre chose selon la cohérence des données requise par votre application.</span><span class="sxs-lookup"><span data-stu-id="568b9-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-207">Vous pouvez utiliser la méthode `FindFailedActionsToRetry` pour construire un nouveau lot contenant uniquement les actions qui ont échoué lors d’un précédent appel à `Index`.</span><span class="sxs-lookup"><span data-stu-id="568b9-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="568b9-208">La méthode est documentée [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_). Vous trouverez sur [StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry) un fil de discussion sur l’utilisation adéquate de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="568b9-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="568b9-209">Enfin, la méthode `UploadDocuments` retarde son exécution de deux secondes.</span><span class="sxs-lookup"><span data-stu-id="568b9-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="568b9-210">L'indexation s’exécutant en mode asynchrone dans votre service Azure Search, l'exemple d'application doit attendre quelque temps afin de s'assurer que les documents sont disponibles pour la recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="568b9-211">Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.</span><span class="sxs-lookup"><span data-stu-id="568b9-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="568b9-212">Gestion des documents par le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="568b9-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="568b9-213">Vous demandez peut-être comment le SDK .NET Azure Search peut charger des instances d’une classe définie par l'utilisateur, comme `Hotel` , dans l'index.</span><span class="sxs-lookup"><span data-stu-id="568b9-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="568b9-214">Pour répondre à cette question, examinons la classe `Hotel` :</span><span class="sxs-lookup"><span data-stu-id="568b9-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="568b9-215">La première chose à remarquer est que chaque propriété publique de `Hotel` correspond à un champ dans la définition de l'index, mais à une différence près : le nom de chaque champ commence par une minuscule, tandis que le nom de chaque propriété publique de `Hotel` commence par une majuscule.</span><span class="sxs-lookup"><span data-stu-id="568b9-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="568b9-216">Il s'agit d'un scénario courant dans les applications .NET qui effectuent une liaison de données là où le schéma cible est en dehors du contrôle du développeur de l'application.</span><span class="sxs-lookup"><span data-stu-id="568b9-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="568b9-217">Plutôt que de violer les consignes d’affectation de noms de .NET en faisant commencer les noms de propriété par une minuscule, vous pouvez demander au SDK d’attribuer automatiquement une casse minuscule aux noms de propriété avec l’attribut `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="568b9-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-218">Le SDK .NET Azure Search utilise la bibliothèque [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) pour sérialiser et désérialiser vos objets de modèle personnalisés vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="568b9-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="568b9-219">Vous pouvez personnaliser cette sérialisation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="568b9-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="568b9-220">Pour plus d’informations, consultez [Sérialisation personnalisée avec JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="568b9-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="568b9-221">Le deuxième élément à prendre est compte, ce sont les attributs tels que `IsFilterable`, `IsSearchable`, `Key`, et `Analyzer`, qui décorent chaque propriété publique.</span><span class="sxs-lookup"><span data-stu-id="568b9-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="568b9-222">Ces attributs sont mappés directement aux [attributs correspondants de l’index de la Recherche Azure](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="568b9-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="568b9-223">La classe `FieldBuilder` les utilise pour construire des définitions de champ pour l’index.</span><span class="sxs-lookup"><span data-stu-id="568b9-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="568b9-224">La troisième chose importante sur la classe `Hotel` concerne les types de données des propriétés publiques.</span><span class="sxs-lookup"><span data-stu-id="568b9-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="568b9-225">Les types .NET de ces propriétés correspondent à leurs types de champ équivalents dans la définition de l’index.</span><span class="sxs-lookup"><span data-stu-id="568b9-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="568b9-226">Par exemple, la propriété de chaîne `Category` correspond au champ `category`, qui est de type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="568b9-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="568b9-227">Il existe des mappages de type similaires entre `bool?` et `Edm.Boolean`, `DateTimeOffset?` et `Edm.DateTimeOffset`, etc. Les règles spécifiques pour le mappage de type sont documentées avec la méthode `Documents.Get` dans [l’article de référence sur le Kit de développement logiciel (SDK) .NET du service Recherche Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="568b9-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="568b9-228">La classe `FieldBuilder` effectue ce mappage pour vous, mais il peut toutefois être utile de comprendre son fonctionnement, pour les situations éventuelles de résolution des problèmes de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="568b9-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="568b9-229">Cette capacité à utiliser vos propres classes comme des documents fonctionne dans les deux sens. Vous pouvez également récupérer les résultats de la recherche et laisser le SDK les désérialiser automatiquement à un type de votre choix, comme nous le verrons dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="568b9-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-230">Le SDK .NET Azure Search prend également en charge les documents dynamiquement typés à l’aide de la classe `Document`, qui est un mappage de type clé/valeur entre des noms de champ et des valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="568b9-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="568b9-231">Cela est utile dans les cas où vous ne connaissez pas le schéma de l’index lors de sa conception et où il serait peu pratique d’établir une liaison à des classes de modèles spécifiques.</span><span class="sxs-lookup"><span data-stu-id="568b9-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="568b9-232">Toutes les méthodes du SDK qui gèrent les documents ont des surcharges qui fonctionnent avec la classe `Document` , ainsi que des surcharges fortement typées qui acceptent un paramètre de type générique.</span><span class="sxs-lookup"><span data-stu-id="568b9-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="568b9-233">Seules ces dernières sont utilisées dans l'exemple de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="568b9-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="568b9-234">La classe `Document` hérite des données de l’élément `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="568b9-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="568b9-235">Vous trouverez plus d’informations [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="568b9-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="568b9-236">**Pourquoi utiliser des types de données Nullable**</span><span class="sxs-lookup"><span data-stu-id="568b9-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="568b9-237">Lorsque vous créez vos propres classes de modèles à mapper à un index Azure Search, nous vous recommandons de déclarer les propriétés des types de valeurs, par exemple `bool` et `int`, comme acceptant la valeur null (par exemple, `bool?` au lieu de `bool`).</span><span class="sxs-lookup"><span data-stu-id="568b9-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="568b9-238">Si vous utilisez une propriété ne pouvant être définie sur null, vous devez **garantir** qu’aucun document de cet index ne contient de valeur null pour le champ correspondant.</span><span class="sxs-lookup"><span data-stu-id="568b9-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="568b9-239">Ni le Kit de développement logiciel ni le service Azure Search ne vous aideront à appliquer cette recommandation.</span><span class="sxs-lookup"><span data-stu-id="568b9-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="568b9-240">Il ne s’agit pas d’une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ à un index existant qui est de type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="568b9-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="568b9-241">Après la mise à jour de la définition d’index, ce nouveau champ prendra la valeur null pour tous les documents (car tous les types peuvent avoir la valeur null dans Azure Search).</span><span class="sxs-lookup"><span data-stu-id="568b9-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="568b9-242">Si vous utilisez ensuite une classe de modèle avec une propriété `int` ne pouvant être définie sur null pour ce champ, vous obtiendrez l’exception `JsonSerializationException` ci-dessous lorsque vous tenterez de récupérer des documents :</span><span class="sxs-lookup"><span data-stu-id="568b9-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="568b9-243">Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.</span><span class="sxs-lookup"><span data-stu-id="568b9-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="568b9-244">Sérialisation personnalisée avec JSON.NET</span><span class="sxs-lookup"><span data-stu-id="568b9-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="568b9-245">Le kit de développement logiciel utilise JSON.NET pour sérialiser et désérialiser les documents.</span><span class="sxs-lookup"><span data-stu-id="568b9-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="568b9-246">Si nécessaire, vous pouvez personnaliser la sérialisation et la désérialisation en définissant votre propre `JsonConverter` ou `IContractResolver` (pour plus d’informations, consultez la [documentation JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm)).</span><span class="sxs-lookup"><span data-stu-id="568b9-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="568b9-247">Cela peut s’avérer utile lorsque vous souhaitez adapter une classe de modèle existante de votre application à utiliser avec Azure Search et d’autres scénarios plus avancés.</span><span class="sxs-lookup"><span data-stu-id="568b9-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="568b9-248">Par exemple, avec la sérialisation personnalisée, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="568b9-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="568b9-249">Incluez ou exclure certaines propriétés de votre classe de modèle dans le stockage en tant que champs de document.</span><span class="sxs-lookup"><span data-stu-id="568b9-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="568b9-250">Mappez des noms de propriété dans le code et des noms de champ de votre index.</span><span class="sxs-lookup"><span data-stu-id="568b9-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="568b9-251">Créez des attributs personnalisés qui peuvent être utilisés pour le mappage des propriétés aux champs du document.</span><span class="sxs-lookup"><span data-stu-id="568b9-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="568b9-252">Vous pouvez trouver des exemples d’implémentation de sérialisation personnalisée dans les tests d’unités du kit de développement logiciel Azure Search .NET Azure GitHub.</span><span class="sxs-lookup"><span data-stu-id="568b9-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="568b9-253">[Ce dossier](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="568b9-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="568b9-254">Il contient des classes qui sont utilisées par les tests de sérialisation personnalisés.</span><span class="sxs-lookup"><span data-stu-id="568b9-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="568b9-255">Recherche de documents dans l'index</span><span class="sxs-lookup"><span data-stu-id="568b9-255">Searching for documents in the index</span></span>
<span data-ttu-id="568b9-256">La dernière étape dans l'exemple d'application consiste à rechercher certains documents dans l'index.</span><span class="sxs-lookup"><span data-stu-id="568b9-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="568b9-257">La méthode suivante effectue cette opération :</span><span class="sxs-lookup"><span data-stu-id="568b9-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="568b9-258">Chaque fois qu’elle exécute une requête, cette méthode crée tout d’abord un objet `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="568b9-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="568b9-259">Cela permet de spécifier des options supplémentaires pour la requête, comme le tri, le filtrage, la pagination et la facettisation.</span><span class="sxs-lookup"><span data-stu-id="568b9-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="568b9-260">Dans cette méthode, nous définissons les propriétés `Filter`, `Select`, `OrderBy`, et `Top` pour différentes requêtes.</span><span class="sxs-lookup"><span data-stu-id="568b9-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="568b9-261">Toutes les propriétés `SearchParameters` sont documentées [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="568b9-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="568b9-262">L'étape suivante consiste à exécuter la requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="568b9-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="568b9-263">Cette opération est effectuée avec la méthode `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="568b9-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="568b9-264">Pour chaque requête, nous transmettons le texte de recherche à utiliser en tant que chaîne (ou l’élément `"*"`, s’il n’en existe aucun), ainsi que les paramètres de recherche créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="568b9-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="568b9-265">Nous spécifions également `Hotel` comme paramètre de type pour `Documents.Search`, qui demande au SDK de désérialiser les documents figurant dans les résultats de recherche, en objets de type `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="568b9-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="568b9-266">Pour plus d’informations sur la syntaxe des requêtes de recherche, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="568b9-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="568b9-267">Enfin, après l’exécution de chaque requête, cette méthode parcourt toutes les correspondances dans les résultats de la recherche et imprime chaque document dans la console :</span><span class="sxs-lookup"><span data-stu-id="568b9-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="568b9-268">Examinons de plus près chacune des requêtes exécutées.</span><span class="sxs-lookup"><span data-stu-id="568b9-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="568b9-269">Voici le code permettant d’exécuter la première requête :</span><span class="sxs-lookup"><span data-stu-id="568b9-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="568b9-270">Dans ce cas, nous recherchons des hôtels qui correspondent au mot « budget ». Nous voulons uniquement obtenir uniquement les noms de ces hôtels, comme l’indique le paramètre `Select`.</span><span class="sxs-lookup"><span data-stu-id="568b9-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="568b9-271">Voici les résultats :</span><span class="sxs-lookup"><span data-stu-id="568b9-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="568b9-272">Ensuite, nous souhaitons rechercher les hôtels proposant des chambres à moins de 150 $ par nuit, et obtenir uniquement l’ID de l’hôtel et sa description :</span><span class="sxs-lookup"><span data-stu-id="568b9-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="568b9-273">Cette requête utilise une expression `$filter` OData (`baseRate lt 150`) pour filtrer les documents dans l’index.</span><span class="sxs-lookup"><span data-stu-id="568b9-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="568b9-274">Pour plus d’informations sur la syntaxe OData prise en charge par Azure Search, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="568b9-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="568b9-275">Voici les résultats de la requête :</span><span class="sxs-lookup"><span data-stu-id="568b9-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="568b9-276">Ensuite, nous souhaitons rechercher les deux hôtels ayant été le plus récemment rénovés, et afficher le nom et la date de la dernière rénovation de ces derniers.</span><span class="sxs-lookup"><span data-stu-id="568b9-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="568b9-277">Voici le code :</span><span class="sxs-lookup"><span data-stu-id="568b9-277">Here is the code:</span></span> 

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

<span data-ttu-id="568b9-278">Dans ce cas, nous utilisons à nouveau la syntaxe OData pour spécifier le paramètre `OrderBy` en tant que `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="568b9-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="568b9-279">Nous définissons également le paramètre `Top` sur 2 pour vérifier que nous obtenons uniquement les deux premiers documents.</span><span class="sxs-lookup"><span data-stu-id="568b9-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="568b9-280">Comme précédemment, nous définissons le paramètre `Select` pour spécifier les champs qui doivent être renvoyés.</span><span class="sxs-lookup"><span data-stu-id="568b9-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="568b9-281">Voici les résultats :</span><span class="sxs-lookup"><span data-stu-id="568b9-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="568b9-282">Pour finir, nous souhaitons rechercher tous les hôtels correspondant au mot « motel » :</span><span class="sxs-lookup"><span data-stu-id="568b9-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="568b9-283">Voici les résultats, qui incluent tous les champs, dans la mesure où nous n’avons pas spécifié la propriété `Select` :</span><span class="sxs-lookup"><span data-stu-id="568b9-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="568b9-284">Cette étape termine le didacticiel, mais ne vous arrêtez pas en si bon chemin.</span><span class="sxs-lookup"><span data-stu-id="568b9-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="568b9-285">**Étapes suivantes** fournit des ressources supplémentaires pour en apprendre davantage sur Azure Search.</span><span class="sxs-lookup"><span data-stu-id="568b9-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="568b9-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="568b9-286">Next steps</span></span>
* <span data-ttu-id="568b9-287">Parcourez les références relatives au [Kit de développement logiciel (SDK) .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et à [l’API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="568b9-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="568b9-288">Approfondissez vos connaissances grâce aux [vidéos et autres exemples et didacticiels](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="568b9-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="568b9-289">Consultez les [conventions d’affectation de noms](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) pour apprendre les règles de dénomination des différents objets.</span><span class="sxs-lookup"><span data-stu-id="568b9-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="568b9-290">Faites connaissance avec les [types de données pris en charge](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) par Azure Search.</span><span class="sxs-lookup"><span data-stu-id="568b9-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
