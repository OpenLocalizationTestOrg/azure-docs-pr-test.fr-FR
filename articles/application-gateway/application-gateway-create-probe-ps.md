---
title: "aaaCreate personnalisé sonde - passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate personnalisé sondage pour la passerelle d’Application à l’aide de PowerShell dans le Gestionnaire de ressources"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="f8f1d-103">Création d'une sonde personnalisée pour Azure Application Gateway avec PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8f1d-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8f1d-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f8f1d-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="f8f1d-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8f1d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="f8f1d-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8f1d-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="f8f1d-107">Dans cet article, vous ajoutez une passerelle existante d’application sonde personnalisée tooan avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="f8f1d-108">Les sondes personnalisés sont utiles pour les applications qui ont une page de vérification d’intégrité spécifique ou pour les applications qui ne fournissent pas une réponse correcte sur l’application web de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="f8f1d-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f8f1d-110">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="f8f1d-111">Créer une passerelle d’application avec une sonde personnalisée</span><span class="sxs-lookup"><span data-stu-id="f8f1d-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="f8f1d-112">Se connecter et créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f8f1d-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="f8f1d-113">Utilisez `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="f8f1d-114">Obtient les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="f8f1d-115">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="f8f1d-116">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-116">Create a resource group.</span></span> <span data-ttu-id="f8f1d-117">Vous pouvez ignorer cette étape si vous disposez d’un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="f8f1d-118">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f8f1d-119">Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="f8f1d-120">Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="f8f1d-121">Bonjour précédent exemple, nous avons créé un groupe de ressources appelé **appgw-RG** dans emplacement **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="f8f1d-122">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="f8f1d-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="f8f1d-123">Hello exemple suivant crée un réseau virtuel et un sous-réseau pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="f8f1d-124">La passerelle d’application a besoin d’utiliser son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="f8f1d-125">Pour cette raison, sous-réseau hello créé pour la passerelle d’application hello doit être inférieure à l’espace d’adressage hello de tooallow de réseau virtuel hello pour les autres toobe sous-réseaux créés et utilisés.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="f8f1d-126">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="f8f1d-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="f8f1d-127">Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="f8f1d-128">Cet exemple utilise une adresse IP publique pour les adresses IP frontales hello de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="f8f1d-129">Passerelle d’application nécessite hello publique IP adresse toohave un nom DNS créé dynamiquement par conséquent hello `-DomainNameLabel` ne peut pas être spécifié lors de la création de hello d’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="f8f1d-130">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f8f1d-130">Create an application gateway</span></span>

<span data-ttu-id="f8f1d-131">Pour configurer tous les éléments de configuration avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="f8f1d-132">Hello exemple suivant crée hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="f8f1d-133">**Composant**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-133">**Component**</span></span> | <span data-ttu-id="f8f1d-134">**Description**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="f8f1d-135">**Configuration IP de la passerelle**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="f8f1d-136">Configuration IP d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="f8f1d-137">**Pool back-end**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-137">**Backend pool**</span></span> | <span data-ttu-id="f8f1d-138">Un pool d’adresses IP, du nom de domaine complet ou aux cartes réseau qui sont des serveurs d’applications toohello hello web application hôte</span><span class="sxs-lookup"><span data-stu-id="f8f1d-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="f8f1d-139">**Sonde d’intégrité**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-139">**Health probe**</span></span> | <span data-ttu-id="f8f1d-140">Une sonde personnalisée utilisée intégrité hello toomonitor membres du pool principal hello</span><span class="sxs-lookup"><span data-stu-id="f8f1d-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="f8f1d-141">**Paramètres HTTP**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-141">**HTTP settings**</span></span> | <span data-ttu-id="f8f1d-142">Collection de paramètres comprenant le port, le protocole, l’affinité basée sur les cookies, la sonde et le délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="f8f1d-143">Ces paramètres déterminent la façon dont le trafic est routé toohello les membres du pool principal</span><span class="sxs-lookup"><span data-stu-id="f8f1d-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="f8f1d-144">**Port frontal**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-144">**Frontend port**</span></span> | <span data-ttu-id="f8f1d-145">port Hello hello passerelle d’application écoute le trafic sur</span><span class="sxs-lookup"><span data-stu-id="f8f1d-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="f8f1d-146">**Écouteur**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-146">**Listener**</span></span> | <span data-ttu-id="f8f1d-147">Combinaison d’un protocole, d’une configuration d’adresses IP frontales et d’un port frontal.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="f8f1d-148">C’est ce qui écoute les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="f8f1d-149">**Règle**</span><span class="sxs-lookup"><span data-stu-id="f8f1d-149">**Rule**</span></span>| <span data-ttu-id="f8f1d-150">Itinéraires hello trafic toohello approprié back-end basé sur les paramètres HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="f8f1d-151">Ajouter une passerelle d’application existant sonde tooan</span><span class="sxs-lookup"><span data-stu-id="f8f1d-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="f8f1d-152">Hello extrait de code suivant ajoute une passerelle d’application sonde tooan existant.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="f8f1d-153">Supprimer une sonde d’une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="f8f1d-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="f8f1d-154">Hello suivant extrait de code supprime une sonde d’une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f8f1d-155">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f8f1d-155">Get application gateway DNS name</span></span>

<span data-ttu-id="f8f1d-156">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f8f1d-157">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f8f1d-158">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello un enregistrement CNAME peut être utilisé toopoint toohello public point de terminaison de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f8f1d-159">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f8f1d-160">toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f8f1d-161">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f8f1d-162">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f8f1d-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8f1d-163">Next steps</span></span>

<span data-ttu-id="f8f1d-164">En savoir tooconfigure le déchargement SSL en vous rendant sur : [configurer le déchargement SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="f8f1d-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

