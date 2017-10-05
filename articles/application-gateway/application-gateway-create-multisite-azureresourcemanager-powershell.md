---
title: "Créer une passerelle Application Gateway pour héberger plusieurs sites | Microsoft Docs"
description: "Cette page fournit des instructions pour créer, configurer une passerelle Application Gateway Azure pour l’hébergement de plusieurs applications web sur la même passerelle."
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
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="35964-103">Créer une passerelle Application Gateway pour l’hébergement de plusieurs applications web</span><span class="sxs-lookup"><span data-stu-id="35964-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35964-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="35964-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="35964-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35964-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="35964-106">L’hébergement de plusieurs sites vous permet de déployer plusieurs applications web sur la même passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="35964-107">Il s’appuie sur la présence de l’en-tête de l’hôte dans la requête HTTP entrante pour déterminer l’écouteur qui doit recevoir le trafic.</span><span class="sxs-lookup"><span data-stu-id="35964-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="35964-108">L’écouteur dirige ensuite le trafic vers le pool principal approprié tel que configuré dans la définition des règles de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="35964-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="35964-109">Dans les applications web SSL, la passerelle Application Gateway s’appuie sur l’extension d’indication du nom du serveur (SNI) pour choisir l’écouteur approprié au trafic web.</span><span class="sxs-lookup"><span data-stu-id="35964-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="35964-110">Une utilisation courante de l’hébergement de plusieurs sites consiste à équilibrer la charge des demandes pour différents domaines Web entre différents pools de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="35964-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="35964-111">De même, plusieurs sous-domaines du même domaine racine pourraient également être hébergés sur la même passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="35964-112">Scénario</span><span class="sxs-lookup"><span data-stu-id="35964-112">Scenario</span></span>

<span data-ttu-id="35964-113">Dans l’exemple suivant, la passerelle Application Gateway gère le trafic pour contoso.com et fabrikam.com avec deux pools de serveurs principaux : un pool de serveurs contoso et un pool de serveurs fabrikam.</span><span class="sxs-lookup"><span data-stu-id="35964-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="35964-114">Une configuration similaire pourrait servir à héberger des sous-domaines hôtes comme app.contoso.com et blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="35964-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="35964-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="35964-116">Before you begin</span></span>

1. <span data-ttu-id="35964-117">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="35964-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="35964-118">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="35964-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="35964-119">Les serveurs ajoutés au pool principal pour utiliser la passerelle Application Gateway doivent exister, ou vous devez créer leurs points de terminaison sur le réseau virtuel dans un autre sous-réseau ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="35964-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="35964-120">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="35964-120">Requirements</span></span>

* <span data-ttu-id="35964-121">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="35964-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="35964-122">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="35964-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="35964-123">Le nom de domaine complet peut également être utilisé.</span><span class="sxs-lookup"><span data-stu-id="35964-123">FQDN can also be used.</span></span>
* <span data-ttu-id="35964-124">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="35964-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="35964-125">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="35964-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="35964-126">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="35964-127">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="35964-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="35964-128">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="35964-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="35964-129">Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.</span><span class="sxs-lookup"><span data-stu-id="35964-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="35964-130">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux, et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="35964-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="35964-131">Les règles sont traitées dans l’ordre où elles sont répertoriées, et le trafic est orienté selon la première règle correspondante, quelle que soit sa spécificité.</span><span class="sxs-lookup"><span data-stu-id="35964-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="35964-132">Par exemple, si une règle utilise un écouteur de base et qu’une autre utilise un écouteur multisite sur le même port, la règle avec l’écouteur multisite doit être répertoriée avant la règle avec l’écouteur de base pour que la règle multisite fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="35964-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="35964-133">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35964-133">Create an application gateway</span></span>

