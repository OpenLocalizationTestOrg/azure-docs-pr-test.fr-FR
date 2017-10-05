---
title: "À propos de la configuration de périphériques VPN tiers pour se connecter à des passerelles VPN Azure | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des configurations de périphériques VPN tiers pour une connexion à des passerelles VPN Azure."
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
ms.openlocfilehash: 72dab85bb882b05d72cef26bef70437695b70416
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="d736a-103">Vue d’ensemble des configurations de périphériques VPN tiers</span><span class="sxs-lookup"><span data-stu-id="d736a-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="d736a-104">Cet article fournit une vue d’ensemble des configurations de périphériques VPN locaux pour une connexion à des passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="d736a-104">This article provides an overview of on-premises VPN device configurations for connecting to Azure VPN gateways.</span></span> <span data-ttu-id="d736a-105">L’exemple de configuration de réseau virtuel et de passerelle VPN Azure permet de se connecter à différents périphériques VPN locaux avec les mêmes paramètres.</span><span class="sxs-lookup"><span data-stu-id="d736a-105">The sample Azure virtual network and VPN gateway setup will be used to connect to different on-premises VPN devices with the same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="d736a-106">Configuration requise du périphérique</span><span class="sxs-lookup"><span data-stu-id="d736a-106">Device requirements</span></span>
<span data-ttu-id="d736a-107">Les passerelles VPN Azure utilisent des suites de protocoles IPsec/IKE standard pour les tunnels VPN site à site (S2S).</span><span class="sxs-lookup"><span data-stu-id="d736a-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="d736a-108">Reportez-vous à la page [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) pour connaître les paramètres détaillés du protocole IPsec/IKE et les algorithmes de chiffrement par défaut des passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="d736a-108">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="d736a-109">Vous pouvez éventuellement spécifier la combinaison exacte d’algorithmes de chiffrement et les forces de clé souhaitée d’une connexion spécifique, comme décrit dans la rubrique [À propos des exigences de chiffrement](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="d736a-109">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="d736a-110"><a name ="singletunnel"></a>Tunnel VPN unique</span><span class="sxs-lookup"><span data-stu-id="d736a-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="d736a-111">La première topologie présente un tunnel VPN S2S unique entre une passerelle VPN Azure et votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="d736a-111">The first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="d736a-112">Vous pouvez éventuellement configurer le protocole BGP sur le tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="d736a-112">You can optionally configure BGP across the VPN tunnel.</span></span>

