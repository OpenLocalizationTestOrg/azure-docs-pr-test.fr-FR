---
title: "aaaCreate et gérer une passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure à l’aide du Gestionnaire de ressources Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="61a7f-103">Créer, démarrer ou supprimer une passerelle Application Gateway à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61a7f-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="61a7f-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="61a7f-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="61a7f-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61a7f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="61a7f-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="61a7f-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="61a7f-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61a7f-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="61a7f-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="61a7f-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="61a7f-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="61a7f-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="61a7f-110">Il fournit de basculement et le routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="61a7f-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="61a7f-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc.</span><span class="sxs-lookup"><span data-stu-id="61a7f-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="61a7f-112">toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="61a7f-113">Cet article vous guide tout au long des hello étapes toocreate, configurer, démarrer et supprimer une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="61a7f-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61a7f-114">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources et classique.</span><span class="sxs-lookup"><span data-stu-id="61a7f-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="61a7f-115">Attention à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="61a7f-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="61a7f-116">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="61a7f-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="61a7f-117">Ce document traite de la création d’une passerelle Application Gateway à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61a7f-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="61a7f-118">version classique de toouse hello, accédez trop[créer un déploiement classique passerelle d’application à l’aide de PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="61a7f-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="61a7f-119">Before you begin</span></span>

1. <span data-ttu-id="61a7f-120">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="61a7f-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="61a7f-121">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="61a7f-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="61a7f-122">Si vous avez un réseau virtuel existant, sélectionnez un sous-réseau vide existant ou créer un sous-réseau dans votre réseau virtuel existant uniquement pour une utilisation par la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="61a7f-123">Vous ne pouvez pas déployer hello application passerelle tooa autre réseau virtuel que les ressources hello vous avez l’intention toodeploy derrière la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="61a7f-124">serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.</span><span class="sxs-lookup"><span data-stu-id="61a7f-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="61a7f-125">Qu’est requis toocreate une passerelle d’application ?</span><span class="sxs-lookup"><span data-stu-id="61a7f-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="61a7f-126">**Pool de serveurs principaux :** liste hello d’adresses IP, des noms de domaine complets ou des cartes réseau des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="61a7f-127">Si les adresses IP sont utilisées, elles doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="61a7f-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="61a7f-128">**Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="61a7f-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="61a7f-129">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="61a7f-130">**port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="61a7f-131">Le trafic atteint ce port et obtient ensuite redirigé tooone des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="61a7f-132">**Écouteur :** écouteur de hello possède un port de serveur frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="61a7f-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="61a7f-133">**La règle :** règle de hello lie écouteur hello, pool de serveurs principaux hello et définit le principal serveur pool hello le trafic doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="61a7f-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="61a7f-134">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61a7f-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="61a7f-135">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="61a7f-136">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="61a7f-137">Connectez-vous à tooAzure et entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="61a7f-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="61a7f-138">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="61a7f-139">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="61a7f-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="61a7f-140">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="61a7f-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="61a7f-141">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="61a7f-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="61a7f-142">Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61a7f-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="61a7f-143">Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61a7f-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="61a7f-144">Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **ContosoRG** et l’emplacement **États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="61a7f-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="61a7f-145">Si vous avez besoin de tooconfigure une sonde personnalisée pour votre passerelle d’application, visitez : [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="61a7f-146">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="61a7f-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="61a7f-147">Créer des objets de configuration de passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="61a7f-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="61a7f-148">Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="61a7f-149">Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="61a7f-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="61a7f-150">Lorsque vous avez terminé, récupérer les détails DNS et adresse IP virtuelle de passerelle d’application hello à partir de la passerelle d’application hello publique IP ressource toohello attaché.</span><span class="sxs-lookup"><span data-stu-id="61a7f-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="61a7f-151">Suppression de la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="61a7f-151">Delete hello application gateway</span></span>

<span data-ttu-id="61a7f-152">Hello exemple suivant supprime passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="61a7f-153">Hello **-force** commutateur peut être le message de confirmation de suppression de hello toosuppress utilisé.</span><span class="sxs-lookup"><span data-stu-id="61a7f-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="61a7f-154">tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureRmApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="61a7f-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="61a7f-155">Cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="61a7f-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="61a7f-156">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="61a7f-156">Get application gateway DNS name</span></span>

<span data-ttu-id="61a7f-157">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="61a7f-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="61a7f-158">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="61a7f-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="61a7f-159">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="61a7f-160">toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="61a7f-161">Cela est possible avec Azure DNS ou d’autres fournisseurs DNS, en créant un enregistrement CNAME qui pointe toohello [adresse IP publique](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="61a7f-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="61a7f-162">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="61a7f-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="61a7f-163">Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.</span><span class="sxs-lookup"><span data-stu-id="61a7f-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="61a7f-164">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="61a7f-164">Delete all resources</span></span>

<span data-ttu-id="61a7f-165">toodelete toutes les ressources créées dans cet article, hello complet suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="61a7f-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="61a7f-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61a7f-166">Next steps</span></span>

<span data-ttu-id="61a7f-167">Si vous souhaitez tooconfigure le déchargement SSL, visitez : [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="61a7f-168">Si vous voulez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, visitez : [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="61a7f-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="61a7f-169">Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :</span><span class="sxs-lookup"><span data-stu-id="61a7f-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="61a7f-170">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="61a7f-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="61a7f-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="61a7f-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
