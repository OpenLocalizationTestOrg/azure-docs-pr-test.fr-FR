---
title: "pare-feu d’applications web aaaConfigure - passerelle d’Application Azure | Documents Microsoft"
description: "Cet article fournit des conseils sur comment toostart à l’aide de web des pare-feu d’applications sur une passerelle d’application existant ou nouveau."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="b4854-103">Configurer un pare-feu d’application web sur une passerelle Application Gateway nouvelle ou existante avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4854-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4854-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b4854-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="b4854-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4854-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="b4854-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b4854-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="b4854-107">Découvrez comment toocreate un pare-feu d’applications web activé la passerelle d’application ou ajouter web application pare-feu tooan existant passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="b4854-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="b4854-108">pare-feu d’applications Hello web (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session.</span><span class="sxs-lookup"><span data-stu-id="b4854-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="b4854-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="b4854-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b4854-110">Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="b4854-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b4854-111">La passerelle d’application offre de nombreuses fonctionnalités du contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement de protocole SSL, sondes d’intégrité personnalisées, prise en charge multisite, etc.</span><span class="sxs-lookup"><span data-stu-id="b4854-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b4854-112">toofind une liste complète des fonctionnalités prises en charge, visitez : [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4854-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="b4854-113">Hello ci-dessous montre comment trop[ajouter web application pare-feu tooan existant application passerelle](#add-web-application-firewall-to-an-existing-application-gateway) et [créer une passerelle d’application qui utilise le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="b4854-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![image du scénario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="b4854-115">Condition préalable : Installez hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b4854-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="b4854-116">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b4854-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="b4854-117">Différences de configuration WAF</span><span class="sxs-lookup"><span data-stu-id="b4854-117">WAF configuration differences</span></span>

<span data-ttu-id="b4854-118">Si vous avez lu [créer une passerelle d’Application avec Azure CLI](application-gateway-create-gateway-cli.md), vous comprenez tooconfigure de paramètres de référence (SKU) hello lors de la création d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="b4854-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="b4854-119">WAF fournit des paramètres supplémentaires toodefine lors de la configuration de référence (SKU) de hello sur une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="b4854-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="b4854-120">Il n’y a aucune modification supplémentaire que vous apportez sur la passerelle d’application hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="b4854-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="b4854-121">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="b4854-121">**Setting**</span></span> | <span data-ttu-id="b4854-122">**Détails**</span><span class="sxs-lookup"><span data-stu-id="b4854-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="b4854-123">**Référence (SKU)**</span><span class="sxs-lookup"><span data-stu-id="b4854-123">**SKU**</span></span> |<span data-ttu-id="b4854-124">Une passerelle d’application normale sans WAF prend en charge les tailles **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="b4854-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="b4854-125">Avec l’introduction de hello de WAF, il existe deux références supplémentaires, **WAF\_support** et **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="b4854-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="b4854-126">WAF n’est pas pris en charge sur les petites passerelles d’application.</span><span class="sxs-lookup"><span data-stu-id="b4854-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="b4854-127">**Mode**</span><span class="sxs-lookup"><span data-stu-id="b4854-127">**Mode**</span></span> | <span data-ttu-id="b4854-128">Ce paramètre est le mode de WAF hello.</span><span class="sxs-lookup"><span data-stu-id="b4854-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="b4854-129">Les valeurs autorisées sont **Détection** et **Prévention**.</span><span class="sxs-lookup"><span data-stu-id="b4854-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="b4854-130">Lorsque WAF est configuré en mode de détection, toutes les menaces sont stockées dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="b4854-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="b4854-131">En mode de prévention, les événements sont toujours enregistrés, mais les intrus hello reçoive une réponse non autorisé 403 passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="b4854-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="b4854-132">Ajouter web application pare-feu tooan existant passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="b4854-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="b4854-133">Hello suivre les modifications de commande une passerelle d’application activé de tooa WAF de passerelle standard d’application existant.</span><span class="sxs-lookup"><span data-stu-id="b4854-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="b4854-134">Cette commande met à jour la passerelle d’application hello avec pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="b4854-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="b4854-135">Visitez [Application Diagnostics de passerelle](application-gateway-diagnostics.md) toounderstand comment tooview se connecte pour la passerelle de votre application.</span><span class="sxs-lookup"><span data-stu-id="b4854-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="b4854-136">En raison de la nature de sécurité toohello de WAF, journaux besoin toobe révisé régulièrement posture de sécurité hello toounderstand de vos applications web.</span><span class="sxs-lookup"><span data-stu-id="b4854-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="b4854-137">Créer une passerelle Application Gateway avec le pare-feu d’applications web</span><span class="sxs-lookup"><span data-stu-id="b4854-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="b4854-138">Hello commande suivante crée une passerelle d’Application avec le pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="b4854-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="b4854-139">Passerelles d’application créés avec la configuration du pare-feu application hello web de base sont configurés avec CRS 3.0 pour les protections.</span><span class="sxs-lookup"><span data-stu-id="b4854-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b4854-140">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b4854-140">Get application gateway DNS name</span></span>

<span data-ttu-id="b4854-141">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="b4854-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b4854-142">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="b4854-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b4854-143">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="b4854-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="b4854-144">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4854-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="b4854-145">tooconfigure un enregistrement CNAME, récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="b4854-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="b4854-146">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="b4854-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="b4854-147">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="b4854-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="b4854-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4854-148">Next steps</span></span>

<span data-ttu-id="b4854-149">Découvrez le fonctionnement des règles de toocustomize WAF en visitant : [personnaliser les règles de pare-feu d’applications web via hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4854-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
