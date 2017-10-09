---
title: aaaUpgrading toohello Azure Search .NET SDK version 1.1 | Documents Microsoft
description: "La mise à niveau toohello Azure Search .NET SDK version 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>La mise à niveau toohello Azure Search .NET SDK version 3
Si vous utilisez une version préliminaire de la version 2.0 ou antérieure de hello [Azure Search .NET SDK](https://aka.ms/search-sdk), cet article va vous aider à mettre à niveau votre version de toouse application 3.

Pour une procédure pas à pas plus de hello SDK, y compris des exemples, consultez [comment toouse Azure recherche à partir d’une Application .NET](search-howto-dotnet-sdk.md).

Version 3 du hello Azure Search .NET SDK contient des modifications à partir de versions antérieures. Elles sont pour la plupart mineures, et donc, la modification de votre code devrait ne nécessiter que peu d’effort. Consultez [étapes tooupgrade](#UpgradeSteps) pour obtenir des instructions sur la façon de toochange votre code toouse hello nouvelle SDK version.

> [!NOTE]
> Si vous utilisez la version 1.0.2-preview ou antérieure, vous devez mettre à niveau tooversion 1.1 premier et, puis mettre à niveau tooversion 3. Consultez [annexe : étapes tooupgrade tooversion 1.1](#UpgradeStepsV1) pour obtenir des instructions.
>
> Votre instance du service Azure Search prend en charge plusieurs versions de l’API REST, y compris hello version la plus récente. Vous pouvez continuer toouse une version lorsqu’il n’est plus hello version la plus récente, mais nous vous recommandons de migrer votre code toouse hello dernière version. Lorsque vous utilisez l’API REST de hello, vous devez spécifier la version de l’API hello dans chaque demande via un paramètre de version de l’api hello. Lorsque vous utilisez hello .NET SDK, version hello Hello SDK que vous utilisez détermine hello correspond à la version de l’API REST de hello. Si vous utilisez un kit de développement plus anciens, vous pouvez continuer toorun que le code sans aucune modification même si le service de hello est mis à niveau toosupport une API la plus récente version.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Nouveautés de la version 3
Version 3 du Bonjour Azure Search .NET SDK cibles Bonjour dernière version disponible de hello API REST de Azure Search, spécifiquement 2016-09-01. Cela rend possible toouse nombreuses nouvelles fonctionnalités d’Azure Search à partir d’une application .NET, y compris hello suivantes :

* [Analyseurs personnalisés](https://aka.ms/customanalyzers)
* Prise en charge des indexeurs [Stockage Blob Azure](search-howto-indexing-azure-blob-storage.md) et [Stockage Table Azure](search-howto-indexing-azure-tables.md)
* Personnalisation des indexeurs avec les [mappages de champs](search-indexer-field-mappings.md)
* Prend en charge les ETags tooenable simultanées mise à jour sûre des index définitions, indexeurs et sources de données
* Prise en charge pour la création des définitions de champs d’index de façon déclarative à décoration de votre classe de modèle et à l’aide de nouveau hello `FieldBuilder` classe.
* Prise en charge de .NET Core et .NET Portable Profile 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Étapes tooupgrade
Tout d’abord, mettre à jour votre référence de NuGet pour `Microsoft.Azure.Search` soit hello Console du Gestionnaire de Package NuGet ou en cliquant sur vos références de projet et en sélectionnant « Gérer NuGet Packages... » dans Visual Studio.

Une fois que NuGet a téléchargé les nouveaux packages de hello et leurs dépendances, régénérez votre projet. En fonction de la structure de votre code, la recompilation peut réussir. Dans ce cas, vous êtes prêt toogo !

Si votre build échoue, vous devez voir une erreur de build hello suivante :

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

étape suivante de Hello est toofix cette erreur de build. Consultez [modifications avec rupture dans la version 3](#ListOfChanges) pour plus d’informations sur ce qui provoque l’erreur de hello et comment toofix il.

Vous pouvez voir la build supplémentaire avertissements liés tooobsolete méthodes ou propriétés. avertissements de Hello inclut des instructions sur le toouse à la place de hello fonctionnalité déconseillée. Par exemple, si votre application utilise hello `IndexingParameters.Base64EncodeKeys` propriété, vous devez obtenir un avertissement indiquant que`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Une fois que vous avez résolu toutes les erreurs de build, vous pouvez apporter des modifications tooyour application tootake tirer parti de nouvelle fonctionnalité si vous le souhaitez. Nouvelles fonctionnalités dans le Kit de développement logiciel de hello sont détaillées dans [quelles sont les nouveautés dans la version 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Dernières modifications dans la version 3
Il un petit nombre de modifications avec rupture dans la version 3 qui peuvent nécessiter de code modifie en outre toorebuilding votre application.

### <a name="indexesgetclient-return-type"></a>Type de retour Indexes.GetClient
Hello `Indexes.GetClient` méthode a un nouveau type de retour. Auparavant, elle retournait `SearchIndexClient`, mais il a été modifié trop`ISearchIndexClient` dans la version 2.0-preview et qui comporte des modification sur tooversion 3. Il s’agit de toosupport les clients qui souhaitent toomock hello `GetClient` méthode pour les tests unitaires en retournant une implémentation fictive du `ISearchIndexClient`.

#### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, type de données et d’autres ne sont plus toostrings implicitement convertible
Bonjour Azure Search .NET SDK qui dérivent de nombreux types `ExtensibleEnum`. Auparavant ces types étaient toutes implicitement convertible tootype `string`. Toutefois, un bogue a été détecté dans hello `Object.Equals` implémentation de ces classes et de correction bogue hello requis la désactivation de cette conversion implicite. Conversion explicite trop`string` est toujours autorisé.

#### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Membres obsolètes supprimés

Vous pouvez voir toomethods connexes des erreurs de build ou les propriétés qui ont été marquées comme obsolètes dans la version 2.0-version préliminaire et supprimées par la suite dans la version 3. Si vous rencontrez ces erreurs, voici comment tooresolve les :

- Si vous utilisiez ce constructeur : `ScoringParameter(string name, string value)`, remplacez-le par `ScoringParameter(string name, IEnumerable<string> values)`
- Si vous utilisiez hello `ScoringParameter.Value` propriété, utilisez hello `ScoringParameter.Values` propriété ou hello `ToString` méthode à la place.
- Si vous utilisiez hello `SearchRequestOptions.RequestId` propriété, utilisez hello `ClientRequestId` propriété à la place.

### <a name="removed-preview-features"></a>Fonctionnalités préliminaires supprimées

Si vous mettez à niveau à partir de la version 2.0-preview tooversion 3, n’oubliez pas que JSON et CSV de l’analyse de la prise en charge pour les indexeurs d’objet Blob a été supprimé, car ces fonctionnalités sont encore en version préliminaire. Plus précisément, hello suivant les méthodes de hello `IndexingParametersExtensions` classe ont été supprimées :

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Si votre application a une dépendance dure sur ces fonctionnalités, vous ne serez pas en mesure de tooupgrade tooversion 3 Hello Azure Search .NET SDK. Vous pouvez continuer d’aperçu toouse version 2.0. Mais n’oubliez pas que **nous déconseillons l’utilisation de Kits de développement logiciel en version préliminaire dans les applications de production**. Les fonctionnalités préliminaires servent uniquement à des fins d’évaluation et peuvent changer.

## <a name="conclusion"></a>Conclusion
Si vous avez besoin de plus de détails sur l’utilisation de hello Azure Search .NET SDK, consultez notre récemment mis à jour [procédures](search-howto-dotnet-sdk.md).

Nous apprécions vos commentaires sur le Kit de développement logiciel de hello. Si vous rencontrez des problèmes, vous pouvez tooask libre nous de l’aide sur hello [forum MSDN de recherche Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Si vous trouvez un bogue, vous pouvez signaler un problème Bonjour [référentiel GitHub de kit de développement logiciel Azure .NET](https://github.com/Azure/azure-sdk-for-net/issues). Assurez-vous que tooprefix le titre de votre problème avec « Search SDK : ».

Merci d’utiliser Azure Search !

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Annexe : Étapes tooupgrade tooversion 1.1
> [!NOTE]
> Cette section s’applique uniquement les toousers de hello Azure Search .NET SDK version 1.0.2-preview et antérieures.
> 
> 

Tout d’abord, mettre à jour votre référence de NuGet pour `Microsoft.Azure.Search` soit hello Console du Gestionnaire de Package NuGet ou en cliquant sur vos références de projet et en sélectionnant « Gérer NuGet Packages... » dans Visual Studio.

Une fois que NuGet a téléchargé les nouveaux packages de hello et leurs dépendances, régénérez votre projet.

Si vous étiez précédemment à l’aide de la version 1.0.0-preview, 1.0.1-preview ou 1.0.2-preview, génération de hello doit réussir et vous êtes prêt toogo !

Si vous utilisiez auparavant version 0.13.0-preview ou antérieure, vous devez voir erreurs hello suivante de build :

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

étape suivante de Hello est erreurs de build hello toofix un par un. La majorité nécessite la modification de certains noms de classes et des méthodes qui ont été renommés dans hello SDK. [Liste des dernières modifications dans la version 1.1](#ListOfChangesV1) répertorie ces changements de nom.

Si vous utilisez des classes personnalisées toomodel vos documents, et ces classes ont des propriétés de types primitifs non nullable (par exemple, `int` ou `bool` en c#), il existe un bogue dans la version 1.1 de hello du SDK hello dont vous devez être conscient. Consultez [Résolution des bogues dans la version 1.1](#BugFixesV1) pour plus de détails.

Enfin, une fois que vous avez résolu toutes les erreurs de build, vous pouvez apporter des modifications parti de tootake tooyour application des nouvelles fonctionnalités si vous le souhaitez.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Liste des dernières modifications dans la version 1.1
Hello liste suivante est classée par probabilité de hello que hello modification affecte votre code d’application.

#### <a name="indexbatch-and-indexaction-changes"></a>Modifications IndexBatch et IndexAction
`IndexBatch.Create`a été renommé trop`IndexBatch.New` et n’a plus un `params` argument. Vous pouvez utiliser `IndexBatch.New` pour les lots qui combinent différents types d’actions (fusions, suppressions, etc.). En outre, des nouvelles méthodes statiques pour la création de lots où toutes les actions de hello sont même hello : `Delete`, `Merge`, `MergeOrUpload`, et `Upload`.

`IndexAction` ne contient plus de constructeurs publics et ses propriétés sont immuables. Vous devez utiliser les méthodes statiques nouvelle hello pour la création d’actions à des fins différentes : `Delete`, `Merge`, `MergeOrUpload`, et `Upload`. `IndexAction.Create` a été supprimé. Si vous avez utilisé la surcharge qui accepte uniquement un document hello, assurez-vous que toouse `Upload` à la place.

##### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Si vous le souhaitez, vous pouvez encore simplifier il toothis :

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>Modifications IndexBatchException
Hello `IndexBatchException.IndexResponse` propriété a été renommée trop`IndexingResults`, et son type est désormais `IList<IndexingResult>`.

##### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Modifications des méthodes d’opération
Chaque opération Bonjour Azure Search .NET SDK est exposée comme un ensemble de surcharges de méthode pour les appelants synchrones et asynchrones. Hello factorisation de ces surcharges de méthode et les signatures a changé dans la version 1.1.

Par exemple, hello opération « Obtenir des statistiques d’Index » dans les versions antérieures du Kit de développement logiciel de hello exposées ces signatures :

Dans `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

Dans `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

les signatures de méthode Hello pour hello même opération dans la version 1.1 présentent cet aspect :

Dans `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

Dans `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Depuis la version 1.1, hello Azure Search .NET SDK organise les méthodes d’opération différemment :

* Les paramètres facultatifs sont désormais modélisés en tant que paramètres par défaut plutôt que les surcharges de méthode supplémentaires. Cela réduit nombre hello des surcharges de méthode, parfois considérablement.
* méthodes d’extension Hello masquent maintenant un grand nombre de hello superflus des détails HTTP à partir de l’appelant de hello. Par exemple, les versions antérieures du Kit de développement logiciel a retourné un objet de réponse avec un code d’état HTTP que vous pouvez souvent de hello n’a pas besoin des toocheck lever des méthodes d’opération `CloudException` sur n’importe quel code d’état qui indique une erreur. Bonjour des nouveaux objets de modèle de retourner simplement de méthodes d’extension, l’enregistrement vous hello des problèmes d’avoir toounwrap dans votre code.
* À l’inverse, hello interfaces principales maintenant exposent des méthodes qui vous permettent de mieux contrôler au niveau de hello HTTP si vous en avez besoin. Vous pouvez à présent passer dans personnalisé toobe d’en-têtes HTTP inclus dans les demandes et hello nouvelle `AzureOperationResponse<T>` retourner le type vous donne un accès direct toohello `HttpRequestMessage` et `HttpResponseMessage` pour l’opération de hello. `AzureOperationResponse`est défini dans hello `Microsoft.Rest.Azure` espace de noms et les remplace `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>Modifications ScoringParameters
Une nouvelle classe nommée `ScoringParameter` a été ajoutée dans hello dernier Kit de développement logiciel toomake plus faciles profils tooscoring de paramètres tooprovide dans une requête de recherche. Hello précédemment `ScoringProfiles` propriété Hello `SearchParameters` entré en tant que classe `IList<string>`; Maintenant qu’il est de type `IList<ScoringParameter>`.

##### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Vous pouvez le modifier toothis toofix toutes les erreurs de build : 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Modifications de modèles de classe
En raison de modifications de signature toohello décrites dans [changement de méthode d’opération](#OperationMethodChanges), de nombreuses classes Bonjour `Microsoft.Azure.Search.Models` espace de noms ont été renommés ou supprimés. Par exemple :

* `IndexDefinitionResponse` a été remplacé par `AzureOperationResponse<Index>`
* `DocumentSearchResponse`a été renommé en trop`DocumentSearchResult`
* `IndexResult`a été renommé en trop`IndexingResult`
* `Documents.Count()`Retourne un `long` avec le nombre de documents hello au lieu d’un`DocumentCountResponse`
* `IndexGetStatisticsResponse`a été renommé en trop`IndexGetStatisticsResult`
* `IndexListResponse`a été renommé en trop`IndexListResult`

toosummarize, `OperationResponse`-classes dérivées qui existaient uniquement les toowrap un objet de modèle ont été supprimés. Hello autres classes ont eu leur suffixe a été remplacée par `Response` trop`Result`.

##### <a name="example"></a>Exemple
Si votre code ressemble à ce qui suit :

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Les classes de réponse et IEnumerable
Une modification supplémentaire pouvant affecter votre code est que les classes de réponse contenant des collections ne sont plus mises en œuvre `IEnumerable<T>`. Au lieu de cela, vous pouvez accéder à propriété de collection hello directement. Par exemple, si votre code ressemble à ceci :

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Cas particulier pour les applications web
Si vous avez une application web qui sérialise `DocumentSearchResponse` directement les résultats de recherche de toosend toohello navigateur, vous devez toochange votre code ou les résultats hello ne sérialisent pas correctement. Par exemple, si votre code ressemble à ceci :

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Vous pouvez le modifier en obtenant hello `.Results` propriété du rendu de résultat hello recherche réponse toofix recherche :

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Vous aurez toolook pour ces cas dans votre code **hello compilateur pas vous avertit** car `JsonResult.Data` est de type `object`.

#### <a name="cloudexception-changes"></a>Modifications CloudException
Hello `CloudException` classe a été déplacé de hello `Hyak.Common` toohello de l’espace de noms `Microsoft.Rest.Azure` espace de noms. En outre, sa `Error` propriété a été renommée trop`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Modifications de SearchServiceClient et SearchIndexClient
Hello de type Hello `Credentials` propriété a été modifiée à partir de `SearchCredentials` tooits classe de base, `ServiceClientCredentials`. Si vous avez besoin de tooaccess hello `SearchCredentials` d’un `SearchIndexClient` ou `SearchServiceClient`, utilisez hello nouveau `SearchCredentials` propriété.

Dans les versions antérieures de hello SDK, `SearchServiceClient` et `SearchIndexClient` a des constructeurs qui ont eu une `HttpClient` paramètre. Ils ont été remplacés par des constructeurs qui incluent un élément `HttpClientHandler` et un tableau d’objets `DelegatingHandler`. Il est ainsi plus faciles tooinstall gestionnaires personnalisés toopre-traitent les requêtes HTTP si nécessaire.

Enfin, hello constructeurs qui ont eu une `Uri` et `SearchCredentials` ont été modifiés. Par exemple, si vous avez un code qui ressemble à c qui suit :

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Également Remarque informations d’identification de type hello Hello paramètre a changé trop`ServiceClientCredentials`. Il s’agit de tooaffect peu probable que votre code depuis `SearchCredentials` est dérivée de `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Transfert d’un ID de requête
Dans les versions antérieures de hello SDK, vous pouvez définir un ID de demande sur hello `SearchServiceClient` ou `SearchIndexClient` et il est inclus dans chaque toohello demande API REST. Cela est utile pour résoudre les problèmes avec votre service de recherche si vous avez besoin de toocontact. Toutefois, il est plus utile tooset un ID de demande unique pour chaque opération plutôt que toouse hello ID même pour toutes les opérations. Pour cette raison, hello `SetClientRequestId` méthodes de `SearchServiceClient` et `SearchIndexClient` ont été supprimés. Au lieu de cela, vous pouvez passer une méthode d’opération de demande ID tooeach via hello facultatif `SearchRequestOptions` paramètre.

> [!NOTE]
> Dans une prochaine version du Kit de développement logiciel de hello, nous allons ajouter un nouveau mécanisme permettant de définir globalement un ID de demande sur le client de hello objets qui est cohérent avec l’approche hello utilisé par d’autres kits de développement logiciel Azure.
> 
> 

#### <a name="example"></a>Exemple
Si vous avez un code qui ressemble à ce qui suit :

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Vous pouvez le modifier toothis toofix toutes les erreurs de build :

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Modifications de nom d’interface
noms d’interface Hello opération groupe ont toutes les toobe modifiées cohérentes avec les noms de propriété correspondants :

* Hello du type de `ISearchServiceClient.Indexes` a été renommé à partir de `IIndexOperations` trop`IIndexesOperations`.
* Hello du type de `ISearchServiceClient.Indexers` a été renommé à partir de `IIndexerOperations` trop`IIndexersOperations`.
* Hello du type de `ISearchServiceClient.DataSources` a été renommé à partir de `IDataSourceOperations` trop`IDataSourcesOperations`.
* Hello du type de `ISearchIndexClient.Documents` a été renommé à partir de `IDocumentOperations` trop`IDocumentsOperations`.

Cette modification est peu probable tooaffect votre code, sauf si vous avez créé des objets factices de ces interfaces à des fins de test.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Résolution des bogues dans la version 1.1
Il a été un bogue dans les versions antérieures de hello Azure Search .NET SDK de tooserialization concernant des classes de modèle personnalisé. bogue de Hello peut se produire si vous avez créé une classe de modèle personnalisé à la propriété d’un type valeur non nullable.

#### <a name="steps-tooreproduce"></a>Étapes tooreproduce
Créez une classe de modèle personnalisé avec une propriété de type avec valeur ne pouvant être définie sur null. Par exemple, ajoutez une propriété `UnitCount` publique de type `int` au lieu de `int?`.

Si vous indexez un document avec la valeur par défaut de hello de ce type (par exemple, 0 pour `int`), champ de hello sera null dans Azure Search. Si vous recherchez par la suite de ce document, hello `Search` appel lève `JsonSerializationException` signale qu’il ne peut pas convertir que `null` trop`int`.

En outre, les filtres peuvent ne pas fonctionnent comme prévu, car la valeur null a été écrite index toohello au lieu de la valeur de hello prévu.

#### <a name="fix-details"></a>Corriger des détails
Nous avons résolu ce problème dans la version 1.1 du Kit de développement logiciel de hello. Maintenant, si vous avez une classe de modèle comme suit :

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

et que vous définissez `IntValue` too0, que valeur est maintenant correctement sérialisée en tant que 0 sur le câble de hello et stockée en tant que 0 dans les index hello. Le retour fonctionne également comme prévu.

Il connaît une toobe problème potentiel avec cette approche : Si vous utilisez un type de modèle avec une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index. Hello SDK, ni hello API REST Azure Search aidera à vous tooenforce cela.

Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `Edm.Int32`. Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search). Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Pour cette raison, nous vous recommandons d’utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.

Pour plus d’informations sur ce correctif de bogue et hello, consultez [ce problème sur GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

