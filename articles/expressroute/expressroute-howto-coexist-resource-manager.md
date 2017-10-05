---
title: "Configuration de connexions ExpressRoute et VPN de site à site pouvant coexister : Resource Manager :Azure | Microsoft Docs"
description: "Cet article vous guide tout au long de la configuration d’une connexion ExpressRoute et d’une connexion VPN de site à site pouvant coexister pour le modèle de déploiement Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="e0ece-103">Configurer la coexistence de connexions de site à site et ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0ece-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0ece-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e0ece-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="e0ece-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="e0ece-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="e0ece-106">La configuration de connexions VPN de site à site et ExpressRoute coexistantes possède plusieurs avantages.</span><span class="sxs-lookup"><span data-stu-id="e0ece-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="e0ece-107">Vous pouvez configurer un VPN de site à site comme un chemin de basculement sécurisé pour ExpressRoute, ou utiliser des VPN de site à site pour vous connecter à des sites qui ne sont pas connectés via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="e0ece-108">Dans cet article, nous décrirons les étapes de configuration de ces deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="e0ece-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="e0ece-109">Cet article concerne le modèle de déploiement Resource Manager et utilise PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0ece-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="e0ece-110">Cette configuration n'est pas disponible dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ece-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0ece-111">Les circuits ExpressRoute doivent être préconfigurés avant que vous suiviez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e0ece-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="e0ece-112">Avant de suivre les étapes ci-dessous, assurez-vous que vous avez suivi les guides pour [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [configurer le routage](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="e0ece-113">Limites et limitations</span><span class="sxs-lookup"><span data-stu-id="e0ece-113">Limits and limitations</span></span>
* <span data-ttu-id="e0ece-114">**Le routage de transit n’est pas pris en charge.**</span><span class="sxs-lookup"><span data-stu-id="e0ece-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="e0ece-115">Vous ne pouvez effectuer de routage (via Azure) entre votre réseau local connecté via le réseau VPN de site à site et votre réseau local connecté via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="e0ece-116">**La passerelle de référence de base n’est pas prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="e0ece-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="e0ece-117">Vous devez utiliser une passerelle de référence SKU autre que De base pour la [passerelle ExpressRoute](expressroute-about-virtual-network-gateways.md) et la [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="e0ece-118">**Seule la passerelle VPN basée sur un itinéraire est prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="e0ece-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="e0ece-119">Vous devez utiliser une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="e0ece-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="e0ece-120">L’**itinéraire statique doit être configuré pour votre passerelle VPN.**</span><span class="sxs-lookup"><span data-stu-id="e0ece-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="e0ece-121">Si votre réseau local est connecté à la fois à ExpressRoute et à un VPN de site à site, vous devez avoir configuré un itinéraire statique sur votre réseau local pour acheminer la connexion VPN de site à site vers l’Internet public.</span><span class="sxs-lookup"><span data-stu-id="e0ece-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="e0ece-122">La **passerelle ExpressRoute doit être configurée en premier et liée à un circuit.**</span><span class="sxs-lookup"><span data-stu-id="e0ece-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="e0ece-123">Vous devez commencer par créer la passerelle ExpressRoute et la lier à un circuit avant d’ajouter la passerelle VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="e0ece-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="e0ece-124">Modèles de configuration</span><span class="sxs-lookup"><span data-stu-id="e0ece-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="e0ece-125">Configurer un réseau VPN de site à site comme un chemin d’accès de basculement pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0ece-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="e0ece-126">Vous pouvez configurer une connexion VPN de site à site en tant que sauvegarde pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="e0ece-127">Cela s’applique uniquement aux réseaux virtuels liés au chemin d’homologation privé Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ece-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="e0ece-128">Il n’existe aucune solution de basculement basée sur des réseaux VPN pour les services accessibles via les homologations Azure public et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0ece-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="e0ece-129">Le circuit ExpressRoute est toujours le lien principal.</span><span class="sxs-lookup"><span data-stu-id="e0ece-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="e0ece-130">Si le circuit ExpressRoute échoue, les données circulent via le chemin du réseau VPN de site à site uniquement.</span><span class="sxs-lookup"><span data-stu-id="e0ece-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="e0ece-131">Bien que le circuit ExpressRoute soit préférable au réseau VPN de site à site lorsque les deux itinéraires sont identiques, Azure utilise la correspondance de préfixe la plus longue pour choisir l’itinéraire vers la destination du paquet.</span><span class="sxs-lookup"><span data-stu-id="e0ece-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="e0ece-133">Configurer un réseau VPN de site à site pour se connecter à des sites non connectés via ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0ece-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="e0ece-134">Vous pouvez configurer votre réseau là où certains sites se connectent directement à Azure via des réseaux VPN de site à site ou via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="e0ece-136">Vous ne pouvez pas configurer un réseau virtuel comme un routeur de transit.</span><span class="sxs-lookup"><span data-stu-id="e0ece-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="e0ece-137">Sélection des étapes à suivre</span><span class="sxs-lookup"><span data-stu-id="e0ece-137">Selecting the steps to use</span></span>
<span data-ttu-id="e0ece-138">Vous avez le choix entre deux ensembles de procédures.</span><span class="sxs-lookup"><span data-stu-id="e0ece-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="e0ece-139">La procédure de configuration que vous sélectionnez varie selon que vous disposez déjà d’un réseau virtuel auquel vous connecter ou que vous voulez créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0ece-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="e0ece-140">Je n’ai pas de réseau virtuel et dois en créer un</span><span class="sxs-lookup"><span data-stu-id="e0ece-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="e0ece-141">Cette procédure vous guide dans la création d’un réseau virtuel si vous n’en possédez pas encore un. Elle vous demande d’utiliser le modèle de déploiement Resource Manager et de créer de nouvelles connexions ExpressRoute et VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="e0ece-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="e0ece-142">Pour configurer un réseau virtuel, suivez les étapes décrites dans la section [Créer un réseau virtuel et des connexions qui coexistent](#new).</span><span class="sxs-lookup"><span data-stu-id="e0ece-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="e0ece-143">J’ai déjà un réseau virtuel répondant au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0ece-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="e0ece-144">Vous disposez peut-être déjà d’un réseau virtuel avec une connexion VPN de site à site existante ou une connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="e0ece-145">La section [Configurer des connexions qui coexistent pour un réseau virtuel existant](#add) vous guide tout au long des étapes de suppression de la passerelle puis de création de connexions ExpressRoute et VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="e0ece-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="e0ece-146">Attention au moment de créer les connexions. Notez que vous devez effectuer les étapes dans un ordre bien précis.</span><span class="sxs-lookup"><span data-stu-id="e0ece-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="e0ece-147">N’utilisez pas les instructions contenues dans d’autres articles pour créer des connexions et des passerelles.</span><span class="sxs-lookup"><span data-stu-id="e0ece-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="e0ece-148">Dans le cadre de cette procédure, si vous créez des connexions pouvant coexister, vous devez supprimer votre passerelle, puis configurer de nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="e0ece-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="e0ece-149">Lorsque vous supprimez et recréez la passerelle et les connexions, vous constatez un temps d’arrêt pour vos connexions entre les différents locaux. Toutefois, vous n’avez pas besoin de migrer les machines virtuelles ni les services vers un nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0ece-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="e0ece-150">Les machines virtuelles et les services sont toujours en mesure de communiquer via l’équilibreur de charge lorsque vous configurez votre passerelle s’ils sont configurés pour ce faire.</span><span class="sxs-lookup"><span data-stu-id="e0ece-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="e0ece-151"><a name="new"></a>Créer un réseau virtuel et des connexions qui coexistent</span><span class="sxs-lookup"><span data-stu-id="e0ece-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="e0ece-152">Cette procédure vous guide dans la création d’un réseau virtuel et de connexions de site à site et ExpressRoute appelées à coexister.</span><span class="sxs-lookup"><span data-stu-id="e0ece-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="e0ece-153">Installez la version la plus récente des cmdlets PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0ece-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e0ece-154">Pour plus d’informations sur l’installation de ces cmdlets, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0ece-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="e0ece-155">Les cmdlets que vous utilisez pour cette configuration peuvent être légèrement différentes de celles que vous connaissez.</span><span class="sxs-lookup"><span data-stu-id="e0ece-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="e0ece-156">Utilisez les applets de commande spécifiées dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="e0ece-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="e0ece-157">Connectez-vous à votre compte et configurez l’environnement.</span><span class="sxs-lookup"><span data-stu-id="e0ece-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="e0ece-158">Créez un réseau virtuel et un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e0ece-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="e0ece-159">Pour plus d’informations sur la configuration d'un réseau virtuel, consultez la rubrique [Configuration du réseau virtuel Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e0ece-160">Le sous-réseau de la passerelle doit être défini sur /27 ou un préfixe plus court (comme /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="e0ece-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="e0ece-161">Créez un nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0ece-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="e0ece-162">Ajoutez des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="e0ece-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="e0ece-163">Enregistrez la configuration du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0ece-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="e0ece-164"><a name="gw"></a>Créez une passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="e0ece-165">Pour plus d'informations sur la configuration de la passerelle ExpressRoute, consultez la rubrique [Configuration de la passerelle ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="e0ece-166">La valeur de GatewaySKU doit être *Standard*, *HighPerformance*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="e0ece-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="e0ece-167">Liez la passerelle ExpressRoute au circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="e0ece-168">Une fois cette étape terminée, la connexion entre votre réseau local et Azure est établie via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0ece-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="e0ece-169">Pour plus d'informations sur l'opération de liaison, voir l'article [Liaison de réseaux virtuels à ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="e0ece-170"><a name="vpngw"></a>Créez ensuite la passerelle VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="e0ece-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="e0ece-171">Pour plus d’informations sur la configuration de la passerelle VPN, consultez la rubrique [Configuration d’un réseau virtuel avec une connexion de site à site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="e0ece-172">La valeur de GatewaySKU doit être *Standard*, *HighPerformance*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="e0ece-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="e0ece-173">La valeur VpnType doit être *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="e0ece-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="e0ece-174">La passerelle VPN Azure prend en charge le protocole de routage BGP.</span><span class="sxs-lookup"><span data-stu-id="e0ece-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="e0ece-175">Vous pouvez spécifier le numéro ASN (numéro AS) pour ce réseau virtuel en ajoutant le commutateur -Asn dans la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="e0ece-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="e0ece-176">Si vous ne spécifiez pas ce paramètre, la valeur par défaut sera le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="e0ece-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="e0ece-177">Vous pouvez trouver l’IP d’homologation BGP et le numéro AS qu’Azure utilise pour la passerelle VPN dans $azureVpn.BgpSettings.BgpPeeringAddress et $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="e0ece-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="e0ece-178">Pour plus d’informations, consultez [Configurer BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) pour la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ece-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="e0ece-179">Créez une entité de passerelle VPN de site local.</span><span class="sxs-lookup"><span data-stu-id="e0ece-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="e0ece-180">Cette commande ne configure pas votre passerelle VPN locale.</span><span class="sxs-lookup"><span data-stu-id="e0ece-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="e0ece-181">Elle vous permet d’indiquer les paramètres de la passerelle locale, par exemple l’adresse IP publique et l’espace d’adressage local afin que la passerelle VPN Azure puisse s’y connecter.</span><span class="sxs-lookup"><span data-stu-id="e0ece-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="e0ece-182">Si votre périphérique VPN local prend uniquement en charge le routage statique, vous pouvez configurer des itinéraires statiques de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="e0ece-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="e0ece-183">Si votre périphérique VPN local prend en charge le protocole BGP et que vous souhaitez activer le routage dynamique, vous devez connaître l’IP d’homologation BGP et le numéro AS utilisé par votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="e0ece-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="e0ece-184">Configurez votre périphérique VPN local à connecter à la nouvelle passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ece-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="e0ece-185">Pour plus d’informations sur la configuration du périphérique VPN, consultez la rubrique [Configuration de périphérique VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="e0ece-186">Liez la passerelle VPN de site à site dans Azure à la passerelle locale.</span><span class="sxs-lookup"><span data-stu-id="e0ece-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="e0ece-187"><a name="add"></a>Pour configurer des connexions coexistantes pour un réseau virtuel existant</span><span class="sxs-lookup"><span data-stu-id="e0ece-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="e0ece-188">Si vous disposez déjà d’un réseau virtuel, vérifiez la taille du sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e0ece-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="e0ece-189">Si le sous-réseau de passerelle est /28 ou /29, vous devez tout d’abord supprimer la passerelle de réseau virtuel et augmenter la taille du sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e0ece-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="e0ece-190">Les étapes décrites dans cette section vous indiquent la marche à suivre.</span><span class="sxs-lookup"><span data-stu-id="e0ece-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="e0ece-191">Si le sous-réseau de passerelle est défini sur/27 ou plus et si le réseau virtuel est connecté via ExpressRoute, vous pouvez ignorer les étapes ci-dessous et passer à [« Étape 6 : créer une passerelle VPN de site à site »](#vpngw) dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="e0ece-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0ece-192">Lorsque vous supprimez la passerelle existante, votre site local perdra la connexion à votre réseau virtuel lorsque vous effectuerez cette configuration.</span><span class="sxs-lookup"><span data-stu-id="e0ece-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="e0ece-193">Vous aurez besoin d’installer la dernière version des applets de commande PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ece-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e0ece-194">Pour plus d’informations sur l’installation des cmdlets, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0ece-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="e0ece-195">Les cmdlets que vous utilisez pour cette configuration peuvent être légèrement différentes de celles que vous connaissez.</span><span class="sxs-lookup"><span data-stu-id="e0ece-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="e0ece-196">Utilisez les applets de commande spécifiées dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="e0ece-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="e0ece-197">Supprimez la passerelle VPN ExpressRoute ou de site à site existante.</span><span class="sxs-lookup"><span data-stu-id="e0ece-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="e0ece-198">Supprimez le sous-réseau de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="e0ece-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="e0ece-199">Ajoutez un sous-réseau de passerelle défini sur /27 ou plus.</span><span class="sxs-lookup"><span data-stu-id="e0ece-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e0ece-200">S’il ne vous reste pas suffisamment d’adresses IP dans votre réseau virtuel pour augmenter la taille du sous-réseau de passerelle, vous devez augmenter l’espace d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="e0ece-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="e0ece-201">Enregistrez la configuration du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0ece-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="e0ece-202">À ce stade, vous disposez d’un réseau virtuel sans passerelle.</span><span class="sxs-lookup"><span data-stu-id="e0ece-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="e0ece-203">Pour créer de nouvelles passerelles et finaliser vos connexions, vous pouvez passer à l’ [Étape 4 : Créer une passerelle ExpressRoute](#gw), dans les étapes qui précèdent.</span><span class="sxs-lookup"><span data-stu-id="e0ece-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="e0ece-204">Pour ajouter une configuration point à site à la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="e0ece-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="e0ece-205">Vous pouvez suivre les étapes ci-dessous pour ajouter une configuration point à site à votre passerelle VPN dans une configuration de coexistence.</span><span class="sxs-lookup"><span data-stu-id="e0ece-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="e0ece-206">Ajoutez le pool d’adresses des clients VPN.</span><span class="sxs-lookup"><span data-stu-id="e0ece-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="e0ece-207">Téléchargez le certificat racine VPN dans Azure pour votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="e0ece-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="e0ece-208">Dans cet exemple, nous supposons que le certificat racine est stocké dans l'ordinateur local où sont exécutées les applets de commande PowerShell suivantes.</span><span class="sxs-lookup"><span data-stu-id="e0ece-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="e0ece-209">Pour plus d’informations sur le réseau VPN point à site, consultez la rubrique [Configuration d’une connexion point à site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ece-210">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0ece-210">Next steps</span></span>
<span data-ttu-id="e0ece-211">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e0ece-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
