---
title: "Didacticiel de version préliminaire des synonymes dans la Recherche Azure | Microsoft Docs"
description: "Ajoutez la fonctionnalité de version préliminaire des synonymes à un index dans la Recherche Azure."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="fc411-103">Didacticiel C# des synonymes (version préliminaire) pour la Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="fc411-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="fc411-104">Les synonymes développent une requête en faisant correspondre les termes considérés comme sémantiquement équivalents à l’expression entrée.</span><span class="sxs-lookup"><span data-stu-id="fc411-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="fc411-105">Par exemple, vous souhaiterez peut-être que le terme « voiture » vous permette de trouver des documents contenant les mots « automobile » ou « véhicule ».</span><span class="sxs-lookup"><span data-stu-id="fc411-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="fc411-106">Dans la Recherche Azure, les synonymes sont définis dans une *carte de synonymes*, via des *règles de mappage* qui associent des termes équivalents.</span><span class="sxs-lookup"><span data-stu-id="fc411-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="fc411-107">Vous pouvez créer plusieurs cartes de synonymes, les valider en tant que ressources du service disponible pour tout index, et ensuite référencer ceux que vous souhaitez utiliser au niveau du champ.</span><span class="sxs-lookup"><span data-stu-id="fc411-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="fc411-108">Au moment de la requête, outre la recherche dans un index, la Recherche Azure effectue une recherche dans une carte de synonymes, si une carte est spécifiée dans les champs utilisés dans la requête.</span><span class="sxs-lookup"><span data-stu-id="fc411-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="fc411-109">La fonctionnalité de synonymes est actuellement en version préliminaire et prise en charge uniquement dans les dernières versions d’API et de Kit de développement logiciel (SDK) préliminaires (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="fc411-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="fc411-110">Il n’existe aucune prise en charge sur le portail Azure pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="fc411-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="fc411-111">Les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="fc411-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc411-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fc411-112">Prerequisites</span></span>

<span data-ttu-id="fc411-113">La configuration requise du didacticiel est la suivante :</span><span class="sxs-lookup"><span data-stu-id="fc411-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="fc411-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc411-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="fc411-115">Service Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="fc411-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="fc411-116">Version préliminaire de la bibliothèque Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="fc411-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="fc411-117">Comment utiliser la Recherche Azure à partir d’une application .NET</span><span class="sxs-lookup"><span data-stu-id="fc411-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="fc411-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fc411-118">Overview</span></span>

<span data-ttu-id="fc411-119">Les requêtes avant et après présentent la valeur des synonymes.</span><span class="sxs-lookup"><span data-stu-id="fc411-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="fc411-120">Dans ce didacticiel, nous utilisons un exemple d’application qui exécute des requêtes et retourne des résultats sur un index d’exemples.</span><span class="sxs-lookup"><span data-stu-id="fc411-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="fc411-121">L’exemple d’application crée un petit index nommé « hotels » comprenant deux documents.</span><span class="sxs-lookup"><span data-stu-id="fc411-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="fc411-122">L’application exécute des requêtes de recherche à l’aide de termes et d’expressions qui n’apparaissent pas dans l’index, active la fonctionnalité de synonymes, puis lance les mêmes recherches une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="fc411-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="fc411-123">Le code ci-dessous montre le flux global.</span><span class="sxs-lookup"><span data-stu-id="fc411-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="fc411-124">Les étapes pour créer et remplir l’index des exemples sont expliquées dans [Comment utiliser la Recherche Azure à partir d’une application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="fc411-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="fc411-125">Requêtes « avant »</span><span class="sxs-lookup"><span data-stu-id="fc411-125">"Before" queries</span></span>

<span data-ttu-id="fc411-126">Dans `RunQueriesWithNonExistentTermsInIndex`, nous lançons des requêtes de recherche avec « five star », « internet » et « economy AND hotel ».</span><span class="sxs-lookup"><span data-stu-id="fc411-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="fc411-127">Aucun des deux documents indexés ne contient les termes, nous avons donc la sortie suivante à partir du premier `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="fc411-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="fc411-128">Activation des synonymes</span><span class="sxs-lookup"><span data-stu-id="fc411-128">Enable synonyms</span></span>