![tunnel unique](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="d736a-114">Reportez-vous à la page [Création d’une connexion de site à site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) pour obtenir des instructions détaillées, étape par étape.</span><span class="sxs-lookup"><span data-stu-id="d736a-114">Refer to [Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="d736a-115">Les sections suivantes répertorient les paramètres nécessaires et fournissent un exemple de script PowerShell pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="d736a-115">The following sections list the parameters and provide a sample PowerShell script to help you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="d736a-116">Informations sur le réseau et la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="d736a-116">Network and VPN gateway information</span></span>
<span data-ttu-id="d736a-117">Cette section répertorie les paramètres de l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d736a-117">This section list the parameters for the examples above.</span></span>

| <span data-ttu-id="d736a-118">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="d736a-118">**Parameter**</span></span>                | <span data-ttu-id="d736a-119">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="d736a-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="d736a-120">Préfixes d’adresse du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d736a-120">VNet address prefixes</span></span>        | <span data-ttu-id="d736a-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d736a-121">10.11.0.0/16</span></span><br><span data-ttu-id="d736a-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d736a-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="d736a-123">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="d736a-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="d736a-124">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="d736a-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="d736a-125">Préfixes d’adresse locale</span><span class="sxs-lookup"><span data-stu-id="d736a-125">On-premises address prefixes</span></span> | <span data-ttu-id="d736a-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d736a-126">10.51.0.0/16</span></span><br><span data-ttu-id="d736a-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d736a-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="d736a-128">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="d736a-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="d736a-129">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="d736a-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="d736a-130">* ASN BGP du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d736a-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="d736a-131">65010</span><span class="sxs-lookup"><span data-stu-id="d736a-131">65010</span></span>                        |
| <span data-ttu-id="d736a-132">* IP d’homologue BGP Azure</span><span class="sxs-lookup"><span data-stu-id="d736a-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="d736a-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="d736a-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="d736a-134">* ASN BGP local</span><span class="sxs-lookup"><span data-stu-id="d736a-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="d736a-135">65050</span><span class="sxs-lookup"><span data-stu-id="d736a-135">65050</span></span>                        |
| <span data-ttu-id="d736a-136">* IP d’homologue BGP local</span><span class="sxs-lookup"><span data-stu-id="d736a-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="d736a-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="d736a-137">10.52.255.254</span></span>                |

* <span data-ttu-id="d736a-138">(*) Paramètres facultatifs pour BGP uniquement</span><span class="sxs-lookup"><span data-stu-id="d736a-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="d736a-139">Exemple de script PowerShell</span><span class="sxs-lookup"><span data-stu-id="d736a-139">Sample PowerShell script</span></span>
<span data-ttu-id="d736a-140">L’article [Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) contient des instructions détaillées à ce propos.</span><span class="sxs-lookup"><span data-stu-id="d736a-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has the detailed instructions.</span></span> <span data-ttu-id="d736a-141">Cette section fournit un exemple de script pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="d736a-141">This section provides a sample script to get you started.</span></span>

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

# Connect to your subscription and create a new resource group

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

# Create the S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="d736a-142"><a name ="policybased"></a> [Facultatif] Utilisez une stratégie IPsec/IKE personnalisée avec l’option « UsePolicyBasedTrafficSelectors »</span><span class="sxs-lookup"><span data-stu-id="d736a-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="d736a-143">Si vos périphériques VPN ne prennent pas en charge les sélecteurs de trafic « universel » (configuration basée sur le routage/basée sur une interface virtuelle de tunnel), vous devrez créer une stratégie IPsec/IKE personnalisée et configurer l’option « UsePolicyBasedTrafficSelectors » comme indiqué dans [cet article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d736a-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need to create a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d736a-144">Vous devez créer une stratégie IPsec/IKE afin d’activer l’option « UsePolicyBasedTrafficSelectors » sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="d736a-144">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="d736a-145">L’exemple de script ci-dessous crée une stratégie IPsec/IKE avec les paramètres et les algorithmes suivants :</span><span class="sxs-lookup"><span data-stu-id="d736a-145">The sample script below creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="d736a-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="d736a-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="d736a-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="d736a-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="d736a-148">Ensuite, il applique la stratégie et active l’option « UsePolicyBasedTrafficSelectors » sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="d736a-148">It then applies the policy and enables "UesPolicyBasedTrafficSelectors" on the connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="d736a-149"><a name ="bgp"></a>[Facultatif] Utiliser le protocole BGP sur la connexion VPN S2S</span><span class="sxs-lookup"><span data-stu-id="d736a-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="d736a-150">Vous pouvez éventuellement utiliser le protocole BGP sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="d736a-150">You can optionally use BGP on the connection.</span></span> <span data-ttu-id="d736a-151">Consultez l’article [Configurer BGP sur des passerelles VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d736a-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="d736a-152">Deux différences sont à noter :</span><span class="sxs-lookup"><span data-stu-id="d736a-152">There are two differences:</span></span>

<span data-ttu-id="d736a-153">Les préfixes d’adresse locale peuvent être une adresse d’hôte unique, l’adresse IP de l’homologue BGP local :</span><span class="sxs-lookup"><span data-stu-id="d736a-153">The on-premises address prefixes can be a single host address, the on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="d736a-154">Vous devez définir « -EnableBGP » sur $True lors de la création de la connexion :</span><span class="sxs-lookup"><span data-stu-id="d736a-154">You must set "-EnableBGP" to $True when creating the connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="d736a-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d736a-155">Next steps</span></span>
<span data-ttu-id="d736a-156">Pour connaître les étapes de configuration des connexions en mode actif-actif entre des réseaux locaux ou entre deux réseaux virtuels, consultez la page [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) (Configuration des passerelles VPN actif-actif pour des connexions entre des réseaux locaux et entre deux réseaux virtuels).</span><span class="sxs-lookup"><span data-stu-id="d736a-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

