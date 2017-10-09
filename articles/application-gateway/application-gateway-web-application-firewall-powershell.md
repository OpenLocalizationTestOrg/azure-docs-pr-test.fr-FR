---
title: "pare-feu d’applications web aaaConfigure - passerelle d’Application Azure | Documents Microsoft"
description: "Cet article fournit des conseils sur comment toostart à l’aide de web des pare-feu d’applications sur une passerelle d’Application existant ou nouveau."
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
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="814a0-103">Configurer un pare-feu d’application web sur une passerelle Application Gateway nouvelle ou existante</span><span class="sxs-lookup"><span data-stu-id="814a0-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="814a0-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="814a0-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="814a0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="814a0-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="814a0-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="814a0-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="814a0-107">Découvrez comment toocreate un pare-feu d’applications web activé la passerelle d’Application, ou ajoutez des tooan de pare-feu d’application web existante de passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="814a0-108">pare-feu d’applications Hello web (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session.</span><span class="sxs-lookup"><span data-stu-id="814a0-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="814a0-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="814a0-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="814a0-110">Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="814a0-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="814a0-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement de protocole SSL, sondes d’intégrité personnalisées, prise en charge multisite, etc.</span><span class="sxs-lookup"><span data-stu-id="814a0-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="814a0-112">toofind une liste complète des fonctionnalités prises en charge, visitez : [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="814a0-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="814a0-113">Hello ci-dessous montre comment trop[ajouter tooan de pare-feu d’application web existante Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) et [créer une passerelle d’Application qui utilise le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="814a0-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![image du scénario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="814a0-115">Différences de configuration WAF</span><span class="sxs-lookup"><span data-stu-id="814a0-115">WAF configuration differences</span></span>

<span data-ttu-id="814a0-116">Si vous avez lu [créer une passerelle d’Application avec PowerShell](application-gateway-create-gateway-arm.md), vous comprenez tooconfigure de paramètres de référence (SKU) hello lors de la création d’une passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="814a0-117">WAF fournit des paramètres supplémentaires toodefine lors de la configuration de référence (SKU) de hello sur une passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="814a0-118">Il n’y a aucune modification supplémentaire que vous apportez sur hello passerelle d’Application lui-même.</span><span class="sxs-lookup"><span data-stu-id="814a0-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="814a0-119">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="814a0-119">**Setting**</span></span> | <span data-ttu-id="814a0-120">**Détails**</span><span class="sxs-lookup"><span data-stu-id="814a0-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="814a0-121">**Référence (SKU)**</span><span class="sxs-lookup"><span data-stu-id="814a0-121">**SKU**</span></span> |<span data-ttu-id="814a0-122">Une passerelle Application Gateway normale sans WAF prend en charge les tailles **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="814a0-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="814a0-123">Avec l’introduction de hello de WAF, il existe deux références supplémentaires, **WAF\_support** et **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="814a0-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="814a0-124">WAF n’est pas pris en charge sur les petites passerelles Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="814a0-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="814a0-125">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="814a0-125">**Tier**</span></span> | <span data-ttu-id="814a0-126">les valeurs disponibles Hello sont **Standard** ou **WAF**.</span><span class="sxs-lookup"><span data-stu-id="814a0-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="814a0-127">Lorsque vous utilisez un pare-feu d’applications web, vous devez choisir **WAF**.</span><span class="sxs-lookup"><span data-stu-id="814a0-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="814a0-128">**Mode**</span><span class="sxs-lookup"><span data-stu-id="814a0-128">**Mode**</span></span> | <span data-ttu-id="814a0-129">Ce paramètre est le mode de WAF hello.</span><span class="sxs-lookup"><span data-stu-id="814a0-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="814a0-130">Les valeurs autorisées sont **Détection** et **Prévention**.</span><span class="sxs-lookup"><span data-stu-id="814a0-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="814a0-131">Lorsque WAF est configuré en mode de détection, toutes les menaces sont stockées dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="814a0-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="814a0-132">En mode de prévention, les événements sont toujours enregistrés, mais les intrus hello reçoive une réponse non autorisé 403 hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="814a0-133">Ajouter tooan de pare-feu d’application web existante Application Gateway</span><span class="sxs-lookup"><span data-stu-id="814a0-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="814a0-134">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="814a0-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="814a0-135">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="814a0-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="814a0-136">Ouvrez une session dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="814a0-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="814a0-137">Sélectionnez toouse d’abonnement hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="814a0-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="814a0-138">Récupérer la passerelle hello que vous ajoutez au pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="814a0-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="814a0-139">Configurer la référence (SKU) de hello web application pare-feu.</span><span class="sxs-lookup"><span data-stu-id="814a0-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="814a0-140">les tailles disponibles Hello sont **WAF\_grande** et **WAF\_support**.</span><span class="sxs-lookup"><span data-stu-id="814a0-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="814a0-141">Pare-feu d’applications web est utilisé lors de la couche de hello doit être **WAF**, capacité de hello doit être confirmée lors de la configuration de référence (SKU) hello.</span><span class="sxs-lookup"><span data-stu-id="814a0-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="814a0-142">Configurer les paramètres de hello WAF tel que défini dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="814a0-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="814a0-143">Pour **FirewallMode**, les valeurs disponibles hello sont la détection et la prévention.</span><span class="sxs-lookup"><span data-stu-id="814a0-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="814a0-144">Mettre à jour hello passerelle d’Application avec les paramètres de hello définis dans hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="814a0-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="814a0-145">Cette commande met à jour hello passerelle d’Application avec le pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="814a0-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="814a0-146">Visitez [diagnostics de la passerelle d’Application](application-gateway-diagnostics.md) toounderstand comment tooview se connecte pour la passerelle de votre Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="814a0-147">En raison de la nature de sécurité toohello de WAF, journaux besoin toobe révisé régulièrement posture de sécurité hello toounderstand de vos applications web.</span><span class="sxs-lookup"><span data-stu-id="814a0-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="814a0-148">Créer une passerelle Application Gateway avec le pare-feu d’applications web</span><span class="sxs-lookup"><span data-stu-id="814a0-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="814a0-149">Hello étapes suivantes vous guident tout processus de hello de tooend de début pour la création d’une passerelle d’Application avec le pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="814a0-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="814a0-150">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="814a0-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="814a0-151">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="814a0-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="814a0-152">Connectez-vous à tooAzure en exécutant `Login-AzureRmAccount`, vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="814a0-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="814a0-153">Vérifier les abonnements hello pour le compte de hello en exécutant`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="814a0-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="814a0-154">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="814a0-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="814a0-155">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="814a0-155">Create a resource group</span></span>

<span data-ttu-id="814a0-156">Créer un groupe de ressources pour hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="814a0-157">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="814a0-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="814a0-158">Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="814a0-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="814a0-159">Assurez-vous que toutes les commandes toocreate une passerelle d’Application utilise hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="814a0-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="814a0-160">Bonjour précédent exemple, nous avons créé un groupe de ressources appelé « Appgw-RG » et l’emplacement « ouest des États-Unis. »</span><span class="sxs-lookup"><span data-stu-id="814a0-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="814a0-161">Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’Application, consultez [créer une passerelle d’Application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="814a0-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="814a0-162">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="814a0-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="814a0-163">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="814a0-163">Configure virtual network</span></span>

<span data-ttu-id="814a0-164">Application Gateway nécessite son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="814a0-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="814a0-165">Dans cette étape, vous créez un réseau virtuel avec un espace d’adressage de 10.0.0.0/16 et deux sous-réseaux, un pour hello passerelle d’Application et l’autre pour les membres du pool principal.</span><span class="sxs-lookup"><span data-stu-id="814a0-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="814a0-166">Configurer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="814a0-166">Configure public IP address</span></span>

<span data-ttu-id="814a0-167">Dans l’ordre toohandle les demandes externes, passerelle d’Application requiert une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="814a0-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="814a0-168">Cette adresse IP publique ne doit pas avoir un `DomainNameLabel` défini toobe utilisé par hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="814a0-169">Configurer hello Application Gateway</span><span class="sxs-lookup"><span data-stu-id="814a0-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="814a0-170">Passerelles d’application créés avec la configuration du pare-feu application hello web de base sont configurés avec CRS 3.0 pour les protections.</span><span class="sxs-lookup"><span data-stu-id="814a0-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="814a0-171">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="814a0-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="814a0-172">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="814a0-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="814a0-173">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="814a0-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="814a0-174">les utilisateurs finaux de tooensure pouvez atteindre hello passerelle d’Application, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="814a0-175">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="814a0-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="814a0-176">tooconfigure un alias, de récupérer les détails de hello passerelle d’Application et son nom IP/DNS associé à l’aide de hello PublicIPAddress élément attaché toohello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="814a0-177">nom DNS de la passerelle d’Application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="814a0-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="814a0-178">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="814a0-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="814a0-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="814a0-179">Next steps</span></span>

<span data-ttu-id="814a0-180">Découvrez comment tooconfigure journalisation des diagnostics, événements de hello toolog détectés ou prévenir pare-feu d’applications web en vous rendant sur [Diagnostics de passerelle d’Application](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="814a0-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
