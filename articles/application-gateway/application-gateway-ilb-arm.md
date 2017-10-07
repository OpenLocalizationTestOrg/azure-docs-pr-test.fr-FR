---
title: "aaaUsing passerelle d’Application Azure avec l’équilibrage de charge interne - PowerShell | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure avec équilibrage de charge interne (ILB) pour le Gestionnaire de ressources Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="9be46-103">Créer une passerelle Application Gateway avec un équilibrage de charge interne (ILB) à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9be46-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9be46-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="9be46-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="9be46-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9be46-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="9be46-106">Passerelle d’Application Azure peut être configuré avec une adresse IP virtuelle sur Internet ou avec un point de terminaison interne qui n’est pas exposé toohello Internet, également appelée charge interne (ILB) d’équilibrage point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9be46-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="9be46-107">Configuration de passerelle hello avec un équilibrage de charge interne est utile pour les applications de métier internes qui ne sont pas exposé toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="9be46-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="9be46-108">Il est également utile pour les services et niveaux au sein d’une application multicouche qui se trouvent dans une limite de sécurité qui n’est pas exposé toohello Internet mais nécessitent toujours alternée chargement distribution, caractère collant de session ou l’arrêt de Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="9be46-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="9be46-109">Cet article vous guide tout au long des étapes de hello tooconfigure une passerelle d’application avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="9be46-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9be46-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9be46-110">Before you begin</span></span>

1. <span data-ttu-id="9be46-111">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="9be46-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9be46-112">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9be46-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9be46-113">Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9be46-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="9be46-114">Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="9be46-115">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9be46-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="9be46-116">serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.</span><span class="sxs-lookup"><span data-stu-id="9be46-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="9be46-117">Qu’est requis toocreate une passerelle d’application ?</span><span class="sxs-lookup"><span data-stu-id="9be46-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="9be46-118">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="9be46-119">Hello adresses IP répertoriées doivent soit appartenir toohello des réseaux virtuels, mais dans un autre sous-réseau pour la passerelle d’application hello ou doit être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="9be46-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="9be46-120">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="9be46-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9be46-121">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9be46-122">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9be46-123">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="9be46-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9be46-124">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ils respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="9be46-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9be46-125">**La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="9be46-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="9be46-126">Actuellement, seuls hello *base* règle est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9be46-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="9be46-127">Hello *base* règle est la distribution de la charge de tourniquet.</span><span class="sxs-lookup"><span data-stu-id="9be46-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="9be46-128">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9be46-128">Create an application gateway</span></span>

<span data-ttu-id="9be46-129">Hello diffère entre l’utilisation classique Azure et Azure Resource Manager commande hello dans lequel vous créez passerelle d’application hello et articles hello toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="9be46-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="9be46-130">Avec le Gestionnaire de ressources, tous les éléments qui rendent une passerelle d’application est configuré individuellement et rassembler puis toocreate ressource de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="9be46-131">Voici les étapes hello qui sont nécessaire toocreate une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="9be46-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="9be46-132">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9be46-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="9be46-133">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="9be46-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="9be46-134">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9be46-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="9be46-135">Créer une ressource de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="9be46-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9be46-136">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9be46-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9be46-137">Assurez-vous que vous basculez des applets de commande PowerShell en mode toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9be46-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="9be46-138">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9be46-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9be46-139">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9be46-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="9be46-140">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9be46-140">Step 2</span></span>

<span data-ttu-id="9be46-141">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9be46-142">Vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9be46-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="9be46-143">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9be46-143">Step 3</span></span>

<span data-ttu-id="9be46-144">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9be46-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="9be46-145">Étape 4</span><span class="sxs-lookup"><span data-stu-id="9be46-145">Step 4</span></span>

