---
title: "aaaSynonyms afficher un aperçu de didacticiel dans Azure Search | Documents Microsoft"
description: "Ajouter des index tooan des fonctionnalités de visualisation hello synonymes dans Azure Search."
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
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="37668-103">Didacticiel C# des synonymes (version préliminaire) pour la Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="37668-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="37668-104">Synonymes développer une requête en mettant en correspondance sur les termes du contrat considéré comme toohello sémantiquement équivalentes d’entrée.</span><span class="sxs-lookup"><span data-stu-id="37668-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="37668-105">Vous pourriez par exemple, les documents de toomatch « car » contenant les termes du contrat de hello « automobile » ou « vehicle ».</span><span class="sxs-lookup"><span data-stu-id="37668-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="37668-106">Dans la Recherche Azure, les synonymes sont définis dans une *carte de synonymes*, via des *règles de mappage* qui associent des termes équivalents.</span><span class="sxs-lookup"><span data-stu-id="37668-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="37668-107">Vous pouvez créer plusieurs mappages de synonyme, les valider en tant qu’index tooany disponibles à l’échelle du service de ressource et ensuite référencer l’un toouse au niveau du champ hello.</span><span class="sxs-lookup"><span data-stu-id="37668-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="37668-108">Au moment de la requête, en outre toosearching un index, Azure Search effectue une recherche dans un mappage de synonyme, s’il est spécifié sur les champs utilisés dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="37668-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="37668-109">afficher un aperçu de synonymes Hello fonctionnalité n’est en cours et uniquement pris en charge dans hello API préliminaire la plus récente et les versions du Kit de développement logiciel (api-version = 2016-09-01-Preview, version SDK 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="37668-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="37668-110">Il n’existe aucune prise en charge sur le portail Azure pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="37668-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="37668-111">Les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.</span><span class="sxs-lookup"><span data-stu-id="37668-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37668-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37668-112">Prerequisites</span></span>

<span data-ttu-id="37668-113">Configuration requise du didacticiel hello suivants :</span><span class="sxs-lookup"><span data-stu-id="37668-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="37668-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37668-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="37668-115">Service Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="37668-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="37668-116">Version préliminaire de la bibliothèque Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="37668-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="37668-117">Comment effectuer une recherche toouse Azure à partir d’une Application .NET</span><span class="sxs-lookup"><span data-stu-id="37668-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="37668-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="37668-118">Overview</span></span>

