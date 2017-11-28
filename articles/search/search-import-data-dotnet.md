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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="336eb-103">À l’aide de téléchargement données tooAzure recherche hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="336eb-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="336eb-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="336eb-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="336eb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="336eb-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="336eb-106">REST</span><span class="sxs-lookup"><span data-stu-id="336eb-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="336eb-107">Cet article vous indiquent comment toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport les données dans un index Azure Search.</span><span class="sxs-lookup"><span data-stu-id="336eb-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="336eb-108">Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="336eb-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="336eb-109">Cet article suppose également que vous avez déjà créé un `SearchServiceClient` de l’objet, comme indiqué dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="336eb-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="336eb-110">Tous les exemples de code figurant dans cet article sont écrits en C#.</span><span class="sxs-lookup"><span data-stu-id="336eb-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="336eb-111">Vous pouvez trouver le code source complet hello [sur GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="336eb-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="336eb-112">Vous pouvez également lire sur hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) pour une présentation plus détaillée de l’exemple de code hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="336eb-113">Dans les documents de toopush commande dans votre index à l’aide de hello .NET SDK, vous devez :</span><span class="sxs-lookup"><span data-stu-id="336eb-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="336eb-114">Créer un `SearchIndexClient` objet tooconnect tooyour index de recherche.</span><span class="sxs-lookup"><span data-stu-id="336eb-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="336eb-115">Créer un `IndexBatch` contenant hello documents toobe ajouté, modifié ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="336eb-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="336eb-116">Appelez hello `Documents.Index` méthode de votre `SearchIndexClient` toosend hello `IndexBatch` tooyour les index de recherche.</span><span class="sxs-lookup"><span data-stu-id="336eb-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="336eb-117">Créez une instance de hello SearchIndexClient classe</span><span class="sxs-lookup"><span data-stu-id="336eb-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="336eb-118">données tooimport votre index à l’aide de hello Azure Search .NET SDK, vous devez toocreate une instance de hello `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="336eb-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="336eb-119">Vous pouvez construire cette instance vous-même, mais il plus facile si vous avez déjà un `SearchServiceClient` instance toocall son `Indexes.GetClient` (méthode).</span><span class="sxs-lookup"><span data-stu-id="336eb-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="336eb-120">Par exemple, voici comment obtenir un `SearchIndexClient` pour les index hello nommé « hôtels » à partir d’un `SearchServiceClient` nommé `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="336eb-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="336eb-121">Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="336eb-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="336eb-122">`Indexes.GetClient`est pratique pour remplir un index, car vous épargne hello des difficultés à fournir un autre `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="336eb-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="336eb-123">Pour ce faire, il en passant la clé d’administration hello que hello utilisé toocreate vous `SearchServiceClient` toohello nouveau `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="336eb-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="336eb-124">Toutefois, dans la partie hello de votre application qui exécute des requêtes, il est mieux toocreate hello `SearchIndexClient` directement afin que vous pouvez passer d’une clé de requête au lieu d’une clé d’administration.</span><span class="sxs-lookup"><span data-stu-id="336eb-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="336eb-125">Cela est cohérent avec hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege) et vous aide à toomake votre application plus sécurisée.</span><span class="sxs-lookup"><span data-stu-id="336eb-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="336eb-126">Vous trouverez plus d’informations sur les clés d’administration et les clés de requête Bonjour [référence d’API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="336eb-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="336eb-127">`SearchIndexClient` a une propriété `Documents`.</span><span class="sxs-lookup"><span data-stu-id="336eb-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="336eb-128">Cette propriété fournit toutes les méthodes de hello que vous devez tooadd, modifier, supprimer ou interroger des documents dans votre index.</span><span class="sxs-lookup"><span data-stu-id="336eb-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="336eb-129">Décidez quels toouse action d’indexation</span><span class="sxs-lookup"><span data-stu-id="336eb-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="336eb-130">données de tooimport à l’aide de hello .NET SDK, vous devez toopackage vos données dans un `IndexBatch` objet.</span><span class="sxs-lookup"><span data-stu-id="336eb-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="336eb-131">Un `IndexBatch` encapsule une collection de `IndexAction` objets, chacun d’eux contenant un document et une propriété qui indique quel tooperform action à Azure Search sur ce document (téléchargement, fusionner, supprimer, etc.).</span><span class="sxs-lookup"><span data-stu-id="336eb-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="336eb-132">En fonction de hello ci-dessous les actions que vous choisissez, uniquement certains champs doivent être inclus pour chaque document :</span><span class="sxs-lookup"><span data-stu-id="336eb-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="336eb-133">Action</span><span class="sxs-lookup"><span data-stu-id="336eb-133">Action</span></span> | <span data-ttu-id="336eb-134">Description</span><span class="sxs-lookup"><span data-stu-id="336eb-134">Description</span></span> | <span data-ttu-id="336eb-135">Champs requis pour chaque document</span><span class="sxs-lookup"><span data-stu-id="336eb-135">Necessary fields for each document</span></span> | <span data-ttu-id="336eb-136">Remarques</span><span class="sxs-lookup"><span data-stu-id="336eb-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="336eb-137">Un `Upload` action est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe.</span><span class="sxs-lookup"><span data-stu-id="336eb-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="336eb-138">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="336eb-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="336eb-139">Lors de la mise à jour/remplacement d’un document existant, un champ qui n’est pas spécifié dans la demande hello aura son champ défini trop`null`.</span><span class="sxs-lookup"><span data-stu-id="336eb-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="336eb-140">Cela se produit même lorsque hello a été défini précédemment tooa nulle.</span><span class="sxs-lookup"><span data-stu-id="336eb-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="336eb-141">Mises à jour existant de document avec hello spécifié des champs.</span><span class="sxs-lookup"><span data-stu-id="336eb-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="336eb-142">Si le document de hello n’existe pas dans l’index de hello, la fusion de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="336eb-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="336eb-143">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="336eb-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="336eb-144">N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="336eb-145">Cela inclut les champs de type `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="336eb-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="336eb-146">Par exemple, si hello document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour `tags`, hello valeur finale de hello `tags` champ sera `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="336eb-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="336eb-147">et non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="336eb-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="336eb-148">Cette action se comporte comme `Merge` si un document avec hello donné clé déjà existe dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="336eb-149">Si le document de hello n’existe pas, il se comporte comme `Upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="336eb-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="336eb-150">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="336eb-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="336eb-151">Supprime l’index de hello de document spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="336eb-152">clé uniquement</span><span class="sxs-lookup"><span data-stu-id="336eb-152">key only</span></span> |<span data-ttu-id="336eb-153">Tous les champs que vous spécifiez d’autres que le champ de clé hello sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="336eb-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="336eb-154">Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `Merge` à la place et simplement définir explicitement les champs de hello toonull.</span><span class="sxs-lookup"><span data-stu-id="336eb-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="336eb-155">Vous pouvez spécifier quelle action toouse avec hello plusieurs méthodes statiques de hello `IndexBatch` et `IndexAction` des classes, comme indiqué dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="336eb-156">Construire votre IndexBatch</span><span class="sxs-lookup"><span data-stu-id="336eb-156">Construct your IndexBatch</span></span>
<span data-ttu-id="336eb-157">Maintenant que vous savez quels tooperform actions sur vos documents, vous êtes prêt tooconstruct hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="336eb-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="336eb-158">Hello exemple ci-dessous montre comment toocreate un lot avec quelques actions différentes.</span><span class="sxs-lookup"><span data-stu-id="336eb-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="336eb-159">Notez que notre exemple utilise une classe personnalisée appelée `Hotel` qui mappe le document tooa dans l’index de « hôtels » hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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

<span data-ttu-id="336eb-160">Dans ce cas, nous utilisons `Upload`, `MergeOrUpload`, et `Delete` en tant que nos actions de recherche, tel que spécifié par les méthodes hello appelées sur hello `IndexAction` classe.</span><span class="sxs-lookup"><span data-stu-id="336eb-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="336eb-161">Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents.</span><span class="sxs-lookup"><span data-stu-id="336eb-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="336eb-162">Notez la façon dont nous n’avait pas toospecify tous les champs de document possible hello lors de l’utilisation `MergeOrUpload` et comment nous spécifiée uniquement clé de document hello (`HotelId`) lors de l’utilisation `Delete`.</span><span class="sxs-lookup"><span data-stu-id="336eb-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="336eb-163">Notez également que vous ne pouvez inclure des documents de too1000 dans une seule demande d’indexation.</span><span class="sxs-lookup"><span data-stu-id="336eb-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="336eb-164">Dans cet exemple, nous appliquons documents toodifferent de différentes actions.</span><span class="sxs-lookup"><span data-stu-id="336eb-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="336eb-165">Si vous souhaitiez tooperform hello les mêmes actions sur tous les documents dans un lot de hello, au lieu d’appeler `IndexBatch.New`, vous pouvez utiliser hello autres méthodes statiques de `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="336eb-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="336eb-166">Par exemple, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="336eb-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="336eb-167">Ces méthodes prennent une collection de documents (objets de type `Hotel` dans cet exemple) à la place d’objets `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="336eb-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="336eb-168">Importation données toohello index</span><span class="sxs-lookup"><span data-stu-id="336eb-168">Import data toohello index</span></span>
<span data-ttu-id="336eb-169">Maintenant que vous avez initialisé `IndexBatch` de l’objet, vous pouvez l’envoyer toohello index en appelant `Documents.Index` sur votre `SearchIndexClient` objet.</span><span class="sxs-lookup"><span data-stu-id="336eb-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="336eb-170">Hello suivant montre l’exemple de comment toocall `Index`, ainsi que certaines étapes supplémentaires, vous devez tooperform :</span><span class="sxs-lookup"><span data-stu-id="336eb-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

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

<span data-ttu-id="336eb-171">Hello de note `try` / `catch` entourant hello appel toohello `Index` (méthode).</span><span class="sxs-lookup"><span data-stu-id="336eb-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="336eb-172">bloc catch de Hello gère un cas d’erreur importants pour l’indexation.</span><span class="sxs-lookup"><span data-stu-id="336eb-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="336eb-173">Si votre service Azure Search échoue tooindex hello certains documents dans un lot de hello, un `IndexBatchException` est levée par `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="336eb-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="336eb-174">Cela peut se produire si vous indexez des documents lorsque votre service est surchargé.</span><span class="sxs-lookup"><span data-stu-id="336eb-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="336eb-175">**Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.**</span><span class="sxs-lookup"><span data-stu-id="336eb-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="336eb-176">Vous pouvez retarder et réessayez d’indexation des documents hello ayant échoué, ou vous pouvez ouvrir une session et continuer comme l’exemple hello réalise, ou vous pouvez faire quelque chose d’autre selon les exigences de cohérence de données de votre application.</span><span class="sxs-lookup"><span data-stu-id="336eb-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="336eb-177">Enfin, hello code dans l’exemple hello au-dessus des délais de deux secondes.</span><span class="sxs-lookup"><span data-stu-id="336eb-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="336eb-178">L’indexation se produit à l’en mode asynchrone dans votre service Azure Search, par conséquent, exemple d’application hello doit toowait un tooensure peu de temps que les documents hello sont disponibles pour la recherche.</span><span class="sxs-lookup"><span data-stu-id="336eb-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="336eb-179">Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.</span><span class="sxs-lookup"><span data-stu-id="336eb-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="336eb-180">Comment hello .NET SDK traite les documents</span><span class="sxs-lookup"><span data-stu-id="336eb-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="336eb-181">Vous vous demandez peut-être comment hello Azure Search .NET SDK est instances tooupload en mesure d’une classe définie par l’utilisateur comme `Hotel` toohello index.</span><span class="sxs-lookup"><span data-stu-id="336eb-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="336eb-182">toohelp répondre à cette question, examinons hello `Hotel` (classe), qui mappe le schéma d’index toohello définie dans [créer un index Azure Search à l’aide de hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="336eb-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="336eb-183">Hello première toonotice est que chaque propriété publique `Hotel` correspond tooa champ dans la définition de l’index hello, mais avec une différence essentielle : hello le nom de chaque champ commence par une lettre minuscule (« casse mixte »), tandis que nom hello chaque public propriété de `Hotel` commence par une lettre majuscule (« casse Pascal »).</span><span class="sxs-lookup"><span data-stu-id="336eb-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="336eb-184">Il s’agit d’un scénario courant dans les applications .NET d’effectuer une liaison de données où le schéma cible hello est contrôle hello en dehors du développeur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="336eb-185">Au lieu de .NET de hello tooviolate affectation de noms en rendant la propriété noms casse mixte, vous pouvez indiquer à hello SDK toomap hello noms toocamel en cas de propriété automatiquement avec hello `[SerializePropertyNamesAsCamelCase]` attribut.</span><span class="sxs-lookup"><span data-stu-id="336eb-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="336eb-186">Bonjour Azure Search .NET SDK utilise hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de bibliothèque et de désérialiser vos tooand d’objets de modèle personnalisé à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="336eb-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="336eb-187">Vous pouvez personnaliser cette sérialisation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="336eb-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="336eb-188">Pour plus d’informations, consultez l’article [Sérialisation personnalisée avec JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="336eb-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="336eb-189">Un exemple de cela est utilisation hello Hello `[JsonProperty]` attribut sur hello `DescriptionFr` propriété dans le code d’exemple hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="336eb-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="336eb-190">Hello seconde le plus important de hello `Hotel` classe sont les types de données hello des propriétés publiques de hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="336eb-191">les types .NET Hello de ces propriétés mappent les types de champ équivalent tootheir dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="336eb-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="336eb-192">Par exemple, hello `Category` propriété de chaîne mappe toohello `category` champ, ce qui est de type `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="336eb-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="336eb-193">Il existe des mappages de type similaires entre `bool?` et `DataType.Boolean`, `DateTimeOffset?` et `DataType.DateTimeOffset`, etc.</span><span class="sxs-lookup"><span data-stu-id="336eb-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="336eb-194">Hello des règles spécifiques pour le mappage de type hello sont documentées par hello `Documents.Get` méthode Bonjour [référence du Kit de développement .NET Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="336eb-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="336eb-195">Cette possibilité toouse vos propres classes en tant que documents fonctionne dans les deux directions ; Vous pouvez également récupérer les résultats de la recherche et hello SDK automatiquement désérialiser les tooa type de votre choix, comme indiqué dans hello [l’article suivant](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="336eb-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="336eb-196">Bonjour Azure Search .NET SDK prend également en charge les documents typées dynamiquement à l’aide de hello `Document` (classe), qui est un mappage de clé/valeur noms toofield des valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="336eb-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="336eb-197">Cela est utile dans les scénarios où vous ne connaissez pas schéma d’index hello au moment du design ou dans lesquelles il serait pas pratique toobind toospecific de classes de modèle.</span><span class="sxs-lookup"><span data-stu-id="336eb-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="336eb-198">Toutes les méthodes hello hello SDK qui traitent des documents ont des surcharges qui fonctionnent avec hello `Document` classe, ainsi que les surcharges fortement typée qui prennent un paramètre de type générique.</span><span class="sxs-lookup"><span data-stu-id="336eb-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="336eb-199">Uniquement les hello ce dernier sont utilisées dans l’exemple de code hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="336eb-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="336eb-200">**Pourquoi utiliser des types de données Nullable**</span><span class="sxs-lookup"><span data-stu-id="336eb-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="336eb-201">Lorsque vous créez votre propre index Azure Search de modèle classes toomap tooan, nous vous recommandons de déclarer des propriétés de types valeur tels que `bool` et `int` toobe nullable (par exemple, `bool?` au lieu de `bool`).</span><span class="sxs-lookup"><span data-stu-id="336eb-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="336eb-202">Si vous utilisez une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index.</span><span class="sxs-lookup"><span data-stu-id="336eb-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="336eb-203">Hello SDK, ni hello service Azure Search aidera à vous tooenforce cela.</span><span class="sxs-lookup"><span data-stu-id="336eb-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="336eb-204">Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="336eb-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="336eb-205">Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search).</span><span class="sxs-lookup"><span data-stu-id="336eb-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="336eb-206">Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :</span><span class="sxs-lookup"><span data-stu-id="336eb-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="336eb-207">Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.</span><span class="sxs-lookup"><span data-stu-id="336eb-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="336eb-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="336eb-208">Next steps</span></span>
<span data-ttu-id="336eb-209">Remplissage de l’index Azure Search, vous serez prêt toostart émission toosearch de requêtes pour les documents.</span><span class="sxs-lookup"><span data-stu-id="336eb-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="336eb-210">Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="336eb-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

