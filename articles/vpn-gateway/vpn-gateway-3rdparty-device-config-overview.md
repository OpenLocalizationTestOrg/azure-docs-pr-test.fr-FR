---
title: "aaaAbout 3e partie périphérique configuration tooconnect tooAzure VPN passerelles VPN | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de 3 configurations d’appareil VPN tiers pour la connexion des passerelles VPN tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="e1170-103">Vue d’ensemble des configurations de périphériques VPN tiers</span><span class="sxs-lookup"><span data-stu-id="e1170-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="e1170-104">Cet article fournit une vue d’ensemble des configurations de périphérique VPN local pour la connexion des passerelles VPN tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1170-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="e1170-105">l’exemple Hello réseau virtuel Azure et VPN passerelle le programme d’installation sera utilisé tooconnect toodifferent les périphériques VPN local avec hello mêmes paramètres.</span><span class="sxs-lookup"><span data-stu-id="e1170-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="e1170-106">Configuration requise du périphérique</span><span class="sxs-lookup"><span data-stu-id="e1170-106">Device requirements</span></span>
<span data-ttu-id="e1170-107">Les passerelles VPN Azure utilisent des suites de protocoles IPsec/IKE standard pour les tunnels VPN site à site (S2S).</span><span class="sxs-lookup"><span data-stu-id="e1170-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="e1170-108">Consultez trop[propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) pour hello plus les paramètres de protocole IPsec/IKE et les algorithmes de chiffrement par défaut pour les passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="e1170-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="e1170-109">Vous pouvez éventuellement spécifier la combinaison de hello exacte des algorithmes de chiffrement et des avantages clés pour une connexion spécifique comme décrit dans [sur les exigences de chiffrement](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="e1170-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="e1170-110"><a name ="singletunnel"></a>Tunnel VPN unique</span><span class="sxs-lookup"><span data-stu-id="e1170-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="e1170-111">topologie de première Hello se compose d’un seul tunnel S2S VPN entre une passerelle VPN Azure et votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="e1170-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="e1170-112">Vous pouvez éventuellement configurer BGP via un tunnel VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="e1170-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![tunnel unique](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="e1170-114">Consultez trop[configurer une connexion site à site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) pour obtenir des instructions détaillées, étape par étape.</span><span class="sxs-lookup"><span data-stu-id="e1170-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="e1170-115">Hello sections suivantes répertorient les paramètres hello et fournissent un toohelp de script PowerShell exemple commencer.</span><span class="sxs-lookup"><span data-stu-id="e1170-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="e1170-116">Informations sur le réseau et la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="e1170-116">Network and VPN gateway information</span></span>
<span data-ttu-id="e1170-117">Cette section répertorie les paramètres hello pour obtenir des exemples hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e1170-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="e1170-118">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="e1170-118">**Parameter**</span></span>                | <span data-ttu-id="e1170-119">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="e1170-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="e1170-120">Préfixes d’adresse du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e1170-120">VNet address prefixes</span></span>        | <span data-ttu-id="e1170-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e1170-121">10.11.0.0/16</span></span><br><span data-ttu-id="e1170-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e1170-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="e1170-123">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="e1170-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="e1170-124">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="e1170-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="e1170-125">Préfixes d’adresse locale</span><span class="sxs-lookup"><span data-stu-id="e1170-125">On-premises address prefixes</span></span> | <span data-ttu-id="e1170-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e1170-126">10.51.0.0/16</span></span><br><span data-ttu-id="e1170-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e1170-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="e1170-128">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="e1170-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="e1170-129">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="e1170-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="e1170-130">* ASN BGP du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e1170-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="e1170-131">65010</span><span class="sxs-lookup"><span data-stu-id="e1170-131">65010</span></span>                        |
| <span data-ttu-id="e1170-132">* IP d’homologue BGP Azure</span><span class="sxs-lookup"><span data-stu-id="e1170-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="e1170-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="e1170-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="e1170-134">* ASN BGP local</span><span class="sxs-lookup"><span data-stu-id="e1170-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="e1170-135">65050</span><span class="sxs-lookup"><span data-stu-id="e1170-135">65050</span></span>                        |
| <span data-ttu-id="e1170-136">* IP d’homologue BGP local</span><span class="sxs-lookup"><span data-stu-id="e1170-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="e1170-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="e1170-137">10.52.255.254</span></span>                |

* <span data-ttu-id="e1170-138">(*) Paramètres facultatifs pour BGP uniquement</span><span class="sxs-lookup"><span data-stu-id="e1170-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="e1170-139">Exemple de script PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1170-139">Sample PowerShell script</span></span>
<span data-ttu-id="e1170-140">[Créer une connexion VPN de S2S à l’aide de PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) a hello des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="e1170-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="e1170-141">Cette section fournit une tooget de script d’exemple que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="e1170-141">This section provides a sample script tooget you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="e1170-142"><a name ="policybased"></a> [Facultatif] Utilisez une stratégie IPsec/IKE personnalisée avec l’option « UsePolicyBasedTrafficSelectors »</span><span class="sxs-lookup"><span data-stu-id="e1170-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="e1170-143">Si vos périphériques VPN ne prennent pas en charge les sélecteurs de trafic « pour tout » (itinéraire en fonction/VTI basés sur la configuration), vous devez toocreate une stratégie IPsec/IKE personnalisée, configurez l’option de « UsePolicyBasedTrafficSelectors » comme décrit dans [cet article ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1170-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1170-144">Vous devez toocreate une stratégie IPsec/IKE dans l’ordre tooenable option « UsePolicyBasedTrafficSelectors » sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="e1170-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="e1170-145">script d’exemple Hello ci-dessous crée une stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :</span><span class="sxs-lookup"><span data-stu-id="e1170-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="e1170-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="e1170-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="e1170-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="e1170-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="e1170-148">Ensuite, il applique la stratégie de hello et permet de « UesPolicyBasedTrafficSelectors » sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="e1170-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="e1170-149"><a name ="bgp"></a>[Facultatif] Utiliser le protocole BGP sur la connexion VPN S2S</span><span class="sxs-lookup"><span data-stu-id="e1170-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="e1170-150">Vous pouvez éventuellement utiliser le protocole BGP sur une connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="e1170-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="e1170-151">Consultez l’article [Configurer BGP sur des passerelles VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1170-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="e1170-152">Deux différences sont à noter :</span><span class="sxs-lookup"><span data-stu-id="e1170-152">There are two differences:</span></span>

<span data-ttu-id="e1170-153">les préfixes d’adresse Hello local peuvent être une adresse d’hôte unique, l’adresse IP l’homologue BGP hello local :</span><span class="sxs-lookup"><span data-stu-id="e1170-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="e1170-154">Vous devez définir «-cette propriété « trop$ True lors de la création de connexions de hello :</span><span class="sxs-lookup"><span data-stu-id="e1170-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="e1170-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1170-155">Next steps</span></span>
<span data-ttu-id="e1170-156">Consultez [configuration des passerelles VPN actif pour entre différents locaux et les connexions de réseau à](vpn-gateway-activeactive-rm-powershell.md) pour les étapes tooconfigure actif entre différents locaux et les connexions au réseau.</span><span class="sxs-lookup"><span data-stu-id="e1170-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

