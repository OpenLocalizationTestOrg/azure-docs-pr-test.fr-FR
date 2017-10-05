---
title: "Créer une sonde personnalisée - Passerelle Azure Application Gateway - PowerShell | Microsoft Docs"
description: "Apprenez à créer une sonde personnalisée pour la passerelle Application Gateway à l'aide de PowerShell dans Resource Manager"
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
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="0f126-103">Création d'une sonde personnalisée pour Azure Application Gateway avec PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f126-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f126-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0f126-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="0f126-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f126-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="0f126-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f126-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="0f126-107">Dans cet article, une sonde personnalisée est ajoutée à une passerelle d’application existante à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f126-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="0f126-108">Les sondes personnalisées sont utiles pour les applications qui ont une page de contrôle d’intégrité spécifique ou pour les applications qui ne fournissent pas de réponse correcte dans l’application web par défaut.</span><span class="sxs-lookup"><span data-stu-id="0f126-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="0f126-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0f126-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0f126-110">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du [modèle de déploiement classique](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0f126-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="0f126-111">Créer une passerelle d’application avec une sonde personnalisée</span><span class="sxs-lookup"><span data-stu-id="0f126-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="0f126-112">Se connecter et créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0f126-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="0f126-113">Utilisez `Login-AzureRmAccount` pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f126-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="0f126-114">Obtenez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="0f126-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="0f126-115">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="0f126-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="0f126-116">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f126-116">Create a resource group.</span></span> <span data-ttu-id="0f126-117">Vous pouvez ignorer cette étape si vous disposez d’un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="0f126-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="0f126-118">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="0f126-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0f126-119">Celui-ci est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="0f126-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="0f126-120">Assurez-vous que toutes les commandes pour la création d'une passerelle Application Gateway utiliseront le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f126-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="0f126-121">Dans l’exemple précédent, nous avons créé un groupe de ressources appelé **appgw-RG** à l’emplacement **West US**.</span><span class="sxs-lookup"><span data-stu-id="0f126-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="0f126-122">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="0f126-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="0f126-123">L’exemple suivant crée un réseau virtuel et un sous-réseau pour la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="0f126-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="0f126-124">La passerelle d’application a besoin d’utiliser son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0f126-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="0f126-125">C’est pourquoi le sous-réseau créé pour la passerelle d’application doit être plus petit que l’espace d’adressage du réseau virtuel de façon à permettre la création et l’utilisation d’autres sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="0f126-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="0f126-126">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="0f126-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="0f126-127">Créez une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région « West US ».</span><span class="sxs-lookup"><span data-stu-id="0f126-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="0f126-128">Cet exemple utilise une adresse IP publique comme adresse IP frontale de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="0f126-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="0f126-129">Sachant que la passerelle d’application exige que l’adresse IP publique possède un nom DNS créé dynamiquement, `-DomainNameLabel` ne peut pas être spécifié pendant la création de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="0f126-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="0f126-130">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0f126-130">Create an application gateway</span></span>

<span data-ttu-id="0f126-131">Avant de créer la passerelle Application Gateway, vous devez installer tous les éléments de configuration.</span><span class="sxs-lookup"><span data-stu-id="0f126-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="0f126-132">L’exemple suivant crée les éléments de configuration nécessaires à une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="0f126-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="0f126-133">**Composant**</span><span class="sxs-lookup"><span data-stu-id="0f126-133">**Component**</span></span> | <span data-ttu-id="0f126-134">**Description**</span><span class="sxs-lookup"><span data-stu-id="0f126-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="0f126-135">**Configuration IP de la passerelle**</span><span class="sxs-lookup"><span data-stu-id="0f126-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="0f126-136">Configuration IP d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="0f126-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="0f126-137">**Pool back-end**</span><span class="sxs-lookup"><span data-stu-id="0f126-137">**Backend pool**</span></span> | <span data-ttu-id="0f126-138">Pool d’adresses IP, noms de domaine complets ou cartes d’interface réseau pour les serveurs d’applications qui hébergent l’application web.</span><span class="sxs-lookup"><span data-stu-id="0f126-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="0f126-139">**Sonde d’intégrité**</span><span class="sxs-lookup"><span data-stu-id="0f126-139">**Health probe**</span></span> | <span data-ttu-id="0f126-140">Sonde personnalisée utilisée pour surveiller l’état des membres du pool back-end.</span><span class="sxs-lookup"><span data-stu-id="0f126-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="0f126-141">**Paramètres HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f126-141">**HTTP settings**</span></span> | <span data-ttu-id="0f126-142">Collection de paramètres comprenant le port, le protocole, l’affinité basée sur les cookies, la sonde et le délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="0f126-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="0f126-143">Ces paramètres déterminent la façon dont le trafic est acheminé vers les membres du pool back-end.</span><span class="sxs-lookup"><span data-stu-id="0f126-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="0f126-144">**Port frontal**</span><span class="sxs-lookup"><span data-stu-id="0f126-144">**Frontend port**</span></span> | <span data-ttu-id="0f126-145">Port sur lequel la passerelle d’application écoute le trafic.</span><span class="sxs-lookup"><span data-stu-id="0f126-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="0f126-146">**Écouteur**</span><span class="sxs-lookup"><span data-stu-id="0f126-146">**Listener**</span></span> | <span data-ttu-id="0f126-147">Combinaison d’un protocole, d’une configuration d’adresses IP frontales et d’un port frontal.</span><span class="sxs-lookup"><span data-stu-id="0f126-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="0f126-148">C’est ce qui écoute les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="0f126-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="0f126-149">**Règle**</span><span class="sxs-lookup"><span data-stu-id="0f126-149">**Rule**</span></span>| <span data-ttu-id="0f126-150">Route le trafic vers le back-end approprié en fonction des paramètres HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f126-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="0f126-151">Ajouter une sonde à une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="0f126-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="0f126-152">L’extrait de code suivant ajoute une sonde à une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="0f126-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="0f126-153">Supprimer une sonde d’une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="0f126-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="0f126-154">L’extrait de code suivant supprime une sonde au niveau d’une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="0f126-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0f126-155">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0f126-155">Get application gateway DNS name</span></span>

<span data-ttu-id="0f126-156">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="0f126-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="0f126-157">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="0f126-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0f126-158">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle Application Gateway, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0f126-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="0f126-159">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f126-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="0f126-160">Pour ce faire, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0f126-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="0f126-161">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="0f126-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="0f126-162">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0f126-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0f126-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f126-163">Next steps</span></span>

<span data-ttu-id="0f126-164">Apprenez à configurer le déchargement SSL en consultant [Configurer le déchargement SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="0f126-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

