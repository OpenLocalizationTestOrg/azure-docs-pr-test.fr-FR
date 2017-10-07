---
title: "aaaHosting plusieurs sites sur la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello prise en charge de plusieurs site de passerelle d’Application."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Hébergement de plusieurs sites Application Gateway

Hébergement de plusieurs sites vous permet de tooconfigure plus d’une application web sur hello même instance de passerelle d’application. Cette fonctionnalité vous permet de tooconfigure une topologie plus efficace de vos déploiements en additionnant la passerelle d’application tooone too20 sites Web. Chaque site Web peut être dirigé tooits propre pool principal. Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com à partir de deux pools de serveur principal appelés ContosoServerPool et FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Règles sont traitées dans l’ordre de hello qu’ils sont répertoriés dans le portail de hello. Il est tooconfiguring préalable première de plusieurs sites écouteurs de tooconfigure fortement recommandé un écouteur de base.  Cela permettra de mettre fin à sa que toohello de routé Obtient le trafic. Si un écouteur de base est indiqué en premier et correspond à une demande entrante, elle est traitée par cet écouteur.

Demandes de http://contoso.com sont routé tooContosoServerPool et http://fabrikam.com sont tooFabrikamServerPool routé.

De même, deux sous-domaines de hello même domaine parent peut être hébergé sur hello même déploiement de passerelle d’application. Parmi les exemples d’utilisation de sous-domaines, peuvent figurer http://blog.contoso.com et http://app.contoso.com hébergés sur un déploiement de passerelle Application Gateway unique.

## <a name="host-headers-and-server-name-indication-sni"></a>En-têtes d’hôte et Indication du nom du serveur (SNI)

Il existe trois mécanismes pour l’activation de plusieurs sites d’hébergement sur hello même infrastructure.

1. Hébergez plusieurs applications web, chacune sur une adresse IP unique.
2. Nom d’hôte de l’utilisation toohost plusieurs applications web sur hello même adresse IP.
3. Utilisez différents ports toohost plusieurs applications web sur hello même adresse IP.

Actuellement, une passerelle Application Gateway obtient une adresse IP publique unique sur laquelle elle écoute le trafic. Par conséquent, la prise en charge de plusieurs applications, chacune avec sa propre adresse IP, n’est pas disponible actuellement. Passerelle d’application prend en charge plusieurs applications d’hébergement chaque à l’écoute sur des ports différents mais ce scénario nécessiterait hello applications tooaccept le trafic sur des ports non standard et n’est pas souvent la configuration souhaitée. Passerelle d’application s’appuie sur HTTP 1.1 hôte en-têtes toohost plus d’un site Web sur hello même adresse IP publique et le port. les sites Hello hébergés sur la passerelle d’application peuvent également prise en charge de déchargement SSL avec l’extension d’Indication de nom de serveur (SNI) TLS. Ce scénario signifie que hello client navigateur et le serveur principal batterie de serveurs web doit prendre en charge HTTP/1.1 et extension TLS tel que défini dans RFC 6066.

## <a name="listener-configuration-element"></a>Élément de configuration d’écouteur

HTTPListener existant est de l’élément de configuration améliorée toosupport nom et le serveur nom indication éléments hôtes, qui est utilisé par le pool principal d’application passerelle tooroute trafic tooappropriate. Bonjour exemple de code suivant est extrait de code hello d’élément élève à partir du fichier de modèle.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Vous pouvez visiter [modèle du Gestionnaire de ressources à l’aide d’hébergement de plusieurs sites](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) pour un déploiement basé sur un modèle de fin tooend.

## <a name="routing-rule"></a>Règle de routage

Aucune modification n’est requise dans la règle de routage hello. Hello 'Base' doit se poursuivre toobe choisi tootie hello site approprié écouteur toohello correspondante pool d’adresses principales de règle de routage.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Étapes suivantes

Après avoir d’apprendre à l’hébergement de plusieurs sites, passez trop[créer une passerelle d’application à l’aide d’hébergement de plusieurs sites](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate une passerelle d’application avec capacité toosupport plus d’une application web.

