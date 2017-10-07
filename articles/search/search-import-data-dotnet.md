---
title: "AAA « télécharger des données (.NET - Azure Search) | Documents Microsoft »"
description: "Découvrez comment index tooupload de tooan des données à l’aide d’Azure Search hello du SDK .NET."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>À l’aide de téléchargement données tooAzure recherche hello .NET SDK
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Cet article vous indiquent comment toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport les données dans un index Azure Search.

Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md). Cet article suppose également que vous avez déjà créé un `SearchServiceClient` de l’objet, comme indiqué dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Tous les exemples de code figurant dans cet article sont écrits en C#. Vous pouvez trouver le code source complet hello [sur GitHub](http://aka.ms/search-dotnet-howto). Vous pouvez également lire sur hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) pour une présentation plus détaillée de l’exemple de code hello.

Dans les documents de toopush commande dans votre index à l’aide de hello .NET SDK, vous devez :

1. Créer un `SearchIndexClient` objet tooconnect tooyour index de recherche.
2. Créer un `IndexBatch` contenant hello documents toobe ajouté, modifié ou supprimé.
3. Appelez hello `Documents.Index` méthode de votre `SearchIndexClient` toosend hello `IndexBatch` tooyour les index de recherche.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Créez une instance de hello SearchIndexClient classe
données tooimport votre index à l’aide de hello Azure Search .NET SDK, vous devez toocreate une instance de hello `SearchIndexClient` classe. Vous pouvez construire cette instance vous-même, mais il plus facile si vous avez déjà un `SearchServiceClient` instance toocall son `Indexes.GetClient` (méthode). Par exemple, voici comment obtenir un `SearchIndexClient` pour les index hello nommé « hôtels » à partir d’un `SearchServiceClient` nommé `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche. `Indexes.GetClient`est pratique pour remplir un index, car vous épargne hello des difficultés à fournir un autre `SearchCredentials`. Pour ce faire, il en passant la clé d’administration hello que hello utilisé toocreate vous `SearchServiceClient` toohello nouveau `SearchIndexClient`. Toutefois, dans la partie hello de votre application qui exécute des requêtes, il est mieux toocreate hello `SearchIndexClient` directement afin que vous pouvez passer d’une clé de requête au lieu d’une clé d’administration. Cela est cohérent avec hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege) et vous aide à toomake votre application plus sécurisée. Vous trouverez plus d’informations sur les clés d’administration et les clés de requête Bonjour [référence d’API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` a une propriété `Documents`. Cette propriété fournit toutes les méthodes de hello que vous devez tooadd, modifier, supprimer ou interroger des documents dans votre index.

## <a name="decide-which-indexing-action-toouse"></a>Décidez quels toouse action d’indexation
données de tooimport à l’aide de hello .NET SDK, vous devez toopackage vos données dans un `IndexBatch` objet. Un `IndexBatch` encapsule une collection de `IndexAction` objets, chacun d’eux contenant un document et une propriété qui indique quel tooperform action à Azure Search sur ce document (téléchargement, fusionner, supprimer, etc.). En fonction de hello ci-dessous les actions que vous choisissez, uniquement certains champs doivent être inclus pour chaque document :

| Action | Description | Champs requis pour chaque document | Remarques |
| --- | --- | --- | --- |
| `Upload` |Un `Upload` action est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |Lors de la mise à jour/remplacement d’un document existant, un champ qui n’est pas spécifié dans la demande hello aura son champ défini trop`null`. Cela se produit même lorsque hello a été défini précédemment tooa nulle. |
| `Merge` |Mises à jour existant de document avec hello spécifié des champs. Si le document de hello n’existe pas dans l’index de hello, la fusion de hello échoue. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello. Cela inclut les champs de type `DataType.Collection(DataType.String)`. Par exemple, si hello document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour `tags`, hello valeur finale de hello `tags` champ sera `["economy", "pool"]`. et non `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Cette action se comporte comme `Merge` si un document avec hello donné clé déjà existe dans les index hello. Si le document de hello n’existe pas, il se comporte comme `Upload` avec un nouveau document. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |- |
| `Delete` |Supprime l’index de hello de document spécifié de hello. |clé uniquement |Tous les champs que vous spécifiez d’autres que le champ de clé hello sera ignoré. Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `Merge` à la place et simplement définir explicitement les champs de hello toonull. |

Vous pouvez spécifier quelle action toouse avec hello plusieurs méthodes statiques de hello `IndexBatch` et `IndexAction` des classes, comme indiqué dans la section suivante de hello.

## <a name="construct-your-indexbatch"></a>Construire votre IndexBatch
Maintenant que vous savez quels tooperform actions sur vos documents, vous êtes prêt tooconstruct hello `IndexBatch`. Hello exemple ci-dessous montre comment toocreate un lot avec quelques actions différentes. Notez que notre exemple utilise une classe personnalisée appelée `Hotel` qui mappe le document tooa dans l’index de « hôtels » hello.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
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
            }),
        IndexAction.Upload(
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
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

Dans ce cas, nous utilisons `Upload`, `MergeOrUpload`, et `Delete` en tant que nos actions de recherche, tel que spécifié par les méthodes hello appelées sur hello `IndexAction` classe.

Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents. Notez la façon dont nous n’avait pas toospecify tous les champs de document possible hello lors de l’utilisation `MergeOrUpload` et comment nous spécifiée uniquement clé de document hello (`HotelId`) lors de l’utilisation `Delete`.

Notez également que vous ne pouvez inclure des documents de too1000 dans une seule demande d’indexation.

> [!NOTE]
> Dans cet exemple, nous appliquons documents toodifferent de différentes actions. Si vous souhaitiez tooperform hello les mêmes actions sur tous les documents dans un lot de hello, au lieu d’appeler `IndexBatch.New`, vous pouvez utiliser hello autres méthodes statiques de `IndexBatch`. Par exemple, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`. Ces méthodes prennent une collection de documents (objets de type `Hotel` dans cet exemple) à la place d’objets `IndexAction`.
> 
> 