<span data-ttu-id="37668-119">Avant et après les requêtes présentent la valeur hello de synonymes.</span><span class="sxs-lookup"><span data-stu-id="37668-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="37668-120">Dans ce didacticiel, nous utilisons un exemple d’application qui exécute des requêtes et retourne des résultats sur un index d’exemples.</span><span class="sxs-lookup"><span data-stu-id="37668-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="37668-121">exemple d’application Hello crée un petit index nommé « hôtels » renseignées avec les deux documents.</span><span class="sxs-lookup"><span data-stu-id="37668-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="37668-122">application Hello exécute des requêtes de recherche à l’aide de termes ou expressions qui n’apparaissent pas dans l’index de hello, Active la fonctionnalité de synonymes hello, puis problèmes hello à nouveau les mêmes recherches.</span><span class="sxs-lookup"><span data-stu-id="37668-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="37668-123">code Hello ci-dessous montre hello flux global.</span><span class="sxs-lookup"><span data-stu-id="37668-123">hello code below demonstrates hello overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="37668-124">Hello toocreate d’étapes et de remplir des index d’exemple hello sont expliquées dans [comment toouse Azure recherche à partir d’une Application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="37668-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="37668-125">Requêtes « avant »</span><span class="sxs-lookup"><span data-stu-id="37668-125">"Before" queries</span></span>

<span data-ttu-id="37668-126">Dans `RunQueriesWithNonExistentTermsInIndex`, nous lançons des requêtes de recherche avec « five star », « internet » et « economy AND hotel ».</span><span class="sxs-lookup"><span data-stu-id="37668-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="37668-127">Aucun des deux documents d’indexée hello contiennent des termes de hello, donc nous obtenons suivant hello tout d’abord la sortie à partir de hello `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="37668-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="37668-128">Activation des synonymes</span><span class="sxs-lookup"><span data-stu-id="37668-128">Enable synonyms</span></span>

<span data-ttu-id="37668-129">L’activation des synonymes est un processus en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="37668-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="37668-130">Nous avons tout d’abord définir et charger les règles de synonyme et puis configurez les champs toouse les.</span><span class="sxs-lookup"><span data-stu-id="37668-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="37668-131">processus de Hello est présenté dans `UploadSynonyms` et `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="37668-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="37668-132">Ajouter un service de recherche de synonyme carte tooyour.</span><span class="sxs-lookup"><span data-stu-id="37668-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="37668-133">Dans `UploadSynonyms`, nous définissons quatre règles notre Map synonyme 'desc-synonymmap' et que vous téléchargez toohello service.</span><span class="sxs-lookup"><span data-stu-id="37668-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="37668-134">Un mappage de synonyme doit être conforme standard d’open source toohello `solr` format.</span><span class="sxs-lookup"><span data-stu-id="37668-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="37668-135">format de Hello est expliquée dans [synonymes dans Azure Search](search-synonyms.md) section hello `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="37668-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="37668-136">Configurer le mappage de champs interrogeables toouse hello synonyme dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="37668-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="37668-137">Dans `EnableSynonymsInHotelsIndex`, nous allons activer les synonymes sur les deux champs `category` et `tags` en définissant un hello `synonymMaps` toohello nom de la propriété de hello téléchargé qui vient d’être carte de synonyme.</span><span class="sxs-lookup"><span data-stu-id="37668-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="37668-138">Lorsque vous ajoutez une carte de synonymes, les reconstructions d’index ne sont pas requises.</span><span class="sxs-lookup"><span data-stu-id="37668-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="37668-139">Vous pouvez ajouter un service de tooyour de carte de synonyme et ensuite modifier les définitions de champ existant dans n’importe quel index toouse hello nouveau synonyme mappage.</span><span class="sxs-lookup"><span data-stu-id="37668-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="37668-140">Ajout de Hello de nouveaux attributs n’a aucun impact sur la disponibilité de l’index.</span><span class="sxs-lookup"><span data-stu-id="37668-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="37668-141">Hello que même règle s’applique la désactivation des synonymes pour un champ.</span><span class="sxs-lookup"><span data-stu-id="37668-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="37668-142">Vous pouvez simplement affecter hello `synonymMaps` tooan Liste_Propriétés vide.</span><span class="sxs-lookup"><span data-stu-id="37668-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="37668-143">Requêtes « après »</span><span class="sxs-lookup"><span data-stu-id="37668-143">"After" queries</span></span>

<span data-ttu-id="37668-144">Une fois le mappage de synonyme hello est téléchargé et les index hello est carte de synonyme hello toouse mis à jour, hello deuxième `RunQueriesWithNonExistentTermsInIndex` appel extrait hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="37668-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="37668-145">Hello première requête recherche hello document à partir de la règle de hello `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="37668-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="37668-146">seconde Hello s’étend à l’aide de recherche hello `internet,wifi` et hello troisième à la fois `hotel, motel` et `economy,inexpensive=>budget` dans la recherche de documents de hello elles mises en correspondance.</span><span class="sxs-lookup"><span data-stu-id="37668-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="37668-147">Ajout de synonymes complètement modifie expérience de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="37668-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="37668-148">Dans ce didacticiel, les requêtes d’origine hello échec des résultats significatifs tooreturn même si les documents hello dans notre index ont été pertinentes.</span><span class="sxs-lookup"><span data-stu-id="37668-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="37668-149">En activant les synonymes, nous pouvons développer un tooinclude index conditions utilisation en commun, sans données toounderlying de modifications dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="37668-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="37668-150">Code source de l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="37668-150">Sample application source code</span></span>
<span data-ttu-id="37668-151">Vous pouvez trouver le code source complet de l’exemple d’application hello utilisé dans cette procédure pas à pas sur hello [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="37668-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="37668-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37668-152">Next steps</span></span>

* <span data-ttu-id="37668-153">Révision [comment toouse des synonymes dans Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="37668-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="37668-154">Consultez la [documentation sur l’API REST de synonymes](https://aka.ms/rgm6rq).</span><span class="sxs-lookup"><span data-stu-id="37668-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="37668-155">Parcourir les références hello pour hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="37668-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
