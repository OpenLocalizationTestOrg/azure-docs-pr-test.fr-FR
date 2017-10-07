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
# <a name="how-toouse-azure-search-from-a-net-application"></a>Comment effectuer une recherche toouse Azure à partir d’une Application .NET
Cet article est un tooget de procédure pas à pas vous opérationnel avec hello [Azure Search .NET SDK](https://aka.ms/search-sdk). Vous pouvez utiliser hello .NET SDK tooimplement une riche expérience de recherche dans votre application à l’aide d’Azure Search.

## <a name="whats-in-hello-azure-search-sdk"></a>Nouveautés dans hello recherche Azure SDK
Hello SDK se compose d’une bibliothèque cliente, `Microsoft.Azure.Search`. Il vous toomanage votre index, les sources de données et les indexeurs, ainsi que télécharger et gérer des documents et exécuter des requêtes, le tout sans avoir toodeal avec les détails de hello de HTTP et JSON.

bibliothèque cliente de Hello définit des classes telles que `Index`, `Field`, et `Document`, ainsi que des opérations telles que `Indexes.Create` et `Documents.Search` sur hello `SearchServiceClient` et `SearchIndexClient` classes. Ces classes sont organisés en hello suivant des espaces de noms :

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models.](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

version actuelle de Hello Hello Azure Search .NET SDK est désormais disponible. Si vous souhaitez que les commentaires tooprovide pour nous tooincorporate dans la version suivante de hello, visitez notre [page de commentaires](https://feedback.azure.com/forums/263029-azure-search/).

Hello .NET SDK prend en charge la version `2016-09-01` Hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/). Cette version inclut désormais la prise en charge des analyseurs personnalisés et de l’indexeur de table Azure et des objets Blob Azure. Afficher un aperçu des fonctionnalités qui sont *pas* dans le cadre de cette version, telles que la prise en charge pour l’indexation de fichiers JSON et les volumes partagés de cluster, sont dans [aperçu](search-api-2015-02-28-preview.md) et disponibles via hello plus anciens [2.0 préversion de hello .NET SDK ](https://aka.ms/search-sdk-preview).

Ce Kit de développement logiciel (SDK) ne prend pas en charge les [opérations de gestion](https://docs.microsoft.com/rest/api/searchmanagement/) telles que la création et la mise à l’échelle des services de recherche, ainsi que la gestion des clés API. Si vous devez toomanage vos ressources de recherche à partir d’une application .NET, vous pouvez utiliser hello [SDK de gestion Azure Search .NET](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Mise à niveau de la version la plus récente du Kit de développement logiciel de hello toohello
Si vous utilisez déjà une version antérieure de hello Azure Search .NET SDK et que vous souhaitez tooupgrade toohello version nouvelle disponible de manière générale, [cet article](search-dotnet-sdk-migration.md) explique comment.

## <a name="requirements-for-hello-sdk"></a>Configuration requise pour le Kit de développement logiciel de hello
1. Visual Studio 2017.
2. Votre propre service Azure Search. Bonjour toouse de l’ordre SDK, vous devez nom hello de votre service et une ou plusieurs clés API. [Créer un service dans le portail de hello](search-create-service-portal.md) vous aidera tout au long de ces étapes.
3. Télécharger hello Azure Search .NET SDK [package NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) à l’aide de « Gérer les Packages NuGet » dans Visual Studio. Nom du package hello simplement rechercher `Microsoft.Azure.Search` sur NuGet.org.

Bonjour Azure Search .NET SDK prend en charge les applications qui ciblent hello .NET Framework 4.6 et .NET Core.

## <a name="core-scenarios"></a>Principaux scénarios
Il existe plusieurs choses que vous aurez besoin de toodo dans votre application de recherche. Dans ce didacticiel, nous aborderons ces principaux scénarios :

* Création d'un index
* Remplissage d’index hello avec des documents
* Recherche de documents à l'aide de filtres et de la recherche en texte intégral

exemple de code Hello qui suit illustre chacune d’elles. Vous pouvez toouse libre des extraits de code hello dans votre propre application.

### <a name="overview"></a>Vue d'ensemble
Hello exemple d’application nous allons nous intéresser à crée un index nommé « hôtels », le remplit avec des documents, puis exécute des requêtes de recherche. Voici le programme principal hello, montrant hello flux global :

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
> Vous pouvez trouver le code source complet de l’exemple d’application hello utilisé dans cette procédure pas à pas sur hello [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Nous allons le détailler, étape par étape. Tout d’abord, nous devons toocreate un nouveau `SearchServiceClient`. Cet objet vous permet de toomanage index. Dans l’ordre tooconstruct une, vous devez tooprovide le nom de votre service Azure Search ainsi que d’une clé d’API d’administration. Vous pouvez entrer ces informations dans hello `appsettings.json` fichier Hello [exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

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
> Si vous fournissez une clé incorrecte (par exemple, une clé de requête où une clé d’administration a été requise), hello `SearchServiceClient` lèvera une `CloudException` avec hello « Interdit » du message erreur hello première fois que vous appelez une méthode d’opération, tel que `Indexes.Create`. Si cela produit tooyou, vérifiez la clé d’API.
> 
> 

Hello quelques lignes appellent méthodes toocreate un index nommé « hôtels », suppression de tout d’abord s’il existe déjà. Nous étudierons ces méthodes un peu plus tard.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Ensuite, les index hello doit toobe rempli. toodo, nous devons un `SearchIndexClient`. Il existe deux tooobtain manières une : en construction, ou en appelant `Indexes.GetClient` sur hello `SearchServiceClient`. Nous utilisons hello ce dernier pour des raisons pratiques.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche. `Indexes.GetClient`est pratique pour remplir un index, car vous épargne hello des difficultés à fournir un autre `SearchCredentials`. Pour ce faire, il en passant la clé d’administration hello que hello utilisé toocreate vous `SearchServiceClient` toohello nouveau `SearchIndexClient`. Toutefois, dans la partie hello de votre application qui exécute des requêtes, il est mieux toocreate hello `SearchIndexClient` directement afin que vous pouvez passer d’une clé de requête au lieu d’une clé d’administration. Cela est conforme au principe hello du privilège minimum et permettra de toomake votre application plus sécurisée. Pour en savoir plus sur les clés d’administration et les clés de requête, cliquez [ici](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Maintenant que nous avons un `SearchIndexClient`, nous pouvons remplir des index de hello. Cette opération est exécutée par une autre méthode que nous étudierons ultérieurement.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Enfin, nous exécuter des requêtes de recherche et afficher les résultats de hello. Cette fois-ci, nous utilisons un `SearchIndexClient` différent :

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Nous allons étudier hello `RunQueries` méthode ultérieurement. Voici hello de toocreate code hello nouveau `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Cette fois, nous utilisons une clé de requête, car nous n’avez pas besoin d’un accès en écriture toohello index. Vous pouvez entrer ces informations dans hello `appsettings.json` fichier Hello [exemple d’application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Si vous exécutez cette application avec un nom de service valide et les clés API, la sortie de hello doit ressembler à ceci :

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

le code source complet de l’application hello Hello est fourni à la fin de hello de cet article.

Ensuite, nous allons étudier chacune des méthodes hello appelées par `Main`.

### <a name="creating-an-index"></a>Création d'un index
Après avoir créé un `SearchServiceClient`, présent hello `Main` est est index des hôtels « delete hello » s’il existe déjà. Qui est effectuée par hello suivant de méthode :

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Cette méthode utilise hello donné `SearchServiceClient` toocheck s’il existe des index de hello et si tel est le cas, supprimez-le.

> [!NOTE]
> exemple de code Hello dans cet article utilise des méthodes synchrones de hello Hello Azure Search .NET SDK pour plus de simplicité. Nous vous recommandons d’utiliser les méthodes asynchrones hello dans vos propres applications tookeep les évolutives et réactives. Par exemple, Bonjour méthode ci-dessus, vous pouvez utiliser `ExistsAsync` et `DeleteAsync` au lieu de `Exists` et `Delete`.
> 
> 

Ensuite, `Main` crée un index « hotels » en appelant cette méthode :

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

Cette méthode crée un nouveau `Index` objet avec une liste de `Field` objets qui définit le schéma de hello du nouvel index de hello. Chaque champ a un nom, un type de données et plusieurs attributs qui définissent son comportement de recherche. Hello `FieldBuilder` classe utilise réflexion toocreate une liste de `Field` objets pour les index hello en examinant hello propriétés publiques et les attributs de hello donné `Hotel` classe de modèle. Nous allons étudier hello `Hotel` classe ultérieurement.

> [!NOTE]
> Vous pouvez toujours créer la liste des hello `Field` objets directement au lieu d’utiliser `FieldBuilder` si nécessaire. Par exemple, vous ne souhaitez pas toouse une classe de modèle ou vous devrez peut-être toouse une classe de modèle existante que vous ne souhaitez pas toomodify en ajoutant des attributs.
>
> 

En outre toofields, vous pouvez également ajouter les profils de calcul de score, générateurs de suggestions ou CORS options toohello Index (omis à partir de l’exemple hello par souci de concision). Vous trouverez plus d’informations sur l’objet d’Index hello et ses parties constituantes Bonjour [référence SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), ainsi que dans hello [référence d’API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Remplissage d’index de hello
étape suivante Hello `Main` est toopopulate hello nouvellement créés par index. Cette opération est effectuée dans hello suivant de méthode :

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

Cette méthode présente quatre parties. Hello crée d’abord un tableau de `Hotel` les objets qui serviront de notre index toohello de tooupload des données d’entrée. Ces données sont codées en dur pour plus de simplicité. Dans votre application, vos données seront probablement issues d'une source de données externe, comme une base de données SQL.

deuxième partie de Hello crée un `IndexBatch` contenant des documents de hello. Vous spécifiez hello opération tooapply toohello lot au moment de sa création, dans ce cas en appelant l’hello `IndexBatch.Upload`. Hello lot est alors téléchargé toohello Azure Search index par hello `Documents.Index` (méthode).

> [!NOTE]
> Dans cet exemple, nous allons simplement charger les documents. Si vous souhaitiez toomerge change dans des documents existants ou supprimer les documents, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, ou `IndexBatch.Delete` à la place. Vous pouvez également combiner plusieurs opérations dans un lot unique en appelant `IndexBatch.New`, qui accepte une collection de `IndexAction` objets, chacun d’eux indique une opération spécifique sur un document à Azure Search tooperform. Vous pouvez créer chaque `IndexAction` avec son propre opération en appelant méthode correspondante hello comme `IndexAction.Merge`, `IndexAction.Upload`, et ainsi de suite.
> 
> 

Hello troisième partie de cette méthode est un bloc catch qui gère un cas d’erreur importants pour l’indexation. Si votre service Azure Search échoue tooindex hello certains documents dans un lot de hello, un `IndexBatchException` est levée par `Documents.Index`. Cela peut se produire si vous indexez des documents lorsque votre service est surchargé. **Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.** Vous pouvez retarder et réessayez d’indexation des documents hello ayant échoué, ou vous pouvez ouvrir une session et continuer comme l’exemple hello réalise, ou vous pouvez faire quelque chose d’autre selon les exigences de cohérence de données de votre application.

> [!NOTE]
> Vous pouvez utiliser hello `FindFailedActionsToRetry` tooconstruct méthode un nouveau lot contenant hello uniquement les actions qui ont échoué dans un appel précédent trop`Index`. méthode Hello est documenté [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) et qu’il existe une présentation de la façon dont le tooproperly utilisent [sur StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Enfin, hello `UploadDocuments` des délais de méthode pour les deux secondes. L’indexation se produit à l’en mode asynchrone dans votre service Azure Search, par conséquent, exemple d’application hello doit toowait un tooensure peu de temps que les documents hello sont disponibles pour la recherche. Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.

#### <a name="how-hello-net-sdk-handles-documents"></a>Comment hello .NET SDK traite les documents
Vous vous demandez peut-être comment hello Azure Search .NET SDK est instances tooupload en mesure d’une classe définie par l’utilisateur comme `Hotel` toohello index. toohelp répondre à cette question, examinons hello `Hotel` classe :

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

Hello première toonotice est que chaque propriété publique `Hotel` correspond tooa champ dans la définition de l’index hello, mais avec une différence essentielle : hello le nom de chaque champ commence par une lettre minuscule (« casse mixte »), tandis que nom hello chaque public propriété de `Hotel` commence par une lettre majuscule (« casse Pascal »). Il s’agit d’un scénario courant dans les applications .NET d’effectuer une liaison de données où le schéma cible hello est contrôle hello en dehors du développeur de l’application hello. Au lieu de .NET de hello tooviolate affectation de noms en rendant la propriété noms casse mixte, vous pouvez indiquer à hello SDK toomap hello noms toocamel en cas de propriété automatiquement avec hello `[SerializePropertyNamesAsCamelCase]` attribut.

> [!NOTE]
> Bonjour Azure Search .NET SDK utilise hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de bibliothèque et de désérialiser vos tooand d’objets de modèle personnalisé à partir de JSON. Vous pouvez personnaliser cette sérialisation si nécessaire. Pour plus d’informations, consultez [Sérialisation personnalisée avec JSON.NET](#JsonDotNet).
> 
> 

Hello deuxième chose toonotice sont les attributs hello comme `IsFilterable`, `IsSearchable`, `Key`, et `Analyzer` qui décorent chaque propriété publique. Ces attributs sont mappés directement toohello [des attributs correspondants de l’index de recherche de Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Hello `FieldBuilder` classe utilise ces définitions de champ tooconstruct pour les index hello.

Hello tiers le plus important de hello `Hotel` classe sont les types de données hello des propriétés publiques de hello. les types .NET Hello de ces propriétés mappent les types de champ équivalent tootheir dans la définition de l’index hello. Par exemple, hello `Category` propriété de chaîne mappe toohello `category` champ, ce qui est de type `Edm.String`. Il existe des mappages de type similaire entre `bool?` et `Edm.Boolean`, `DateTimeOffset?` et `Edm.DateTimeOffset`, etc. hello des règles spécifiques pour le mappage de type hello sont documentées par hello `Documents.Get` méthode Bonjour [Azure Search .NET SDK référence](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Hello `FieldBuilder` classe prend en charge ce mappage pour vous, mais il peut toujours être toounderstand utile en cas de besoin tootroubleshoot les problèmes de sérialisation.

Cette possibilité toouse vos propres classes en tant que documents fonctionne dans les deux directions ; Vous pouvez également récupérer les résultats de la recherche et hello SDK automatiquement désérialiser les tooa type de votre choix, comme nous le verrons dans la section suivante de hello.

> [!NOTE]
> Bonjour Azure Search .NET SDK prend également en charge les documents typées dynamiquement à l’aide de hello `Document` (classe), qui est un mappage de clé/valeur noms toofield des valeurs de champ. Cela est utile dans les scénarios où vous ne connaissez pas schéma d’index hello au moment du design ou dans lesquelles il serait pas pratique toobind toospecific de classes de modèle. Toutes les méthodes hello hello SDK qui traitent des documents ont des surcharges qui fonctionnent avec hello `Document` classe, ainsi que les surcharges fortement typée qui prennent un paramètre de type générique. Uniquement les hello ce dernier sont utilisées dans l’exemple de code hello dans ce didacticiel. Hello `Document` hérite de la classe `Dictionary<string, object>`. Vous trouverez plus d’informations [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Pourquoi utiliser des types de données Nullable**

Lorsque vous créez votre propre index Azure Search de modèle classes toomap tooan, nous vous recommandons de déclarer des propriétés de types valeur tels que `bool` et `int` toobe nullable (par exemple, `bool?` au lieu de `bool`). Si vous utilisez une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index. Hello SDK, ni hello service Azure Search aidera à vous tooenforce cela.

Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `Edm.Int32`. Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search). Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Sérialisation personnalisée avec JSON.NET
Hello SDK utilise JSON.NET pour sérialiser et désérialiser des documents. Vous pouvez personnaliser la sérialisation et la désérialisation si nécessaire en définissant votre propre `JsonConverter` ou `IContractResolver` (voir hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) pour plus d’informations). Cela peut être utile lorsque vous souhaitez tooadapt une classe de modèle existante à partir de votre application pour une utilisation avec Azure Search et d’autres scénarios plus avancés. Par exemple, avec la sérialisation personnalisée, vous pouvez :

* Incluez ou exclure certaines propriétés de votre classe de modèle dans le stockage en tant que champs de document.
* Mappez des noms de propriété dans le code et des noms de champ de votre index.
* Créer des attributs personnalisés qui peuvent être utilisés pour le mappage des champs de propriétés toodocument.

Vous trouverez des exemples d’implémentation de sérialisation personnalisée dans les tests unitaires de hello pour hello Azure Search .NET SDK sur GitHub. [Ce dossier](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) est un bon point de départ. Il contient des classes qui sont utilisées par les tests de sérialisation personnalisée hello.

### <a name="searching-for-documents-in-hello-index"></a>Recherche de documents dans l’index de hello
dernière étape de Hello dans l’exemple d’application hello est toosearch pour certains documents dans l’index de hello. Hello méthode effectue cette opération :

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

Chaque fois qu’elle exécute une requête, cette méthode crée tout d’abord un objet `SearchParameters`. Il s’agit de toospecify utilisé des options supplémentaires pour la requête hello telles que le tri, le filtrage, la pagination et des facettes. Dans cette méthode, nous allons définir hello `Filter`, `Select`, `OrderBy`, et `Top` propriété pour des requêtes différentes. Tous les hello `SearchParameters` propriétés sont documentées [ici](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

étape suivante de Hello est tooactually exécuter la requête de recherche hello. Cette opération est effectuée à l’aide de hello `Documents.Search` (méthode). Pour chaque requête, nous passons hello recherche texte toouse sous forme de chaîne (ou `"*"` si aucun texte de recherche), ainsi que hello créés précédemment des paramètres de recherche. Nous avons également de spécifier `Hotel` en tant que paramètre de type hello `Documents.Search`, ce qui indique à des documents toodeserialize hello SDK dans les résultats de recherche hello dans des objets de type `Hotel`.

> [!NOTE]
> Vous trouverez plus d’informations sur la syntaxe d’expression de requête recherche hello [ici](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Enfin, après chaque requête cette méthode effectue une itération dans toutes les correspondances hello dans les résultats de recherche hello, l’impression de chaque console toohello de document :

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

Jetons un œil plus proche à chacune des requêtes de hello à son tour. Voici la première requête hello code tooexecute hello :

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

Dans ce cas, nous recherchons hôtels qui hello mot « budget », et nous souhaitons tooget uniquement hello hôtel noms, tel que spécifié par hello `Select` paramètre. Voici les résultats hello :

    Name: Roach Motel

Ensuite, nous souhaitez hôtels de hello toofind avec un taux nocturne de moins de 150 $ et retourne uniquement l’ID d’hôtel hello et description :

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

Cette requête utilise un OData `$filter` expression, `baseRate lt 150`, documents de hello toofilter dans les index hello. Vous trouverez plus d’informations sur hello syntaxe OData prenant en charge Azure Search [ici](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Voici des résultats de requête de hello hello :

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

Ensuite, nous souhaitons toofind hello supérieur deux hôtels qui ont été rénovés plus récemment et affichent le nom de l’hôtel hello et de la dernière date de rénovation. Voici le code de hello : 

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

Dans ce cas, nous utilisons à nouveau hello de toospecify syntaxe OData `OrderBy` paramètre en tant que `lastRenovationDate desc`. Nous définissons également `Top` too2 tooensure nous obtenir uniquement des documents des deux premiers hello. Comme précédemment, nous avons défini `Select` toospecify les champs qui doivent être retournés.

Voici les résultats hello :

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Enfin, nous souhaitons toofind tous les hôtels qui hello mot « motel » :

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

Voici les résultats de hello, qui incluent tous les champs dans la mesure où nous ne spécifiait pas hello `Select` propriété :

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Cette étape achève le didacticiel de hello, mais ne pas vous arrêter là. **Étapes suivantes** fournit des ressources supplémentaires pour en apprendre davantage sur Azure Search.

## <a name="next-steps"></a>Étapes suivantes
* Parcourir les références hello pour hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) et [API REST](https://docs.microsoft.com/rest/api/searchservice/).
* Approfondissez vos connaissances grâce aux [vidéos et autres exemples et didacticiels](search-video-demo-tutorial-list.md).
* Révision [conventions de dénomination](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello modalités d’affectation de noms différents objets.
* Faites connaissance avec les [types de données pris en charge](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) par Azure Search.
