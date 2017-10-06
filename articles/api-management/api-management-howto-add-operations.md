---
title: aaaHow tooadd operations tooan API de gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooadd opérations tooan API de gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Comment tooadd opérations tooan API de gestion des API Azure
Pour qu'une API puisse être utilisée dans Gestion des API, vous devez ajouter des opérations. Ce guide montre comment tooadd et configurer les différents types d’opérations tooan API de gestion des API.

## <a name="add-operation"></a>Ajout d’une opération
Les opérations sont ajoutées et configurés tooan API dans le portail de publication hello. tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Sélectionnez hello souhaité API dans le portail de publication hello et puis sélectionnez hello **Operations** onglet. 

![Opérations][api-management-operations]

Cliquez sur **ajouter une opération** tooadd une nouvelle opération. Hello **nouvelle opération** s’affichera et hello **Signature** est activée par défaut.

![Ajouter une opération][api-management-add-operation]

Spécifiez hello **verbe HTTP** en choisissant dans la liste déroulante de hello.

![HTTP method][api-management-http-method]

<a name="url-template"></a>

Définir le modèle d’URL hello en tapant dans un fragment d’URL consistant en un ou plusieurs segments de chemin d’accès d’URL et zéro ou plusieurs paramètres de chaîne de requête. modèle d’URL Hello, URL de base toohello ajouté de hello API, identifie une seule opération HTTP. Il peut contenir une ou plusieurs parties variables identifiées par des accolades. Ces parties variables sont appelées des paramètres de modèle et sont affectés dynamiquement les valeurs extraites à partir de l’URL de la demande hello lors de la demande de hello est traitée par la plateforme de gestion des API hello.

> modèle d’URL Hello peut inclure des caractères génériques. Par exemple, la spécification `/*` par progression toutes les demandes de nouveau ce toohello de méthode HTTP ne pourront service.

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

Si vous le souhaitez, spécifier hello **modèle de réécrire les URL**. Cela vous permet de modèle d’URL standard toouse hello pour le traitement des demandes entrantes sur hello frontal, lors de l’appel hello principal via une URL convertie selon toohello Réécrivez le modèle. Paramètres de modèle à partir du modèle d’URL hello doivent être utilisés dans le modèle de réécriture hello. Hello suivant montre comment le contenu type encodé comme segment de chemin d’accès dans le service web pour hello hello précédent exemple peut être fourni comme paramètre de requête Bonjour API publiés via hello plateforme de gestion des API à l’aide de modèles d’URL hello.

![URL template rewrite][api-management-url-template-rewrite]

Opération de toohello appelants utilisent hello format `/customers?customerid=ALFKI` et il sera mappé trop`/Customers('ALFKI')` lorsque le service principal de hello est appelé.

**Affichage** nom et **Description** fournissent une description de l’opération de hello et est utilisés tooprovide documentation toohello les développeurs utilisant cette API dans le portail des développeurs hello.

![Description][api-management-description]

description de l’opération Hello peut être spécifiée en tant que texte brut ou HTML Bonjour **Description** zone de texte.

## <a name="operation-caching"></a>Mise en cache de l’opération
Réponse mise en cache réduit la latence perçue par les consommateurs hello API, permet de réduire la consommation de bande passante et la charge de hello diminue sur l’implémentation du service web hello HTTP hello API. 

tooeasily et d’activer rapidement la mise en cache pour l’opération de hello, sélectionnez hello **mise en cache** et vérifiez hello **activer** case à cocher.

![Mise en cache][api-management-caching-tab]

**Durée** spécifie hello laps de temps pendant le hello réponse d’opération reste dans le cache de hello. Hello par défaut est 3 600 secondes ou 1 heure.

Les clés de cache sont toodifferentiate utilisé entre les réponses afin que la réponse hello correspondant de clé de cache différents tooeach obtiendra sa propre valeur de mise en cache distinct. Si vous le souhaitez, entrez les paramètres de chaîne de requête spécifique et/ou toobe d’en-têtes HTTP utilisés dans le calcul de valeurs de clé de cache Bonjour **variation par paramètres de chaîne de requête** et **variation par en-têtes** respectivement des zones de texte. Lorsque aucun sont des URL de demande spécifié, complète et hello valeurs d’en-tête HTTP suivantes est utilisée dans la génération de clé de cache : **accepter** et **Accept-Charset**.

> Pour plus d’informations sur la mise en cache et la mise en cache des stratégies, consultez [affichage des résultats dans la gestion des API Azure toocache opération][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Paramètres de la demande
Paramètres de l’opération sont gérés sur l’onglet Paramètres de hello. Paramètres spécifiés dans hello **modèle d’URL** sur hello **Signature** onglet sont ajoutés automatiquement et peut être modifiée qu’en modifiant le modèle d’URL hello. D'autres paramètres peuvent être ajoutés manuellement.

tooadd un nouveau paramètre de requête, cliquez sur **ajouter un paramètre de requête** et entrez hello informations suivantes :

* **Nom** : nom du paramètre.
* **Description** -une brève description du paramètre hello (facultatif).
* **Type** -type de paramètre, sélectionné dans la liste déroulante hello.
* **Valeurs** -valeurs pouvant être affectées toothis paramètre. Une des valeurs de hello peut être marquée comme valeur par défaut (facultative).
* **Requis** -que le paramètre hello obligatoire en activant la case à cocher hello. 

![Paramètres de la demande][api-management-request-parameters]

## <a name="request-body"></a>Corps de la demande
Si l’opération de hello permet (par exemple, PUT, POST) et nécessite un corps, vous pouvez fournir un exemple de celui-ci dans toutes les hello pris en charge les formats de représentation (par exemple, au format json, XML). 

> corps de la demande Hello est utilisé uniquement à des fins de documentation et n’est pas validé.
> 
> 

tooenter un corps de demande, basculez toohello **corps** onglet.

Cliquez sur **ajouter la représentation sous forme**, commencez à taper le nom du type de contenu de votre choix (par exemple, application/json), sélectionnez-le dans la liste déroulante de hello et coller hello souhaité d’exemple de corps de demande dans le format sélectionné de hello dans la zone de texte hello. 

![Corps de la demande][api-management-request-body]

Dans toorepresentations supplémentaires, vous pouvez également spécifier une description facultative dans hello **Description** zone de texte.

## <a name="responses"></a>Réponses
Il s’agit d’une bonne pratique tooprovide obtenir des exemples de réponses pour tous les codes d’état hello opération risque de générer. Chaque code d’état peut avoir plus d’un exemple de corps de réponse, une pour chaque hello pris en charge les types de contenu. 

tooadd une réponse, cliquez sur **ajouter** et commencez à taper le code d’état hello souhaité. Dans cet exemple hello d’état est code **200 OK**. Une fois que le code de hello s’affiche dans hello de liste déroulante, sélectionnez-la et code de réponse hello est créé et ajouté tooyour opération.

![Response code][api-management-response-code]

Cliquez sur **ajouter la représentation sous forme**, commencez à taper le nom de type de contenu souhaité hello (par exemple, application/json) et sélectionnez dans hello déroulante.

![Body content type][api-management-response-body-content-type]

Collez l’exemple de corps de réponse hello dans le format sélectionné de hello dans la zone de texte hello. 

![Response body][api-management-response-body]

Si vous le souhaitez, ajoutez une description facultative dans hello **Description** zone de texte.

Une fois l’opération de hello est configurée, cliquez sur **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Une fois les opérations de hello ajoutées tooan API, étape suivante de hello est tooassociate hello API avec un produit et la publier afin que les développeurs peuvent appeler ses opérations.

* [Comment toocreate et publier un produit][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
