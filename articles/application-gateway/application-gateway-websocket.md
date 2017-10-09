---
title: "prise en charge d’aaaWebSocket dans la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello prise en charge de WebSocket de passerelle d’Application."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Vue d’ensemble de la prise en charge de WebSocket dans Application Gateway

Application Gateway prend en charge WebSocket de manière native, quelle que soit la taille de la passerelle. Il n’existe aucun paramètre configurable par l’utilisateur tooselectively activer ou la désactiver la prise en charge de WebSocket. 

Le protocole WebSocket, standardisé dans la [RFC6455](https://tools.ietf.org/html/rfc6455), permet une communication en duplex intégral entre le serveur et le client via une connexion TCP de longue durée. Cette fonctionnalité permet une communication plus interactive entre le serveur web de hello et client hello, qui peut être bidirectionnel sans avoir besoin de hello pour l’interrogation en tant que requis dans les implémentations basées sur HTTP. WebSocket a faible surcharge Contrairement à HTTP et pouvez réutiliser hello même connexion TCP pour plusieurs demande/réponse entraîne une utilisation plus efficace des ressources. WebSocket protocoles sont conçu toowork traditionnels ports HTTP 80 et 443.

Vous pouvez continuer à l’aide d’un écouteur HTTP standard sur le port 80 ou 443 tooreceive le trafic WebSocket. Le trafic WebSocket est ensuite dirigé toohello WebSocket activée serveur principal à l’aide du pool principal approprié de hello comme spécifié dans les règles de passerelle d’application. serveur principal de Hello doit répondre sondes de passerelle d’application toohello, qui sont décrites dans hello [vue d’ensemble de la sonde d’intégrité](application-gateway-probe-overview.md) section. Les sondes d’intégrité d’Application Gateway n’utilisent que les protocoles HTTP/HTTPS. Chaque serveur principal doit répondre sondes tooHTTP application serveur de passerelle tooroute WebSocket trafic toohello.

## <a name="listener-configuration-element"></a>Élément de configuration d’écouteur

Un écouteur HTTP existant peut être utilisé toosupport le trafic WebSocket. Hello Voici un extrait de code d’un élément élève à partir d’un exemple de fichier de modèle. Vous devez les protocoles HTTP et HTTPS toosupport écouteurs WebSocket et sécuriser le trafic de WebSocket. De même, vous pouvez utiliser hello [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate une passerelle d’application avec des écouteurs sur le trafic du port 80/443 toosupport WebSocket.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Configuration des règles de routage, BackendHttpSetting et BackendAddressPool

Un BackendAddressPool est toodefine utilisé un pool principal avec des serveurs de WebSocket activée. Hello backendHttpSetting est défini avec un port principal 80 et 443. propriétés Hello pour affinité de basé sur cookie et requestTimeouts ne sont pas pertinentes tooWebSocket trafic. Aucune modification n’est requise dans la règle de routage hello, « Base » est utilisé tootie hello écouteur appropriée toohello correspondant du pool d’adresses principales. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>Serveur principal compatible WebSocket

Votre serveur principal doit avoir un serveur web HTTP/HTTPS sous hello configuré le port pour le WebSocket toowork (généralement 80/443). Cette exigence est car protocole WebSocket requiert hello négociation initiale toobe HTTP avec le protocole de mise à niveau tooWebSocket comme un champ d’en-tête. Hello Voici un exemple d’en-tête :

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

Autre raison : la sonde d’intégrité principale d’Application Gateway ne prend en charge que les protocoles HTTP/HTTPS. Si le serveur principal de hello ne répond pas tooHTTP ou les sondes HTTPS, elle est effectuée en dehors du pool principal.

## <a name="next-steps"></a>Étapes suivantes

Une fois l’apprentissage sur la prise en charge de WebSocket, rendez-vous trop[créer une passerelle d’application](application-gateway-create-gateway.md) tooget a démarré avec un WebSocket activé l’application web.