<span data-ttu-id="9be46-146">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)</span><span class="sxs-lookup"><span data-stu-id="9be46-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="9be46-147">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="9be46-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9be46-148">Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9be46-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9be46-149">Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9be46-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="9be46-150">Bonjour précédent exemple, nous avons créé un groupe de ressources appelé « Appgw-rg » et l’emplacement « ouest des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="9be46-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="9be46-151">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="9be46-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="9be46-152">Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="9be46-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="9be46-153">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9be46-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="9be46-154">Cette étape affecte hello adresse plage 10.0.0.0/24 tooa sous-réseau toobe variable utilisée toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9be46-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="9be46-155">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9be46-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="9be46-156">Cette étape crée un réseau virtuel nommé « appgwvnet » dans la ressource groupe « appgw-rg » pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="9be46-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="9be46-157">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9be46-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="9be46-158">Cette étape affecte hello sous-réseau objet toovariable $subnet pour les étapes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="9be46-159">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9be46-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="9be46-160">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9be46-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="9be46-161">Crée une configuration IP de passerelle Application Gateway nommée « gatewayIP01 ».</span><span class="sxs-lookup"><span data-stu-id="9be46-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="9be46-162">Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="9be46-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9be46-163">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="9be46-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="9be46-164">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9be46-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="9be46-165">Cette étape configure le pool d’adresses IP principal hello nommé « pool01 » avec adresse IP adresses « 10.1.1.8, 10.1.1.9, 10.1.1.10 ».</span><span class="sxs-lookup"><span data-stu-id="9be46-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="9be46-166">Ce sont les adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="9be46-167">Vous remplacez hello précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.</span><span class="sxs-lookup"><span data-stu-id="9be46-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="9be46-168">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9be46-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="9be46-169">Cette étape configure le trafic réseau de passerelle paramètre « poolsetting01 » pour la charge hello équilibrés application dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="9be46-170">Étape 4</span><span class="sxs-lookup"><span data-stu-id="9be46-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="9be46-171">Cette étape configure le port IP frontal hello nommé « frontendport01 » pour hello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="9be46-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="9be46-172">Étape 5</span><span class="sxs-lookup"><span data-stu-id="9be46-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="9be46-173">Cette étape crée la configuration IP frontale hello appelée « fipconfig01 » et l’associe à une adresse IP privée à partir du sous-réseau de réseau virtuel en cours hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="9be46-174">Étape 6</span><span class="sxs-lookup"><span data-stu-id="9be46-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="9be46-175">Cette étape crée écouteur hello appelé « listener01 » et associe la configuration IP frontale de hello port frontal toohello.</span><span class="sxs-lookup"><span data-stu-id="9be46-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="9be46-176">Étape 7</span><span class="sxs-lookup"><span data-stu-id="9be46-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="9be46-177">Cette étape crée hello règle équilibreur de charge routage appelé « rule01 » qui configure le comportement de programme d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="9be46-178">Étape 8</span><span class="sxs-lookup"><span data-stu-id="9be46-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="9be46-179">Cette étape configure la taille de l’instance de la passerelle d’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="9be46-180">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="9be46-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="9be46-181">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="9be46-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="9be46-182">Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="9be46-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="9be46-183">Créer une passerelle Application Gateway avec New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="9be46-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="9be46-184">Crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="9be46-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="9be46-185">Dans cet exemple, passerelle d’application hello est appelé « appgwtest ».</span><span class="sxs-lookup"><span data-stu-id="9be46-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="9be46-186">Cette étape crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="9be46-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="9be46-187">Dans l’exemple de hello, passerelle d’application hello est appelé « appgwtest ».</span><span class="sxs-lookup"><span data-stu-id="9be46-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="9be46-188">Supprimer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9be46-188">Delete an application gateway</span></span>

<span data-ttu-id="9be46-189">toodelete une passerelle d’application, vous devez hello toodo comme suit dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="9be46-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="9be46-190">Hello d’utilisation `Stop-AzureRmApplicationGateway` passerelle de hello toostop applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9be46-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="9be46-191">Hello d’utilisation `Remove-AzureRmApplicationGateway` passerelle de hello tooremove applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9be46-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="9be46-192">Vérifiez cette passerelle hello a été supprimée à l’aide de hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9be46-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="9be46-193">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9be46-193">Step 1</span></span>

<span data-ttu-id="9be46-194">Obtenir l’objet de passerelle d’application hello et associez-le tooa variable « $getgw ».</span><span class="sxs-lookup"><span data-stu-id="9be46-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="9be46-195">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9be46-195">Step 2</span></span>

<span data-ttu-id="9be46-196">Utilisez `Stop-AzureRmApplicationGateway` passerelle d’application toostop hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="9be46-197">Cet exemple montre hello `Stop-AzureRmApplicationGateway` applet de commande sur la première ligne de hello, suivie des hello.</span><span class="sxs-lookup"><span data-stu-id="9be46-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="9be46-198">Une fois que la passerelle d’application hello est dans un état arrêté, utilisez hello `Remove-AzureRmApplicationGateway` service de hello tooremove applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9be46-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="9be46-199">Hello **-force** commutateur peut être le message de confirmation de suppression de hello toosuppress utilisé.</span><span class="sxs-lookup"><span data-stu-id="9be46-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="9be46-200">tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureRmApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9be46-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="9be46-201">Cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="9be46-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="9be46-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9be46-202">Next steps</span></span>

<span data-ttu-id="9be46-203">Si vous souhaitez tooconfigure le déchargement SSL, consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9be46-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="9be46-204">Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="9be46-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="9be46-205">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="9be46-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="9be46-206">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="9be46-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="9be46-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9be46-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

