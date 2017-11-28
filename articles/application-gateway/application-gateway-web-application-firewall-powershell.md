---
title: "Configurer un pare-feu d’applications web : passerelle Application Gateway Azure | Microsoft Docs"
description: "Cet article explique comment utiliser un pare-feu d’applications web sur une passerelle Application Gateway nouvelle ou existante."
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="cd449-103">Configurer un pare-feu d’application web sur une passerelle Application Gateway nouvelle ou existante</span><span class="sxs-lookup"><span data-stu-id="cd449-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd449-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="cd449-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="cd449-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd449-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="cd449-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cd449-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="cd449-107">Découvrez comment créer une passerelle Application Gateway avec un pare-feu d’applications web activé ou comment ajouter des pare-feu d’applications web à une passerelle Application Gateway existante.</span><span class="sxs-lookup"><span data-stu-id="cd449-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="cd449-108">Le pare-feu d’applications web (WAF, Web Application Firewall) d’Azure Application Gateway protège les applications web des attaques basées sur le web courantes comme l’injection de code SQL, les attaques de script de site à site et les piratages de session.</span><span class="sxs-lookup"><span data-stu-id="cd449-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="cd449-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="cd449-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="cd449-110">Elle assure l’exécution des requêtes HTTP de basculement et de routage des performances entre serveurs locaux ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="cd449-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="cd449-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement de protocole SSL, sondes d’intégrité personnalisées, prise en charge multisite, etc.</span><span class="sxs-lookup"><span data-stu-id="cd449-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="cd449-112">Pour obtenir une liste complète des fonctionnalités prises en charge, consultez : [Vue d’ensemble d’Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="cd449-113">L’article suivant montre comment [ajouter un pare-feu d’applications web à une passerelle Application Gateway existante](#add-web-application-firewall-to-an-existing-application-gateway) et comment [créer une passerelle Application Gateway qui utilise le pare-feu d’applications web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="cd449-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![image du scénario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="cd449-115">Différences de configuration WAF</span><span class="sxs-lookup"><span data-stu-id="cd449-115">WAF configuration differences</span></span>

<span data-ttu-id="cd449-116">Si vous avez lu la rubrique [Création d’une passerelle Application Gateway avec PowerShell](application-gateway-create-gateway-arm.md), vous connaissez les paramètres de référence (SKU) à configurer lors de la création d’une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="cd449-117">WAF inclut des paramètres supplémentaires à définir lors de la configuration de la référence SKU sur une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="cd449-118">Aucune autre modification n’est nécessaire sur la passerelle Application Gateway elle-même.</span><span class="sxs-lookup"><span data-stu-id="cd449-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="cd449-119">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="cd449-119">**Setting**</span></span> | <span data-ttu-id="cd449-120">**Détails**</span><span class="sxs-lookup"><span data-stu-id="cd449-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="cd449-121">**Référence (SKU)**</span><span class="sxs-lookup"><span data-stu-id="cd449-121">**SKU**</span></span> |<span data-ttu-id="cd449-122">Une passerelle Application Gateway normale sans WAF prend en charge les tailles **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="cd449-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="cd449-123">Avec l’introduction de WAF, deux autres SKU sont disponibles : **WAF\_Medium** et **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="cd449-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="cd449-124">WAF n’est pas pris en charge sur les petites passerelles Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="cd449-125">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="cd449-125">**Tier**</span></span> | <span data-ttu-id="cd449-126">Les valeurs disponibles sont **Standard** ou **WAF**.</span><span class="sxs-lookup"><span data-stu-id="cd449-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="cd449-127">Lorsque vous utilisez un pare-feu d’applications web, vous devez choisir **WAF**.</span><span class="sxs-lookup"><span data-stu-id="cd449-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="cd449-128">**Mode**</span><span class="sxs-lookup"><span data-stu-id="cd449-128">**Mode**</span></span> | <span data-ttu-id="cd449-129">Ce paramètre indique le mode de WAF.</span><span class="sxs-lookup"><span data-stu-id="cd449-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="cd449-130">Les valeurs autorisées sont **Détection** et **Prévention**.</span><span class="sxs-lookup"><span data-stu-id="cd449-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="cd449-131">Lorsque WAF est configuré en mode de détection, toutes les menaces sont stockées dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="cd449-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="cd449-132">En mode de prévention, les événements sont toujours consignés, mais l’attaquant reçoit une erreur d’autorisation de type 403 de la part de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="cd449-133">Ajout d’un pare-feu d’applications web à une passerelle Application Gateway existante</span><span class="sxs-lookup"><span data-stu-id="cd449-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="cd449-134">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd449-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="cd449-135">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="cd449-136">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cd449-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="cd449-137">Sélectionnez l’abonnement à utiliser pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="cd449-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="cd449-138">Récupérez la passerelle à laquelle vous ajoutez un pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="cd449-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="cd449-139">Configurez la référence SKU du pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="cd449-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="cd449-140">Les tailles disponibles sont **WAF\_Large** et **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="cd449-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="cd449-141">Lorsque le pare-feu d’application web est utilisé, le niveau doit être **WAF**, la capacité doit être confirmée lors de la définition de la référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="cd449-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="cd449-142">Configurez les paramètres WAF comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd449-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="cd449-143">Pour **FirewallMode**, les valeurs disponibles sont Prévention et Détection.</span><span class="sxs-lookup"><span data-stu-id="cd449-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="cd449-144">Mettez à jour la passerelle Application Gateway avec les paramètres définis à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="cd449-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="cd449-145">Cette commande met à jour la passerelle Application Gateway avec le pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="cd449-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="cd449-146">Consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md) pour comprendre comment afficher les journaux de votre passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="cd449-147">En raison des critères de sécurité inhérents à WAF, les journaux doivent être régulièrement examinés pour comprendre la politique de sécurité appliquée à vos applications web.</span><span class="sxs-lookup"><span data-stu-id="cd449-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="cd449-148">Créer une passerelle Application Gateway avec le pare-feu d’applications web</span><span class="sxs-lookup"><span data-stu-id="cd449-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="cd449-149">Les étapes suivantes vous guident lors du processus de création d’une passerelle Application Gateway avec un pare-feu d’applications web et ce, du début à la fin.</span><span class="sxs-lookup"><span data-stu-id="cd449-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="cd449-150">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd449-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="cd449-151">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="cd449-152">Connectez-vous à Azure en exécutant `Login-AzureRmAccount`. Vous êtes invité à vous authentifier avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="cd449-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="cd449-153">Vérifiez les abonnements pour le compte en exécutant `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="cd449-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="cd449-154">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="cd449-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="cd449-155">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="cd449-155">Create a resource group</span></span>

<span data-ttu-id="cd449-156">Créez un groupe de ressources pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="cd449-157">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="cd449-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="cd449-158">Celui-ci est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="cd449-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="cd449-159">Assurez-vous que toutes les commandes pour la création d’une passerelle Application Gateway utilisent le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cd449-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="cd449-160">Dans l’exemple précédent, nous avons créé un groupe de ressources appelé « appgw-RG », ainsi que l’emplacement « West US ».</span><span class="sxs-lookup"><span data-stu-id="cd449-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="cd449-161">Si vous devez configurer une sonde personnalisée pour votre passerelle Application Gateway, consultez [Création d’une passerelle Application Gateway avec des sondes personnalisées à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="cd449-162">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="cd449-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="cd449-163">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cd449-163">Configure virtual network</span></span>

<span data-ttu-id="cd449-164">Application Gateway nécessite son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="cd449-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="cd449-165">Dans cette étape, vous allez créer un réseau virtuel avec un espace d’adressage de 10.0.0.0/16 et deux sous-réseaux, un pour la passerelle Application Gateway et un pour les membres du pool backend.</span><span class="sxs-lookup"><span data-stu-id="cd449-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="cd449-166">Configurer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="cd449-166">Configure public IP address</span></span>

<span data-ttu-id="cd449-167">Pour pouvoir traiter les demandes externes, Application Gateway a besoin d’une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="cd449-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="cd449-168">Cette adresse IP publique ne doit pas avoir un `DomainNameLabel` défini pour être utilisé par la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="cd449-169">Configurer la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cd449-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="cd449-170">Les passerelles Application Gateway créées avec la configuration de pare-feu d’application web de base sont définies avec la solution CRS 3.0 dédiée aux protections.</span><span class="sxs-lookup"><span data-stu-id="cd449-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cd449-171">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cd449-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="cd449-172">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="cd449-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="cd449-173">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="cd449-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cd449-174">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle Application Gateway, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="cd449-175">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="cd449-176">Pour configurer un alias, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="cd449-177">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="cd449-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="cd449-178">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cd449-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cd449-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd449-179">Next steps</span></span>

<span data-ttu-id="cd449-180">Apprenez à configurer la journalisation des diagnostics et à consigner les événements détectés ou bloqués par le pare-feu d’application web en consultant la rubrique [Diagnostics de la passerelle Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="cd449-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
