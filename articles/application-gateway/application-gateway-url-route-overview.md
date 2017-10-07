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
# <a name="url-path-based-routing-overview"></a>Présentation du routage basé sur le chemin d’accès de l’URL

URL du chemin d’accès de routage permet de vous tooroute trafic tooback-end pools de serveurs basés sur les chemins d’accès de l’URL de demande de hello. 

Un des scénarios de hello est tooroute des demandes pour les pools de serveurs principaux différents types de contenu toodifferent.

Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com, à partir de trois pools de serveur principal par exemple : VideoServerPool, ImageServerPool et DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Demandes de http://contoso.com/video * sont routé tooVideoServerPool et http://contoso.com/images * sont routé tooImageServerPool. DefaultServerPool est sélectionnée si aucun des modèles de chemin d’accès hello correspondent.

> [!IMPORTANT]
> Règles sont traitées dans l’ordre de hello qu’ils sont répertoriés dans le portail de hello. Il est tooconfiguring préalable première de plusieurs sites écouteurs de tooconfigure fortement recommandé un écouteur de base.  Cela garantit sa que toohello de routé Obtient le trafic de fin. Si un écouteur de base est indiqué en premier et correspond à une demande entrante, elle est traitée par cet écouteur.

## <a name="urlpathmap-configuration-element"></a>Élément de configuration UrlPathMap

élément d’urlPathMap Hello est utilisé toospecify tooback-fin de modèles de chemin d’accès des mappages de pool de serveurs. Bonjour exemple de code suivant est extrait de code hello d’élément urlPathMap à partir du fichier de modèle.

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
> PathPattern : Ce paramètre est une liste de toomatch des modèles de chemin d’accès. Chacun doit commencer par / et hello uniquement une « * » est autorisé à hello fin suit une « / ». chaîne Hello fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord ? ou bien, # et ces caractères ne sont pas autorisés ici.

Pour plus d’informations, vous pouvez consulter un [modèle Resource Manager utilisant le routage basé sur URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .

## <a name="pathbasedrouting-rule"></a>Règle PathBasedRouting

RequestRoutingRule de type PathBasedRouting est toobind utilisé un urlPathMap de tooa d’écouteur. Toutes les demandes qui sont reçues par cet écouteur sont acheminées en fonction de la stratégie spécifiée dans l’élément urlPathMap.
Exemple de la règle PathBasedRouting :

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

## <a name="next-steps"></a>Étapes suivantes

Une fois l’apprentissage sur le routage de contenu basée sur URL, rendez-vous trop[créer une passerelle d’application à l’aide de routage basé sur les URL](application-gateway-create-url-route-portal.md) toocreate une passerelle d’application avec les règles de routage d’URL.