<span data-ttu-id="fc411-129">L’activation des synonymes est un processus en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="fc411-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="fc411-130">Tout d’abord nous définissons et chargeons les règles de synonymes, puis nous configurons les champs pour les utiliser.</span><span class="sxs-lookup"><span data-stu-id="fc411-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="fc411-131">Le processus est décrit dans `UploadSynonyms` et `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="fc411-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="fc411-132">Ajoutez une carte de synonymes à votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fc411-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="fc411-133">Dans `UploadSynonyms`, nous définissons quatre règles de notre carte de synonymes « desc-synonymmap » et effectuons le téléchargement vers le service.</span><span class="sxs-lookup"><span data-stu-id="fc411-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="fc411-134">Une carte de synonymes doit être conforme au format `solr` standard Open Source.</span><span class="sxs-lookup"><span data-stu-id="fc411-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="fc411-135">Le format est expliqué dans [Synonyms in Azure Search (Synonymes dans la Recherche Azure)](search-synonyms.md) sous la section `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="fc411-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="fc411-136">Configurez les champs pouvant faire l’objet d’une recherche pour utiliser la carte de synonymes dans la définition d’index.</span><span class="sxs-lookup"><span data-stu-id="fc411-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="fc411-137">Dans `EnableSynonymsInHotelsIndex`, nous activons les synonymes sur deux champs `category` et `tags` en affectant à la propriété `synonymMaps` le nom de la carte de synonymes qui vient d’être téléchargée.</span><span class="sxs-lookup"><span data-stu-id="fc411-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="fc411-138">Lorsque vous ajoutez une carte de synonymes, les reconstructions d’index ne sont pas requises.</span><span class="sxs-lookup"><span data-stu-id="fc411-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="fc411-139">Vous pouvez ajouter une carte de synonymes à votre service, puis modifier les définitions de champ existantes dans n’importe quel index pour utiliser la nouvelle carte de synonymes.</span><span class="sxs-lookup"><span data-stu-id="fc411-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="fc411-140">L’ajout de nouveaux attributs n’a aucun impact sur la disponibilité de l’index.</span><span class="sxs-lookup"><span data-stu-id="fc411-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="fc411-141">Il en va de même pour la désactivation de synonymes pour un champ.</span><span class="sxs-lookup"><span data-stu-id="fc411-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="fc411-142">Vous pouvez simplement affecter à la propriété `synonymMaps` une liste vide.</span><span class="sxs-lookup"><span data-stu-id="fc411-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="fc411-143">Requêtes « après »</span><span class="sxs-lookup"><span data-stu-id="fc411-143">"After" queries</span></span>

<span data-ttu-id="fc411-144">Une fois que la carte de synonymes est téléchargée et l’index mis à jour pour utiliser la carte de synonymes, le deuxième appel `RunQueriesWithNonExistentTermsInIndex` affiche les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fc411-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="fc411-145">La première requête trouve le document à partir de la règle `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="fc411-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="fc411-146">La deuxième requête étend la recherche à l’aide de `internet,wifi` et la troisième avec à la fois `hotel, motel` et `economy,inexpensive=>budget` pour trouver les documents en correspondance.</span><span class="sxs-lookup"><span data-stu-id="fc411-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="fc411-147">L’ajout de synonymes modifie complètement l’expérience de recherche.</span><span class="sxs-lookup"><span data-stu-id="fc411-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="fc411-148">Dans ce didacticiel, les requêtes d’origine n’ont pas pu retourner de résultats significatifs même si les documents dans notre index étaient pertinents.</span><span class="sxs-lookup"><span data-stu-id="fc411-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="fc411-149">En activant les synonymes, nous pouvons développer un index pour inclure les termes communément utilisés, sans modification de données sous-jacentes dans l’index.</span><span class="sxs-lookup"><span data-stu-id="fc411-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="fc411-150">Code source de l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="fc411-150">Sample application source code</span></span>
<span data-ttu-id="fc411-151">Vous trouverez le code source complet de l’exemple d’application utilisé dans cette procédure sur [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="fc411-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc411-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc411-152">Next steps</span></span>

* <span data-ttu-id="fc411-153">Consultez [How to use synonyms in Azure Search (Comment utiliser les synonymes dans la Recherche Azure)](search-synonyms.md).</span><span class="sxs-lookup"><span data-stu-id="fc411-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="fc411-154">Consultez la [documentation sur l’API REST de synonymes](https://aka.ms/rgm6rq).</span><span class="sxs-lookup"><span data-stu-id="fc411-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="fc411-155">Parcourez les références relatives au [Kit de développement logiciel (SDK) .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et à [l’API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="fc411-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
