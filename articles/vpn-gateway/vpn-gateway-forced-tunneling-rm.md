---
title: "Configurer le tunneling forcé pour les connexions de site à site - Resource Manager | Microsoft Docs"
description: "Comment rediriger ou « forcer » tout le trafic Internet vers votre emplacement local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="92800-103">Configuration du tunneling forcé à l’aide du modèle de déploiement Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92800-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="92800-104">Le tunneling forcé vous permet de rediriger ou de « forcer » tout le trafic Internet vers votre emplacement local via un tunnel VPN site à site pour l’inspection et l’audit.</span><span class="sxs-lookup"><span data-stu-id="92800-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="92800-105">Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="92800-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="92800-106">Sans le tunneling forcé, le trafic Internet depuis vos machines virtuelles dans Azure se fait toujours à travers l’infrastructure du réseau Azure directement vers Internet, sans vous permettre d’inspecter ou de vérifier le trafic.</span><span class="sxs-lookup"><span data-stu-id="92800-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="92800-107">L’accès Internet non autorisés est susceptible d’entraîner la divulgation d’informations ou tout autre type de violation de sécurité.</span><span class="sxs-lookup"><span data-stu-id="92800-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="92800-108">Cet article vous guide dans la configuration du tunneling forcé pour les réseaux virtuels créés à l’aide du modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="92800-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="92800-109">Le tunneling forcé peut être configuré à l’aide de PowerShell, et non pas dans le portail.</span><span class="sxs-lookup"><span data-stu-id="92800-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="92800-110">Si vous souhaitez configurer le tunneling forcé pour le modèle de déploiement de classique, sélectionnez l’article Classique dans la liste déroulante suivante :</span><span class="sxs-lookup"><span data-stu-id="92800-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="92800-111">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="92800-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="92800-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92800-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="92800-113">À propos du tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="92800-113">About forced tunneling</span></span>

<span data-ttu-id="92800-114">Le diagramme suivant illustre le fonctionnement du tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="92800-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Tunneling forcé](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="92800-116">Dans l’exemple ci-dessus, le sous-réseau frontal n’utilise pas le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="92800-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="92800-117">Les charges de travail du sous-réseau frontal peuvent continuer à accepter et à répondre aux demandes des clients directement à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="92800-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="92800-118">Les sous-réseaux intermédiaire et principal utilisent le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="92800-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="92800-119">Toutes les connexions sortantes à partir de ces deux sous-réseaux vers Internet seront forcées ou redirigées vers un site local via l’un des tunnels VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="92800-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="92800-120">Cela vous permet de restreindre et d’inspecter l’accès à Internet à partir de vos machines virtuelles ou des services cloud dans Azure, tout en continuant d’activer votre architecture de service multiniveaux requise.</span><span class="sxs-lookup"><span data-stu-id="92800-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="92800-121">Vous avez également la possibilité d’appliquer le tunneling forcé à tous les réseaux virtuels s’il n’existe aucune charge de travail Internet dans vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="92800-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="92800-122">Conditions requises et éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="92800-122">Requirements and considerations</span></span>

