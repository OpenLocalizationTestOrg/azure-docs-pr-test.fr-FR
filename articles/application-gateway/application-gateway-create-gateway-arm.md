---
title: "Créer et gérer une Azure Application Gateway à l’aide de PowerShell | Microsoft Docs"
description: "Cette page fournit des instructions pour la création, la configuration, le démarrage et la suppression d’une passerelle Azure Application Gateway à l’aide d’Azure Resource Manager"
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
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="7b521-103">Créer, démarrer ou supprimer une passerelle Application Gateway à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b521-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b521-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="7b521-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="7b521-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b521-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="7b521-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b521-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="7b521-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b521-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="7b521-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7b521-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="7b521-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="7b521-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="7b521-110">Elle assure l’exécution des requêtes HTTP de basculement et de routage des performances entre des serveurs locaux ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="7b521-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="7b521-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc.</span><span class="sxs-lookup"><span data-stu-id="7b521-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="7b521-112">Pour obtenir une liste complète des fonctionnalités prises en charge, consultez [Vue d’ensemble d’Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="7b521-113">Cet article vous guide lors des étapes de création, de configuration, de démarrage et de suppression d’une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b521-114">Avant d’utiliser des ressources Azure, il est important de comprendre qu’Azure dispose actuellement de deux modèles de déploiement : Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="7b521-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="7b521-115">Attention à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="7b521-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="7b521-116">Pour consulter la documentation relative aux différents outils, cliquez sur les onglets situés en haut de cet article.</span><span class="sxs-lookup"><span data-stu-id="7b521-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="7b521-117">Ce document traite de la création d’une passerelle Application Gateway à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b521-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="7b521-118">Pour utiliser la version classique, accédez à [Création d’un déploiement classique de passerelle Application Gateway à l’aide de PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7b521-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7b521-119">Before you begin</span></span>

1. <span data-ttu-id="7b521-120">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="7b521-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="7b521-121">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7b521-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="7b521-122">Si vous disposez d’un réseau virtuel, sélectionnez un sous-réseau vide existant ou créez un sous-réseau de votre réseau virtuel existant uniquement pour une utilisation par la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="7b521-123">Vous ne pouvez pas déployer la passerelle d’application sur un autre réseau virtuel constitué par les ressources que vous avez l’intention de déployer derrière la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="7b521-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="7b521-124">Les serveurs que vous configurez pour utiliser la passerelle Application Gateway doivent exister ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="7b521-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="7b521-125">Quels sont les éléments nécessaires pour créer une passerelle Application Gateway ?</span><span class="sxs-lookup"><span data-stu-id="7b521-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="7b521-126">**Pool de serveurs principaux :** liste des adresses IP, noms de domaine complets ou cartes réseau des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="7b521-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="7b521-127">Si vous avez recours aux adresses IP, elles doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/adresse IP virtuelle publique.</span><span class="sxs-lookup"><span data-stu-id="7b521-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="7b521-128">**Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="7b521-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="7b521-129">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="7b521-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="7b521-130">**Port frontal :** il s’agit du port public ouvert sur Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="7b521-131">Le trafic atteint ce port, puis il est redirigé vers l'un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="7b521-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="7b521-132">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="7b521-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="7b521-133">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux et définit le pool de serveurs principaux vers lequel le trafic doit être dirigé lorsqu’il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="7b521-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="7b521-134">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b521-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="7b521-135">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b521-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="7b521-136">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="7b521-137">Connectez-vous à Azure et entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7b521-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="7b521-138">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="7b521-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="7b521-139">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="7b521-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="7b521-140">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="7b521-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="7b521-141">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="7b521-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7b521-142">Celui-ci est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="7b521-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="7b521-143">Assurez-vous que toutes les commandes pour la création d’une passerelle Application Gateway utilisent le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7b521-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="7b521-144">Dans l’exemple ci-dessus, nous avons créé un groupe de ressources appelé **ContosoRG** et un emplacement **Est des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="7b521-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="7b521-145">Si vous devez configurer une sonde personnalisée pour votre passerelle Application Gateway, consultez la page [Création d’une passerelle Application Gateway avec des sondes personnalisées à l’aide de PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="7b521-146">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="7b521-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="7b521-147">Créer les objets de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7b521-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="7b521-148">Tous les éléments de configuration doivent être installés avant de créer la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="7b521-149">Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="7b521-150">Une fois terminées, récupérez les informations relatives au DNS et à l’adresse IP virtuelle d’Application Gateway à partir de la ressource IP publique attachée à Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="7b521-151">Supprimer la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7b521-151">Delete the application gateway</span></span>

<span data-ttu-id="7b521-152">L’exemple suivant illustre comment supprimer Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="7b521-153">Il est possible d’utiliser le commutateur **-force** pour supprimer le message de confirmation de suppression.</span><span class="sxs-lookup"><span data-stu-id="7b521-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="7b521-154">Pour vérifier que le service a été supprimé, vous pouvez utiliser l’applet de commande `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="7b521-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="7b521-155">Cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="7b521-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="7b521-156">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="7b521-156">Get application gateway DNS name</span></span>

<span data-ttu-id="7b521-157">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="7b521-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="7b521-158">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="7b521-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="7b521-159">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="7b521-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="7b521-160">Pour ce faire, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="7b521-161">Cela est possible avec un DNS Azure ou d’autres fournisseurs de DNS, en créant un enregistrement CNAME qui pointe vers [l’adresse IP publique](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="7b521-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="7b521-162">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="7b521-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="7b521-163">Une adresse IP est affectée à la passerelle Application Gateway au démarrage du service.</span><span class="sxs-lookup"><span data-stu-id="7b521-163">An IP address is assigned to the application gateway when the service starts.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="7b521-164">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="7b521-164">Delete all resources</span></span>

<span data-ttu-id="7b521-165">Pour supprimer toutes les ressources créées dans cet article, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b521-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="7b521-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7b521-166">Next steps</span></span>

<span data-ttu-id="7b521-167">Si vous souhaitez configurer le déchargement SSL, consultez la page [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="7b521-168">Si vous voulez configurer une passerelle Application Gateway à utiliser avec l’équilibreur de charge interne, consultez la page [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="7b521-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="7b521-169">Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :</span><span class="sxs-lookup"><span data-stu-id="7b521-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="7b521-170">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="7b521-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="7b521-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="7b521-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
