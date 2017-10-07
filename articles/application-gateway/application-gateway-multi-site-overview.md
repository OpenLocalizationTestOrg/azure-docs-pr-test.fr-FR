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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="8c31f-103">Hébergement de plusieurs sites Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8c31f-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="8c31f-104">Hébergement de plusieurs sites vous permet de tooconfigure plus d’une application web sur hello même instance de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="8c31f-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="8c31f-105">Cette fonctionnalité vous permet de tooconfigure une topologie plus efficace de vos déploiements en additionnant la passerelle d’application tooone too20 sites Web.</span><span class="sxs-lookup"><span data-stu-id="8c31f-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="8c31f-106">Chaque site Web peut être dirigé tooits propre pool principal.</span><span class="sxs-lookup"><span data-stu-id="8c31f-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="8c31f-107">Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com à partir de deux pools de serveur principal appelés ContosoServerPool et FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="8c31f-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="8c31f-109">Règles sont traitées dans l’ordre de hello qu’ils sont répertoriés dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8c31f-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="8c31f-110">Il est tooconfiguring préalable première de plusieurs sites écouteurs de tooconfigure fortement recommandé un écouteur de base.</span><span class="sxs-lookup"><span data-stu-id="8c31f-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="8c31f-111">Cela permettra de mettre fin à sa que toohello de routé Obtient le trafic.</span><span class="sxs-lookup"><span data-stu-id="8c31f-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="8c31f-112">Si un écouteur de base est indiqué en premier et correspond à une demande entrante, elle est traitée par cet écouteur.</span><span class="sxs-lookup"><span data-stu-id="8c31f-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="8c31f-113">Demandes de http://contoso.com sont routé tooContosoServerPool et http://fabrikam.com sont tooFabrikamServerPool routé.</span><span class="sxs-lookup"><span data-stu-id="8c31f-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="8c31f-114">De même, deux sous-domaines de hello même domaine parent peut être hébergé sur hello même déploiement de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="8c31f-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="8c31f-115">Parmi les exemples d’utilisation de sous-domaines, peuvent figurer http://blog.contoso.com et http://app.contoso.com hébergés sur un déploiement de passerelle Application Gateway unique.</span><span class="sxs-lookup"><span data-stu-id="8c31f-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="8c31f-116">En-têtes d’hôte et Indication du nom du serveur (SNI)</span><span class="sxs-lookup"><span data-stu-id="8c31f-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="8c31f-117">Il existe trois mécanismes pour l’activation de plusieurs sites d’hébergement sur hello même infrastructure.</span><span class="sxs-lookup"><span data-stu-id="8c31f-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="8c31f-118">Hébergez plusieurs applications web, chacune sur une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="8c31f-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="8c31f-119">Nom d’hôte de l’utilisation toohost plusieurs applications web sur hello même adresse IP.</span><span class="sxs-lookup"><span data-stu-id="8c31f-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="8c31f-120">Utilisez différents ports toohost plusieurs applications web sur hello même adresse IP.</span><span class="sxs-lookup"><span data-stu-id="8c31f-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="8c31f-121">Actuellement, une passerelle Application Gateway obtient une adresse IP publique unique sur laquelle elle écoute le trafic.</span><span class="sxs-lookup"><span data-stu-id="8c31f-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="8c31f-122">Par conséquent, la prise en charge de plusieurs applications, chacune avec sa propre adresse IP, n’est pas disponible actuellement.</span><span class="sxs-lookup"><span data-stu-id="8c31f-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="8c31f-123">Passerelle d’application prend en charge plusieurs applications d’hébergement chaque à l’écoute sur des ports différents mais ce scénario nécessiterait hello applications tooaccept le trafic sur des ports non standard et n’est pas souvent la configuration souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8c31f-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="8c31f-124">Passerelle d’application s’appuie sur HTTP 1.1 hôte en-têtes toohost plus d’un site Web sur hello même adresse IP publique et le port.</span><span class="sxs-lookup"><span data-stu-id="8c31f-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="8c31f-125">les sites Hello hébergés sur la passerelle d’application peuvent également prise en charge de déchargement SSL avec l’extension d’Indication de nom de serveur (SNI) TLS.</span><span class="sxs-lookup"><span data-stu-id="8c31f-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="8c31f-126">Ce scénario signifie que hello client navigateur et le serveur principal batterie de serveurs web doit prendre en charge HTTP/1.1 et extension TLS tel que défini dans RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="8c31f-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="8c31f-127">Élément de configuration d’écouteur</span><span class="sxs-lookup"><span data-stu-id="8c31f-127">Listener configuration element</span></span>

<span data-ttu-id="8c31f-128">HTTPListener existant est de l’élément de configuration améliorée toosupport nom et le serveur nom indication éléments hôtes, qui est utilisé par le pool principal d’application passerelle tooroute trafic tooappropriate.</span><span class="sxs-lookup"><span data-stu-id="8c31f-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="8c31f-129">Bonjour exemple de code suivant est extrait de code hello d’élément élève à partir du fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="8c31f-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="8c31f-130">Vous pouvez visiter [modèle du Gestionnaire de ressources à l’aide d’hébergement de plusieurs sites](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) pour un déploiement basé sur un modèle de fin tooend.</span><span class="sxs-lookup"><span data-stu-id="8c31f-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="8c31f-131">Règle de routage</span><span class="sxs-lookup"><span data-stu-id="8c31f-131">Routing rule</span></span>

<span data-ttu-id="8c31f-132">Aucune modification n’est requise dans la règle de routage hello.</span><span class="sxs-lookup"><span data-stu-id="8c31f-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="8c31f-133">Hello 'Base' doit se poursuivre toobe choisi tootie hello site approprié écouteur toohello correspondante pool d’adresses principales de règle de routage.</span><span class="sxs-lookup"><span data-stu-id="8c31f-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c31f-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c31f-134">Next steps</span></span>

<span data-ttu-id="8c31f-135">Après avoir d’apprendre à l’hébergement de plusieurs sites, passez trop[créer une passerelle d’application à l’aide d’hébergement de plusieurs sites](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate une passerelle d’application avec capacité toosupport plus d’une application web.</span><span class="sxs-lookup"><span data-stu-id="8c31f-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

