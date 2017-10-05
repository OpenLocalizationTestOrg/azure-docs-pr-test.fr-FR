---
title: "Charger des données (.NET - Recherche Azure) | Microsoft Docs"
description: "Découvrez comment charger des données dans un index dans Azure Search à l’aide du Kit de développement logiciel (SDK) .NET."
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
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="5d565-103">Charger des données dans Azure Search à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="5d565-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d565-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5d565-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="5d565-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5d565-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="5d565-106">REST</span><span class="sxs-lookup"><span data-stu-id="5d565-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="5d565-107">Cet article vous explique comment utiliser le [Kit de développement logiciel (SDK) .NET Azure Search](https://aka.ms/search-sdk) pour importer des données dans un index Azure Search.</span><span class="sxs-lookup"><span data-stu-id="5d565-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="5d565-108">Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="5d565-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="5d565-109">Cet article suppose également que vous avez déjà créé un objet `SearchServiceClient` , comme indiqué dans [Créer un index Azure Search à l’aide du Kit de développement logiciel (SDK) .NET](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="5d565-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="5d565-110">Tous les exemples de code figurant dans cet article sont écrits en C#.</span><span class="sxs-lookup"><span data-stu-id="5d565-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="5d565-111">L’intégralité du code source est disponible [sur GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="5d565-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="5d565-112">Vous pouvez également consulter le [kit de développement logiciel (SDK) .NET Azure Search](search-howto-dotnet-sdk.md) pour une description plus détaillée de l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="5d565-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="5d565-113">Afin de transmettre des documents à l’index à l’aide du Kit de développement logiciel (SDK) .NET, vous devez :</span><span class="sxs-lookup"><span data-stu-id="5d565-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="5d565-114">Créer un objet `SearchIndexClient` à connecter à votre index de recherche.</span><span class="sxs-lookup"><span data-stu-id="5d565-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="5d565-115">Créer un `IndexBatch` contenant les documents à ajouter, à modifier ou à supprimer.</span><span class="sxs-lookup"><span data-stu-id="5d565-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="5d565-116">Appeler la méthode `Documents.Index` de votre `SearchIndexClient` pour envoyer `IndexBatch` à votre index de recherche.</span><span class="sxs-lookup"><span data-stu-id="5d565-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="5d565-117">Créer une instance de la classe SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="5d565-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="5d565-118">Pour importer des données dans l’index à l’aide du Kit de développement logiciel (SDK) .NET Azure Search, vous devez créer une instance de la classe `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="5d565-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="5d565-119">Vous pouvez construire cette instance vous-même, mais la procédure est plus facile si vous avez déjà une instance `SearchServiceClient` pour appeler sa méthode `Indexes.GetClient`.</span><span class="sxs-lookup"><span data-stu-id="5d565-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="5d565-120">Par exemple, voici comment vous obtenez un `SearchIndexClient` pour l’index nommé « hotels » d’un `SearchServiceClient` nommé `serviceClient` :</span><span class="sxs-lookup"><span data-stu-id="5d565-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="5d565-121">Dans une application de recherche classique, le remplissage et la gestion des index sont gérés par un composant séparé des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="5d565-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="5d565-122">`Indexes.GetClient` est pratique pour remplir un index car il vous évite de fournir un autre `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="5d565-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="5d565-123">Pour ce faire, il transmet la clé d’administration que vous avez utilisée afin de créer le `SearchServiceClient` dans le nouveau `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="5d565-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="5d565-124">Toutefois, dans la partie de votre application qui exécute des requêtes, il vaut mieux créer le `SearchIndexClient` directement afin de transmettre une clé de requête au lieu d'une clé d'administration.</span><span class="sxs-lookup"><span data-stu-id="5d565-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="5d565-125">Cela est conforme au [principe du moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) et vous permet de mieux sécuriser votre application.</span><span class="sxs-lookup"><span data-stu-id="5d565-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="5d565-126">Pour plus d’informations sur les clés d’administration et les clés de requête, consultez [l’article de référence sur l’API REST du service Recherche Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="5d565-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="5d565-127">`SearchIndexClient` a une propriété `Documents`.</span><span class="sxs-lookup"><span data-stu-id="5d565-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="5d565-128">Cette propriété fournit toutes les méthodes dont vous avez besoin pour ajouter, modifier, supprimer ou interroger des documents dans l’index.</span><span class="sxs-lookup"><span data-stu-id="5d565-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="5d565-129">Déterminer l’action d’indexation à utiliser</span><span class="sxs-lookup"><span data-stu-id="5d565-129">Decide which indexing action to use</span></span>
<span data-ttu-id="5d565-130">Pour importer des données à l’aide du Kit de développement logiciel (SDK) .NET, vous devez empaqueter vos données dans un objet `IndexBatch` .</span><span class="sxs-lookup"><span data-stu-id="5d565-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="5d565-131">Un `IndexBatch` encapsule une collection d’objets `IndexAction`, chacun d’entre eux contenant un document et une propriété qui indique à Azure Search les actions à effectuer sur ce document (téléchargement, fusion, suppression, etc.).</span><span class="sxs-lookup"><span data-stu-id="5d565-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="5d565-132">Selon le type d’action que vous allez choisir, seuls certains champs doivent être inclus dans chaque document :</span><span class="sxs-lookup"><span data-stu-id="5d565-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="5d565-133">Action</span><span class="sxs-lookup"><span data-stu-id="5d565-133">Action</span></span> | <span data-ttu-id="5d565-134">Description</span><span class="sxs-lookup"><span data-stu-id="5d565-134">Description</span></span> | <span data-ttu-id="5d565-135">Champs requis pour chaque document</span><span class="sxs-lookup"><span data-stu-id="5d565-135">Necessary fields for each document</span></span> | <span data-ttu-id="5d565-136">Remarques</span><span class="sxs-lookup"><span data-stu-id="5d565-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="5d565-137">Une action `Upload` est similaire à celle d’un « upsert », où le document est inséré s’il est nouveau et mis à jour/remplacé s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="5d565-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="5d565-138">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="5d565-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="5d565-139">Lors de la mise à jour ou du remplacement d’un document existant, un champ qui n’est pas spécifié dans la requête sera défini sur la valeur `null`,</span><span class="sxs-lookup"><span data-stu-id="5d565-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="5d565-140">y compris lorsque le champ a été précédemment défini sur une valeur non null.</span><span class="sxs-lookup"><span data-stu-id="5d565-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="5d565-141">Met à jour un document existant avec les champs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="5d565-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="5d565-142">Si le document n’existe pas dans l’index, la fusion échoue.</span><span class="sxs-lookup"><span data-stu-id="5d565-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="5d565-143">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="5d565-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="5d565-144">N'importe quel champ que vous spécifiez dans une fusion remplace le champ existant dans le document.</span><span class="sxs-lookup"><span data-stu-id="5d565-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="5d565-145">Cela inclut les champs de type `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="5d565-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="5d565-146">Par exemple, si le document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour le champ `tags`, la valeur finale du champ `tags` sera `["economy", "pool"]`,</span><span class="sxs-lookup"><span data-stu-id="5d565-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="5d565-147">et non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="5d565-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="5d565-148">Cette action est similaire à celle d’une action `Merge` s’il existe déjà dans l’index un document comportant la clé spécifiée.</span><span class="sxs-lookup"><span data-stu-id="5d565-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="5d565-149">Dans le cas contraire, elle exécutera une action `Upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="5d565-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="5d565-150">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="5d565-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="5d565-151">Cette action supprime de l’index le document spécifié.</span><span class="sxs-lookup"><span data-stu-id="5d565-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="5d565-152">clé uniquement</span><span class="sxs-lookup"><span data-stu-id="5d565-152">key only</span></span> |<span data-ttu-id="5d565-153">Tous les champs que vous spécifiez en dehors du champ de clé sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="5d565-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="5d565-154">Si vous souhaitez supprimer un champ individuel dans un document, utilisez plutôt `Merge` et définissez simplement le champ de manière explicite sur la valeur null.</span><span class="sxs-lookup"><span data-stu-id="5d565-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="5d565-155">Vous pouvez spécifier quelle action vous souhaitez utiliser avec les différentes méthodes statiques des classes `IndexBatch` et `IndexAction`, comme indiqué dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="5d565-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="5d565-156">Construire votre IndexBatch</span><span class="sxs-lookup"><span data-stu-id="5d565-156">Construct your IndexBatch</span></span>
<span data-ttu-id="5d565-157">Maintenant que vous connaissez les actions à effectuer sur vos documents, vous êtes prêt à construire `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="5d565-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="5d565-158">L’exemple ci-dessous montre comment créer un lot avec différentes actions.</span><span class="sxs-lookup"><span data-stu-id="5d565-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="5d565-159">Notez que notre exemple utilise une classe personnalisée appelée `Hotel` qui est mappée à un document dans l’index « hotels ».</span><span class="sxs-lookup"><span data-stu-id="5d565-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

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
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="5d565-160">Dans ce cas, nous utilisons `Upload`, `MergeOrUpload` et `Delete` comme actions de recherche, tel que spécifié par les méthodes appelées sur la classe `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="5d565-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="5d565-161">Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents.</span><span class="sxs-lookup"><span data-stu-id="5d565-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="5d565-162">Notez que nous n’avons pas eu à spécifier tous les champs de document possibles en utilisant `MergeOrUpload` et que nous n’avons fait que spécifier la clé de document (`HotelId`) avec la commande `Delete`.</span><span class="sxs-lookup"><span data-stu-id="5d565-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="5d565-163">Notez également que chaque requête d’indexation ne peut contenir que 1 000 documents maximum.</span><span class="sxs-lookup"><span data-stu-id="5d565-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="5d565-164">Dans cet exemple, nous appliquons différentes actions à différents documents.</span><span class="sxs-lookup"><span data-stu-id="5d565-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="5d565-165">Si vous souhaitez effectuer ces mêmes actions sur tous les documents du lot, au lieu d’appeler `IndexBatch.New`, vous pouvez utiliser les autres méthodes statiques de `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="5d565-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="5d565-166">Par exemple, vous pouvez créer des lots en appelant `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="5d565-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="5d565-167">Ces méthodes prennent une collection de documents (objets de type `Hotel` dans cet exemple) à la place d’objets `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="5d565-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="5d565-168">Importer les données dans l’index</span><span class="sxs-lookup"><span data-stu-id="5d565-168">Import data to the index</span></span>
<span data-ttu-id="5d565-169">Maintenant qu’un objet `IndexBatch` a été initialisé, vous pouvez l’envoyer à l’index en appelant `Documents.Index` sur votre objet `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="5d565-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="5d565-170">L’exemple suivant illustre l’appel à `Index`, ainsi que des étapes supplémentaires que vous devez effectuer :</span><span class="sxs-lookup"><span data-stu-id="5d565-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
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
```

