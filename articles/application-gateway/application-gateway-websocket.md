---
title: Prise en charge de WebSocket pour la passerelle Application Gateway | Microsoft Docs
description: "Cette page fournit une vue d’ensemble de la prise en charge de WebSocket pour la passerelle Application Gateway."
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="280a2-103">Vue d’ensemble de la prise en charge de WebSocket dans Application Gateway</span><span class="sxs-lookup"><span data-stu-id="280a2-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="280a2-104">Application Gateway prend en charge WebSocket de manière native, quelle que soit la taille de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="280a2-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="280a2-105">Il n’existe aucun paramètre configurable par l’utilisateur permettant d’activer ou de désactiver de manière sélective la prise en charge de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="280a2-106">Le protocole WebSocket, standardisé dans la [RFC6455](https://tools.ietf.org/html/rfc6455), permet une communication en duplex intégral entre le serveur et le client via une connexion TCP de longue durée.</span><span class="sxs-lookup"><span data-stu-id="280a2-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="280a2-107">Il assure une communication plus interactive entre le serveur web et le client, qui peut être bidirectionnelle sans nécessiter d’interrogations, comme c’est le cas pour les implémentations basées sur le protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="280a2-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="280a2-108">Contrairement au protocole HTTP, WebSocket génère une faible surcharge et peut réutiliser la même connexion TCP pour plusieurs demandes/réponses, ce qui entraîne une utilisation plus efficace des ressources.</span><span class="sxs-lookup"><span data-stu-id="280a2-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="280a2-109">Les protocoles WebSocket sont conçus pour fonctionner sur les ports HTTP traditionnels (80 et 443).</span><span class="sxs-lookup"><span data-stu-id="280a2-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="280a2-110">Vous pouvez continuer d’utiliser un élément écouteur HTTP standard sur le port 80 ou 443 pour recevoir le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="280a2-111">Le trafic WebSocket est ensuite dirigé vers le serveur principal compatible WebSocket à l’aide du pool principal approprié tel que spécifié dans les règles Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="280a2-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="280a2-112">Le serveur principal doit répondre aux sondes de la passerelle Application Gateway, qui sont décrites dans la section [Vue d’ensemble de la sonde d’intégrité](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="280a2-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="280a2-113">Les sondes d’intégrité d’Application Gateway n’utilisent que les protocoles HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="280a2-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="280a2-114">Chaque serveur principal doit répondre aux sondes HTTP de la passerelle Application Gateway pour acheminer le trafic WebSocket au serveur.</span><span class="sxs-lookup"><span data-stu-id="280a2-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="280a2-115">Élément de configuration d’écouteur</span><span class="sxs-lookup"><span data-stu-id="280a2-115">Listener configuration element</span></span>

<span data-ttu-id="280a2-116">Un écouteur HTTP permet de prendre en charge le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="280a2-117">Voici un extrait d’un élément HttpListeners provenant d’un exemple de fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="280a2-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="280a2-118">Vous auriez besoin d’écouteurs HTTP et HTTPS pour prendre en charge WebSocket et sécuriser le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="280a2-119">De même, vous pouvez utiliser le [portail](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) afin de créer une passerelle Application Gateway avec des écouteurs sur le port 80/443 pour prendre en charge le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="280a2-120">Configuration des règles de routage, BackendHttpSetting et BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="280a2-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="280a2-121">Un élément BackendAddressPool permet de définir un pool principal avec des serveurs compatibles WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="280a2-122">L’élément backendHttpSetting est défini avec un port principal 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="280a2-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="280a2-123">Les propriétés de l’affinité basée sur les cookies et de requestTimeouts ne sont pas pertinentes pour le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="280a2-124">La règle de routage n’est pas modifiée. La règle « De base » sert à lier l’écouteur approprié au pool d’adresses principal correspondant.</span><span class="sxs-lookup"><span data-stu-id="280a2-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="280a2-125">Serveur principal compatible WebSocket</span><span class="sxs-lookup"><span data-stu-id="280a2-125">WebSocket enabled backend</span></span>

<span data-ttu-id="280a2-126">Votre serveur principal doit exécuter un serveur web HTTP/HTTPS sur le port configuré (généralement 80/443) pour que WebSocket fonctionne.</span><span class="sxs-lookup"><span data-stu-id="280a2-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="280a2-127">En effet, le protocole WebSocket impose que la négociation initiale s’effectue en HTTP avec mise à niveau vers le protocole WebSocket comme champ d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="280a2-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="280a2-128">Voici un exemple d’en-tête :</span><span class="sxs-lookup"><span data-stu-id="280a2-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="280a2-129">Autre raison : la sonde d’intégrité principale d’Application Gateway ne prend en charge que les protocoles HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="280a2-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="280a2-130">Si le serveur principal ne répond pas aux sondes HTTP ou HTTPS, il est retiré du pool principal.</span><span class="sxs-lookup"><span data-stu-id="280a2-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="280a2-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="280a2-131">Next steps</span></span>

<span data-ttu-id="280a2-132">Après avoir découvert la prise en charge de WebSocket, consultez [Créer une passerelle Application Gateway](application-gateway-create-gateway.md) pour commencer à utiliser une application web compatible avec WebSocket.</span><span class="sxs-lookup"><span data-stu-id="280a2-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

