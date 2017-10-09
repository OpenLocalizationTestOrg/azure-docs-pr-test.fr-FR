---
title: "AAA « télécharger des données (API REST - Azure Search) | Documents Microsoft »"
description: "Découvrez comment les index de tooan tooupload données à l’aide d’Azure Search hello API REST."
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
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="d43cb-103">À l’aide de téléchargement données tooAzure recherche hello API REST</span><span class="sxs-lookup"><span data-stu-id="d43cb-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="d43cb-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d43cb-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="d43cb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d43cb-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="d43cb-106">REST</span><span class="sxs-lookup"><span data-stu-id="d43cb-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="d43cb-107">Cet article vous indiquent comment toouse hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/) tooimport les données dans un index Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d43cb-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="d43cb-108">Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="d43cb-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="d43cb-109">Documents de toopush de commande dans votre index à l’aide de hello API REST, vous prévoyez d’émettre des point de terminaison URL HTTP POST demande tooyour d’un index.</span><span class="sxs-lookup"><span data-stu-id="d43cb-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="d43cb-110">corps Hello Hello demande HTTP corps est un objet JSON qui contient les documents hello toobe ajouté, modifié ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="d43cb-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="d43cb-111">Identifier la clé API d’administration de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="d43cb-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="d43cb-112">Lors de l’émission des demandes HTTP sur votre service à l’aide de hello API REST, *chaque* demande d’API doit inclure hello clé api qui a été généré pour hello service de recherche que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="d43cb-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="d43cb-113">Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.</span><span class="sxs-lookup"><span data-stu-id="d43cb-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="d43cb-114">toofind les clés de votre service api, vous pouvez vous connecter toohello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="d43cb-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="d43cb-115">Panneau du service tooyour accédez Azure Search</span><span class="sxs-lookup"><span data-stu-id="d43cb-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="d43cb-116">Cliquez sur hello icône « Clés »</span><span class="sxs-lookup"><span data-stu-id="d43cb-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="d43cb-117">Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.</span><span class="sxs-lookup"><span data-stu-id="d43cb-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="d43cb-118">Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données.</span><span class="sxs-lookup"><span data-stu-id="d43cb-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="d43cb-119">Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.</span><span class="sxs-lookup"><span data-stu-id="d43cb-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="d43cb-120">Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="d43cb-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="d43cb-121">Pour des raisons de hello de l’importation de données dans un index, vous pouvez utiliser votre clé d’administration principal ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="d43cb-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="d43cb-122">Décidez quels toouse action d’indexation</span><span class="sxs-lookup"><span data-stu-id="d43cb-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="d43cb-123">Lorsque vous utilisez hello API REST, vous prévoyez d’émettre les requêtes HTTP POST avec l’URL du demande organismes tooyour Azure Search index JSON point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d43cb-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="d43cb-124">objet JSON de Hello dans le corps de la requête HTTP contient un tableau JSON nommé « valeur » qui contient des objets JSON représentant les documents que vous aimeriez tooadd tooyour index, update ou delete.</span><span class="sxs-lookup"><span data-stu-id="d43cb-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="d43cb-125">Chaque objet JSON dans le tableau de « value » hello représente un toobe document indexé.</span><span class="sxs-lookup"><span data-stu-id="d43cb-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="d43cb-126">Chacun de ces objets contient la clé du document hello et spécifie l’action de l’indexation hello souhaitée (téléchargement, fusionner, supprimer, etc.).</span><span class="sxs-lookup"><span data-stu-id="d43cb-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="d43cb-127">En fonction de hello ci-dessous les actions que vous choisissez, uniquement certains champs doivent être inclus pour chaque document :</span><span class="sxs-lookup"><span data-stu-id="d43cb-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="d43cb-128">Description</span><span class="sxs-lookup"><span data-stu-id="d43cb-128">Description</span></span> | <span data-ttu-id="d43cb-129">Champs requis pour chaque document</span><span class="sxs-lookup"><span data-stu-id="d43cb-129">Necessary fields for each document</span></span> | <span data-ttu-id="d43cb-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="d43cb-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="d43cb-131">Un `upload` action est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe.</span><span class="sxs-lookup"><span data-stu-id="d43cb-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="d43cb-132">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="d43cb-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="d43cb-133">Lors de la mise à jour/remplacement d’un document existant, un champ qui n’est pas spécifié dans la demande hello aura son champ défini trop`null`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="d43cb-134">Cela se produit même lorsque hello a été défini précédemment tooa nulle.</span><span class="sxs-lookup"><span data-stu-id="d43cb-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="d43cb-135">Mises à jour existant de document avec hello spécifié des champs.</span><span class="sxs-lookup"><span data-stu-id="d43cb-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="d43cb-136">Si le document de hello n’existe pas dans l’index de hello, la fusion de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="d43cb-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="d43cb-137">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="d43cb-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="d43cb-138">N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="d43cb-139">Cela inclut les champs de type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="d43cb-140">Par exemple, si hello document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour `tags`, hello valeur finale de hello `tags` champ sera `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="d43cb-141">et non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="d43cb-142">Cette action se comporte comme `merge` si un document avec hello donné clé déjà existe dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="d43cb-143">Si le document de hello n’existe pas, il se comporte comme `upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="d43cb-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="d43cb-144">clé, ainsi que tous les autres champs que vous souhaitez toodefine</span><span class="sxs-lookup"><span data-stu-id="d43cb-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="d43cb-145">Supprime l’index de hello de document spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="d43cb-146">clé uniquement</span><span class="sxs-lookup"><span data-stu-id="d43cb-146">key only</span></span> |<span data-ttu-id="d43cb-147">Tous les champs que vous spécifiez d’autres que le champ de clé hello sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="d43cb-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="d43cb-148">Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `merge` à la place et simplement définir explicitement les champs de hello toonull.</span><span class="sxs-lookup"><span data-stu-id="d43cb-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="d43cb-149">Construire votre requête HTTP et le corps de la requête</span><span class="sxs-lookup"><span data-stu-id="d43cb-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="d43cb-150">Maintenant que vous avez rassemblé les valeurs de champ nécessaire hello pour les actions de votre index, vous demande de prêt tooconstruct hello réelle HTTP et tooimport de corps de demande JSON vos données.</span><span class="sxs-lookup"><span data-stu-id="d43cb-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="d43cb-151">Requête et en-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="d43cb-151">Request and Request Headers</span></span>
<span data-ttu-id="d43cb-152">Dans l’URL de hello, vous devez tooprovide votre nom de service, nom de l’index (« hôtels » dans ce cas), ainsi que les version appropriée de l’API hello (version actuelle de l’API hello est `2016-09-01` au moment de hello de publication de ce document).</span><span class="sxs-lookup"><span data-stu-id="d43cb-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="d43cb-153">Vous devez toodefine hello `Content-Type` et `api-key` en-têtes de demande.</span><span class="sxs-lookup"><span data-stu-id="d43cb-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="d43cb-154">Pourquoi ce dernier, utilisez une des clés d’administration de votre service.</span><span class="sxs-lookup"><span data-stu-id="d43cb-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="d43cb-155">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="d43cb-155">Request Body</span></span>
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
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="d43cb-156">Dans ce cas, nous utilisons `upload`, `mergeOrUpload` et `delete` comme actions de recherche.</span><span class="sxs-lookup"><span data-stu-id="d43cb-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="d43cb-157">Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents.</span><span class="sxs-lookup"><span data-stu-id="d43cb-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="d43cb-158">Notez la façon dont nous n’avait pas toospecify tous les champs de document possible hello lors de l’utilisation `mergeOrUpload` et comment nous spécifiée uniquement clé de document hello (`hotelId`) lors de l’utilisation `delete`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="d43cb-159">Notez également que vous ne pouvez inclure des documents de too1000 (ou 16 Mo) dans une seule demande d’indexation.</span><span class="sxs-lookup"><span data-stu-id="d43cb-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="d43cb-160">Comprendre votre code de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="d43cb-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="d43cb-161">200</span><span class="sxs-lookup"><span data-stu-id="d43cb-161">200</span></span>
<span data-ttu-id="d43cb-162">Lorsque votre demande d’indexation aboutit, vous recevez une réponse HTTP avec le code d’état `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="d43cb-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="d43cb-163">Hello corps JSON de hello réponse HTTP sera comme suit :</span><span class="sxs-lookup"><span data-stu-id="d43cb-163">hello JSON body of hello HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="d43cb-164">207</span><span class="sxs-lookup"><span data-stu-id="d43cb-164">207</span></span>
<span data-ttu-id="d43cb-165">Un code d’état `207` est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="d43cb-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="d43cb-166">Hello corps JSON de la réponse HTTP de hello contiennent des informations sur les documents ayant échoué hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="d43cb-167">Cela signifie souvent qu’une charge hello sur votre recherche service atteint un point où l’indexation des demandes commence tooreturn `503` réponses.</span><span class="sxs-lookup"><span data-stu-id="d43cb-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="d43cb-168">Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="d43cb-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="d43cb-169">Cela donnera système de hello toorecover quelques temps, augmenter les chances de hello succès des futures demandes.</span><span class="sxs-lookup"><span data-stu-id="d43cb-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="d43cb-170">Rapidement une nouvelle tentative de vos demandes sera prolonger uniquement la situation de hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="d43cb-171">429</span><span class="sxs-lookup"><span data-stu-id="d43cb-171">429</span></span>
<span data-ttu-id="d43cb-172">Code d’état `429` s’affichera lorsque vous avez dépassé votre quota de nombre hello de documents par index.</span><span class="sxs-lookup"><span data-stu-id="d43cb-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="d43cb-173">503</span><span class="sxs-lookup"><span data-stu-id="d43cb-173">503</span></span>
<span data-ttu-id="d43cb-174">Code d’état `503` sera retourné si aucun des éléments hello dans la demande hello ont été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="d43cb-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="d43cb-175">Cette erreur signifie que le système de hello est surchargé et que votre demande ne peut pas être traitée pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="d43cb-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="d43cb-176">Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="d43cb-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="d43cb-177">Cela donnera système de hello toorecover quelques temps, augmenter les chances de hello succès des futures demandes.</span><span class="sxs-lookup"><span data-stu-id="d43cb-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="d43cb-178">Rapidement une nouvelle tentative de vos demandes sera prolonger uniquement la situation de hello.</span><span class="sxs-lookup"><span data-stu-id="d43cb-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="d43cb-179">Pour plus d’informations sur les actions de document et les réponses de réussite/d’erreur, consultez la page [Ajouter, mettre à jour ou supprimer des documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="d43cb-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="d43cb-180">Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="d43cb-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43cb-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d43cb-181">Next steps</span></span>
<span data-ttu-id="d43cb-182">Remplissage de l’index Azure Search, vous serez prêt toostart émission toosearch de requêtes pour les documents.</span><span class="sxs-lookup"><span data-stu-id="d43cb-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="d43cb-183">Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="d43cb-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
