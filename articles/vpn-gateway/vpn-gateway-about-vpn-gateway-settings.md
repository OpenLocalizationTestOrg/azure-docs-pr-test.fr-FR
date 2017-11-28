---
title: "paramètres de la passerelle pour les connexions Azure entre différents locaux aaaVPN | Documents Microsoft"
description: "Découvrez les paramètres de passerelle VPN pour les passerelles de réseau virtuel Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="719e8-103">À propos des paramètres de configuration de la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="719e8-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="719e8-104">Une passerelle VPN est un type de passerelle de réseau virtuel qui envoie le trafic chiffré entre votre réseau virtuel et votre emplacement local à travers une connexion publique.</span><span class="sxs-lookup"><span data-stu-id="719e8-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="719e8-105">Vous pouvez également utiliser un trafic de toosend de passerelle VPN entre les réseaux virtuels entre hello backbone Azure.</span><span class="sxs-lookup"><span data-stu-id="719e8-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="719e8-106">Une connexion de passerelle VPN s’appuie sur la configuration hello de ressources, chacune contenant des paramètres configurables.</span><span class="sxs-lookup"><span data-stu-id="719e8-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="719e8-107">sections de Hello dans cet article décrivent les ressources hello et les paramètres qui concernent la passerelle VPN de tooa pour un réseau virtuel créé dans le modèle de déploiement de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="719e8-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="719e8-108">Vous pouvez trouver des descriptions et des diagrammes de topologie pour chaque solution connexion Bonjour [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="719e8-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="719e8-109"><a name="gwtype"></a>Types de passerelle</span><span class="sxs-lookup"><span data-stu-id="719e8-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="719e8-110">Chaque réseau virtuel ne peut posséder qu’une seule passerelle de réseau virtuel de chaque type.</span><span class="sxs-lookup"><span data-stu-id="719e8-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="719e8-111">Lorsque vous créez une passerelle de réseau virtuel, il se peut que vous devez vous assurer que le type de passerelle hello est correcte pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="719e8-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="719e8-112">Hello les valeurs disponibles pour le type de passerelle - sont :</span><span class="sxs-lookup"><span data-stu-id="719e8-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="719e8-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="719e8-113">Vpn</span></span>
* <span data-ttu-id="719e8-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="719e8-114">ExpressRoute</span></span>

<span data-ttu-id="719e8-115">Une passerelle VPN requiert hello `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="719e8-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="719e8-116">Exemple :</span><span class="sxs-lookup"><span data-stu-id="719e8-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="719e8-117"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="719e8-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="719e8-118">Configurer la passerelle de hello référence (SKU)</span><span class="sxs-lookup"><span data-stu-id="719e8-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="719e8-119">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="719e8-119">Azure portal</span></span>

<span data-ttu-id="719e8-120">Si vous utilisez hello toocreate portail Azure une passerelle de réseau virtuel du Gestionnaire de ressources, vous pouvez sélectionner la passerelle de hello référence (SKU) à l’aide du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="719e8-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="719e8-121">options de Hello avec que vous sont présentées correspondent toohello type de la passerelle et le type VPN que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="719e8-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="719e8-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="719e8-122">PowerShell</span></span>

<span data-ttu-id="719e8-123">exemple PowerShell suivant Hello spécifie hello `-GatewaySku` comme VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="719e8-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="719e8-124"><a name="resize"></a>Modifier (redimensionner) une référence SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="719e8-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="719e8-125">Si vous souhaitez tooupgrade votre tooa de référence (SKU) de passerelle SKU plus puissant, vous pouvez utiliser hello `Resize-AzureRmVirtualNetworkGateway` applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="719e8-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="719e8-126">Vous pouvez également rétrograder taille hello de référence (SKU) de passerelle à l’aide de cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="719e8-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="719e8-127">Hello PowerShell l’exemple suivant montre qu'une passerelle SKU redimensionnée tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="719e8-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="719e8-128"><a name="connectiontype"></a>Types de connexion</span><span class="sxs-lookup"><span data-stu-id="719e8-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="719e8-129">Dans le modèle de déploiement du Gestionnaire de ressources hello, chaque configuration nécessite un type de connexion de passerelle de réseau virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="719e8-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="719e8-130">Hello PowerShell Gestionnaire de ressources disponibles les valeurs pour `-ConnectionType` sont :</span><span class="sxs-lookup"><span data-stu-id="719e8-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="719e8-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="719e8-131">IPsec</span></span>
* <span data-ttu-id="719e8-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="719e8-132">Vnet2Vnet</span></span>
* <span data-ttu-id="719e8-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="719e8-133">ExpressRoute</span></span>
* <span data-ttu-id="719e8-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="719e8-134">VPNClient</span></span>

<span data-ttu-id="719e8-135">Bonjour PowerShell l’exemple suivant, nous créer une connexion de S2S qui requiert le type de connexion hello *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="719e8-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="719e8-136"><a name="vpntype"></a>Types de VPN</span><span class="sxs-lookup"><span data-stu-id="719e8-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="719e8-137">Lorsque vous créez la passerelle de réseau virtuel hello pour une configuration de passerelle VPN, vous devez spécifier un type VPN.</span><span class="sxs-lookup"><span data-stu-id="719e8-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="719e8-138">Hello type VPN que vous choisissez dépend de la topologie de connexion hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="719e8-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="719e8-139">Par exemple, une connexion P2S nécessite un VPN de type basé sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="719e8-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="719e8-140">Un type VPN peut également dépendre de matériel hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="719e8-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="719e8-141">Les configurations S2S nécessitent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="719e8-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="719e8-142">Certains périphériques VPN seront ne prennent en charge qu’un certain type de VPN.</span><span class="sxs-lookup"><span data-stu-id="719e8-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="719e8-143">Hello type VPN que vous sélectionnez doit satisfaire toutes les exigences de connexion hello pour les solutions hello souhaité toocreate.</span><span class="sxs-lookup"><span data-stu-id="719e8-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="719e8-144">Par exemple, si vous souhaitez toocreate une connexion de passerelle S2S VPN et une connexion de passerelle VPN de P2S pour hello même réseau virtuel, vous utiliseriez le type de VPN *RouteBased* car P2S nécessite un type RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="719e8-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="719e8-145">Vous devez également tooverify que votre périphérique VPN pris en charge une connexion VPN de RouteBased.</span><span class="sxs-lookup"><span data-stu-id="719e8-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="719e8-146">Une fois qu’une passerelle de réseau virtuel a été créée, vous ne pouvez pas modifier le type de VPN hello.</span><span class="sxs-lookup"><span data-stu-id="719e8-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="719e8-147">Vous avez toodelete hello passerelle de réseau virtuel et créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="719e8-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="719e8-148">Il existe deux types de VPN :</span><span class="sxs-lookup"><span data-stu-id="719e8-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="719e8-149">exemple PowerShell suivant Hello spécifie hello `-VpnType` en tant que *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="719e8-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="719e8-150">Lorsque vous créez une passerelle, vous devez vous assurer que hello - VpnType est correcte pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="719e8-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="719e8-151"><a name="requirements"></a>Conditions requises de la passerelle</span><span class="sxs-lookup"><span data-stu-id="719e8-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="719e8-152"><a name="gwsub"></a>Sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="719e8-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="719e8-153">Avant de créer votre passerelle VPN, vous devez d’abord créer un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="719e8-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="719e8-154">sous-réseau de passerelle Hello contient des adresses IP hello cette passerelle de réseau virtuel hello machines virtuelles et services utilisent.</span><span class="sxs-lookup"><span data-stu-id="719e8-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="719e8-155">Lorsque vous créez votre passerelle de réseau virtuel, lors passerelle machines virtuelles sont sous-réseau de passerelle toohello déployé et configuré avec les paramètres de la passerelle VPN hello requis.</span><span class="sxs-lookup"><span data-stu-id="719e8-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="719e8-156">Vous ne devez jamais déployer sous-réseau de passerelle toohello n’importe quel autre (par exemple, les machines virtuelles supplémentaires).</span><span class="sxs-lookup"><span data-stu-id="719e8-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="719e8-157">sous-réseau de passerelle Hello doit être nommé « GatewaySubnet » toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="719e8-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="719e8-158">Sous-réseau de passerelle hello d’affectation de noms « GatewaySubnet » permet Azure savoir qu’il est la passerelle de réseau virtuel hello hello sous-réseau toodeploy machines virtuelles et services.</span><span class="sxs-lookup"><span data-stu-id="719e8-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="719e8-159">Lorsque vous créez le sous-réseau de passerelle hello, vous spécifiez hello d’adresses IP qui hello sous-réseau contient.</span><span class="sxs-lookup"><span data-stu-id="719e8-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="719e8-160">adresses IP de Hello dans le sous-réseau de passerelle hello sont des ordinateurs virtuels de passerelle toohello alloué et les services de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="719e8-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="719e8-161">Certaines configurations nécessitent plus d’adresses IP que d’autres.</span><span class="sxs-lookup"><span data-stu-id="719e8-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="719e8-162">Consulter les instructions hello pour configuration hello que vous souhaitez toocreate et vérifiez que vous souhaitez toocreate le sous-réseau passerelle hello répondait à ces critères.</span><span class="sxs-lookup"><span data-stu-id="719e8-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="719e8-163">En outre, vous souhaiterez toomake que votre sous-réseau de passerelle contient suffisamment IP adresses tooaccommodate possibles futures des configurations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="719e8-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="719e8-164">Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau de passerelle de taille /28 ou supérieure (/28, /27, /26, etc.).</span><span class="sxs-lookup"><span data-stu-id="719e8-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="719e8-165">De cette façon, si vous ajoutez des fonctionnalités Bonjour futures, vous n’ont tootear votre passerelle, puis supprimez et recréez tooallow de sous-réseau de passerelle hello pour plus d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="719e8-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="719e8-166">Hello exemple de gestionnaire de ressources PowerShell suivant montre un sous-réseau de passerelle nommé GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="719e8-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="719e8-167">Vous pouvez voir la notation CIDR hello spécifie un /27, ce qui permet de suffisamment d’adresses IP pour la plupart des configurations qui existent actuellement.</span><span class="sxs-lookup"><span data-stu-id="719e8-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="719e8-168"><a name="lng"></a>Passerelles de réseau local</span><span class="sxs-lookup"><span data-stu-id="719e8-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="719e8-169">Lorsque vous créez une configuration de passerelle VPN, passerelle de réseau local hello représente souvent votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="719e8-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="719e8-170">Dans le modèle de déploiement classique de hello, passerelle de réseau local hello a tooas auxquels un Site Local.</span><span class="sxs-lookup"><span data-stu-id="719e8-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="719e8-171">Vous donnez un nom à passerelle de réseau local hello hello adresse IP publique de l’appareil VPN local hello et spécifiez les préfixes d’adresse hello qui sont trouvent sur un emplacement local de hello.</span><span class="sxs-lookup"><span data-stu-id="719e8-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="719e8-172">Azure examine les préfixes d’adresse de destination hello pour le trafic réseau, consulte configuration hello que vous avez spécifiées pour votre passerelle de réseau local et route les paquets en conséquence.</span><span class="sxs-lookup"><span data-stu-id="719e8-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="719e8-173">Vous spécifiez également des passerelles de réseau local pour les configurations avec interconnexion de réseaux virtuels qui utilisent une connexion de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="719e8-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="719e8-174">Hello l’exemple PowerShell suivant crée une nouvelle passerelle de réseau local :</span><span class="sxs-lookup"><span data-stu-id="719e8-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="719e8-175">Vous avez parfois besoin de paramètres de passerelle du réseau local toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="719e8-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="719e8-176">Par exemple, lorsque vous ajoutez ou modifiez la plage d’adresses hello, ou si hello adresseIP du périphérique VPN de hello change.</span><span class="sxs-lookup"><span data-stu-id="719e8-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="719e8-177">Pour un réseau virtuel classique, vous pouvez modifier ces paramètres dans le portail classique de hello sur la page de réseaux locaux hello.</span><span class="sxs-lookup"><span data-stu-id="719e8-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="719e8-178">Pour Resource Manager, voir [Modification des paramètres de passerelle de réseau local à l’aide de PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="719e8-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="719e8-179"><a name="resources"></a>API REST et applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="719e8-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="719e8-180">Pour les ressources techniques supplémentaires en matière de syntaxe spécifique lors de l’utilisation des API REST, les applets de commande PowerShell ou CLI d’Azure pour les configurations de passerelle VPN, consultez hello suivant pages :</span><span class="sxs-lookup"><span data-stu-id="719e8-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="719e8-181">**Classique**</span><span class="sxs-lookup"><span data-stu-id="719e8-181">**Classic**</span></span> | <span data-ttu-id="719e8-182">**Gestionnaire de ressources**</span><span class="sxs-lookup"><span data-stu-id="719e8-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="719e8-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="719e8-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="719e8-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="719e8-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="719e8-185">API REST</span><span class="sxs-lookup"><span data-stu-id="719e8-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="719e8-186">API REST</span><span class="sxs-lookup"><span data-stu-id="719e8-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="719e8-187">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="719e8-187">Not supported</span></span> | [<span data-ttu-id="719e8-188">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="719e8-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="719e8-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="719e8-189">Next steps</span></span>

<span data-ttu-id="719e8-190">Pour plus d’informations sur les configurations de connexion disponible, consultez la rubrique [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="719e8-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>