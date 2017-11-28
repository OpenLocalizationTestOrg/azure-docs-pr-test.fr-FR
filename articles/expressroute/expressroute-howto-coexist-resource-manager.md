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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="5def0-103">Configurer la coexistence de connexions de site à site et ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5def0-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5def0-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5def0-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="5def0-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="5def0-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="5def0-106">La configuration de connexions VPN de site à site et ExpressRoute coexistantes possède plusieurs avantages.</span><span class="sxs-lookup"><span data-stu-id="5def0-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="5def0-107">Vous pouvez configurer un VPN de Site à Site comme un chemin d’accès sécurisé de basculement pour ExressRoute, ou utiliser des VPN de Site à Site tooconnect toosites qui ne sont pas connectés via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="5def0-108">Nous aborderons hello étapes tooconfigure les deux scénarios dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5def0-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="5def0-109">Cet article s’applique le modèle de déploiement du Gestionnaire de ressources toohello et utilise PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5def0-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="5def0-110">Cette configuration n’est pas disponible dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5def0-111">Circuits ExpressRoute doivent être préconfigurés avant de suivre les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5def0-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="5def0-112">Assurez-vous que vous avez suivi les guides hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [configurer le routage](expressroute-howto-routing-arm.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="5def0-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="5def0-113">Limites et limitations</span><span class="sxs-lookup"><span data-stu-id="5def0-113">Limits and limitations</span></span>
* <span data-ttu-id="5def0-114">**Le routage de transit n’est pas pris en charge.**</span><span class="sxs-lookup"><span data-stu-id="5def0-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="5def0-115">Vous ne pouvez effectuer de routage (via Azure) entre votre réseau local connecté via le réseau VPN de site à site et votre réseau local connecté via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="5def0-116">**La passerelle de référence de base n’est pas prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="5def0-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="5def0-117">Vous devez utiliser une passerelle de base SKU pour les deux hello [passerelle ExpressRoute](expressroute-about-virtual-network-gateways.md) et hello [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="5def0-118">**Seule la passerelle VPN basée sur un itinéraire est prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="5def0-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="5def0-119">Vous devez utiliser une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="5def0-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="5def0-120">L’**itinéraire statique doit être configuré pour votre passerelle VPN.**</span><span class="sxs-lookup"><span data-stu-id="5def0-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="5def0-121">Si votre réseau local est connecté tooboth ExpressRoute et un Site à Site VPN, vous devez disposer un itinéraire statique configuré dans votre toohello de connexion de réseau local tooroute hello Site-à-Site VPN Internet public.</span><span class="sxs-lookup"><span data-stu-id="5def0-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="5def0-122">**Passerelle ExpressRoute doit être configurée en premier et lié tooa circuit.**</span><span class="sxs-lookup"><span data-stu-id="5def0-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="5def0-123">Vous devez créez d’abord passerelle ExpressRoute de hello et liez-le tooa circuit avant d’ajouter de la passerelle VPN de hello Site-à-Site.</span><span class="sxs-lookup"><span data-stu-id="5def0-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="5def0-124">Modèles de configuration</span><span class="sxs-lookup"><span data-stu-id="5def0-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="5def0-125">Configurer un réseau VPN de site à site comme un chemin d’accès de basculement pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5def0-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="5def0-126">Vous pouvez configurer une connexion VPN de site à site en tant que sauvegarde pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="5def0-127">Cela s’applique uniquement toovirtual réseaux lié toohello chemin d’accès d’homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="5def0-128">Il n’existe aucune solution de basculement basée sur des réseaux VPN pour les services accessibles via les homologations Azure public et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5def0-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="5def0-129">lien principal de hello est toujours Hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="5def0-130">Les données transitent via le chemin d’accès de Site à Site VPN hello uniquement si hello circuit ExpressRoute échoue.</span><span class="sxs-lookup"><span data-stu-id="5def0-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="5def0-131">Alors que le circuit ExpressRoute est préférable à VPN de Site à Site lorsque les deux itinéraires sont hello même, Azure utilisera itinéraire de hello plus long préfixe correspondance toochoose hello vers la destination du paquet hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="5def0-133">Configurer un toosites tooconnect VPN de Site à Site ne pas connecté via ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5def0-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="5def0-134">Vous pouvez configurer votre réseau où certains sites connectent directement tooAzure via le VPN de Site à Site, et certains sites via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="5def0-136">Vous ne pouvez pas configurer un réseau virtuel comme un routeur de transit.</span><span class="sxs-lookup"><span data-stu-id="5def0-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="5def0-137">En sélectionnant hello étapes toouse</span><span class="sxs-lookup"><span data-stu-id="5def0-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="5def0-138">Il existe deux ensembles de toochoose de procédures à partir de différents.</span><span class="sxs-lookup"><span data-stu-id="5def0-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="5def0-139">procédure de configuration de Hello que vous sélectionnez dépend de si vous disposez d’un réseau virtuel existant que vous souhaitez tooconnect à, ou que vous voulez toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5def0-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="5def0-140">Je ne disposer d’un réseau virtuel et devez toocreate une.</span><span class="sxs-lookup"><span data-stu-id="5def0-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="5def0-141">Cette procédure vous guide dans la création d’un réseau virtuel si vous n’en possédez pas encore un. Elle vous demande d’utiliser le modèle de déploiement Resource Manager et de créer de nouvelles connexions ExpressRoute et VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="5def0-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="5def0-142">tooconfigure un réseau virtuel, suivez les étapes de hello dans [toocreate un nouveau réseau virtuel et les connexions de coexistence](#new).</span><span class="sxs-lookup"><span data-stu-id="5def0-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="5def0-143">J’ai déjà un réseau virtuel répondant au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5def0-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="5def0-144">Vous disposez peut-être déjà d’un réseau virtuel avec une connexion VPN de site à site existante ou une connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="5def0-145">Hello [tooconfigure de coexistence connexions pour un réseau virtuel existant déjà](#add) section vous présente la suppression de la passerelle de hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="5def0-146">Lorsque vous créez hello de nouvelles connexions, les étapes de hello doivent être effectuées dans un ordre spécifique.</span><span class="sxs-lookup"><span data-stu-id="5def0-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="5def0-147">N’utilisez pas les instructions hello dans d’autres articles de toocreate vos passerelles et les connexions.</span><span class="sxs-lookup"><span data-stu-id="5def0-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="5def0-148">Dans cette procédure, la création de connexions peuvent coexister requiert vous toodelete votre passerelle, puis configurez les nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="5def0-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="5def0-149">Vous devez les temps d’arrêt pour les connexions entre différents locaux pendant que vous supprimez et recréez la passerelle et les connexions, mais vous n’aurez pas toomigrate un de vos machines virtuelles ou services tooa nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5def0-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="5def0-150">Vos machines virtuelles et les services seront toujours en mesure de toocommunicate sortantes via l’équilibrage de charge hello lorsque vous configurez votre passerelle s’ils ne sont donc toodo configuré.</span><span class="sxs-lookup"><span data-stu-id="5def0-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="5def0-151"><a name="new"></a>toocreate un nouveau réseau virtuel et la coexistence de connexions</span><span class="sxs-lookup"><span data-stu-id="5def0-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="5def0-152">Cette procédure vous guide dans la création d’un réseau virtuel et de connexions de site à site et ExpressRoute appelées à coexister.</span><span class="sxs-lookup"><span data-stu-id="5def0-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="5def0-153">Installez hello dernière version de hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5def0-154">Pour plus d’informations sur l’installation des applets de commande hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5def0-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5def0-155">les applets de commande Hello que vous utilisez pour cette configuration peuvent être légèrement différentes de celle que vous connaissez peut-être.</span><span class="sxs-lookup"><span data-stu-id="5def0-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="5def0-156">Applets de commande hello toouse vraiment être spécifié dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="5def0-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="5def0-157">Connectez-vous au compte de tooyour et configurer hello environnement.</span><span class="sxs-lookup"><span data-stu-id="5def0-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="5def0-158">Créez un réseau virtuel et un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="5def0-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="5def0-159">Pour plus d’informations sur la configuration du réseau virtuel hello, consultez [configuration de réseau virtuel Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5def0-160">Hello sous-réseau de passerelle doit être /27 ou un préfixe plus court (par exemple, /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="5def0-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="5def0-161">Créez un nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5def0-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="5def0-162">Ajoutez des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="5def0-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="5def0-163">Enregistrer la configuration du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="5def0-164"><a name="gw"></a>Créez une passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5def0-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="5def0-165">Pour plus d’informations sur la configuration de passerelle ExpressRoute hello, consultez [configuration de la passerelle ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="5def0-166">Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="5def0-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="5def0-167">Lier le circuit ExpressRoute toohello hello ExpressRoute passerelle.</span><span class="sxs-lookup"><span data-stu-id="5def0-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="5def0-168">Une fois cette étape terminée, hello entre votre réseau local et le Azure via ExpressRoute, est établie.</span><span class="sxs-lookup"><span data-stu-id="5def0-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="5def0-169">Pour plus d’informations sur l’opération de liaison hello, consultez [des réseaux virtuels lien tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="5def0-170"><a name="vpngw"></a>Créez ensuite la passerelle VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="5def0-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="5def0-171">Pour plus d’informations sur la configuration de passerelle VPN hello, consultez [configurer un réseau virtuel avec une connexion Site à Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="5def0-172">Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="5def0-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="5def0-173">doit Hello VpnType *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="5def0-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="5def0-174">La passerelle VPN Azure prend en charge le protocole de routage BGP.</span><span class="sxs-lookup"><span data-stu-id="5def0-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="5def0-175">Vous pouvez spécifier ASN (en tant que nombre) pour ce réseau virtuel en ajoutant le commutateur - Asn de hello Bonjour commande suivante.</span><span class="sxs-lookup"><span data-stu-id="5def0-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="5def0-176">Ne pas spécifier ce paramètre sera par défaut tooAS numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="5def0-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="5def0-177">Vous pouvez trouver hello BGP d’homologation IP et hello en tant que numéro que Azure utilise pour la passerelle du VPN hello dans $azureVpn.BgpSettings.BgpPeeringAddress et $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="5def0-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="5def0-178">Pour plus d’informations, consultez [Configurer BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) pour la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="5def0-179">Créez une entité de passerelle VPN de site local.</span><span class="sxs-lookup"><span data-stu-id="5def0-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="5def0-180">Cette commande ne configure pas votre passerelle VPN locale.</span><span class="sxs-lookup"><span data-stu-id="5def0-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="5def0-181">Au lieu de cela, il vous permet de paramètres de la passerelle locale hello tooprovide, telles que des adresses IP publiques de hello et hello localement l’espace d’adressage, afin que hello passerelle VPN Azure peut se connecter tooit.</span><span class="sxs-lookup"><span data-stu-id="5def0-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="5def0-182">Si votre périphérique VPN local prend uniquement en charge le routage statique, vous pouvez configurer des itinéraires statiques hello Bonjour de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="5def0-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="5def0-183">Si votre périphérique VPN local prend en charge hello BGP et que vous souhaitez utiliser le routage dynamique tooenable, vous devez tooknow hello BGP d’homologation IP et hello comme numéro de votre réseau privé virtuel local qui utilise de périphérique.</span><span class="sxs-lookup"><span data-stu-id="5def0-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="5def0-184">Configurez votre passerelle VPN locale appareil tooconnect toohello nouveau VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="5def0-185">Pour plus d’informations sur la configuration du périphérique VPN, consultez la rubrique [Configuration de périphérique VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="5def0-186">Passerelle VPN de Site à Site du hello lien sur la passerelle locale toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="5def0-187"><a name="add"></a>connexions de coexistence tooconfigure pour un réseau virtuel existant</span><span class="sxs-lookup"><span data-stu-id="5def0-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="5def0-188">Si vous avez un réseau virtuel existant, vérifiez la taille de sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="5def0-189">Si le sous-réseau de passerelle hello est /28 ou /29, vous devez tout d’abord supprimer la passerelle de réseau virtuel hello et augmenter la taille de sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="5def0-190">Hello étapes décrites dans cette section vous montrent comment toodo qui.</span><span class="sxs-lookup"><span data-stu-id="5def0-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="5def0-191">Si le sous-réseau de passerelle hello est /27 ou supérieure et réseau virtuel de hello est connecté via ExpressRoute, vous pouvez ignorer les étapes hello ci-dessous et continuer trop[« Étape 6 : créer une passerelle VPN de Site à Site »](#vpngw) dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="5def0-192">Lorsque vous supprimez la passerelle existante de hello, votre site local perdrez réseau virtuel de hello connexion tooyour lorsque vous travaillez sur cette configuration.</span><span class="sxs-lookup"><span data-stu-id="5def0-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="5def0-193">Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="5def0-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5def0-194">Pour plus d’informations sur l’installation des applets de commande, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5def0-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5def0-195">les applets de commande Hello que vous utilisez pour cette configuration peuvent être légèrement différentes de celle que vous connaissez peut-être.</span><span class="sxs-lookup"><span data-stu-id="5def0-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="5def0-196">Applets de commande hello toouse vraiment être spécifié dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="5def0-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="5def0-197">Supprimer la passerelle hello ExpressRoute ou VPN de Site à Site existante.</span><span class="sxs-lookup"><span data-stu-id="5def0-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="5def0-198">Supprimez le sous-réseau de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="5def0-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="5def0-199">Ajoutez un sous-réseau de passerelle défini sur /27 ou plus.</span><span class="sxs-lookup"><span data-stu-id="5def0-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5def0-200">Si vous n’avez pas suffisamment d’adresses IP dans votre taille de sous-réseau de passerelle de réseau virtuel tooincrease hello, vous devez tooadd plus d’espace d’adressage IP.</span><span class="sxs-lookup"><span data-stu-id="5def0-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="5def0-201">Enregistrer la configuration du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="5def0-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="5def0-202">À ce stade, vous disposez d’un réseau virtuel sans passerelle.</span><span class="sxs-lookup"><span data-stu-id="5def0-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="5def0-203">toocreate nouvelles passerelles et vos connexions, vous pouvez poursuivre [étape 4 : créer une passerelle ExpressRoute](#gw), située dans hello précédant l’ensemble d’étapes.</span><span class="sxs-lookup"><span data-stu-id="5def0-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="5def0-204">passerelle VPN de tooadd point-to-site configuration toohello</span><span class="sxs-lookup"><span data-stu-id="5def0-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="5def0-205">Vous pouvez suivre les étapes de hello ci-dessous passerelle VPN tooyour tooadd Point-to-Site configuration dans une configuration de coexistence.</span><span class="sxs-lookup"><span data-stu-id="5def0-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="5def0-206">Ajoutez le pool d’adresses des clients VPN.</span><span class="sxs-lookup"><span data-stu-id="5def0-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="5def0-207">Téléchargez tooAzure de certificat racine hello VPN pour la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="5def0-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="5def0-208">Dans cet exemple, il est supposé que ce certificat racine de hello est stocké sur l’ordinateur local de hello où hello suivant d’applets de commande PowerShell est exécuté.</span><span class="sxs-lookup"><span data-stu-id="5def0-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="5def0-209">Pour plus d’informations sur le réseau VPN point à site, consultez la rubrique [Configuration d’une connexion point à site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5def0-210">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5def0-210">Next steps</span></span>
<span data-ttu-id="5def0-211">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="5def0-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
