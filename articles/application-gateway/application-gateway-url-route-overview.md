---
title: "en fonction d’aaaURL la vue d’ensemble de routage contenu | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble du routage d’hello basée sur l’URL de la passerelle Application contenu, UrlPathMap configuration et PathBasedRouting règle."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="a3572-103">Présentation du routage basé sur le chemin d’accès de l’URL</span><span class="sxs-lookup"><span data-stu-id="a3572-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="a3572-104">URL du chemin d’accès de routage permet de vous tooroute trafic tooback-end pools de serveurs basés sur les chemins d’accès de l’URL de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a3572-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="a3572-105">Un des scénarios de hello est tooroute des demandes pour les pools de serveurs principaux différents types de contenu toodifferent.</span><span class="sxs-lookup"><span data-stu-id="a3572-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="a3572-106">Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com, à partir de trois pools de serveur principal par exemple : VideoServerPool, ImageServerPool et DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="a3572-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="a3572-108">Demandes de http://contoso.com/video * sont routé tooVideoServerPool et http://contoso.com/images * sont routé tooImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="a3572-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="a3572-109">DefaultServerPool est sélectionnée si aucun des modèles de chemin d’accès hello correspondent.</span><span class="sxs-lookup"><span data-stu-id="a3572-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3572-110">Règles sont traitées dans l’ordre de hello qu’ils sont répertoriés dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a3572-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="a3572-111">Il est tooconfiguring préalable première de plusieurs sites écouteurs de tooconfigure fortement recommandé un écouteur de base.</span><span class="sxs-lookup"><span data-stu-id="a3572-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="a3572-112">Cela garantit sa que toohello de routé Obtient le trafic de fin.</span><span class="sxs-lookup"><span data-stu-id="a3572-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="a3572-113">Si un écouteur de base est indiqué en premier et correspond à une demande entrante, elle est traitée par cet écouteur.</span><span class="sxs-lookup"><span data-stu-id="a3572-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="a3572-114">Élément de configuration UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="a3572-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="a3572-115">élément d’urlPathMap Hello est utilisé toospecify tooback-fin de modèles de chemin d’accès des mappages de pool de serveurs.</span><span class="sxs-lookup"><span data-stu-id="a3572-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="a3572-116">Bonjour exemple de code suivant est extrait de code hello d’élément urlPathMap à partir du fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="a3572-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="a3572-117">PathPattern : Ce paramètre est une liste de toomatch des modèles de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="a3572-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="a3572-118">Chacun doit commencer par / et hello uniquement une « * » est autorisé à hello fin suit une « / ».</span><span class="sxs-lookup"><span data-stu-id="a3572-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="a3572-119">chaîne Hello fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord ? ou bien, # et ces caractères ne sont pas autorisés ici.</span><span class="sxs-lookup"><span data-stu-id="a3572-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="a3572-120">Pour plus d’informations, vous pouvez consulter un [modèle Resource Manager utilisant le routage basé sur URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .</span><span class="sxs-lookup"><span data-stu-id="a3572-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="a3572-121">Règle PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="a3572-121">PathBasedRouting rule</span></span>

<span data-ttu-id="a3572-122">RequestRoutingRule de type PathBasedRouting est toobind utilisé un urlPathMap de tooa d’écouteur.</span><span class="sxs-lookup"><span data-stu-id="a3572-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="a3572-123">Toutes les demandes qui sont reçues par cet écouteur sont acheminées en fonction de la stratégie spécifiée dans l’élément urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="a3572-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="a3572-124">Exemple de la règle PathBasedRouting :</span><span class="sxs-lookup"><span data-stu-id="a3572-124">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="a3572-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3572-125">Next steps</span></span>

<span data-ttu-id="a3572-126">Une fois l’apprentissage sur le routage de contenu basée sur URL, rendez-vous trop[créer une passerelle d’application à l’aide de routage basé sur les URL](application-gateway-create-url-route-portal.md) toocreate une passerelle d’application avec les règles de routage d’URL.</span><span class="sxs-lookup"><span data-stu-id="a3572-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
