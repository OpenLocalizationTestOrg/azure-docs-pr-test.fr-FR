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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Interroger votre index Azure Search à l’aide de hello .NET SDK
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-query-overview.md)
> * [Portail](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Cet article vous montrera comment un index à l’aide de tooquery hello [Azure Search .NET SDK](https://aka.ms/search-sdk).

Avant de commencer cette procédure, vous devez déjà avoir [créé un index de Recherche Azure](search-what-is-an-index.md) et y avoir [ajouté des données](search-what-is-data-import.md).

> [!NOTE]
> Tous les exemples de code figurant dans cet article sont écrits en C#. Vous pouvez trouver le code source complet hello [sur GitHub](http://aka.ms/search-dotnet-howto). Vous pouvez également lire sur hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) pour une présentation plus détaillée de l’exemple de code hello.

## <a name="identify-your-azure-search-services-query-api-key"></a>Identifier la clé API de requête de votre service Azure Search
Maintenant que vous avez créé un index Azure Search, vous êtes requêtes tooissue presque prêt à l’aide de hello .NET SDK. Vous devez tout d’abord, tooobtain d'entre hello clés api de requête qui a été généré pour le service de recherche hello que vous avez configuré. Hello .NET SDK envoie cette clé d’api sur chaque service tooyour de demande. Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.

1. toofind-clés api de votre service vous connectez-vous toohello [portail Azure](https://portal.azure.com/)
2. Panneau du service tooyour accédez Azure Search
3. Cliquez sur hello icône « Clés »

Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.

* Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données. Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.
* Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.

Pour des raisons de hello d’interrogation d’un index, vous pouvez utiliser un de vos clés de requête. Vos clés d’administration peuvent également être utilisés pour les requêtes, mais vous devez utiliser une clé de requête dans votre code d’application, comme cela suit mieux hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Créez une instance de hello SearchIndexClient classe
requêtes tooissue avec hello Azure Search .NET SDK, vous devez toocreate une instance de hello `SearchIndexClient` classe. Cette classe dispose de plusieurs constructeurs. Hello celui que vous souhaitez prend votre nom de service de recherche, le nom de l’index et un `SearchCredentials` objet en tant que paramètres. `SearchCredentials` encapsule votre clé API.

code Hello ci-dessous crée un nouveau `SearchIndexClient` pour l’index de « hôtels » hello (créé dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md)) à l’aide des valeurs pour le nom de service de recherche hello et clé d’api qui sont stockés dans la configuration de l’application hello fichier (`appsettings.json` dans les cas de hello Hello [exemple d’application](http://aka.ms/search-dotnet-howto)) :

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` a une propriété `Documents`. Cette propriété fournit que toutes les hello méthodes que vous devez les index Azure Search tooquery.

## <a name="query-your-index"></a>Interroger votre index
Recherche avec hello .NET SDK est aussi simple que hello appelant `Documents.Search` méthode sur votre `SearchIndexClient`. Cette méthode prend quelques paramètres, y compris le texte de recherche hello, avec un `SearchParameters` objet qui peut être utilisé toofurther affiner hello requête.

#### <a name="types-of-queries"></a>Types de requête
principal de Hello deux [types de requête](search-query-overview.md#types-of-queries) vous utiliserez sont `search` et `filter`. Une requête `search` recherche un ou plusieurs termes dans tous les champs de *recherche* de votre index. Une requête `filter` permet d’évaluer une expression booléenne dans tous les champs *filtrables* d’un index.

Les filtres et les recherches sont effectuées à l’aide de hello `Documents.Search` (méthode). Une requête de recherche peut être passée dans hello `searchText` paramètre, pendant une expression de filtre peut être passée dans hello `Filter` propriété Hello `SearchParameters` classe. toofilter sans rechercher, passez simplement `"*"` pour hello `searchText` paramètre. toosearch sans filtrage, laissez hello `Filter` propriété non définie, ou vous ne pouvez pas passer un `SearchParameters` de l’instance du tout.

#### <a name="example-queries"></a>Exemples de requêtes
Hello suivant l’exemple de code montre différentes manières index défini dans hôtels « hello » tooquery [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#DefineIndex). Notez que les documents hello retournées avec les résultats de la recherche hello sont des instances de hello `Hotel` (classe), qui a été définie dans [importation de données à l’aide d’Azure Search hello .NET SDK](search-import-data-dotnet.md#HotelClass). Hello d’exemple de code utilise un `WriteDocuments` console toohello des résultats de recherche méthode toooutput hello. Cette méthode est décrite dans la section suivante de hello.

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

## <a name="handle-search-results"></a>Traiter les résultats de recherche
Hello `Documents.Search` méthode retourne un `DocumentSearchResult` objet qui contient des résultats de requête de hello hello. exemple Hello dans la section précédente de hello utilisé une méthode appelée `WriteDocuments` console toohello de toooutput hello recherche résultats :

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

Voici les résultats hello aspect pour les requêtes hello dans la section précédente de hello, en supposant un index de « hôtels » de hello est remplie avec les données d’exemple hello dans [importation de données à l’aide d’Azure Search hello .NET SDK](search-import-data-dotnet.md):

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

Hello exemple de code ci-dessus utilise les résultats de recherche toooutput hello console. De même, vous devrez toodisplay les résultats de recherche dans votre propre application. Consultez [cet exemple sur GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) pour obtenir un exemple d’affichage des résultats de recherche de toorender dans une application web basée sur ASP.NET MVC.

