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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Vue d’ensemble des configurations de périphériques VPN tiers
Cet article fournit une vue d’ensemble des configurations de périphérique VPN local pour la connexion des passerelles VPN tooAzure. l’exemple Hello réseau virtuel Azure et VPN passerelle le programme d’installation sera utilisé tooconnect toodifferent les périphériques VPN local avec hello mêmes paramètres.

## <a name="device-requirements"></a>Configuration requise du périphérique
Les passerelles VPN Azure utilisent des suites de protocoles IPsec/IKE standard pour les tunnels VPN site à site (S2S). Consultez trop[propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) pour hello plus les paramètres de protocole IPsec/IKE et les algorithmes de chiffrement par défaut pour les passerelles VPN Azure. Vous pouvez éventuellement spécifier la combinaison de hello exacte des algorithmes de chiffrement et des avantages clés pour une connexion spécifique comme décrit dans [sur les exigences de chiffrement](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Tunnel VPN unique
topologie de première Hello se compose d’un seul tunnel S2S VPN entre une passerelle VPN Azure et votre périphérique VPN sur site. Vous pouvez éventuellement configurer BGP via un tunnel VPN de hello.

![tunnel unique](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Consultez trop[configurer une connexion site à site](vpn-gateway-howto-site-to-site-resource-manager-portal.md) pour obtenir des instructions détaillées, étape par étape. Hello sections suivantes répertorient les paramètres hello et fournissent un toohelp de script PowerShell exemple commencer.

### <a name="network-and-vpn-gateway-information"></a>Informations sur le réseau et la passerelle VPN
Cette section répertorie les paramètres hello pour obtenir des exemples hello ci-dessus.

| **Paramètre**                | **Valeur**                    |
| ---                          | ---                          |
| Préfixes d’adresse du réseau virtuel        | 10.11.0.0/16<br>10.12.0.0/16 |
| IP de la passerelle VPN Azure         | IP de la passerelle VPN Azure         |
| Préfixes d’adresse locale | 10.51.0.0/16<br>10.52.0.0/16 |
| IP du périphérique VPN local    | IP du périphérique VPN local    |
| * ASN BGP du réseau virtuel                | 65010                        |
| * IP d’homologue BGP Azure           | 10.12.255.30                 |
| * ASN BGP local         | 65050                        |
| * IP d’homologue BGP local     | 10.52.255.254                |

* (*) Paramètres facultatifs pour BGP uniquement

### <a name="sample-powershell-script"></a>Exemple de script PowerShell
[Créer une connexion VPN de S2S à l’aide de PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) a hello des instructions détaillées. Cette section fournit une tooget de script d’exemple que vous avez démarré.

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

### <a name ="policybased"></a> [Facultatif] Utilisez une stratégie IPsec/IKE personnalisée avec l’option « UsePolicyBasedTrafficSelectors »
Si vos périphériques VPN ne prennent pas en charge les sélecteurs de trafic « pour tout » (itinéraire en fonction/VTI basés sur la configuration), vous devez toocreate une stratégie IPsec/IKE personnalisée, configurez l’option de « UsePolicyBasedTrafficSelectors » comme décrit dans [cet article ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Vous devez toocreate une stratégie IPsec/IKE dans l’ordre tooenable option « UsePolicyBasedTrafficSelectors » sur la connexion de hello.

script d’exemple Hello ci-dessous crée une stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)

Ensuite, il applique la stratégie de hello et permet de « UesPolicyBasedTrafficSelectors » sur la connexion de hello.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Facultatif] Utiliser le protocole BGP sur la connexion VPN S2S
Vous pouvez éventuellement utiliser le protocole BGP sur une connexion de hello. Consultez l’article [Configurer BGP sur des passerelles VPN](vpn-gateway-bgp-resource-manager-ps.md). Deux différences sont à noter :

les préfixes d’adresse Hello local peuvent être une adresse d’hôte unique, l’adresse IP l’homologue BGP hello local :

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Vous devez définir «-cette propriété « trop$ True lors de la création de connexions de hello :

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Étapes suivantes
Consultez [configuration des passerelles VPN actif pour entre différents locaux et les connexions de réseau à](vpn-gateway-activeactive-rm-powershell.md) pour les étapes tooconfigure actif entre différents locaux et les connexions au réseau.