<span data-ttu-id="92800-123">Le tunneling forcé dans Azure est configuré via les itinéraires de réseau virtuel définis par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92800-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="92800-124">La redirection du trafic vers un site local est exprimée comme un itinéraire par défaut vers la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="92800-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="92800-125">Pour plus d’informations sur les réseaux virtuels et les itinéraires définis par l’utilisateur, consultez [Itinéraires définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92800-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="92800-126">Chaque sous-réseau du réseau virtuel dispose d’une table de routage système intégrée.</span><span class="sxs-lookup"><span data-stu-id="92800-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="92800-127">La table de routage système comporte les trois groupes d’itinéraires suivants :</span><span class="sxs-lookup"><span data-stu-id="92800-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="92800-128">**Itinéraires de réseau virtuel local :** directement vers les machines virtuelles de destination dans le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="92800-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="92800-129">**Itinéraires locaux :** vers la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="92800-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="92800-130">**Itinéraire par défaut :** directement vers Internet.</span><span class="sxs-lookup"><span data-stu-id="92800-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="92800-131">Les paquets destinés aux adresses IP privées non couvertes par les deux itinéraires précédents sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="92800-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="92800-132">Cette procédure utilise des itinéraires définis par l’utilisateur (UDR) pour créer une table de routage et ajouter un itinéraire par défaut, puis associer la table de routage à vos sous-réseaux de réseaux virtuels pour activer le tunneling forcé sur ces sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="92800-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="92800-133">Le tunneling forcé doit être associé à un réseau virtuel équipé d’une passerelle VPN avec itinéraire.</span><span class="sxs-lookup"><span data-stu-id="92800-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="92800-134">Vous devez définir un « site par défaut » parmi les sites locaux intersites connectés au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="92800-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="92800-135">En outre, le périphérique VPN local doit être configuré à l’aide de 0.0.0.0/0 comme des sélecteurs de trafic.</span><span class="sxs-lookup"><span data-stu-id="92800-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="92800-136">Le tunneling forcé ExpressRoute n'est pas configuré de cette manière, mais il est activé par la publication d’un itinéraire par défaut via les sessions d'homologation BGP ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="92800-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="92800-137">Pour plus d’informations, consultez la [Documentation ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="92800-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="92800-138">Présentation de la configuration</span><span class="sxs-lookup"><span data-stu-id="92800-138">Configuration overview</span></span>

<span data-ttu-id="92800-139">La procédure suivante vous aide à créer un groupe de ressources et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="92800-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="92800-140">Vous créerez ensuite une passerelle VPN et configurerez le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="92800-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="92800-141">Dans cette procédure, le réseau virtuel « MultiTier-VNet » comporte trois sous-réseaux : « Frontend », « Midtier » et « Backend », ainsi que quatre connexions intersites : « DefaultSiteHQ » et trois « Branches ».</span><span class="sxs-lookup"><span data-stu-id="92800-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="92800-142">Les étapes de la procédure définissent « DefaultSiteHQ » comme connexion de site par défaut pour le tunneling forcé et configure les sous-réseaux « Midtier » et « Backend » de manière à utiliser le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="92800-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="92800-143">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="92800-143">Before you begin</span></span>

<span data-ttu-id="92800-144">Installez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="92800-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="92800-145">Pour plus d’informations sur l’installation des applets de commande PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="92800-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="92800-146">Pour se connecter</span><span class="sxs-lookup"><span data-stu-id="92800-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="92800-147">Configurer un tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="92800-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="92800-148">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="92800-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="92800-149">Créez un réseau virtuel et spécifiez vos sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="92800-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="92800-150">Créez les passerelles de réseau local.</span><span class="sxs-lookup"><span data-stu-id="92800-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="92800-151">Créez la table d’itinéraires et la règle de routage.</span><span class="sxs-lookup"><span data-stu-id="92800-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="92800-152">Associez la table d’itinéraire vers le niveau intermédiaire et les sous-réseaux principaux.</span><span class="sxs-lookup"><span data-stu-id="92800-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="92800-153">Créez la passerelle avec un site par défaut.</span><span class="sxs-lookup"><span data-stu-id="92800-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="92800-154">Cette opération prend un certain temps, parfois 45 minutes voire plus, car vous créez et configurez la passerelle.</span><span class="sxs-lookup"><span data-stu-id="92800-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="92800-155">**-GatewayDefaultSite** est le paramètre d’applet de commande qui permet à la configuration de routage forcé de fonctionner. Configurez ce paramètre correctement.</span><span class="sxs-lookup"><span data-stu-id="92800-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="92800-156">Il est disponible uniquement dans PowerShell 1.0 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="92800-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="92800-157">Établissez des connexions VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="92800-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```