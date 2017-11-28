---
title: "aaaCreate une passerelle d’application à l’aide de routage d’URL règles | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure à l’aide des règles de routage d’URL"
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="e108e-103">Créer une passerelle Application Gateway à l’aide du routage basé sur le chemin</span><span class="sxs-lookup"><span data-stu-id="e108e-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e108e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e108e-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="e108e-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e108e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="e108e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e108e-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="e108e-107">Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous selon le chemin d’URL de hello d’une requête Http.</span><span class="sxs-lookup"><span data-stu-id="e108e-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="e108e-108">Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour hello les URL présentée dans hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="e108e-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="e108e-109">Il envoie ensuite toohello de trafic réseau hello défini par pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="e108e-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="e108e-110">Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.</span><span class="sxs-lookup"><span data-stu-id="e108e-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="e108e-111">Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle.</span><span class="sxs-lookup"><span data-stu-id="e108e-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="e108e-112">La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="e108e-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="e108e-113">Type de règle de base fournit des service tourniquet pour les principaux hello pools lors PathBasedRouting en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte lors du choix du pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="e108e-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="e108e-114">Scenario</span></span>

<span data-ttu-id="e108e-115">Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com avec deux pools de serveur principal : pool de serveurs vidéo et pool de serveurs d’image.</span><span class="sxs-lookup"><span data-stu-id="e108e-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="e108e-116">Les demandes d’http://contoso.com/image * sont acheminés pool de serveurs tooimage (pool1) et http://contoso.com/video * sont acheminés pool de serveurs toovideo (pool2).</span><span class="sxs-lookup"><span data-stu-id="e108e-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="e108e-117">Si aucun des modèles de chemin d’accès hello correspondent, un pool de serveurs par défaut (pool1) est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e108e-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![itinéraire d’URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="e108e-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e108e-119">Before you begin</span></span>

1. <span data-ttu-id="e108e-120">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="e108e-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="e108e-121">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e108e-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e108e-122">Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e108e-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="e108e-123">Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="e108e-124">passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e108e-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="e108e-125">les serveurs Hello ajouté passerelle d’application hello toohello principal pool toouse doit exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello ou avec une adresse IP publique/VIP attribué.</span><span class="sxs-lookup"><span data-stu-id="e108e-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="e108e-126">Qu’est requis toocreate une passerelle d’application ?</span><span class="sxs-lookup"><span data-stu-id="e108e-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="e108e-127">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="e108e-128">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="e108e-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="e108e-129">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="e108e-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e108e-130">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="e108e-131">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="e108e-132">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="e108e-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="e108e-133">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="e108e-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="e108e-134">**La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="e108e-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="e108e-135">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e108e-135">Create an application gateway</span></span>

<span data-ttu-id="e108e-136">Hello diffère entre l’utilisation classique Azure et Azure Resource Manager commande hello dans lequel vous créez passerelle d’application hello et articles hello toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="e108e-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="e108e-137">Avec le Gestionnaire de ressources, tous les éléments qui rendent une passerelle d’application sont configurées individuellement et rassembler puis toocreate ressource de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="e108e-138">Voici les étapes hello qui sont nécessaire toocreate une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="e108e-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="e108e-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e108e-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="e108e-140">Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="e108e-141">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e108e-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="e108e-142">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e108e-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="e108e-143">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e108e-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="e108e-144">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="e108e-145">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e108e-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="e108e-146">Étape 1</span><span class="sxs-lookup"><span data-stu-id="e108e-146">Step 1</span></span>

<span data-ttu-id="e108e-147">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="e108e-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e108e-148">Vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e108e-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="e108e-149">Étape 2</span><span class="sxs-lookup"><span data-stu-id="e108e-149">Step 2</span></span>

<span data-ttu-id="e108e-150">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="e108e-151">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="e108e-151">Step 3</span></span>

<span data-ttu-id="e108e-152">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="e108e-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="e108e-153">Étape 4</span><span class="sxs-lookup"><span data-stu-id="e108e-153">Step 4</span></span>

<span data-ttu-id="e108e-154">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="e108e-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="e108e-155">Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="e108e-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="e108e-156">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="e108e-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e108e-157">Ce groupe de ressources est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e108e-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="e108e-158">Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e108e-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="e108e-159">Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé « appgw-RG » et l’emplacement « Ouest des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="e108e-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="e108e-160">Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e108e-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="e108e-161">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="e108e-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="e108e-162">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="e108e-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="e108e-163">Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="e108e-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="e108e-164">Cet exemple crée un réseau virtuel pour hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="e108e-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="e108e-165">Passerelle d’application nécessite son propre sous-réseau, c’est pourquoi sous-réseau hello créé pour hello passerelle d’Application est plus petit que hello espace d’adressage de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e108e-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="e108e-166">Ainsi, pour les autres ressources, y compris mais non limité tooweb serveurs toobe dans hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e108e-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="e108e-167">Étape 1</span><span class="sxs-lookup"><span data-stu-id="e108e-167">Step 1</span></span>

<span data-ttu-id="e108e-168">Affecter hello adresse plage 10.0.0.0/24 toohello sous-réseau toobe variable utilisée toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e108e-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="e108e-169">Cela crée d’objet de configuration de sous-réseau hello pour hello passerelle d’Application, qui est utilisé dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="e108e-170">Étape 2</span><span class="sxs-lookup"><span data-stu-id="e108e-170">Step 2</span></span>

<span data-ttu-id="e108e-171">Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="e108e-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="e108e-172">Configuration de hello Hello réseau virtuel avec un sous-réseau unique pour tooreside de passerelle d’Application hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="e108e-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="e108e-173">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="e108e-173">Step 3</span></span>

<span data-ttu-id="e108e-174">Attribuer variable de sous-réseau de hello hello pour les étapes suivantes, il est passé toohello `New-AzureRMApplicationGateway` applet de commande dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e108e-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="e108e-175">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="e108e-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="e108e-176">Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="e108e-177">Passerelle d’application peut utiliser une adresse IP publique, adresse IP interne ou les deux requêtes tooreceive pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e108e-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="e108e-178">Cet exemple utilise uniquement une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e108e-178">This example only uses a public IP address.</span></span> <span data-ttu-id="e108e-179">Dans l’exemple suivant de hello, aucun nom DNS n’est configuré pour la création d’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="e108e-180">Application Gateway ne prend pas en charge de noms DNS personnalisés sur des adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="e108e-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="e108e-181">Si un nom personnalisé est requis pour le point de terminaison public hello, un enregistrement CNAME doit être créé nom_DNS toopoint toohello généré automatiquement pour l’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="e108e-182">Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="e108e-183">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e108e-183">Create application gateway configuration</span></span>

<span data-ttu-id="e108e-184">Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="e108e-185">Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="e108e-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="e108e-186">Étape 1</span><span class="sxs-lookup"><span data-stu-id="e108e-186">Step 1</span></span>

<span data-ttu-id="e108e-187">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="e108e-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="e108e-188">Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="e108e-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="e108e-189">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="e108e-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="e108e-190">Étape 2</span><span class="sxs-lookup"><span data-stu-id="e108e-190">Step 2</span></span>

<span data-ttu-id="e108e-191">Configurer le pool d’adresses IP principal hello nommé **pool01** et **pool2** avec des adresses IP pour **pool1** et **pool2**.</span><span class="sxs-lookup"><span data-stu-id="e108e-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="e108e-192">Ces adresses IP sont des adresses IP de hello des ressources hello qui hébergent hello web application toobe protégé par la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="e108e-193">Ces membres du pool principal sont tous les toobe validé intègre par les sondes qu’ils soient sondes de base ou des sondes personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e108e-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="e108e-194">Le trafic est alors acheminé toothem lorsque des demandes parviennent à la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="e108e-195">Pools principaux peuvent être utilisées par plusieurs règles au sein de la passerelle d’application hello, ce qui signifie un pool principal peut être utilisé pour plusieurs applications web qui résident sur hello même hôte.</span><span class="sxs-lookup"><span data-stu-id="e108e-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="e108e-196">Dans cet exemple, il existe deux principaux pools tooroute le trafic réseau selon le chemin d’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="e108e-197">Un pool reçoit le trafic du chemin d’URL « /video » et l’autre pool reçoit le trafic du chemin « /image ».</span><span class="sxs-lookup"><span data-stu-id="e108e-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="e108e-198">Remplacez hello précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.</span><span class="sxs-lookup"><span data-stu-id="e108e-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="e108e-199">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="e108e-199">Step 3</span></span>

<span data-ttu-id="e108e-200">Configurer le paramètre de passerelle d’application **poolsetting01** et **poolsetting02** hello équilibrés en charge le trafic réseau dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="e108e-201">Dans cet exemple, vous configurez les paramètres de pool principal différent pour les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="e108e-202">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="e108e-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="e108e-203">Paramètres HTTP du serveur principal sont utilisées par les règles tooroute trafic toohello les membres du pool principal approprié.</span><span class="sxs-lookup"><span data-stu-id="e108e-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="e108e-204">Ce paramètre détermine le protocole de hello et port qui est utilisé lors de l’envoi de trafic toohello les membres du pool principal.</span><span class="sxs-lookup"><span data-stu-id="e108e-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="e108e-205">Sessions basées sur un cookie sont également déterminées par les paramètres HTTP hello principal.</span><span class="sxs-lookup"><span data-stu-id="e108e-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="e108e-206">S’il est activé, l’affinité de basé sur cookie de session envoie le trafic toohello même principal en tant que requêtes précédentes pour chaque paquet.</span><span class="sxs-lookup"><span data-stu-id="e108e-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="e108e-207">Étape 4</span><span class="sxs-lookup"><span data-stu-id="e108e-207">Step 4</span></span>

<span data-ttu-id="e108e-208">Configuration IP frontale de hello avec le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="e108e-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="e108e-209">objet de configuration IP frontale Hello est utilisé par un Bonjour de toorelate écouteur vers l’adresse IP qu’un écouteur hello extérieur.</span><span class="sxs-lookup"><span data-stu-id="e108e-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="e108e-210">Étape 5</span><span class="sxs-lookup"><span data-stu-id="e108e-210">Step 5</span></span>

<span data-ttu-id="e108e-211">Configurer le port frontal de hello pour une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="e108e-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="e108e-212">objet de configuration du port frontal Hello est utilisé par un toodefine écoute le port d’écoute de passerelle d’Application hello pour le trafic sur le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="e108e-213">Étape 6</span><span class="sxs-lookup"><span data-stu-id="e108e-213">Step 6</span></span>

<span data-ttu-id="e108e-214">Configurer un écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-214">Configure hello listener.</span></span> <span data-ttu-id="e108e-215">Cette étape configure l’écouteur hello pour l’adresse IP publique de hello et le port utilisé tooreceive du trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="e108e-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="e108e-216">Hello, l’exemple suivant prend une configuration IP frontale de hello précédemment configuré, la configuration de port frontal et un protocole (http ou https) et configure l’écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="e108e-217">Dans cet exemple, port d’écoute hello écoute tooHTTP du trafic sur le port 80 sur l’adresse IP publique hello qui a été créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e108e-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="e108e-218">Étape 7</span><span class="sxs-lookup"><span data-stu-id="e108e-218">Step 7</span></span>

<span data-ttu-id="e108e-219">Configurer les chemins d’accès de la règle URL pour les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="e108e-220">Cette étape configure le chemin d’accès relatif hello utilisé par la passerelle d’application et définit le mappage hello entre le chemin d’accès des URL hello et pool principal hello qui reçoit le trafic entrant de toohandle hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e108e-221">Chaque chemin d’accès doit commencer par / et hello uniquement une «\*» est autorisé, à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="e108e-222">/xyz, /xyz* ou /xyz/* sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="e108e-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="e108e-223">Hello chaîne fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord « ? » ou « # » et ces caractères ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="e108e-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="e108e-224">Hello exemple suivant crée deux règles : une pour le chemin d’accès « image / » routage du trafic tooback-end « pool1 » et une autre pour « video / » chemin d’accès de routage du trafic tooback-end « pool2 ».</span><span class="sxs-lookup"><span data-stu-id="e108e-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="e108e-225">Ces règles vous assurer que le trafic pour chaque jeu d’URL est routé toohello principal.</span><span class="sxs-lookup"><span data-stu-id="e108e-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="e108e-226">Par exemple, http://contoso.com/image/figure1.jpg devient toopool1 et http://contoso.com/video/example.mp4 devient toopool2.</span><span class="sxs-lookup"><span data-stu-id="e108e-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="e108e-227">Si le chemin d’accès hello ne correspond pas à une des règles de chemin d’accès prédéterminé hello, configuration de mappage de chemin d’accès de règle hello configure également un pool d’adresses principal par défaut.</span><span class="sxs-lookup"><span data-stu-id="e108e-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="e108e-228">Par exemple, http://contoso.com/shoppingcart/test.html devient toopool1 telle qu’elle est définie en tant que pool par défaut de hello pour le trafic non apparié.</span><span class="sxs-lookup"><span data-stu-id="e108e-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="e108e-229">Étape 8</span><span class="sxs-lookup"><span data-stu-id="e108e-229">Step 8</span></span>

<span data-ttu-id="e108e-230">Créez un paramètre de règle.</span><span class="sxs-lookup"><span data-stu-id="e108e-230">Create a rule setting.</span></span> <span data-ttu-id="e108e-231">Cette étape configure hello application passerelle toouse basée sur le chemin d’accès au routage d’URL.</span><span class="sxs-lookup"><span data-stu-id="e108e-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="e108e-232">Hello `$urlPathMap` variable définie dans hello étape antérieure est maintenant utilisé toocreate hello chemin d’accès règle.</span><span class="sxs-lookup"><span data-stu-id="e108e-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="e108e-233">Dans cette étape, nous associons règle de hello avec un écouteur et le mappage de chemin d’accès d’url hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e108e-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="e108e-234">Étape 9</span><span class="sxs-lookup"><span data-stu-id="e108e-234">Step 9</span></span>

<span data-ttu-id="e108e-235">Configurer le nombre de hello d’instances et de taille pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="e108e-236">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e108e-236">Create Application Gateway</span></span>

<span data-ttu-id="e108e-237">Créer une passerelle d’application avec tous les objets de configuration à partir de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="e108e-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e108e-238">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e108e-238">Get application gateway DNS name</span></span>

<span data-ttu-id="e108e-239">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="e108e-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="e108e-240">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="e108e-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e108e-241">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e108e-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="e108e-242">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e108e-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="e108e-243">tooconfigure hello frontal enregistrement CNAME d’IP, de récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="e108e-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="e108e-244">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="e108e-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="e108e-245">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="e108e-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e108e-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e108e-246">Next steps</span></span>

<span data-ttu-id="e108e-247">Si vous souhaitez toolearn décharger de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e108e-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