<span data-ttu-id="35964-134">Procédez comme suit pour créer une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="35964-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="35964-135">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35964-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="35964-136">Créer un réseau virtuel, des sous-réseaux et une adresse IP publique pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="35964-137">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35964-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="35964-138">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="35964-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35964-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="35964-140">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35964-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="35964-141">Pour plus d’informations, voir l’article [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="35964-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="35964-142">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35964-142">Step 1</span></span>

<span data-ttu-id="35964-143">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="35964-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="35964-144">Vous êtes invité à vous authentifier à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="35964-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="35964-145">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="35964-145">Step 2</span></span>

<span data-ttu-id="35964-146">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="35964-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="35964-147">Étape 3</span><span class="sxs-lookup"><span data-stu-id="35964-147">Step 3</span></span>

<span data-ttu-id="35964-148">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="35964-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="35964-149">Étape 4</span><span class="sxs-lookup"><span data-stu-id="35964-149">Step 4</span></span>

<span data-ttu-id="35964-150">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="35964-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="35964-151">Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="35964-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="35964-152">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="35964-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="35964-153">Celui-ci est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="35964-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="35964-154">Assurez-vous que toutes les commandes pour la création d'une passerelle Application Gateway utiliseront le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="35964-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="35964-155">Dans l’exemple ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG** avec pour emplacement **États-Unis de l’Ouest**.</span><span class="sxs-lookup"><span data-stu-id="35964-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="35964-156">Si vous devez configurer une sonde personnalisée pour votre passerelle Application Gateway, consultez [Création d’une passerelle Application Gateway avec des sondes personnalisées à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35964-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="35964-157">Consultez les informations sur les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35964-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="35964-158">Créer un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="35964-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="35964-159">L’exemple ci-après indique comment créer un réseau virtuel à l’aide de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35964-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="35964-160">Deux sous-réseaux sont créés au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="35964-160">Two subnets are created in this step.</span></span> <span data-ttu-id="35964-161">Le premier sous-réseau est pour la passerelle Application Gateway elle-même.</span><span class="sxs-lookup"><span data-stu-id="35964-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="35964-162">La passerelle Application Gateway doit avoir son propre sous-réseau contenant ses instances.</span><span class="sxs-lookup"><span data-stu-id="35964-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="35964-163">Seules d’autres passerelles Application Gateway peuvent être déployées dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="35964-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="35964-164">Le deuxième sous-réseau est utilisé pour contenir les serveurs principaux d’applications.</span><span class="sxs-lookup"><span data-stu-id="35964-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="35964-165">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35964-165">Step 1</span></span>

<span data-ttu-id="35964-166">Attribuez la plage d’adresses 10.0.0.0/24 à la variable subnet à utiliser pour contenir la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="35964-167">Étape 2</span><span class="sxs-lookup"><span data-stu-id="35964-167">Step 2</span></span>

<span data-ttu-id="35964-168">Attribuez la plage d’adresses 10.0.1.0/24 à la variable subnet2 à utiliser pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="35964-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="35964-169">Étape 3</span><span class="sxs-lookup"><span data-stu-id="35964-169">Step 3</span></span>

<span data-ttu-id="35964-170">Créez un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appwrg** pour la région États-Unis de l’Ouest à l’aide du préfixe 10.0.0.0/16 avec les sous-réseaux 10.0.0.0/24 et 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="35964-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="35964-171">Étape 4</span><span class="sxs-lookup"><span data-stu-id="35964-171">Step 4</span></span>

<span data-ttu-id="35964-172">Attribuez une variable de sous-réseau pour les prochaines étapes, qui permet de créer une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="35964-173">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="35964-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="35964-174">Créez une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région « West US ».</span><span class="sxs-lookup"><span data-stu-id="35964-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="35964-175">Une adresse IP est affectée à la passerelle Application Gateway au démarrage du service.</span><span class="sxs-lookup"><span data-stu-id="35964-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="35964-176">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35964-176">Create application gateway configuration</span></span>

<span data-ttu-id="35964-177">Avant de créer la passerelle Application Gateway, vous devez installer tous les éléments de configuration.</span><span class="sxs-lookup"><span data-stu-id="35964-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="35964-178">Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="35964-179">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35964-179">Step 1</span></span>

<span data-ttu-id="35964-180">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="35964-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="35964-181">Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="35964-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="35964-182">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="35964-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="35964-183">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="35964-183">Step 2</span></span>

<span data-ttu-id="35964-184">Configurez les pools d’adresses IP principaux nommés **pool01** et **pool2** avec les adresses IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** pour **pool1** et **134.170.186.46**, **134.170.189.221** et **134.170.186.50** pour **pool2**.</span><span class="sxs-lookup"><span data-stu-id="35964-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="35964-185">Dans cet exemple, il existe deux pools principaux pour acheminer le trafic réseau selon le site demandé.</span><span class="sxs-lookup"><span data-stu-id="35964-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="35964-186">Un pool reçoit le trafic du site « contoso.com » et l’autre le trafic du site « fabrikam.com ».</span><span class="sxs-lookup"><span data-stu-id="35964-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="35964-187">Vous devez remplacer les adresses IP précédentes pour ajouter vos propres points de terminaison d’adresse IP d’application.</span><span class="sxs-lookup"><span data-stu-id="35964-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="35964-188">À la place des adresses IP internes, vous pouvez également utiliser des adresses IP publiques, un nom de domaine complet ou une carte réseau d’une machine virtuelle pour les instances de backend.</span><span class="sxs-lookup"><span data-stu-id="35964-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="35964-189">Utilisez le paramètre « -BackendFQDNs » pour spécifier les noms de domaine complets au lieu des adresses IP dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35964-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="35964-190">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="35964-190">Step 3</span></span>

<span data-ttu-id="35964-191">Configurez les paramètres de passerelle Application Gateway **poolsetting01** et **poolsetting02** pour le trafic réseau à charge équilibrée dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="35964-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="35964-192">Dans cet exemple, vous configurez différents paramètres pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="35964-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="35964-193">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="35964-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="35964-194">Étape 4</span><span class="sxs-lookup"><span data-stu-id="35964-194">Step 4</span></span>

<span data-ttu-id="35964-195">Configurez l’adresse IP frontale avec un point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="35964-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="35964-196">Étape 5</span><span class="sxs-lookup"><span data-stu-id="35964-196">Step 5</span></span>

<span data-ttu-id="35964-197">Configurez le port frontal pour une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="35964-198">Étape 6</span><span class="sxs-lookup"><span data-stu-id="35964-198">Step 6</span></span>

<span data-ttu-id="35964-199">Configurer deux certificats SSL pour les deux sites Web que nous allons traiter dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="35964-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="35964-200">Un certificat est pour le trafic de contoso.com et l’autre pour le trafic fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="35964-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="35964-201">Il doit s’agir de certificats émis par une autorité de certification pour vos sites Web.</span><span class="sxs-lookup"><span data-stu-id="35964-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="35964-202">Les certificats auto-signés sont pris en charge mais déconseillés pour le trafic de production.</span><span class="sxs-lookup"><span data-stu-id="35964-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="35964-203">Étape 7</span><span class="sxs-lookup"><span data-stu-id="35964-203">Step 7</span></span>

<span data-ttu-id="35964-204">Dans cet exemple, configurez deux écouteurs pour les deux sites Web.</span><span class="sxs-lookup"><span data-stu-id="35964-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="35964-205">Cette étape permet de configurer les écouteurs pour l’adresse IP publique, ainsi que le port et l’hôte utilisés pour recevoir le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="35964-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="35964-206">Le paramètre HostName est requis pour la prise en charge de plusieurs sites et doit être défini sur le site Web approprié pour lequel le trafic est reçu.</span><span class="sxs-lookup"><span data-stu-id="35964-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="35964-207">Le paramètre RequireServerNameIndication doit être défini sur true pour les sites web ayant besoin d’une prise en charge SSL dans un scénario à plusieurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="35964-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="35964-208">Si la prise en charge SSL est requise, vous devez également spécifier le certificat SSL utilisé pour sécuriser le trafic de cette application web.</span><span class="sxs-lookup"><span data-stu-id="35964-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="35964-209">L’association de FrontendIPConfiguration, FrontendPort et de HostName doit être unique pour un écouteur.</span><span class="sxs-lookup"><span data-stu-id="35964-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="35964-210">Chaque écouteur peut prendre en charge un seul certificat.</span><span class="sxs-lookup"><span data-stu-id="35964-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="35964-211">Étape 8</span><span class="sxs-lookup"><span data-stu-id="35964-211">Step 8</span></span>

<span data-ttu-id="35964-212">Dans cet exemple, créez deux paramètres de règle pour les deux applications web.</span><span class="sxs-lookup"><span data-stu-id="35964-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="35964-213">Une règle associe les écouteurs, les pools principaux et les paramètres http.</span><span class="sxs-lookup"><span data-stu-id="35964-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="35964-214">Cette étape configure la passerelle Application Gateway afin d’utiliser la règle de routage de base (une pour chaque site web).</span><span class="sxs-lookup"><span data-stu-id="35964-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="35964-215">Le trafic vers chaque site web est reçu par son écouteur configuré, puis dirigé vers son pool principal configuré, à l’aide des propriétés spécifiées dans BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="35964-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="35964-216">Étape 9</span><span class="sxs-lookup"><span data-stu-id="35964-216">Step 9</span></span>

<span data-ttu-id="35964-217">Configurez le nombre d’instances et taille de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="35964-218">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35964-218">Create application gateway</span></span>

<span data-ttu-id="35964-219">Créez une passerelle Application Gateway avec tous les objets de configuration à partir de la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="35964-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="35964-220">L’approvisionnement de la passerelle Application Gateway est une opération longue qui peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="35964-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="35964-221">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35964-221">Get application gateway DNS name</span></span>

<span data-ttu-id="35964-222">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="35964-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="35964-223">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="35964-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="35964-224">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="35964-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="35964-225">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35964-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="35964-226">Pour ce faire, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="35964-227">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="35964-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="35964-228">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35964-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="35964-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35964-229">Next steps</span></span>

<span data-ttu-id="35964-230">Découvrez comment protéger vos sites web grâce au [Pare-feu d’applications web sur Application Gateway](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="35964-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

