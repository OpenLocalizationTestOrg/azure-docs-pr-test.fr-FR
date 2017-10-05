---
title: "Utiliser la passerelle Azure Application Gateway avec équilibreur de charge interne - PowerShell | Microsoft Docs"
description: "Cette page fournit des instructions pour la création, la configuration, le démarrage et la suppression d’une passerelle Application Gateway Azure avec un équilibrage de charge interne (ILB) pour Azure Resource Manager"
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
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="8f379-103">Créer une passerelle Application Gateway avec un équilibrage de charge interne (ILB) à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f379-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f379-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f379-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="8f379-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f379-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="8f379-106">Vous pouvez configurer une passerelle Azure Application Gateway avec une adresse IP virtuelle côté Internet ou avec un point de terminaison interne non exposé à Internet, également appelé point de terminaison d’équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="8f379-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="8f379-107">La configuration de la passerelle avec un équilibrage de charge interne est utile pour les applications métier internes non exposées à Internet.</span><span class="sxs-lookup"><span data-stu-id="8f379-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="8f379-108">Elle est également utile pour les services et niveaux au sein d’une application multiniveau qui se trouve dans une limite de sécurité non exposée à Internet, mais qui requiert tout de même une distribution de charge par tourniquet, une adhérence de session ou une terminaison SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="8f379-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="8f379-109">Cet article vous guidera au cours des étapes de configuration d’une passerelle Application Gateway avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="8f379-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f379-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8f379-110">Before you begin</span></span>

1. <span data-ttu-id="8f379-111">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="8f379-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="8f379-112">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8f379-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8f379-113">Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f379-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="8f379-114">Assurez-vous qu’aucun ordinateur virtuel ou déploiement cloud n’utilise le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8f379-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="8f379-115">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f379-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="8f379-116">Les serveurs que vous configurez pour utiliser la passerelle Application Gateway doivent exister ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="8f379-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="8f379-117">Quels sont les éléments nécessaires pour créer une passerelle Application Gateway ?</span><span class="sxs-lookup"><span data-stu-id="8f379-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="8f379-118">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="8f379-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="8f379-119">Les adresses IP répertoriées doivent appartenir au réseau virtuel, mais à un sous-réseau différent de la plateforme d’application ou elles doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="8f379-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="8f379-120">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="8f379-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8f379-121">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="8f379-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="8f379-122">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f379-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="8f379-123">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="8f379-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="8f379-124">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="8f379-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="8f379-125">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="8f379-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="8f379-126">Actuellement, seule la règle *de base* est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8f379-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="8f379-127">La règle de *base* est la distribution de charge par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="8f379-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="8f379-128">Créez une passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8f379-128">Create an application gateway</span></span>

