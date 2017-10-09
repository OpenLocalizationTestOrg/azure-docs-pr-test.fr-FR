---
title: "une passerelle d’application pour l’hébergement de plusieurs sites d’aaaCreate | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure pour héberger plusieurs applications web sur hello même passerelle."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="9931f-103">Créer une passerelle Application Gateway pour l’hébergement de plusieurs applications web</span><span class="sxs-lookup"><span data-stu-id="9931f-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9931f-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="9931f-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="9931f-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9931f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="9931f-106">Hébergement de plusieurs sites vous permet de toodeploy plus d’une application web sur hello même passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="9931f-107">Il s’appuie sur la présence de l’en-tête d’hôte dans la requête HTTP entrante hello, toodetermine quels écouteur reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="9931f-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="9931f-108">écouteur de Hello dirige ensuite pool principal de tooappropriate trafic tel que configuré dans la définition des règles de passerelle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="9931f-109">Dans les applications web SSL est activé, passerelle d’application s’appuie sur hello Indication de nom de serveur (SNI) extension toochoose hello correct écouteur pour le trafic web hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="9931f-110">Une utilisation courante pour l’hébergement de plusieurs sites est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent web différents domaines.</span><span class="sxs-lookup"><span data-stu-id="9931f-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="9931f-111">De même, plusieurs sous-domaines de hello même domaine racine peut également être hébergé sur hello même passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="9931f-112">Scénario</span><span class="sxs-lookup"><span data-stu-id="9931f-112">Scenario</span></span>

<span data-ttu-id="9931f-113">Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com avec deux pools de serveur principal : contoso pool de serveurs et de pool de serveurs de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="9931f-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="9931f-114">Le programme d’installation similaire peut être sous-domaines toohost utilisés comme app.contoso.com et blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9931f-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="9931f-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9931f-116">Before you begin</span></span>

1. <span data-ttu-id="9931f-117">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="9931f-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9931f-118">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9931f-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9931f-119">les serveurs Hello ajouté passerelle d’application hello toohello principal pool toouse doit exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello dans un sous-réseau distinct ou avec une adresse IP publique/VIP attribué.</span><span class="sxs-lookup"><span data-stu-id="9931f-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="9931f-120">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="9931f-120">Requirements</span></span>

* <span data-ttu-id="9931f-121">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="9931f-122">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="9931f-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="9931f-123">Le nom de domaine complet peut également être utilisé.</span><span class="sxs-lookup"><span data-stu-id="9931f-123">FQDN can also be used.</span></span>
* <span data-ttu-id="9931f-124">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="9931f-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9931f-125">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9931f-126">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9931f-127">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="9931f-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9931f-128">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="9931f-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="9931f-129">Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.</span><span class="sxs-lookup"><span data-stu-id="9931f-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="9931f-130">**La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="9931f-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="9931f-131">Les règles sont traitées dans l’ordre de hello qu’ils sont répertoriés, et le trafic est dirigé via hello première règle qui correspond, quelle que soit la spécificité.</span><span class="sxs-lookup"><span data-stu-id="9931f-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="9931f-132">Par exemple, si vous disposez d’une règle à l’aide d’un écouteur de base et une règle à l’aide d’un écouteur de plusieurs site à la fois sur hello même règle de port, hello avec écouteur de plusieurs sites hello doit figurer avant les règle hello qu’un écouteur de base hello dans l’ordre pour toofunction de règle de plusieurs sites hello en tant que attendu.</span><span class="sxs-lookup"><span data-stu-id="9931f-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="9931f-133">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9931f-133">Create an application gateway</span></span>

<span data-ttu-id="9931f-134">Hello Voici les étapes de hello nécessaires toocreate une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="9931f-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="9931f-135">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9931f-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="9931f-136">Créer un réseau virtuel, des sous-réseaux et adresse IP publique pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="9931f-137">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9931f-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="9931f-138">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9931f-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9931f-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9931f-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9931f-140">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9931f-141">Pour plus d’informations, voir l’article [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9931f-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9931f-142">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9931f-142">Step 1</span></span>

<span data-ttu-id="9931f-143">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="9931f-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="9931f-144">Vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9931f-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="9931f-145">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9931f-145">Step 2</span></span>

<span data-ttu-id="9931f-146">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="9931f-147">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9931f-147">Step 3</span></span>

