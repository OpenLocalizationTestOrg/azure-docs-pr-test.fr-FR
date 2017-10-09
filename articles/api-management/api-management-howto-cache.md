---
title: aaaAdd mise en cache des performances tooimprove dans Gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooimprove hello latence, la consommation de bande passante et service web de charge pour les appels de service de gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Ajouter des performances tooimprove mise en cache dans la gestion des API Azure
Les opérations dans Gestion des API Azure peuvent être configurées pour mettre en cache la réponse. La mise en cache de la réponse peut réduire de façon importante la latence de l'API, la consommation de bande passante et la charge du service web pour les données qui ne changent pas fréquemment.

Ce guide vous montre comment tooadd réponse mise en cache pour votre API et de configurer des stratégies pour les opérations de l’API d’écho exemple hello. Vous pouvez ensuite appeler l’opération de hello de hello développeur tooverify portail mise en cache en action.

> [!NOTE]
> Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Composants requis
Avant de hello suivant les étapes de ce guide, vous devez disposer d’une instance de service de gestion des API avec une API et un produit configuré. Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.

## <a name="configure-caching"></a>Configuration d’une opération de mise en cache
Dans cette étape, vous allez examiner hello mise en cache des paramètres de hello **obtenir des ressources (mise en cache)** l’opération de l’exemple hello Echo API.

> [!NOTE]
> Chaque instance de service de gestion des API est préconfiguré avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API. Pour plus d'informations, consultez la page [Prise en main de Gestion des API Azure][Get started with Azure API Management].
> 
> 

tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello.

![Portail des éditeurs][api-management-management-console]

Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **Echo API**.

![API Echo][api-management-echo-api]

Cliquez sur hello **Operations** onglet, puis cliquez sur hello **obtenir des ressources (mise en cache)** opération hello **Operations** liste.

![Echo API operations][api-management-echo-api-operations]

Cliquez sur hello **mise en cache** hello de tooview onglet mise en cache des paramètres pour cette opération.

![Caching tab][api-management-caching-tab]

tooenable mise en cache pour une opération, sélectionnez hello **activer** case à cocher. Dans cet exemple, la mise en cache est activée.

Chaque réponse de l’opération est indexé, en fonction des valeurs hello hello **variation par paramètres de chaîne de requête** et **variation par en-têtes** champs. Si vous souhaitez toocache plusieurs réponses selon les paramètres de chaîne de requête ou les en-têtes, vous pouvez les configurer dans ces deux champs.

**Durée** Spécifie l’intervalle d’expiration de hello des réponses de hello mis en cache. Dans cet exemple, l’intervalle de salutation est **3600** secondes, ce qui est équivalent tooone heure.

À l’aide de hello mise en cache de configuration dans cet exemple, hello première demande toohello **obtenir des ressources (mise en cache)** opération renvoie une réponse à partir du service principal de hello. Cette réponse est mises en cache, indexé par hello spécifié paramètres de chaîne de requête et les en-têtes. Les appels suivants toohello opération, avec des paramètres, de correspondance aura hello mis en cache la réponse retourné, jusqu'à ce que l’intervalle de durée hello du cache a expiré.

## <a name="caching-policies"></a>Hello révision des stratégies de mise en cache
Dans cette étape, vous passez en revue hello mise en cache des paramètres pour hello **obtenir des ressources (mise en cache)** l’opération de l’exemple hello Echo API.

Lorsque les paramètres de mise en cache sont configurés pour une opération sur hello **mise en cache** sous l’onglet mise en cache des stratégies sont ajoutés pour l’opération de hello. Ces stratégies peuvent être affichées et modifiées dans l’éditeur de stratégie hello.

Cliquez sur **stratégies** de hello **gestion des API** menu hello gauche et sélectionnez **Echo API / obtenir des ressources (mise en cache)** de hello **opération**liste déroulante.

![Policy scope operation][api-management-operation-dropdown]

Cela affiche les stratégies de hello pour cette opération dans l’éditeur de stratégie hello.

![API Management policy editor][api-management-policy-editor]

définition de la stratégie Hello pour cette opération inclut hello stratégies qui définissent hello mise en cache de configuration qui ont été vérifiés à l’aide de hello **mise en cache** onglet à l’étape précédente de hello.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Toohello modifications mise en cache des stratégies dans l’éditeur de stratégie hello apparaîtront sur hello **mise en cache** onglet d’une opération et vice versa.
> 
> 

## <a name="test-operation"></a>Appeler une opération et tester la mise en cache hello
toosee hello mise en cache en action, nous pouvons appeler l’opération de hello à partir du portail des développeurs hello. Cliquez sur **portail des développeurs** dans le menu supérieur droit de hello.

![Portail des développeurs][api-management-developer-portal-menu]

Cliquez sur **API** dans hello menu supérieur, puis sélectionnez **Echo API**.

![API Echo][api-management-apis-echo-api]

> Si vous n'avez qu’une seule API configurée ou tooyour visible compte, puis en cliquant sur API vous amène directement operations toohello pour cette API.
> 
> 

Sélectionnez hello **obtenir des ressources (mise en cache)** opération, puis cliquez sur **ouvrir la Console**.

![Open console][api-management-open-console]

Hello console permet les opérations tooinvoke directement depuis le portail des développeurs hello.

![Console][api-management-console]

Conserver les valeurs par défaut de hello **param1** et **param2**.

Sélectionnez hello clé souhaitée à partir de hello **clé d’abonnement** liste déroulante. Si votre compte n’a qu’un abonnement, celui-ci est déjà sélectionné.

Entrez **sampleheader:value1** Bonjour **en-têtes de demande** zone de texte.

Cliquez sur **HTTP Get** et prenez note de hello en-têtes de réponse.

Entrez **sampleheader:value2** Bonjour **en-têtes de demande** zone de texte, puis cliquez sur **HTTP Get**.

Notez que valeur hello de **sampleheader** est toujours **value1** dans la réponse de hello. Essayez certaines des valeurs différentes, et notez que hello réponse mise en cache à partir du premier appel de hello est retournée.

Entrez **25** dans hello **param2** champ, puis cliquez sur **HTTP Get**.

Notez que valeur hello de **sampleheader** Bonjour réponse est désormais **value2**. Étant donné que les résultats de l’opération hello sont indexées par chaîne de requête, la réponse mise en cache de hello précédente n’a pas retourné.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la mise en cache des stratégies, consultez [mise en cache des stratégies] [ Caching policies] Bonjour [référence de stratégie de gestion des API][API Management policy reference].
* Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