<span data-ttu-id="5d565-171">Notez le signe `try`/`catch` entourant l’appel à la méthode `Index`.</span><span class="sxs-lookup"><span data-stu-id="5d565-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="5d565-172">Le bloc catch gère un cas d’erreur important pour l’indexation.</span><span class="sxs-lookup"><span data-stu-id="5d565-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="5d565-173">Si votre service Azure Search ne parvient pas à indexer certains documents du lot, `Documents.Index` génère un `IndexBatchException`.</span><span class="sxs-lookup"><span data-stu-id="5d565-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="5d565-174">Cela peut se produire si vous indexez des documents lorsque votre service est surchargé.</span><span class="sxs-lookup"><span data-stu-id="5d565-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="5d565-175">**Nous vous recommandons vivement de prendre en charge explicitement ce cas de figure dans votre code.**</span><span class="sxs-lookup"><span data-stu-id="5d565-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="5d565-176">Vous pouvez retarder puis relancer l'indexation des documents qui ont échoué, ouvrir une session et continuer comme dans l’exemple, ou faire autre chose selon la cohérence des données requise par votre application.</span><span class="sxs-lookup"><span data-stu-id="5d565-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="5d565-177">Enfin, le code de l’exemple ci-dessus attend deux secondes.</span><span class="sxs-lookup"><span data-stu-id="5d565-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="5d565-178">L'indexation s’exécutant en mode asynchrone dans votre service Azure Search, l'exemple d'application doit attendre quelque temps afin de s'assurer que les documents sont disponibles pour la recherche.</span><span class="sxs-lookup"><span data-stu-id="5d565-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="5d565-179">Ce genre de retard n’est nécessaire que dans les démonstrations, les tests et les exemples d'applications.</span><span class="sxs-lookup"><span data-stu-id="5d565-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="5d565-180">Gestion des documents par le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="5d565-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="5d565-181">Vous demandez peut-être comment le SDK .NET Azure Search peut charger des instances d’une classe définie par l'utilisateur, comme `Hotel` , dans l'index.</span><span class="sxs-lookup"><span data-stu-id="5d565-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="5d565-182">Pour répondre à cette question, examinons la classe `Hotel` qui mappe le schéma d’index défini dans [Créer un index Azure Search à l’aide du Kit de développement logiciel (SDK) .NET](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="5d565-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="5d565-183">La première chose à remarquer est que chaque propriété publique de `Hotel` correspond à un champ dans la définition de l'index, mais à une différence près : le nom de chaque champ commence par une minuscule, tandis que le nom de chaque propriété publique de `Hotel` commence par une majuscule.</span><span class="sxs-lookup"><span data-stu-id="5d565-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="5d565-184">Il s'agit d'un scénario courant dans les applications .NET qui effectuent une liaison de données là où le schéma cible est en dehors du contrôle du développeur de l'application.</span><span class="sxs-lookup"><span data-stu-id="5d565-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="5d565-185">Plutôt que de violer les consignes d’affectation de noms de .NET en faisant commencer les noms de propriété par une minuscule, vous pouvez demander au SDK d’attribuer automatiquement une casse minuscule aux noms de propriété avec l’attribut `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="5d565-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="5d565-186">Le SDK .NET Azure Search utilise la bibliothèque [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) pour sérialiser et désérialiser vos objets de modèle personnalisés vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="5d565-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="5d565-187">Vous pouvez personnaliser cette sérialisation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5d565-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="5d565-188">Pour plus d’informations, consultez l’article [Sérialisation personnalisée avec JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="5d565-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="5d565-189">En voici un exemple : l’utilisation de l’attribut `[JsonProperty]` sur la propriété `DescriptionFr` dans l’exemple de code ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5d565-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="5d565-190">La deuxième chose importante sur la classe `Hotel` concerne les types de données des propriétés publiques.</span><span class="sxs-lookup"><span data-stu-id="5d565-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="5d565-191">Les types .NET de ces propriétés correspondent à leurs types de champ équivalents dans la définition de l'index.</span><span class="sxs-lookup"><span data-stu-id="5d565-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="5d565-192">Par exemple, la propriété de chaîne `Category` correspond au champ `category`, qui est de type `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="5d565-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="5d565-193">Il existe des mappages de type similaires entre `bool?` et `DataType.Boolean`, `DateTimeOffset?` et `DataType.DateTimeOffset`, etc.</span><span class="sxs-lookup"><span data-stu-id="5d565-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="5d565-194">Les règles spécifiques pour le mappage de type sont documentées avec la méthode `Documents.Get` dans [l’article de référence sur le Kit de développement logiciel (SDK) .NET du service Recherche Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="5d565-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="5d565-195">Cette capacité à utiliser vos propres classes comme des documents fonctionne dans les deux sens. Vous pouvez également récupérer les résultats de la recherche et laisser le Kit de développement logiciel (SDK) les désérialiser automatiquement à un type de votre choix, comme indiqué dans [l’article suivant](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5d565-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5d565-196">Le SDK .NET Azure Search prend également en charge les documents dynamiquement typés à l’aide de la classe `Document`, qui est un mappage de type clé/valeur entre des noms de champ et des valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="5d565-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="5d565-197">Cela est utile dans les cas où vous ne connaissez pas le schéma de l’index lors de sa conception et où il serait peu pratique d’établir une liaison à des classes de modèles spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5d565-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="5d565-198">Toutes les méthodes du SDK qui gèrent les documents ont des surcharges qui fonctionnent avec la classe `Document` , ainsi que des surcharges fortement typées qui acceptent un paramètre de type générique.</span><span class="sxs-lookup"><span data-stu-id="5d565-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="5d565-199">Seules ces dernières sont utilisées dans l’exemple de code de cet article.</span><span class="sxs-lookup"><span data-stu-id="5d565-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="5d565-200">**Pourquoi utiliser des types de données Nullable**</span><span class="sxs-lookup"><span data-stu-id="5d565-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="5d565-201">Lorsque vous créez vos propres classes de modèles à mapper à un index Azure Search, nous vous recommandons de déclarer les propriétés des types de valeurs, par exemple `bool` et `int`, comme acceptant la valeur null (par exemple, `bool?` au lieu de `bool`).</span><span class="sxs-lookup"><span data-stu-id="5d565-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="5d565-202">Si vous utilisez une propriété ne pouvant être définie sur null, vous devez **garantir** qu’aucun document de cet index ne contient de valeur null pour le champ correspondant.</span><span class="sxs-lookup"><span data-stu-id="5d565-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="5d565-203">Ni le Kit de développement logiciel ni le service Azure Search ne vous aideront à appliquer cette recommandation.</span><span class="sxs-lookup"><span data-stu-id="5d565-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="5d565-204">Il ne s’agit pas d’une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ à un index existant qui est de type `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="5d565-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="5d565-205">Après la mise à jour de la définition d’index, ce nouveau champ prendra la valeur null pour tous les documents (car tous les types peuvent avoir la valeur null dans Azure Search).</span><span class="sxs-lookup"><span data-stu-id="5d565-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="5d565-206">Si vous utilisez ensuite une classe de modèle avec une propriété `int` ne pouvant être définie sur null pour ce champ, vous obtiendrez l’exception `JsonSerializationException` ci-dessous lorsque vous tenterez de récupérer des documents :</span><span class="sxs-lookup"><span data-stu-id="5d565-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="5d565-207">Pour cette raison, nous vous recommandons d'utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.</span><span class="sxs-lookup"><span data-stu-id="5d565-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d565-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d565-208">Next steps</span></span>
<span data-ttu-id="5d565-209">Une fois votre index Azure Search renseigné, vous pouvez commencer à exécuter des requêtes de recherche de documents.</span><span class="sxs-lookup"><span data-stu-id="5d565-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="5d565-210">Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="5d565-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

