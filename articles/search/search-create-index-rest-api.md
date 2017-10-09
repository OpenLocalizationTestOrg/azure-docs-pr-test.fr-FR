---
title: "AAA « créer un index (API REST - Azure Search) | Documents Microsoft »"
description: "Créer un index dans le code à l’aide de hello API REST de Azure Search HTTP."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Créer un index Azure Search à l’aide des API REST de hello
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-what-is-an-index.md)
> * [Portail](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Cet article vous guide tout au long des processus de hello de création d’un indexeur Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) à l’aide de hello API REST Azure Search.

Avant de suivre ce guide et de passer à la création d’un index, vous devez avoir déjà [créé un service Azure Search](search-create-service-portal.md).

toocreate un index Azure Search à l’aide de hello API REST, vous prévoyez d’émettre le point de terminaison d’un HTTP POST demande tooyour Azure service de recherche URL. Votre définition de l’index se trouvera dans le corps de la demande hello en tant que contenu JSON bien formé.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identifier la clé API d’administration de votre service Azure Search
Maintenant que vous avez configuré un service Azure Search, vous pouvez émettre des demandes HTTP sur le point de terminaison URL de votre service à l’aide des API REST de hello. *Tous les* demandes API doivent inclure hello clé api qui a été généré pour hello service de recherche que vous avez configuré. Avoir une clé valide établit l’approbation, sur une base de chaque demande, entre la demande d’application de hello envoi hello et service hello qui prend en charge.

1. toofind api-clés de votre service, vous devez vous connecter à hello [portail Azure](https://portal.azure.com/)
2. Panneau du service tooyour accédez Azure Search
3. Cliquez sur hello icône « Clés »

Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.

* Vos sites principaux et secondaires *clés d’administration* accorder des droits d’accès complets tooall opérations, y compris hello capacité toomanage hello service, créer et supprimer des index, indexeurs et sources de données. Il existe deux clés afin que vous puissiez continuer clé secondaire du hello toouse si vous décidez de tooregenerate hello primary key et vice versa.
* Votre *clés de requête* accorder l’accès en lecture seule tooindexes et des documents, et sont des applications distribuées généralement tooclient qui émettent des demandes de recherche.

Pour des raisons de hello de création d’un index, vous pouvez utiliser votre clé d’administration principal ou secondaire.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Définir votre index Azure Search à l’aide d’un code JSON correct
Un seul service tooyour de demande HTTP POST créera votre index. Hello des corps de votre demande HTTP POST contient un seul objet JSON qui définit votre index Azure Search.

1. Hello première propriété de cet objet JSON désigne hello votre index.
2. Hello de deuxième propriété de cet objet JSON est un tableau JSON nommé `fields` qui contient un objet JSON distinct pour chaque champ dans votre index. Chacun de ces objets JSON contiennent plusieurs paires nom/valeur pour chaque hello d’attributs de champ, y compris le « nom », « type », etc..

Il est important de conserver votre recherche utilisateur expérience et des besoins à l’esprit lorsque vous concevez votre index en tant que chaque champ doit être attribuée hello [attributs corrects](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Ces attributs contrôlent qui recherche les fonctionnalités (filtrage, des facettes, le tri de la recherche en texte intégral, etc.) s’appliquent à des champs de toowhich. Pour tout attribut que vous ne spécifiez pas, par défaut de hello sera fonction de recherche correspondante tooenable hello, sauf si vous la désactiviez spécifiquement.

Dans notre exemple, nous avons nommé notre index « hotels » et défini ses champs de la manière suivante :

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Nous avons choisi avec soin les attributs d’index hello pour chaque champ basé sur la manière dont nous ils seront utilisés dans une application. Par exemple, `hotelId` est une clé unique que vous recherchez hôtels probables ne sont pas informés, afin que nous désactiver la recherche en texte intégral pour ce champ en définissant les personnes `searchable` trop`false`, ce qui économise de l’espace dans les index hello.

Veuillez noter qu’exactement un champ dans l’index de type `Edm.String` doit être hello désigné en tant que champ de 'key' hello.

définition de l’index Hello ci-dessus utilise un analyseur de langage pour hello `description_fr` , car il s’agit de texte Français de toostore prévue. Consultez [rubrique prise en charge du langage hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) , ainsi que de hello correspondant [billet de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) pour plus d’informations sur les analyseurs de langage.

## <a name="issue-hello-http-request"></a>Demande d’émission hello HTTP
1. À l’aide de votre définition de l’index en tant que corps de la demande hello, émettre une URL de point de terminaison de service HTTP POST demande tooyour Azure Search. Dans l’URL de hello, être toouse que le nom de votre service en tant que nom d’hôte hello et que hello approprié `api-version` comme paramètre de chaîne de requête (version actuelle de l’API hello est `2016-09-01` au moment de hello de publication de ce document).
2. Dans les en-têtes de demande hello, spécifiez hello `Content-Type` comme `application/json`. Vous devez également tooprovide clé d’administration de votre service que vous avez identifié l’étape I Bonjour `api-key` en-tête.

Vous devez tooprovide votre propre nom et l’api tooissue clé hello demande de service ci-dessous :

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Pour que votre requête aboutisse, vous devez voir le code d’état « 201 créé ». Pour plus d’informations sur la création d’un index via l’API REST de hello, visitez hello [référence d’API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [Codes d’état HTTP (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Lorsque vous avez terminé une toodelete index et que vous souhaitez qu’il, génère une demande HTTP DELETE. Il s’agit par exemple, comment nous serait supprimer les index de « hôtels » hello :

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Étapes suivantes
Après avoir créé un index Azure Search, vous serez prêt trop[télécharger votre contenu dans les index hello](search-what-is-data-import.md) pour que vous puissiez rechercher vos données.
