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
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>À l’aide de téléchargement données tooAzure recherche hello API REST
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

Cet article vous indiquent comment toouse hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/) tooimport les données dans un index Azure Search.

Avant de commencer cette procédure, vous devez déjà avoir [créé un index Azure Search](search-what-is-an-index.md).

Documents de toopush de commande dans votre index à l’aide de hello API REST, vous prévoyez d’émettre des point de terminaison URL HTTP POST demande tooyour d’un index. corps Hello Hello demande HTTP corps est un objet JSON qui contient les documents hello toobe ajouté, modifié ou supprimé.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identifier la clé API d’administration de votre service Azure Search
Lors de l’émission des demandes HTTP sur votre service à l’aide de hello API REST, *chaque* demande d’API doit inclure hello clé api qui a été généré pour hello service de recherche que vous avez configuré. Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.

1. toofind les clés de votre service api, vous pouvez vous connecter toohello [portail Azure](https://portal.azure.com/)
2. Panneau du service tooyour accédez Azure Search
3. Cliquez sur hello icône « Clés »

Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.

* Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données. Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.
* Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.

Pour des raisons de hello de l’importation de données dans un index, vous pouvez utiliser votre clé d’administration principal ou secondaire.

## <a name="decide-which-indexing-action-toouse"></a>Décidez quels toouse action d’indexation
Lorsque vous utilisez hello API REST, vous prévoyez d’émettre les requêtes HTTP POST avec l’URL du demande organismes tooyour Azure Search index JSON point de terminaison. objet JSON de Hello dans le corps de la requête HTTP contient un tableau JSON nommé « valeur » qui contient des objets JSON représentant les documents que vous aimeriez tooadd tooyour index, update ou delete.

Chaque objet JSON dans le tableau de « value » hello représente un toobe document indexé. Chacun de ces objets contient la clé du document hello et spécifie l’action de l’indexation hello souhaitée (téléchargement, fusionner, supprimer, etc.). En fonction de hello ci-dessous les actions que vous choisissez, uniquement certains champs doivent être inclus pour chaque document :

| @search.action | Description | Champs requis pour chaque document | Remarques |
| --- | --- | --- | --- |
| `upload` |Un `upload` action est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |Lors de la mise à jour/remplacement d’un document existant, un champ qui n’est pas spécifié dans la demande hello aura son champ défini trop`null`. Cela se produit même lorsque hello a été défini précédemment tooa nulle. |
| `merge` |Mises à jour existant de document avec hello spécifié des champs. Si le document de hello n’existe pas dans l’index de hello, la fusion de hello échoue. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello. Cela inclut les champs de type `Collection(Edm.String)`. Par exemple, si hello document contient un champ `tags` avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour `tags`, hello valeur finale de hello `tags` champ sera `["economy", "pool"]`. et non `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Cette action se comporte comme `merge` si un document avec hello donné clé déjà existe dans les index hello. Si le document de hello n’existe pas, il se comporte comme `upload` avec un nouveau document. |clé, ainsi que tous les autres champs que vous souhaitez toodefine |- |
| `delete` |Supprime l’index de hello de document spécifié de hello. |clé uniquement |Tous les champs que vous spécifiez d’autres que le champ de clé hello sera ignoré. Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `merge` à la place et simplement définir explicitement les champs de hello toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Construire votre requête HTTP et le corps de la requête
Maintenant que vous avez rassemblé les valeurs de champ nécessaire hello pour les actions de votre index, vous demande de prêt tooconstruct hello réelle HTTP et tooimport de corps de demande JSON vos données.

#### <a name="request-and-request-headers"></a>Requête et en-têtes de requête
Dans l’URL de hello, vous devez tooprovide votre nom de service, nom de l’index (« hôtels » dans ce cas), ainsi que les version appropriée de l’API hello (version actuelle de l’API hello est `2016-09-01` au moment de hello de publication de ce document). Vous devez toodefine hello `Content-Type` et `api-key` en-têtes de demande. Pourquoi ce dernier, utilisez une des clés d’administration de votre service.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Corps de la requête
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

Dans ce cas, nous utilisons `upload`, `mergeOrUpload` et `delete` comme actions de recherche.

Supposons que cet exemple d’index « hotels » contient déjà un certain nombre de documents. Notez la façon dont nous n’avait pas toospecify tous les champs de document possible hello lors de l’utilisation `mergeOrUpload` et comment nous spécifiée uniquement clé de document hello (`hotelId`) lors de l’utilisation `delete`.

Notez également que vous ne pouvez inclure des documents de too1000 (ou 16 Mo) dans une seule demande d’indexation.

## <a name="understand-your-http-response-code"></a>Comprendre votre code de réponse HTTP
#### <a name="200"></a>200
Lorsque votre demande d’indexation aboutit, vous recevez une réponse HTTP avec le code d’état `200 OK`. Hello corps JSON de hello réponse HTTP sera comme suit :

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

#### <a name="207"></a>207
Un code d’état `207` est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé. Hello corps JSON de la réponse HTTP de hello contiennent des informations sur les documents ayant échoué hello.

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
> Cela signifie souvent qu’une charge hello sur votre recherche service atteint un point où l’indexation des demandes commence tooreturn `503` réponses. Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative. Cela donnera système de hello toorecover quelques temps, augmenter les chances de hello succès des futures demandes. Rapidement une nouvelle tentative de vos demandes sera prolonger uniquement la situation de hello.
>
>

#### <a name="429"></a>429
Code d’état `429` s’affichera lorsque vous avez dépassé votre quota de nombre hello de documents par index.

#### <a name="503"></a>503
Code d’état `503` sera retourné si aucun des éléments hello dans la demande hello ont été correctement indexé. Cette erreur signifie que le système de hello est surchargé et que votre demande ne peut pas être traitée pour l’instant.

> [!NOTE]
> Dans ce cas, nous vous recommandons vivement de désactiver votre code client et d’attendre avant d’effectuer une nouvelle tentative. Cela donnera système de hello toorecover quelques temps, augmenter les chances de hello succès des futures demandes. Rapidement une nouvelle tentative de vos demandes sera prolonger uniquement la situation de hello.
>
>

Pour plus d’informations sur les actions de document et les réponses de réussite/d’erreur, consultez la page [Ajouter, mettre à jour ou supprimer des documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Étapes suivantes
Remplissage de l’index Azure Search, vous serez prêt toostart émission toosearch de requêtes pour les documents. Pour plus d’informations, consultez l’article [Interroger votre index Azure Search](search-query-overview.md) .
