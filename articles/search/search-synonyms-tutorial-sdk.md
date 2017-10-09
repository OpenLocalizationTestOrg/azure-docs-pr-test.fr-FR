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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Didacticiel C# des synonymes (version préliminaire) pour la Recherche Azure

Synonymes développer une requête en mettant en correspondance sur les termes du contrat considéré comme toohello sémantiquement équivalentes d’entrée. Vous pourriez par exemple, les documents de toomatch « car » contenant les termes du contrat de hello « automobile » ou « vehicle ».

Dans la Recherche Azure, les synonymes sont définis dans une *carte de synonymes*, via des *règles de mappage* qui associent des termes équivalents. Vous pouvez créer plusieurs mappages de synonyme, les valider en tant qu’index tooany disponibles à l’échelle du service de ressource et ensuite référencer l’un toouse au niveau du champ hello. Au moment de la requête, en outre toosearching un index, Azure Search effectue une recherche dans un mappage de synonyme, s’il est spécifié sur les champs utilisés dans la requête de hello.

> [!NOTE]
> afficher un aperçu de synonymes Hello fonctionnalité n’est en cours et uniquement pris en charge dans hello API préliminaire la plus récente et les versions du Kit de développement logiciel (api-version = 2016-09-01-Preview, version SDK 4.x-preview). Il n’existe aucune prise en charge sur le portail Azure pour l’instant. Les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.

## <a name="prerequisites"></a>Composants requis

Configuration requise du didacticiel hello suivants :

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Service Recherche Azure](search-create-service-portal.md)
* [Version préliminaire de la bibliothèque Microsoft.Azure.Search .NET](https://aka.ms/search-sdk-preview)
* [Comment effectuer une recherche toouse Azure à partir d’une Application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Vue d'ensemble

Avant et après les requêtes présentent la valeur hello de synonymes. Dans ce didacticiel, nous utilisons un exemple d’application qui exécute des requêtes et retourne des résultats sur un index d’exemples. exemple d’application Hello crée un petit index nommé « hôtels » renseignées avec les deux documents. application Hello exécute des requêtes de recherche à l’aide de termes ou expressions qui n’apparaissent pas dans l’index de hello, Active la fonctionnalité de synonymes hello, puis problèmes hello à nouveau les mêmes recherches. code Hello ci-dessous montre hello flux global.

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
Hello toocreate d’étapes et de remplir des index d’exemple hello sont expliquées dans [comment toouse Azure recherche à partir d’une Application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Requêtes « avant »

Dans `RunQueriesWithNonExistentTermsInIndex`, nous lançons des requêtes de recherche avec « five star », « internet » et « economy AND hotel ».
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
Aucun des deux documents d’indexée hello contiennent des termes de hello, donc nous obtenons suivant hello tout d’abord la sortie à partir de hello `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Activation des synonymes

L’activation des synonymes est un processus en deux étapes. Nous avons tout d’abord définir et charger les règles de synonyme et puis configurez les champs toouse les. processus de Hello est présenté dans `UploadSynonyms` et `EnableSynonymsInHotelsIndex`.

1. Ajouter un service de recherche de synonyme carte tooyour. Dans `UploadSynonyms`, nous définissons quatre règles notre Map synonyme 'desc-synonymmap' et que vous téléchargez toohello service.
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
Un mappage de synonyme doit être conforme standard d’open source toohello `solr` format. format de Hello est expliquée dans [synonymes dans Azure Search](search-synonyms.md) section hello `Apache Solr synonym format`.

2. Configurer le mappage de champs interrogeables toouse hello synonyme dans la définition de l’index hello. Dans `EnableSynonymsInHotelsIndex`, nous allons activer les synonymes sur les deux champs `category` et `tags` en définissant un hello `synonymMaps` toohello nom de la propriété de hello téléchargé qui vient d’être carte de synonyme.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Lorsque vous ajoutez une carte de synonymes, les reconstructions d’index ne sont pas requises. Vous pouvez ajouter un service de tooyour de carte de synonyme et ensuite modifier les définitions de champ existant dans n’importe quel index toouse hello nouveau synonyme mappage. Ajout de Hello de nouveaux attributs n’a aucun impact sur la disponibilité de l’index. Hello que même règle s’applique la désactivation des synonymes pour un champ. Vous pouvez simplement affecter hello `synonymMaps` tooan Liste_Propriétés vide.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Requêtes « après »

Une fois le mappage de synonyme hello est téléchargé et les index hello est carte de synonyme hello toouse mis à jour, hello deuxième `RunQueriesWithNonExistentTermsInIndex` appel extrait hello qui suit :

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
Hello première requête recherche hello document à partir de la règle de hello `five star=>luxury`. seconde Hello s’étend à l’aide de recherche hello `internet,wifi` et hello troisième à la fois `hotel, motel` et `economy,inexpensive=>budget` dans la recherche de documents de hello elles mises en correspondance.

Ajout de synonymes complètement modifie expérience de recherche hello. Dans ce didacticiel, les requêtes d’origine hello échec des résultats significatifs tooreturn même si les documents hello dans notre index ont été pertinentes. En activant les synonymes, nous pouvons développer un tooinclude index conditions utilisation en commun, sans données toounderlying de modifications dans les index hello.

## <a name="sample-application-source-code"></a>Code source de l'exemple d'application
Vous pouvez trouver le code source complet de l’exemple d’application hello utilisé dans cette procédure pas à pas sur hello [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Étapes suivantes

* Révision [comment toouse des synonymes dans Azure Search](search-synonyms.md)
* Consultez la [documentation sur l’API REST de synonymes](https://aka.ms/rgm6rq).
* Parcourir les références hello pour hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et [API REST](https://docs.microsoft.com/rest/api/searchservice/).