## <a name="import-data-toohello-index"></a>Importation données toohello index
Maintenant que vous avez initialisé `IndexBatch` de l’objet, vous pouvez l’envoyer toohello index en appelant `Documents.Index` sur votre `SearchIndexClient` objet. Hello suivant montre l’exemple de comment toocall `Index`, ainsi que certaines étapes supplémentaires, vous devez tooperform :

```csharp
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
```

Hello de note `try` / `catch` entourant hello appel toohello `Index` (méthode). bloc catch de Hello gère un cas d’erreur importants pour l’indexation. Si votre service Azure Search échoue tooindex hello certains documents dans un lot de hello, un `IndexBatchException` est levée par `Documents.Index`. Cela peut se produire si vous indexez des documents lorsque votre service est surchargé. **Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.** Vous pouvez retarder et réessayez d’indexation des documents hello ayant échoué, ou vous pouvez ouvrir une session et continuer comme l’exemple hello réalise, ou vous pouvez faire quelque chose d’autre selon les exigences de cohérence de données de votre application.

Enfin, hello code dans l’exemple hello au-dessus des délais de deux secondes. L’indexation se produit à l’en mode asynchrone dans votre service Azure Search, par conséquent, exemple d’application hello doit toowait un tooensure peu de temps que les documents hello sont disponibles pour la recherche. Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Comment hello .NET SDK traite les documents
Vous vous demandez peut-être comment hello Azure Search .NET SDK est instances tooupload en mesure d’une classe définie par l’utilisateur comme `Hotel` toohello index. toohelp répondre à cette question, examinons hello `Hotel` (classe), qui mappe le schéma d’index toohello définie dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
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

    // ToString() method omitted for brevity...
}
```

Hello première toonotice est que chaque propriété publique `Hotel` correspond tooa champ dans la définition de l’index hello, mais avec une différence essentielle : hello le nom de chaque champ commence par une lettre minuscule (« casse mixte »), tandis que nom hello chaque public propriété de `Hotel` commence par une lettre majuscule (« casse Pascal »). Il s’agit d’un scénario courant dans les applications .NET d’effectuer une liaison de données où le schéma cible hello est contrôle hello en dehors du développeur de l’application hello. Au lieu de .NET de hello tooviolate affectation de noms en rendant la propriété noms casse mixte, vous pouvez indiquer à hello SDK toomap hello noms toocamel en cas de propriété automatiquement avec hello `[SerializePropertyNamesAsCamelCase]` attribut.

> [!NOTE]
> Bonjour Azure Search .NET SDK utilise hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de bibliothèque et de désérialiser vos tooand d’objets de modèle personnalisé à partir de JSON. Vous pouvez personnaliser cette sérialisation si nécessaire. Pour plus d’informations, consultez l’article [Sérialisation personnalisée avec JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Un exemple de cela est utilisation hello Hello `[JsonProperty]` attribut sur hello `DescriptionFr` propriété dans le code d’exemple hello ci-dessus.
> 
> 

Hello seconde le plus important de hello `Hotel` classe sont les types de données hello des propriétés publiques de hello. les types .NET Hello de ces propriétés mappent les types de champ équivalent tootheir dans la définition de l’index hello. Par exemple, hello `Category` propriété de chaîne mappe toohello `category` champ, ce qui est de type `DataType.String`. Il existe des mappages de type similaires entre `bool?` et `DataType.Boolean`, `DateTimeOffset?` et `DataType.DateTimeOffset`, etc. Hello des règles spécifiques pour le mappage de type hello sont documentées par hello `Documents.Get` méthode Bonjour [référence du Kit de développement .NET Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Cette possibilité toouse vos propres classes en tant que documents fonctionne dans les deux directions ; Vous pouvez également récupérer les résultats de la recherche et hello SDK automatiquement désérialiser les tooa type de votre choix, comme indiqué dans hello [l’article suivant](search-query-dotnet.md).

> [!NOTE]
> Bonjour Azure Search .NET SDK prend également en charge les documents typées dynamiquement à l’aide de hello `Document` (classe), qui est un mappage de clé/valeur noms toofield des valeurs de champ. Cela est utile dans les scénarios où vous ne connaissez pas schéma d’index hello au moment du design ou dans lesquelles il serait pas pratique toobind toospecific de classes de modèle. Toutes les méthodes hello hello SDK qui traitent des documents ont des surcharges qui fonctionnent avec hello `Document` classe, ainsi que les surcharges fortement typée qui prennent un paramètre de type générique. Uniquement les hello ce dernier sont utilisées dans l’exemple de code hello dans cet article.
> 
> 

**Pourquoi utiliser des types de données Nullable**

Lorsque vous créez votre propre index Azure Search de modèle classes toomap tooan, nous vous recommandons de déclarer des propriétés de types valeur tels que `bool` et `int` toobe nullable (par exemple, `bool?` au lieu de `bool`). Si vous utilisez une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index. Hello SDK, ni hello service Azure Search aidera à vous tooenforce cela.

Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `DataType.Int32`. Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search). Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.

## <a name="next-steps"></a>Étapes suivantes
Remplissage de l’index Azure Search, vous serez prêt toostart émission toosearch de requêtes pour les documents. Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .

