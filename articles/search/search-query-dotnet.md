---
title: "AAA » interroger un index (API .NET - Azure Search) | Documents Microsoft »"
description: "Générer une requête de recherche dans Azure search et utilisez les paramètres toofilter et tri recherche résultats de la recherche."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="9dc6f-103">Interroger votre index Azure Search à l’aide de hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9dc6f-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dc6f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9dc6f-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9dc6f-105">Portail</span><span class="sxs-lookup"><span data-stu-id="9dc6f-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9dc6f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9dc6f-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9dc6f-107">REST</span><span class="sxs-lookup"><span data-stu-id="9dc6f-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="9dc6f-108">Cet article vous montrera comment un index à l’aide de tooquery hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="9dc6f-109">Avant de commencer cette procédure, vous devez déjà avoir [créé un index de Recherche Azure](search-what-is-an-index.md) et y avoir [ajouté des données](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9dc6f-110">Tous les exemples de code figurant dans cet article sont écrits en C#.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="9dc6f-111">Vous pouvez trouver le code source complet hello [sur GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="9dc6f-112">Vous pouvez également lire sur hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) pour une présentation plus détaillée de l’exemple de code hello.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="9dc6f-113">Identifier la clé API de requête de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="9dc6f-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="9dc6f-114">Maintenant que vous avez créé un index Azure Search, vous êtes requêtes tooissue presque prêt à l’aide de hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="9dc6f-115">Vous devez tout d’abord, tooobtain d'entre hello clés api de requête qui a été généré pour le service de recherche hello que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="9dc6f-116">Hello .NET SDK envoie cette clé d’api sur chaque service tooyour de demande.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="9dc6f-117">Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="9dc6f-118">toofind-clés api de votre service vous connectez-vous toohello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9dc6f-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9dc6f-119">Panneau du service tooyour accédez Azure Search</span><span class="sxs-lookup"><span data-stu-id="9dc6f-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="9dc6f-120">Cliquez sur hello icône « Clés »</span><span class="sxs-lookup"><span data-stu-id="9dc6f-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="9dc6f-121">Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9dc6f-122">Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9dc6f-123">Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="9dc6f-124">Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="9dc6f-125">Pour des raisons de hello d’interrogation d’un index, vous pouvez utiliser un de vos clés de requête.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="9dc6f-126">Vos clés d’administration peuvent également être utilisés pour les requêtes, mais vous devez utiliser une clé de requête dans votre code d’application, comme cela suit mieux hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="9dc6f-127">Créez une instance de hello SearchIndexClient classe</span><span class="sxs-lookup"><span data-stu-id="9dc6f-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="9dc6f-128">requêtes tooissue avec hello Azure Search .NET SDK, vous devez toocreate une instance de hello `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="9dc6f-129">Cette classe dispose de plusieurs constructeurs.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-129">This class has several constructors.</span></span> <span data-ttu-id="9dc6f-130">Hello celui que vous souhaitez prend votre nom de service de recherche, le nom de l’index et un `SearchCredentials` objet en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="9dc6f-131">`SearchCredentials` encapsule votre clé API.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="9dc6f-132">code Hello ci-dessous crée un nouveau `SearchIndexClient` pour l’index de « hôtels » hello (créé dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md)) à l’aide des valeurs pour le nom de service de recherche hello et clé d’api qui sont stockés dans la configuration de l’application hello fichier (`appsettings.json` dans les cas de hello Hello [exemple d’application](http://aka.ms/search-dotnet-howto)) :</span><span class="sxs-lookup"><span data-stu-id="9dc6f-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="9dc6f-133">`SearchIndexClient` a une propriété `Documents`.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="9dc6f-134">Cette propriété fournit que toutes les hello méthodes que vous devez les index Azure Search tooquery.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="9dc6f-135">Interroger votre index</span><span class="sxs-lookup"><span data-stu-id="9dc6f-135">Query your index</span></span>
<span data-ttu-id="9dc6f-136">Recherche avec hello .NET SDK est aussi simple que hello appelant `Documents.Search` méthode sur votre `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="9dc6f-137">Cette méthode prend quelques paramètres, y compris le texte de recherche hello, avec un `SearchParameters` objet qui peut être utilisé toofurther affiner hello requête.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="9dc6f-138">Types de requête</span><span class="sxs-lookup"><span data-stu-id="9dc6f-138">Types of Queries</span></span>
<span data-ttu-id="9dc6f-139">principal de Hello deux [types de requête](search-query-overview.md#types-of-queries) vous utiliserez sont `search` et `filter`.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="9dc6f-140">Une requête `search` recherche un ou plusieurs termes dans tous les champs de *recherche* de votre index.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="9dc6f-141">Une requête `filter` permet d’évaluer une expression booléenne dans tous les champs *filtrables* d’un index.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="9dc6f-142">Les filtres et les recherches sont effectuées à l’aide de hello `Documents.Search` (méthode).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="9dc6f-143">Une requête de recherche peut être passée dans hello `searchText` paramètre, pendant une expression de filtre peut être passée dans hello `Filter` propriété Hello `SearchParameters` classe.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="9dc6f-144">toofilter sans rechercher, passez simplement `"*"` pour hello `searchText` paramètre.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="9dc6f-145">toosearch sans filtrage, laissez hello `Filter` propriété non définie, ou vous ne pouvez pas passer un `SearchParameters` de l’instance du tout.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="9dc6f-146">Exemples de requêtes</span><span class="sxs-lookup"><span data-stu-id="9dc6f-146">Example Queries</span></span>
<span data-ttu-id="9dc6f-147">Hello suivant l’exemple de code montre différentes manières index défini dans hôtels « hello » tooquery [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="9dc6f-148">Notez que les documents hello retournées avec les résultats de la recherche hello sont des instances de hello `Hotel` (classe), qui a été définie dans [importation de données à l’aide d’Azure Search hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="9dc6f-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="9dc6f-149">Hello d’exemple de code utilise un `WriteDocuments` console toohello des résultats de recherche méthode toooutput hello.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="9dc6f-150">Cette méthode est décrite dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-150">This method is described in hello next section.</span></span>

```csharp
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
```

## <a name="handle-search-results"></a><span data-ttu-id="9dc6f-151">Traiter les résultats de recherche</span><span class="sxs-lookup"><span data-stu-id="9dc6f-151">Handle search results</span></span>
<span data-ttu-id="9dc6f-152">Hello `Documents.Search` méthode retourne un `DocumentSearchResult` objet qui contient des résultats de requête de hello hello.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="9dc6f-153">exemple Hello dans la section précédente de hello utilisé une méthode appelée `WriteDocuments` console toohello de toooutput hello recherche résultats :</span><span class="sxs-lookup"><span data-stu-id="9dc6f-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

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

<span data-ttu-id="9dc6f-154">Voici les résultats hello aspect pour les requêtes hello dans la section précédente de hello, en supposant un index de « hôtels » de hello est remplie avec les données d’exemple hello dans [importation de données à l’aide d’Azure Search hello .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="9dc6f-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
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
```

<span data-ttu-id="9dc6f-155">Hello exemple de code ci-dessus utilise les résultats de recherche toooutput hello console.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="9dc6f-156">De même, vous devrez toodisplay les résultats de recherche dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="9dc6f-157">Consultez [cet exemple sur GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) pour obtenir un exemple d’affichage des résultats de recherche de toorender dans une application web basée sur ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

