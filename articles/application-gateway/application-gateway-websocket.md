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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="886e7-103">Vue d’ensemble de la prise en charge de WebSocket dans Application Gateway</span><span class="sxs-lookup"><span data-stu-id="886e7-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="886e7-104">Application Gateway prend en charge WebSocket de manière native, quelle que soit la taille de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="886e7-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="886e7-105">Il n’existe aucun paramètre configurable par l’utilisateur tooselectively activer ou la désactiver la prise en charge de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="886e7-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="886e7-106">Le protocole WebSocket, standardisé dans la [RFC6455](https://tools.ietf.org/html/rfc6455), permet une communication en duplex intégral entre le serveur et le client via une connexion TCP de longue durée.</span><span class="sxs-lookup"><span data-stu-id="886e7-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="886e7-107">Cette fonctionnalité permet une communication plus interactive entre le serveur web de hello et client hello, qui peut être bidirectionnel sans avoir besoin de hello pour l’interrogation en tant que requis dans les implémentations basées sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="886e7-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="886e7-108">WebSocket a faible surcharge Contrairement à HTTP et pouvez réutiliser hello même connexion TCP pour plusieurs demande/réponse entraîne une utilisation plus efficace des ressources.</span><span class="sxs-lookup"><span data-stu-id="886e7-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="886e7-109">WebSocket protocoles sont conçu toowork traditionnels ports HTTP 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="886e7-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="886e7-110">Vous pouvez continuer à l’aide d’un écouteur HTTP standard sur le port 80 ou 443 tooreceive le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="886e7-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="886e7-111">Le trafic WebSocket est ensuite dirigé toohello WebSocket activée serveur principal à l’aide du pool principal approprié de hello comme spécifié dans les règles de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="886e7-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="886e7-112">serveur principal de Hello doit répondre sondes de passerelle d’application toohello, qui sont décrites dans hello [vue d’ensemble de la sonde d’intégrité](application-gateway-probe-overview.md) section.</span><span class="sxs-lookup"><span data-stu-id="886e7-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="886e7-113">Les sondes d’intégrité d’Application Gateway n’utilisent que les protocoles HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="886e7-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="886e7-114">Chaque serveur principal doit répondre sondes tooHTTP application serveur de passerelle tooroute WebSocket trafic toohello.</span><span class="sxs-lookup"><span data-stu-id="886e7-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="886e7-115">Élément de configuration d’écouteur</span><span class="sxs-lookup"><span data-stu-id="886e7-115">Listener configuration element</span></span>

<span data-ttu-id="886e7-116">Un écouteur HTTP existant peut être utilisé toosupport le trafic WebSocket.</span><span class="sxs-lookup"><span data-stu-id="886e7-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="886e7-117">Hello Voici un extrait de code d’un élément élève à partir d’un exemple de fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="886e7-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="886e7-118">Vous devez les protocoles HTTP et HTTPS toosupport écouteurs WebSocket et sécuriser le trafic de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="886e7-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="886e7-119">De même, vous pouvez utiliser hello [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate une passerelle d’application avec des écouteurs sur le trafic du port 80/443 toosupport WebSocket.</span><span class="sxs-lookup"><span data-stu-id="886e7-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="886e7-120">Configuration des règles de routage, BackendHttpSetting et BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="886e7-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="886e7-121">Un BackendAddressPool est toodefine utilisé un pool principal avec des serveurs de WebSocket activée.</span><span class="sxs-lookup"><span data-stu-id="886e7-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="886e7-122">Hello backendHttpSetting est défini avec un port principal 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="886e7-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="886e7-123">propriétés Hello pour affinité de basé sur cookie et requestTimeouts ne sont pas pertinentes tooWebSocket trafic.</span><span class="sxs-lookup"><span data-stu-id="886e7-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="886e7-124">Aucune modification n’est requise dans la règle de routage hello, « Base » est utilisé tootie hello écouteur appropriée toohello correspondant du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="886e7-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="886e7-125">Serveur principal compatible WebSocket</span><span class="sxs-lookup"><span data-stu-id="886e7-125">WebSocket enabled backend</span></span>

<span data-ttu-id="886e7-126">Votre serveur principal doit avoir un serveur web HTTP/HTTPS sous hello configuré le port pour le WebSocket toowork (généralement 80/443).</span><span class="sxs-lookup"><span data-stu-id="886e7-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="886e7-127">Cette exigence est car protocole WebSocket requiert hello négociation initiale toobe HTTP avec le protocole de mise à niveau tooWebSocket comme un champ d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="886e7-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="886e7-128">Hello Voici un exemple d’en-tête :</span><span class="sxs-lookup"><span data-stu-id="886e7-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="886e7-129">Autre raison : la sonde d’intégrité principale d’Application Gateway ne prend en charge que les protocoles HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="886e7-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="886e7-130">Si le serveur principal de hello ne répond pas tooHTTP ou les sondes HTTPS, elle est effectuée en dehors du pool principal.</span><span class="sxs-lookup"><span data-stu-id="886e7-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="886e7-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="886e7-131">Next steps</span></span>

<span data-ttu-id="886e7-132">Une fois l’apprentissage sur la prise en charge de WebSocket, rendez-vous trop[créer une passerelle d’application](application-gateway-create-gateway.md) tooget a démarré avec un WebSocket activé l’application web.</span><span class="sxs-lookup"><span data-stu-id="886e7-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