<span data-ttu-id="9931f-148">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9931f-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="9931f-149">Étape 4</span><span class="sxs-lookup"><span data-stu-id="9931f-149">Step 4</span></span>

<span data-ttu-id="9931f-150">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="9931f-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="9931f-151">Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="9931f-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="9931f-152">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="9931f-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9931f-153">Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9931f-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9931f-154">Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9931f-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="9931f-155">Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG** avec un emplacement de **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="9931f-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="9931f-156">Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9931f-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="9931f-157">Consultez les informations sur les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9931f-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="9931f-158">Créer un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="9931f-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="9931f-159">Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="9931f-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="9931f-160">Deux sous-réseaux sont créés au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="9931f-160">Two subnets are created in this step.</span></span> <span data-ttu-id="9931f-161">sous-réseau de première Hello est pour la passerelle d’application hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="9931f-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="9931f-162">Passerelle d’application nécessite son propre toohold sous-réseau ses instances.</span><span class="sxs-lookup"><span data-stu-id="9931f-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="9931f-163">Seules d’autres passerelles Application Gateway peuvent être déployées dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9931f-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="9931f-164">sous-réseau de deuxième Hello est utilisé toohold hello application back-end serveurs.</span><span class="sxs-lookup"><span data-stu-id="9931f-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="9931f-165">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9931f-165">Step 1</span></span>

<span data-ttu-id="9931f-166">Assigner hello adresse plage 10.0.0.0/24 toohello sous-réseau toobe variable toohold utilisé hello application passerelle.</span><span class="sxs-lookup"><span data-stu-id="9931f-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="9931f-167">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9931f-167">Step 2</span></span>

<span data-ttu-id="9931f-168">Affecter hello adresse plage 10.0.1.0/24 toohello subnet2 variable toobe les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="9931f-169">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9931f-169">Step 3</span></span>

<span data-ttu-id="9931f-170">Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello avec le sous-réseau 10.0.0.0/24, à l’aide de hello préfixe 10.0.0.0/16 et 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="9931f-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="9931f-171">Étape 4</span><span class="sxs-lookup"><span data-stu-id="9931f-171">Step 4</span></span>

<span data-ttu-id="9931f-172">Attribuer une variable de sous-réseau pour les étapes suivantes de hello, qui crée une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="9931f-173">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="9931f-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="9931f-174">Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9931f-175">Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="9931f-176">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9931f-176">Create application gateway configuration</span></span>

<span data-ttu-id="9931f-177">Vous avez tooset tous les éléments de configuration avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="9931f-178">Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9931f-179">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9931f-179">Step 1</span></span>

<span data-ttu-id="9931f-180">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="9931f-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9931f-181">Au démarrage de la passerelle d’application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="9931f-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9931f-182">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="9931f-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="9931f-183">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9931f-183">Step 2</span></span>

<span data-ttu-id="9931f-184">Configurer le pool d’adresses IP principal hello nommé **pool01** et **pool2** avec des adresses IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** pour **pool1** et **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  pour **pool2**.</span><span class="sxs-lookup"><span data-stu-id="9931f-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="9931f-185">Dans cet exemple, il existe deux principaux pools tooroute le trafic réseau selon le site demandé de hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="9931f-186">Un pool reçoit le trafic du site « contoso.com » et l’autre le trafic du site « fabrikam.com ».</span><span class="sxs-lookup"><span data-stu-id="9931f-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="9931f-187">Vous avez hello tooreplace précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.</span><span class="sxs-lookup"><span data-stu-id="9931f-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="9931f-188">À la place des adresses IP internes, vous pouvez également utiliser des adresses IP publiques, un nom de domaine complet ou une carte réseau d’une machine virtuelle pour les instances de backend.</span><span class="sxs-lookup"><span data-stu-id="9931f-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="9931f-189">toospecify noms de domaine complets au lieu d’adresses IP dans PowerShell, utilisez «-BackendFQDNs » paramètre.</span><span class="sxs-lookup"><span data-stu-id="9931f-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="9931f-190">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9931f-190">Step 3</span></span>

<span data-ttu-id="9931f-191">Configurer le paramètre de passerelle d’application **poolsetting01** et **poolsetting02** hello équilibrés en charge le trafic réseau dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="9931f-192">Dans cet exemple, vous configurez les paramètres de pool principal différent pour les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="9931f-193">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="9931f-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="9931f-194">Étape 4</span><span class="sxs-lookup"><span data-stu-id="9931f-194">Step 4</span></span>

