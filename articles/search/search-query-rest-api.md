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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Interroger votre index Azure Search à l’aide des API REST de hello
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-query-overview.md)
> * [Portail](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Cet article explique comment un index à l’aide de tooquery hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/).

Avant de commencer cette procédure, vous devez déjà avoir [créé un index de Recherche Azure](search-what-is-an-index.md) et y avoir [ajouté des données](search-what-is-data-import.md). Pour des informations générales, consultez l’article [Fonctionnement de la recherche en texte intégral dans la recherche Azure](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Identifier la clé API de requête de votre service Azure Search
Un composant essentiel de chaque opération de recherche sur hello API REST Azure Search est hello *clé api* qui a été généré pour le service hello vous avez configuré. Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.

1. toofind les clés de votre service api, vous pouvez vous connecter toohello [portail Azure](https://portal.azure.com/)
2. Panneau du service tooyour accédez Azure Search
3. Cliquez sur icône « Clés » de hello

Votre service inclut des *clés d’administration* et des *clés de requête*.

* Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données. Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.
* Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.

Pour des raisons de hello d’interrogation d’un index, vous pouvez utiliser un de vos clés de requête. Vos clés d’administration peuvent également être utilisés pour les requêtes, mais vous devez utiliser une clé de requête dans votre code d’application, comme cela suit mieux hello [principe de privilège minimum](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Formuler votre requête
Il existe deux façons de trop[rechercher votre index à l’aide des API REST de hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Une façon consiste tooissue une requête HTTP POST où vos paramètres de requête sont définis dans un objet JSON dans le corps de la demande hello. Hello autre façon est tooissue une requête HTTP GET dans lequel vos paramètres de requête sont définis dans l’URL de demande hello. POST a plusieurs [assouplie limites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) taille hello de paramètres de requête que GET. Pour cette raison, nous vous recommandons d’utiliser POST, à moins que la situation justifie l’utilisation de GET.

POST ou GET, vous devez tooprovide votre *nom du service*, *nom de l’index*et hello approprié *version de l’API* (version actuelle de l’API hello est `2016-09-01` au moment de hello de la publication de ce document) Bonjour URL de demande. Pour obtenir, hello *chaîne de requête* hello fin de l’URL de hello est où vous fournir les paramètres de requête hello. Voir ci-dessous pour le format d’URL hello :

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Bonjour format pour POST est hello identiques, mais uniquement avec api-version dans les paramètres de chaîne de requête hello.

#### <a name="example-queries"></a>Exemples de requêtes
Voici quelques exemples de requêtes effectuées sur un index nommé « hotels ». Ces requêtes sont présentées aux formats GET et POST.

Rechercher les index tout entier hello hello terme « budget » et de retourner uniquement hello `hotelName` champ :

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Appliquer un hôtels de toofind filtre toohello index moins chère que 150 $ par nuit et retourner hello `hotelId` et `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Index de recherche hello entière, order by, un champ spécifique (`lastRenovationDate`) dans l’ordre décroissant, hello deux premiers résultats, de n’afficher que `hotelName` et `lastRenovationDate`:

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

## <a name="submit-your-http-request"></a>Envoyer votre requête HTTP
Maintenant que vous avez formulé votre requête dans l’URL (pour GET) ou dans le corps (pour POST) de votre requête HTTP, vous pouvez définir vos en-têtes de requête et envoyer votre requête.

#### <a name="request-and-request-headers"></a>Requête et en-têtes de requête
Vous devez définir deux en-têtes de requête pour GET, ou trois en-têtes pour POST :

1. Hello `api-key` en-tête doit être défini de clé de requête toohello trouvé à l’étape I ci-dessus. Vous pouvez également utiliser une clé d’administration en tant que hello `api-key` en-tête, mais il est recommandé d’utiliser une clé de requête car elle exclusivement accorde l’accès en lecture seule tooindexes et des documents.
2. Hello `Accept` en-tête doit être défini trop`application/json`.
3. Pour valider uniquement, hello `Content-Type` en-tête doit également être défini trop`application/json`.

Voir ci-dessous pour un HTTP GET demande toosearch hello « hôtels » index à l’aide de hello API REST Azure Search à l’aide d’une requête simple qui recherche le terme hello « motel » :

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Voici hello même exemple de requête, cette fois à l’aide de HTTP POST :

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Une demande de requête réussie génère un Code d’état de `200 OK` et résultats de la recherche hello sont retournés en tant que JSON dans le corps de la réponse hello. Voici le hello résultats pour hello au-dessus de requête ressemble en supposant que l’index de « hôtels » de hello est remplie avec les données d’exemple hello dans [importation de données à l’aide d’Azure Search hello API REST](search-import-data-rest-api.md) (Notez que hello JSON a été mis en forme par souci de clarté).

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

toolearn plus, visitez section « Réponse » hello [recherche de Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
