---
title: "Créer une passerelle Application Gateway avec des règles de routage d’URL | Microsoft Docs"
description: "Cette page fournit des instructions pour créer et configurer une passerelle Application Gateway Azure avec les règles de routage d’URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="6f0eb-103">Créer une passerelle Application Gateway à l’aide du routage basé sur le chemin</span><span class="sxs-lookup"><span data-stu-id="6f0eb-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f0eb-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6f0eb-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="6f0eb-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f0eb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="6f0eb-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f0eb-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="6f0eb-107">Le routage basé sur le chemin d’URL vous permet d’associer des routes basées sur le chemin d’URL de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="6f0eb-108">Il vérifie s’il existe une route vers un pool principal configuré pour les listes d’URL dans la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="6f0eb-109">Il envoie ensuite le trafic réseau vers le pool principal défini.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="6f0eb-110">Une utilisation courante du routage basé sur l’URL consiste à équilibrer la charge des demandes pour différents types de contenu entre différents pools de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="6f0eb-111">Le routage basé sur l’URL introduit un nouveau type de règle pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="6f0eb-112">La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="6f0eb-113">Le type de règle de base fournit le service de tourniquet (round robin) pour les pools principaux alors que PathBasedRouting, en plus de la distribution de tourniquet, prend également en compte le modèle de chemin de l’URL de demande lors du choix du pool principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="6f0eb-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="6f0eb-114">Scenario</span></span>

<span data-ttu-id="6f0eb-115">Dans l’exemple suivant, la passerelle Application Gateway gère le trafic pour contoso.com avec deux pools de serveurs principaux : un pool de serveurs vidéo et un pool de serveurs d’images.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="6f0eb-116">Les demandes pour http://contoso.com/image* sont routées vers le pool de serveurs d’images (pool1) et celles pour http://contoso.com/video* sont routées vers le pool de serveurs vidéo (pool2).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="6f0eb-117">Si aucun des modèles de chemin ne correspond, un pool de serveurs par défaut (pool1) est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![itinéraire d’URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="6f0eb-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6f0eb-119">Before you begin</span></span>

1. <span data-ttu-id="6f0eb-120">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="6f0eb-121">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6f0eb-122">Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="6f0eb-123">Assurez-vous qu’aucun ordinateur virtuel ou déploiement cloud n’utilise le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="6f0eb-124">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="6f0eb-125">Les serveurs ajoutés au pool principal pour utiliser la passerelle Application Gateway doivent exister, ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="6f0eb-126">Quels sont les éléments nécessaires pour créer une passerelle Application Gateway ?</span><span class="sxs-lookup"><span data-stu-id="6f0eb-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="6f0eb-127">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="6f0eb-128">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="6f0eb-129">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6f0eb-130">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="6f0eb-131">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="6f0eb-132">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="6f0eb-133">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="6f0eb-134">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux, et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="6f0eb-135">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-135">Create an application gateway</span></span>

<span data-ttu-id="6f0eb-136">La différence entre l’utilisation d’Azure Classic et celle d’Azure Resource Manager réside dans l’ordre de création de la passerelle Application Gateway et des éléments à configurer.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="6f0eb-137">Avec Resource Manager, tous les éléments constitutifs d’une passerelle Application Gateway sont configurés individuellement, puis regroupés pour créer la ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="6f0eb-138">Procédure de création d’une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="6f0eb-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="6f0eb-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f0eb-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="6f0eb-140">Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="6f0eb-141">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="6f0eb-142">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="6f0eb-143">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f0eb-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="6f0eb-144">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6f0eb-145">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="6f0eb-146">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="6f0eb-146">Step 1</span></span>

<span data-ttu-id="6f0eb-147">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="6f0eb-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6f0eb-148">Vous êtes invité à vous authentifier à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="6f0eb-149">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="6f0eb-149">Step 2</span></span>

<span data-ttu-id="6f0eb-150">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="6f0eb-151">Étape 3</span><span class="sxs-lookup"><span data-stu-id="6f0eb-151">Step 3</span></span>

<span data-ttu-id="6f0eb-152">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="6f0eb-153">Étape 4</span><span class="sxs-lookup"><span data-stu-id="6f0eb-153">Step 4</span></span>

