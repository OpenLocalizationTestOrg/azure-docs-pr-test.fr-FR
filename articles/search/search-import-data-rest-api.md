---
title: "Charger des données (API REST - Recherche Azure) | Microsoft Docs"
description: "Découvrez comment charger des données sur un index dans Azure Search à l’aide de l’API REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: f22a33ed86fbfc46dfa732239263a49f34c4afee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="879a0-103">Charger des données dans Azure Search à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="879a0-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="879a0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="879a0-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="879a0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="879a0-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="879a0-106">REST</span><span class="sxs-lookup"><span data-stu-id="879a0-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="879a0-107">Cet article vous explique comment utiliser l’ [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/) pour importer des données dans un index Azure Search.</span><span class="sxs-lookup"><span data-stu-id="879a0-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="879a0-108">Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="879a0-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="879a0-109">Pour distribuer des documents dans l’index à l’aide de l’API REST, vous allez envoyer une requête HTTP POST au point de terminaison URL de votre index.</span><span class="sxs-lookup"><span data-stu-id="879a0-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="879a0-110">Le corps de la requête HTTP est un objet JSON contenant les documents à ajouter, à modifier ou à supprimer.</span><span class="sxs-lookup"><span data-stu-id="879a0-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="879a0-111">Identifier la clé API d’administration de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="879a0-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="879a0-112">Lors de l’émission de requêtes HTTP sur votre service à l’aide de l’API REST, *chaque* demande d’API doit inclure la clé API générée pour le service Search que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="879a0-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="879a0-113">L’utilisation d’une clé valide permet d’établir, en fonction de chaque demande, une relation de confiance entre l’application qui envoie la demande et le service qui en assure le traitement.</span><span class="sxs-lookup"><span data-stu-id="879a0-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="879a0-114">Pour accéder aux clés API de votre service, vous pouvez vous connecter au [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="879a0-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="879a0-115">Accédez au panneau de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="879a0-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="879a0-116">Cliquez sur l’icône « Clés »</span><span class="sxs-lookup"><span data-stu-id="879a0-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="879a0-117">Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.</span><span class="sxs-lookup"><span data-stu-id="879a0-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="879a0-118">Les *clés d’administration* principales et secondaires vous accordent des droits d’accès complets à toutes les opérations, avec notamment la possibilité de gérer le service ou de créer et supprimer des index, des indexeurs et des sources de données.</span><span class="sxs-lookup"><span data-stu-id="879a0-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="879a0-119">Deux clés sont à votre disposition afin que vous puissiez continuer à utiliser la clé secondaire si vous décidez de régénérer la clé primaire et inversement.</span><span class="sxs-lookup"><span data-stu-id="879a0-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="879a0-120">Vos *clés de requête* vous accordent un accès en lecture seule aux index et documents ; elles sont généralement distribuées aux applications clientes qui émettent des demandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="879a0-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="879a0-121">Pour importer des données dans un index, vous pouvez utiliser votre clé d’administration principale ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="879a0-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="879a0-122">Déterminer l’action d’indexation à utiliser</span><span class="sxs-lookup"><span data-stu-id="879a0-122">Decide which indexing action to use</span></span>
<span data-ttu-id="879a0-123">Lorsque vous utilisez l’API REST, vous allez émettre des requêtes HTTP POST avec un corps de requête JSON à l’URL de point de terminaison de votre index Azure Search.</span><span class="sxs-lookup"><span data-stu-id="879a0-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="879a0-124">L’objet JSON contenu dans le corps de la requête HTTP comporte un seul tableau JSON nommé « value », qui renferme les objets JSON représentant les documents que vous allez ajouter à votre index, mettre à jour ou supprimer.</span><span class="sxs-lookup"><span data-stu-id="879a0-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="879a0-125">Chaque objet JSON du tableau « value » représente un document à indexer.</span><span class="sxs-lookup"><span data-stu-id="879a0-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="879a0-126">Chacun de ces objets contient les clés du document et spécifie l’action d’indexation souhaitée (téléchargement, fusion, suppression, etc.).</span><span class="sxs-lookup"><span data-stu-id="879a0-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="879a0-127">Selon le type d’action que vous allez choisir, seuls certains champs doivent être inclus dans chaque document :</span><span class="sxs-lookup"><span data-stu-id="879a0-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="879a0-128">Description</span><span class="sxs-lookup"><span data-stu-id="879a0-128">Description</span></span> | <span data-ttu-id="879a0-129">Champs requis pour chaque document</span><span class="sxs-lookup"><span data-stu-id="879a0-129">Necessary fields for each document</span></span> | <span data-ttu-id="879a0-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="879a0-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="879a0-131">Une action `upload` est similaire à celle d’un « upsert », où le document est inséré s’il est nouveau et mis à jour/remplacé s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="879a0-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="879a0-132">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="879a0-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="879a0-133">Lors de la mise à jour ou du remplacement d’un document existant, un champ qui n’est pas spécifié dans la requête sera défini sur la valeur `null`,</span><span class="sxs-lookup"><span data-stu-id="879a0-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="879a0-134">y compris lorsque le champ a été précédemment défini sur une valeur non null.</span><span class="sxs-lookup"><span data-stu-id="879a0-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="879a0-135">Met à jour un document existant avec les champs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="879a0-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="879a0-136">Si le document n’existe pas dans l’index, la fusion échoue.</span><span class="sxs-lookup"><span data-stu-id="879a0-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="879a0-137">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="879a0-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="879a0-138">N'importe quel champ que vous spécifiez dans une fusion remplace le champ existant dans le document.</span><span class="sxs-lookup"><span data-stu-id="879a0-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="879a0-139">Cela inclut les champs de type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="879a0-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="879a0-140">Par exemple, si le document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour le champ `tags`, la valeur finale du champ `tags` sera `["economy", "pool"]`,</span><span class="sxs-lookup"><span data-stu-id="879a0-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="879a0-141">et non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="879a0-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="879a0-142">Cette action est similaire à celle d’une action `merge` s’il existe déjà dans l’index un document comportant la clé spécifiée.</span><span class="sxs-lookup"><span data-stu-id="879a0-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="879a0-143">Dans le cas contraire, elle exécutera une action `upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="879a0-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="879a0-144">une clé, ainsi que tout autre champ que vous souhaitez définir</span><span class="sxs-lookup"><span data-stu-id="879a0-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="879a0-145">Cette action supprime de l’index le document spécifié.</span><span class="sxs-lookup"><span data-stu-id="879a0-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="879a0-146">clé uniquement</span><span class="sxs-lookup"><span data-stu-id="879a0-146">key only</span></span> |<span data-ttu-id="879a0-147">Tous les champs que vous spécifiez en dehors du champ de clé sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="879a0-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="879a0-148">Si vous souhaitez supprimer un champ individuel dans un document, utilisez plutôt `merge` et définissez simplement le champ de manière explicite sur la valeur null.</span><span class="sxs-lookup"><span data-stu-id="879a0-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="879a0-149">Construire votre requête HTTP et le corps de la requête</span><span class="sxs-lookup"><span data-stu-id="879a0-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="879a0-150">Maintenant que vous avez recueilli les valeurs de champ requises pour les actions de votre index, vous pouvez construire votre requête HTTP et le corps de requête JSON pour importer vos données.</span><span class="sxs-lookup"><span data-stu-id="879a0-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="879a0-151">Requête et en-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="879a0-151">Request and Request Headers</span></span>
<span data-ttu-id="879a0-152">Dans l’URL, vous devez fournir le nom de votre service, le nom de l’index (« hotels » dans notre exemple) ainsi que la version d’API appropriée (la version actuelle de l’API est celle du `2016-09-01` au moment de la publication de ce document).</span><span class="sxs-lookup"><span data-stu-id="879a0-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2016-09-01` at the time of publishing this document).</span></span> <span data-ttu-id="879a0-153">Vous devez définir les en-têtes de requête `Content-Type` et `api-key`.</span><span class="sxs-lookup"><span data-stu-id="879a0-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="879a0-154">Pour cette dernière, utilisez l’une des clés d’administration de votre service.</span><span class="sxs-lookup"><span data-stu-id="879a0-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="879a0-155">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="879a0-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="879a0-156">Dans ce cas, nous utilisons `upload`, `mergeOrUpload` et `delete` comme actions de recherche.</span><span class="sxs-lookup"><span data-stu-id="879a0-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="879a0-157">Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents.</span><span class="sxs-lookup"><span data-stu-id="879a0-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="879a0-158">Notez que nous n’avons pas eu à spécifier tous les champs de document possibles en utilisant `mergeOrUpload` et que nous n’avons fait que spécifier la clé de document (`hotelId`) avec la commande `delete`.</span><span class="sxs-lookup"><span data-stu-id="879a0-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="879a0-159">Notez également que chaque requête d’indexation ne peut contenir que 1 000  documents (ou 16 Mo) maximum.</span><span class="sxs-lookup"><span data-stu-id="879a0-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="879a0-160">Comprendre votre code de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="879a0-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="879a0-161">200</span><span class="sxs-lookup"><span data-stu-id="879a0-161">200</span></span>
<span data-ttu-id="879a0-162">Lorsque votre demande d’indexation aboutit, vous recevez une réponse HTTP avec le code d’état `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="879a0-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="879a0-163">Le corps JSON de la réponse HTTP se présentera comme suit :</span><span class="sxs-lookup"><span data-stu-id="879a0-163">The JSON body of the HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="879a0-164">207</span><span class="sxs-lookup"><span data-stu-id="879a0-164">207</span></span>
<span data-ttu-id="879a0-165">Un code d’état `207` est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="879a0-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="879a0-166">Le corps JSON de la réponse HTTP contient des informations sur les documents ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="879a0-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="879a0-167">Cela signifie généralement que la charge de votre service de recherche a atteint un point tel que les demandes d’indexation commencent à renvoyer des réponses `503`.</span><span class="sxs-lookup"><span data-stu-id="879a0-167">This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses.</span></span> <span data-ttu-id="879a0-168">Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="879a0-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="879a0-169">En laissant au système le temps de récupérer, vous aurez davantage de chance de voir vos futures requêtes aboutir.</span><span class="sxs-lookup"><span data-stu-id="879a0-169">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="879a0-170">Si vous renouvelez rapidement vos tentatives de requête, vous ne ferez que prolonger la situation.</span><span class="sxs-lookup"><span data-stu-id="879a0-170">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="879a0-171">429</span><span class="sxs-lookup"><span data-stu-id="879a0-171">429</span></span>
<span data-ttu-id="879a0-172">Le code d’état `429` est renvoyé lorsque vous avez dépassé votre quota de nombre de documents par index.</span><span class="sxs-lookup"><span data-stu-id="879a0-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="879a0-173">503</span><span class="sxs-lookup"><span data-stu-id="879a0-173">503</span></span>
<span data-ttu-id="879a0-174">Le code d’état `503` est renvoyé si aucun des éléments de la requête n’a été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="879a0-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="879a0-175">Cette erreur signifie que le système est surchargé et que votre requête ne peut pas être traitée pour le moment.</span><span class="sxs-lookup"><span data-stu-id="879a0-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="879a0-176">Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="879a0-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="879a0-177">En laissant au système le temps de récupérer, vous aurez davantage de chance de voir vos futures requêtes aboutir.</span><span class="sxs-lookup"><span data-stu-id="879a0-177">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="879a0-178">Si vous renouvelez rapidement vos tentatives de requête, vous ne ferez que prolonger la situation.</span><span class="sxs-lookup"><span data-stu-id="879a0-178">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

<span data-ttu-id="879a0-179">Pour plus d’informations sur les actions de document et les réponses de réussite/d’erreur, consultez la page [Ajouter, mettre à jour ou supprimer des documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="879a0-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="879a0-180">Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="879a0-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="879a0-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="879a0-181">Next steps</span></span>
<span data-ttu-id="879a0-182">Une fois votre index Azure Search renseigné, vous pouvez commencer à exécuter des requêtes de recherche de documents.</span><span class="sxs-lookup"><span data-stu-id="879a0-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="879a0-183">Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="879a0-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
