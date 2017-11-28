---
title: "AAA » interroger un index (API REST - Azure Search) | Documents Microsoft »"
description: "Générer une requête de recherche dans Azure search et utilisez les paramètres toofilter et tri recherche résultats de la recherche."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="b447f-103">Interroger votre index Azure Search à l’aide des API REST de hello</span><span class="sxs-lookup"><span data-stu-id="b447f-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="b447f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b447f-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b447f-105">Portail</span><span class="sxs-lookup"><span data-stu-id="b447f-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="b447f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="b447f-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b447f-107">REST</span><span class="sxs-lookup"><span data-stu-id="b447f-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="b447f-108">Cet article explique comment un index à l’aide de tooquery hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="b447f-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="b447f-109">Avant de commencer cette procédure, vous devez déjà avoir [créé un index de Recherche Azure](search-what-is-an-index.md) et y avoir [ajouté des données](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="b447f-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="b447f-110">Pour des informations générales, consultez l’article [Fonctionnement de la recherche en texte intégral dans la recherche Azure](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="b447f-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="b447f-111">Identifier la clé API de requête de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="b447f-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="b447f-112">Un composant essentiel de chaque opération de recherche sur hello API REST Azure Search est hello *clé api* qui a été généré pour le service hello vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="b447f-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="b447f-113">Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.</span><span class="sxs-lookup"><span data-stu-id="b447f-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="b447f-114">toofind les clés de votre service api, vous pouvez vous connecter toohello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b447f-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="b447f-115">Panneau du service tooyour accédez Azure Search</span><span class="sxs-lookup"><span data-stu-id="b447f-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="b447f-116">Cliquez sur icône « Clés » de hello</span><span class="sxs-lookup"><span data-stu-id="b447f-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="b447f-117">Votre service inclut des *clés d’administration* et des *clés de requête*.</span><span class="sxs-lookup"><span data-stu-id="b447f-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="b447f-118">Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données.</span><span class="sxs-lookup"><span data-stu-id="b447f-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="b447f-119">Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.</span><span class="sxs-lookup"><span data-stu-id="b447f-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="b447f-120">Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="b447f-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="b447f-121">Pour des raisons de hello d’interrogation d’un index, vous pouvez utiliser un de vos clés de requête.</span><span class="sxs-lookup"><span data-stu-id="b447f-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="b447f-122">Vos clés d’administration peuvent également être utilisés pour les requêtes, mais vous devez utiliser une clé de requête dans votre code d’application, comme cela suit mieux hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="b447f-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="b447f-123">Formuler votre requête</span><span class="sxs-lookup"><span data-stu-id="b447f-123">Formulate your query</span></span>
<span data-ttu-id="b447f-124">Il existe deux façons de trop[rechercher votre index à l’aide des API REST de hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="b447f-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="b447f-125">Une façon consiste tooissue une requête HTTP POST où vos paramètres de requête sont définis dans un objet JSON dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="b447f-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="b447f-126">Hello autre façon est tooissue une requête HTTP GET dans lequel vos paramètres de requête sont définis dans l’URL de demande hello.</span><span class="sxs-lookup"><span data-stu-id="b447f-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="b447f-127">POST a plusieurs [assouplie limites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) taille hello de paramètres de requête que GET.</span><span class="sxs-lookup"><span data-stu-id="b447f-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="b447f-128">Pour cette raison, nous vous recommandons d’utiliser POST, à moins que la situation justifie l’utilisation de GET.</span><span class="sxs-lookup"><span data-stu-id="b447f-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="b447f-129">POST ou GET, vous devez tooprovide votre *nom du service*, *nom de l’index*et hello approprié *version de l’API* (version actuelle de l’API hello est `2016-09-01` au moment de hello de la publication de ce document) Bonjour URL de demande.</span><span class="sxs-lookup"><span data-stu-id="b447f-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="b447f-130">Pour obtenir, hello *chaîne de requête* hello fin de l’URL de hello est où vous fournir les paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="b447f-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="b447f-131">Voir ci-dessous pour le format d’URL hello :</span><span class="sxs-lookup"><span data-stu-id="b447f-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="b447f-132">Bonjour format pour POST est hello identiques, mais uniquement avec api-version dans les paramètres de chaîne de requête hello.</span><span class="sxs-lookup"><span data-stu-id="b447f-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="b447f-133">Exemples de requêtes</span><span class="sxs-lookup"><span data-stu-id="b447f-133">Example Queries</span></span>
<span data-ttu-id="b447f-134">Voici quelques exemples de requêtes effectuées sur un index nommé « hotels ».</span><span class="sxs-lookup"><span data-stu-id="b447f-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="b447f-135">Ces requêtes sont présentées aux formats GET et POST.</span><span class="sxs-lookup"><span data-stu-id="b447f-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="b447f-136">Rechercher les index tout entier hello hello terme « budget » et de retourner uniquement hello `hotelName` champ :</span><span class="sxs-lookup"><span data-stu-id="b447f-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="b447f-137">Appliquer un hôtels de toofind filtre toohello index moins chère que 150 $ par nuit et retourner hello `hotelId` et `description`:</span><span class="sxs-lookup"><span data-stu-id="b447f-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="b447f-138">Index de recherche hello entière, order by, un champ spécifique (`lastRenovationDate`) dans l’ordre décroissant, hello deux premiers résultats, de n’afficher que `hotelName` et `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="b447f-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="b447f-139">Envoyer votre requête HTTP</span><span class="sxs-lookup"><span data-stu-id="b447f-139">Submit your HTTP request</span></span>
<span data-ttu-id="b447f-140">Maintenant que vous avez formulé votre requête dans l’URL (pour GET) ou dans le corps (pour POST) de votre requête HTTP, vous pouvez définir vos en-têtes de requête et envoyer votre requête.</span><span class="sxs-lookup"><span data-stu-id="b447f-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="b447f-141">Requête et en-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="b447f-141">Request and Request Headers</span></span>
<span data-ttu-id="b447f-142">Vous devez définir deux en-têtes de requête pour GET, ou trois en-têtes pour POST :</span><span class="sxs-lookup"><span data-stu-id="b447f-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="b447f-143">Hello `api-key` en-tête doit être défini de clé de requête toohello trouvé à l’étape I ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b447f-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="b447f-144">Vous pouvez également utiliser une clé d’administration en tant que hello `api-key` en-tête, mais il est recommandé d’utiliser une clé de requête car elle exclusivement accorde l’accès en lecture seule tooindexes et des documents.</span><span class="sxs-lookup"><span data-stu-id="b447f-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="b447f-145">Hello `Accept` en-tête doit être défini trop`application/json`.</span><span class="sxs-lookup"><span data-stu-id="b447f-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="b447f-146">Pour valider uniquement, hello `Content-Type` en-tête doit également être défini trop`application/json`.</span><span class="sxs-lookup"><span data-stu-id="b447f-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="b447f-147">Voir ci-dessous pour un HTTP GET demande toosearch hello « hôtels » index à l’aide de hello API REST Azure Search à l’aide d’une requête simple qui recherche le terme hello « motel » :</span><span class="sxs-lookup"><span data-stu-id="b447f-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="b447f-148">Voici hello même exemple de requête, cette fois à l’aide de HTTP POST :</span><span class="sxs-lookup"><span data-stu-id="b447f-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="b447f-149">Une demande de requête réussie génère un Code d’état de `200 OK` et résultats de la recherche hello sont retournés en tant que JSON dans le corps de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="b447f-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="b447f-150">Voici le hello résultats pour hello au-dessus de requête ressemble en supposant que l’index de « hôtels » de hello est remplie avec les données d’exemple hello dans [importation de données à l’aide d’Azure Search hello API REST](search-import-data-rest-api.md) (Notez que hello JSON a été mis en forme par souci de clarté).</span><span class="sxs-lookup"><span data-stu-id="b447f-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="b447f-151">toolearn plus, visitez section « Réponse » hello [recherche de Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="b447f-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="b447f-152">Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="b447f-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