<span data-ttu-id="6f0eb-154">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="6f0eb-155">Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="6f0eb-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="6f0eb-156">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6f0eb-157">Ce groupe de ressources est utilisé comme emplacement par défaut pour les ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6f0eb-158">Assurez-vous que toutes les commandes pour la création d'une passerelle Application Gateway utiliseront le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="6f0eb-159">Dans l’exemple ci-dessus, nous avons créé un groupe de ressources appelé « appgw-RG », ainsi que l’emplacement « West US ».</span><span class="sxs-lookup"><span data-stu-id="6f0eb-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="6f0eb-160">Si vous devez configurer une sonde personnalisée pour votre passerelle Application Gateway, consultez [Création d’une passerelle Application Gateway avec des sondes personnalisées à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="6f0eb-161">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="6f0eb-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="6f0eb-162">Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="6f0eb-163">L’exemple ci-après indique comment créer un réseau virtuel à l’aide de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="6f0eb-164">Cet exemple crée un réseau virtuel pour Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="6f0eb-165">Application Gateway requiert son propre sous-réseau. C’est la raison pour laquelle le sous-réseau créé pour Application Gateway est plus petit que l’espace d’adressage du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="6f0eb-166">Ainsi, d’autres ressources, y compris sans s’y limiter les serveurs web, sont configurées dans le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="6f0eb-167">Étape 1</span><span class="sxs-lookup"><span data-stu-id="6f0eb-167">Step 1</span></span>

<span data-ttu-id="6f0eb-168">Attribuez la plage d’adresses 10.0.0.0/24 à la variable subnet à utiliser pour créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="6f0eb-169">Cette étape crée l’objet de configuration du sous-réseau pour Application Gateway, qui est utilisé dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="6f0eb-170">Étape 2</span><span class="sxs-lookup"><span data-stu-id="6f0eb-170">Step 2</span></span>

<span data-ttu-id="6f0eb-171">Créez un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région « West US » à l’aide du préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="6f0eb-172">Cette étape termine la configuration du réseau virtuel avec un seul sous-réseau de résidence d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="6f0eb-173">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="6f0eb-173">Step 3</span></span>

<span data-ttu-id="6f0eb-174">Affectez la variable de sous-réseau pour les étapes suivantes, transmise à l’applet de commande `New-AzureRMApplicationGateway` dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="6f0eb-175">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="6f0eb-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="6f0eb-176">Créez une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région « West US ».</span><span class="sxs-lookup"><span data-stu-id="6f0eb-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="6f0eb-177">Application Gateway peut utiliser une adresse IP publique, l’adresse IP ou les deux pour recevoir les demandes d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="6f0eb-178">Cet exemple utilise uniquement une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-178">This example only uses a public IP address.</span></span> <span data-ttu-id="6f0eb-179">Dans l’exemple suivant, aucun nom DNS n’est configuré pour la création de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="6f0eb-180">Application Gateway ne prend pas en charge de noms DNS personnalisés sur des adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="6f0eb-181">Si un nom personnalisé est requis pour le point de terminaison public, un enregistrement CNAME doit être créé pour pointer vers le nom DNS généré automatiquement pour l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="6f0eb-182">Une adresse IP est affectée à la passerelle Application Gateway au démarrage du service.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="6f0eb-183">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-183">Create application gateway configuration</span></span>

<span data-ttu-id="6f0eb-184">Tous les éléments de configuration doivent être installés avant de créer la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="6f0eb-185">Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="6f0eb-186">Étape 1</span><span class="sxs-lookup"><span data-stu-id="6f0eb-186">Step 1</span></span>

<span data-ttu-id="6f0eb-187">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="6f0eb-188">Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="6f0eb-189">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="6f0eb-190">Étape 2</span><span class="sxs-lookup"><span data-stu-id="6f0eb-190">Step 2</span></span>

<span data-ttu-id="6f0eb-191">Configurez les pools d’adresses IP principaux nommés **pool01** et **pool2** avec les adresses IP pour **pool1** et **pool2**.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="6f0eb-192">Ces adresses IP sont les adresses IP des ressources qui hébergent l’application web devant être protégée par Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="6f0eb-193">L’intégrité des membres du pool principal est validée par des sondes de base ou personnalisées.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="6f0eb-194">Le trafic est alors acheminé vers ces membres lorsque les demandes arrivent dans Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="6f0eb-195">Les pools principaux peuvent être utilisés par plusieurs règles au sein d’Application Gateway, ce qui signifie qu’un pool principal peut être utilisé pour plusieurs applications web résidant sur le même hôte.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="6f0eb-196">Dans cet exemple, il existe deux pools principaux pour acheminer le trafic réseau selon le chemin d’URL.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="6f0eb-197">Un pool reçoit le trafic du chemin d’URL « /video » et l’autre pool reçoit le trafic du chemin « /image ».</span><span class="sxs-lookup"><span data-stu-id="6f0eb-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="6f0eb-198">Remplacez les adresses IP précédentes pour ajouter vos propres points de terminaison d’adresse IP d’application.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="6f0eb-199">Étape 3</span><span class="sxs-lookup"><span data-stu-id="6f0eb-199">Step 3</span></span>

<span data-ttu-id="6f0eb-200">Configurez les paramètres de passerelle Application Gateway **poolsetting01** et **poolsetting02** pour le trafic réseau à charge équilibrée dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="6f0eb-201">Dans cet exemple, vous configurez différents paramètres pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="6f0eb-202">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="6f0eb-203">Les paramètres HTTP du serveur principal sont utilisés par des règles pour router le trafic vers les membres appropriés du pool principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="6f0eb-204">Ils déterminent le protocole et le port utilisés lors de l’envoi du trafic vers les membres du pool principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="6f0eb-205">Les sessions basées sur les cookies sont également déterminées par les paramètres HTTP du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="6f0eb-206">Si elle est activée, l’affinité de session basée sur les cookies envoie le trafic vers le même serveur principal que les requêtes précédentes pour chaque paquet.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="6f0eb-207">Étape 4</span><span class="sxs-lookup"><span data-stu-id="6f0eb-207">Step 4</span></span>

<span data-ttu-id="6f0eb-208">Configurez l’adresse IP frontale avec un point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="6f0eb-209">L’objet de configuration de l’adresse IP frontale est utilisé par un écouteur pour associer l’adresse IP vers l’extérieur avec l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="6f0eb-210">Étape 5</span><span class="sxs-lookup"><span data-stu-id="6f0eb-210">Step 5</span></span>

<span data-ttu-id="6f0eb-211">Configurez le port frontal pour une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="6f0eb-212">L’objet de configuration du port frontal est utilisé par un écouteur pour définir le port écouté par Application Gateway pour connaître le trafic sur l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="6f0eb-213">Étape 6</span><span class="sxs-lookup"><span data-stu-id="6f0eb-213">Step 6</span></span>

<span data-ttu-id="6f0eb-214">Configurez l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-214">Configure the listener.</span></span> <span data-ttu-id="6f0eb-215">Cette étape configure l’écouteur pour l’adresse IP publique et le port utilisé pour recevoir le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="6f0eb-216">L’exemple suivant utilise la configuration de l’adresse IP frontale configurée précédemment, la configuration de port frontal et un protocole (http ou https), et il configure l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="6f0eb-217">Dans cet exemple, l’écouteur écoute le trafic HTTP sur le port 80 sur l’adresse IP publique créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="6f0eb-218">Étape 7</span><span class="sxs-lookup"><span data-stu-id="6f0eb-218">Step 7</span></span>

<span data-ttu-id="6f0eb-219">Configurez les chemins de règles d’URL pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="6f0eb-220">Cette étape configure le chemin d’accès relatif utilisé par la passerelle d’application et définit le mappage entre le chemin d’URL et le pool principal qui est assigné pour gérer le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f0eb-221">Chaque chemin d’accès doit commencer par le signe / et le seul endroit où un astérisque (\*) est autorisé est à la fin.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="6f0eb-222">/xyz, /xyz ou /xyz/ sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="6f0eb-223">La chaîne transmise à l’outil de correspondance de chemin n’inclut pas de texte après le premier signe ? ou #. De plus, ces caractères ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="6f0eb-224">L’exemple suivant crée deux règles : une pour le chemin « /image/ » qui achemine le trafic vers le pool principal « pool1 » et une autre pour le chemin « /video/ » qui achemine le trafic vers le pool principal « pool2 ».</span><span class="sxs-lookup"><span data-stu-id="6f0eb-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="6f0eb-225">Ces règles garantissent que le trafic de chaque jeu d’URL est routé vers le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="6f0eb-226">Par exemple, http://contoso.com/image/figure1.jpg accède à pool1 et http://contoso.com/video/example.mp4 à pool2.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="6f0eb-227">Si le chemin ne correspond à aucune des règles de chemins prédéfinies, la configuration de mappage des chemins de règles configure également un pool d’adresses principal par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="6f0eb-228">Par exemple, http://contoso.com/shoppingcart/test.html accède à pool1, car il est défini en tant que pool par défaut pour le trafic sans correspondance.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="6f0eb-229">Étape 8</span><span class="sxs-lookup"><span data-stu-id="6f0eb-229">Step 8</span></span>

<span data-ttu-id="6f0eb-230">Créez un paramètre de règle.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-230">Create a rule setting.</span></span> <span data-ttu-id="6f0eb-231">Cette étape configure la passerelle Application Gateway pour utiliser le routage basé sur le chemin d’URL.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="6f0eb-232">La variable `$urlPathMap` définie à l’étape précédente est maintenant utilisée pour créer la règle de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="6f0eb-233">Dans cette étape, nous associons la règle avec un écouteur et le mappage de chemin d’accès d’URL créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="6f0eb-234">Étape 9</span><span class="sxs-lookup"><span data-stu-id="6f0eb-234">Step 9</span></span>

<span data-ttu-id="6f0eb-235">Configurez le nombre d’instances et taille de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="6f0eb-236">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-236">Create Application Gateway</span></span>

<span data-ttu-id="6f0eb-237">Créez une passerelle Application Gateway avec tous les objets de configuration à partir de la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6f0eb-238">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6f0eb-238">Get application gateway DNS name</span></span>

<span data-ttu-id="6f0eb-239">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="6f0eb-240">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6f0eb-241">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="6f0eb-242">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6f0eb-243">Pour configurer l’enregistrement CNAME d’adresses IP frontales, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="6f0eb-244">Le nom DNS de la passerelle d’application doit être utilisé pour créer un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="6f0eb-245">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6f0eb-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6f0eb-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f0eb-246">Next steps</span></span>

<span data-ttu-id="6f0eb-247">Pour en savoir plus sur le déchargement SSL (Secure Sockets Layer), consultez [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6f0eb-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