<span data-ttu-id="8f379-129">La différence entre l’utilisation d’Azure Classic et celle d’Azure Resource Manager réside dans l’ordre de création de la passerelle Application Gateway et des éléments à configurer.</span><span class="sxs-lookup"><span data-stu-id="8f379-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="8f379-130">Avec Resource Manager, tous les éléments constitutifs d’une passerelle Application Gateway sont configurés individuellement, puis regroupés pour créer la ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f379-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="8f379-131">Procédure de création d’une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="8f379-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="8f379-132">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f379-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="8f379-133">Création d'un réseau virtuel et d'un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8f379-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="8f379-134">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8f379-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="8f379-135">Créer une ressource de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8f379-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="8f379-136">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f379-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="8f379-137">Veillez à passer en mode PowerShell pour utiliser les applets de commande d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f379-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="8f379-138">Pour plus d’informations, voir l’article [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8f379-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="8f379-139">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8f379-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="8f379-140">Étape 2</span><span class="sxs-lookup"><span data-stu-id="8f379-140">Step 2</span></span>

<span data-ttu-id="8f379-141">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="8f379-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="8f379-142">Vous êtes invité à saisir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8f379-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f379-143">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="8f379-143">Step 3</span></span>

<span data-ttu-id="8f379-144">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8f379-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="8f379-145">Étape 4</span><span class="sxs-lookup"><span data-stu-id="8f379-145">Step 4</span></span>

<span data-ttu-id="8f379-146">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)</span><span class="sxs-lookup"><span data-stu-id="8f379-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="8f379-147">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="8f379-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8f379-148">Ce dernier est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="8f379-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="8f379-149">Assurez-vous que toutes les commandes pour la création d’une passerelle Application Gateway utilisent le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8f379-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="8f379-150">Dans l’exemple précédent, nous avons créé un groupe de ressources appelé « appgw-rg », ainsi que l’emplacement « West US ».</span><span class="sxs-lookup"><span data-stu-id="8f379-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="8f379-151">Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8f379-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="8f379-152">L’exemple ci-après indique comment créer un réseau virtuel à l’aide de Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="8f379-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="8f379-153">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8f379-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="8f379-154">Attribue la plage d’adresses 10.0.0.0/24 à une variable subnet à utiliser pour créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f379-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="8f379-155">Étape 2</span><span class="sxs-lookup"><span data-stu-id="8f379-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="8f379-156">Crée un réseau virtuel nommé « appgwvnet » dans le groupe de ressources « appw-rg » pour la région « West US » à l’aide du préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="8f379-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f379-157">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="8f379-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="8f379-158">Assigne l’objet de sous-réseau à la variable $subnet pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="8f379-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="8f379-159">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8f379-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="8f379-160">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8f379-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="8f379-161">Crée une configuration IP de passerelle Application Gateway nommée « gatewayIP01 ».</span><span class="sxs-lookup"><span data-stu-id="8f379-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="8f379-162">Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="8f379-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="8f379-163">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="8f379-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="8f379-164">Étape 2</span><span class="sxs-lookup"><span data-stu-id="8f379-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="8f379-165">Configure le pool d’adresses IP principal nommé « pool01 » avec les adresses IP « 10.1.1.8, 10.1.1.9, 10.1.1.10 ».</span><span class="sxs-lookup"><span data-stu-id="8f379-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="8f379-166">Il s’agit des adresses IP qui recevront le trafic réseau provenant du point de terminaison IP frontal.</span><span class="sxs-lookup"><span data-stu-id="8f379-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="8f379-167">Remplacez les adresses IP précédentes pour ajouter vos propres points de terminaison d’adresse IP d’application.</span><span class="sxs-lookup"><span data-stu-id="8f379-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f379-168">Étape 3</span><span class="sxs-lookup"><span data-stu-id="8f379-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="8f379-169">Cette étape permet de configurer les paramètres de passerelle Application Gateway « poolsetting01 » pour le trafic réseau à charge équilibrée dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="8f379-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="8f379-170">Étape 4</span><span class="sxs-lookup"><span data-stu-id="8f379-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="8f379-171">Cette étape permet de configurer le port d’adresses IP frontal nommé « frontendport01 » pour l’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="8f379-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="8f379-172">Étape 5</span><span class="sxs-lookup"><span data-stu-id="8f379-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="8f379-173">Cette étape permet de créer la configuration IP frontale nommée « fipconfig01 » et lui associe une adresse IP privée à partir du sous-réseau du réseau virtuel actuel.</span><span class="sxs-lookup"><span data-stu-id="8f379-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="8f379-174">Étape 6</span><span class="sxs-lookup"><span data-stu-id="8f379-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="8f379-175">Cette étape permet de créer l’écouteur nommé « listener01 » et associe le port frontal à la configuration IP frontale.</span><span class="sxs-lookup"><span data-stu-id="8f379-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="8f379-176">Étape 7</span><span class="sxs-lookup"><span data-stu-id="8f379-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="8f379-177">Cette étape permet de créer la règle d’acheminement d’équilibrage de charge nommée « rule01 » qui configure le comportement d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f379-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="8f379-178">Étape 8</span><span class="sxs-lookup"><span data-stu-id="8f379-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="8f379-179">Cette étape permet de configurer la taille d’instance de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f379-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="8f379-180">La valeur par défaut pour *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="8f379-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="8f379-181">La valeur par défaut du paramètre *GatewaySize* est Medium.</span><span class="sxs-lookup"><span data-stu-id="8f379-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="8f379-182">Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="8f379-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="8f379-183">Créer une passerelle Application Gateway avec New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="8f379-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="8f379-184">Créez une passerelle Application Gateway avec tous les éléments de configuration de la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="8f379-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="8f379-185">Dans notre exemple, la passerelle Application Gateway est appelée « appgwtest ».</span><span class="sxs-lookup"><span data-stu-id="8f379-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="8f379-186">Cette étape permet de créer une passerelle Application Gateway avec tous les éléments de configuration de la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="8f379-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="8f379-187">Dans notre exemple, la passerelle Application Gateway est appelée « appgwtest ».</span><span class="sxs-lookup"><span data-stu-id="8f379-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="8f379-188">Supprimer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8f379-188">Delete an application gateway</span></span>

<span data-ttu-id="8f379-189">Pour supprimer une passerelle Application Gateway, vous devez effectuer les opérations suivantes dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="8f379-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="8f379-190">Utilisez l’applet de commande `Stop-AzureRmApplicationGateway` pour arrêter la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8f379-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="8f379-191">Utilisez l’applet de commande `Remove-AzureRmApplicationGateway` pour supprimer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="8f379-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="8f379-192">Vérifiez que la passerelle a été supprimée à l’aide de l’applet de commande `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="8f379-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="8f379-193">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8f379-193">Step 1</span></span>

<span data-ttu-id="8f379-194">Obtenez l’objet de passerelle Application Gateway et associez-le à une variable « $getgw ».</span><span class="sxs-lookup"><span data-stu-id="8f379-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="8f379-195">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="8f379-195">Step 2</span></span>

<span data-ttu-id="8f379-196">Utilisez `Stop-AzureRmApplicationGateway` pour arrêter la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f379-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="8f379-197">Cet exemple montre l'applet de commande `Stop-AzureRmApplicationGateway` sur la première ligne, suivie de la sortie.</span><span class="sxs-lookup"><span data-stu-id="8f379-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

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

<span data-ttu-id="8f379-198">Une fois la passerelle Application Gateway dans un état arrêté, utilisez l’applet de commande `Remove-AzureRmApplicationGateway` pour supprimer le service.</span><span class="sxs-lookup"><span data-stu-id="8f379-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

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
> <span data-ttu-id="8f379-199">Il est possible d’utiliser le commutateur **-force** pour supprimer le message de confirmation de suppression.</span><span class="sxs-lookup"><span data-stu-id="8f379-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="8f379-200">Pour vérifier que le service a été supprimé, vous pouvez utiliser l’applet de commande `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="8f379-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="8f379-201">Cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="8f379-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="8f379-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f379-202">Next steps</span></span>

<span data-ttu-id="8f379-203">Si vous souhaitez configurer le déchargement SSL, consultez [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="8f379-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="8f379-204">Si vous souhaitez configurer une passerelle d’application à utiliser avec l’équilibreur de charge interne, consultez [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="8f379-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="8f379-205">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="8f379-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="8f379-206">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="8f379-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="8f379-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8f379-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