<span data-ttu-id="9931f-195">Configuration IP frontale de hello avec le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="9931f-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="9931f-196">Étape 5</span><span class="sxs-lookup"><span data-stu-id="9931f-196">Step 5</span></span>

<span data-ttu-id="9931f-197">Configurer le port frontal de hello pour une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="9931f-198">Étape 6</span><span class="sxs-lookup"><span data-stu-id="9931f-198">Step 6</span></span>

<span data-ttu-id="9931f-199">Configurer les deux certificats SSL pour les sites Web de hello deux, nous allons toosupport dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9931f-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="9931f-200">Un seul certificat pour le trafic de contoso.com et hello autres est pour le trafic fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="9931f-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="9931f-201">Il doit s’agir de certificats émis par une autorité de certification pour vos sites Web.</span><span class="sxs-lookup"><span data-stu-id="9931f-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="9931f-202">Les certificats auto-signés sont pris en charge mais déconseillés pour le trafic de production.</span><span class="sxs-lookup"><span data-stu-id="9931f-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="9931f-203">Étape 7</span><span class="sxs-lookup"><span data-stu-id="9931f-203">Step 7</span></span>

<span data-ttu-id="9931f-204">Configurez les deux écouteurs pour les deux sites web de hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9931f-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="9931f-205">Cette étape configure les écouteurs hello pour public hôte, port et adresse IP utilisé tooreceive du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="9931f-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="9931f-206">Paramètre de nom d’hôte est requis pour la prise en charge de plusieurs sites et doit être ensemble toohello site Web approprié pour le hello le trafic est reçu.</span><span class="sxs-lookup"><span data-stu-id="9931f-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="9931f-207">RequireServerNameIndication paramètre doit être défini tootrue pour les sites Web à prendre en charge pour le protocole SSL dans un scénario à plusieurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="9931f-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="9931f-208">Si la prise en charge SSL est requis, vous devez également toospecify hello SSL certificat trafic toosecure utilisé pour cette application web.</span><span class="sxs-lookup"><span data-stu-id="9931f-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="9931f-209">combinaison de Hello de configuration IP frontale, port du serveur frontal et de nom d’hôte doit être unique tooa écouteur.</span><span class="sxs-lookup"><span data-stu-id="9931f-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="9931f-210">Chaque écouteur peut prendre en charge un seul certificat.</span><span class="sxs-lookup"><span data-stu-id="9931f-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="9931f-211">Étape 8</span><span class="sxs-lookup"><span data-stu-id="9931f-211">Step 8</span></span>

<span data-ttu-id="9931f-212">Créez deux règle définissant deux applications web pour hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9931f-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="9931f-213">Une règle associe les écouteurs, les pools principaux et les paramètres http.</span><span class="sxs-lookup"><span data-stu-id="9931f-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="9931f-214">Cette étape configure hello application passerelle toouse base règle de routage, un pour chaque site Web.</span><span class="sxs-lookup"><span data-stu-id="9931f-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="9931f-215">Site Web de tooeach le trafic est reçu par son écouteur configuré et est ensuite dirigé de tooits configuré pool principal, à l’aide des propriétés hello spécifiées dans hello serveur principal s’élève.</span><span class="sxs-lookup"><span data-stu-id="9931f-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="9931f-216">Étape 9</span><span class="sxs-lookup"><span data-stu-id="9931f-216">Step 9</span></span>

<span data-ttu-id="9931f-217">Configurer le nombre de hello d’instances et de taille pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="9931f-218">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9931f-218">Create application gateway</span></span>

<span data-ttu-id="9931f-219">Créer une passerelle d’application avec tous les objets de configuration à partir de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="9931f-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="9931f-220">Approvisionnement de passerelle d’application est une opération longue et peut prendre quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="9931f-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9931f-221">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9931f-221">Get application gateway DNS name</span></span>

<span data-ttu-id="9931f-222">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="9931f-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9931f-223">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="9931f-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9931f-224">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9931f-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="9931f-225">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9931f-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9931f-226">toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="9931f-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="9931f-227">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="9931f-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="9931f-228">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="9931f-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9931f-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9931f-229">Next steps</span></span>

<span data-ttu-id="9931f-230">Découvrez comment tooprotect vos sites Web avec [passerelle d’Application - pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9931f-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

