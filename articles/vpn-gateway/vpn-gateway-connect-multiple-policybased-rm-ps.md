---
title: "Connecter des périphériques VPN basée sur des stratégies VPN Azure passerelles toomultiple local : Azure Resource Manager : PowerShell | Documents Microsoft"
description: "Cet article vous guide dans la configuration Azure basée sur un itinéraire VPN passerelle toomultiple basée sur des stratégies VPN des appareils à l’aide du Gestionnaire de ressources Azure et PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Connexion VPN Azure passerelles toomultiple basée sur des stratégies VPN appareils locaux à l’aide de PowerShell

Cet article vous aidera à configurer un Azure basée sur un itinéraire VPN passerelle tooconnect toomultiple locale basée sur des stratégies des dispositifs VPN tirant parti des stratégies IPsec/IKE personnalisées sur les connexions VPN de S2S.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>À propos des passerelles VPN basées sur le routage et les stratégies

Stratégie - *et* périphériques VPN itinéraire diffèrent dans la manière dont les sélecteurs de trafic IPsec hello sont définis sur une connexion :

* **Basée sur des stratégies** périphériques VPN utilisent des combinaisons de hello de préfixes à partir de ces deux toodefine réseaux comment le trafic est chiffré/déchiffré via les tunnels IPsec. En règle générale, ce modèle est construit sur des pare-feu qui se chargent du filtrage des paquets. Chiffrement de tunnel IPsec et le déchiffrement sont ajoutés toohello le filtrage de paquets et le moteur de traitement.
* **Basée sur un itinéraire** périphériques VPN utilisent sélecteurs de trafic pour tout (caractère générique), et permettent de routage/transfert tables les tunnels IPsec toodifferent diriger le trafic. En règle générale, ce modèle est construit sur des plateformes de routeur où chaque tunnel IPsec est modélisé en tant qu’interface réseau ou VTI (interface virtuelle de tunnel).

Hello diagrammes suivants mettre en surbrillance deux modèles de hello :

### <a name="policy-based-vpn-example"></a>Exemple de VPN basé sur des stratégies
![basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Exemple de VPN basé sur le routage
![basé sur le routage](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Prise en charge par Azure des VPN basés sur des stratégies
Actuellement, Azure prend en charge les deux modes de passerelles VPN : les passerelles VPN basées sur le routage et les passerelles VPN basées sur des stratégies. Les deux modes sont construits sur différentes plateformes internes aux caractéristiques différentes :

|                          | **Passerelle VPN basée sur des stratégies** | **Passerelle VPN basée sur le routage**               |
| ---                      | ---                         | ---                                      |
| **Référence SKU de passerelle Azure**    | De base                       | Basic, Standard, HighPerformance         |
| **Version IKE**          | IKEv1                       | IKEv2                                    |
| **IOPS Connexions S2S** | **1**                       | Basic/Standard : 10<br> HighPerformance : 30 |
|                          |                             |                                          |

Avec la stratégie IPsec/IKE personnalisée hello, vous pouvez désormais configurer Azure basée sur un itinéraire VPN passerelles toouse basée sur le préfixe sélecteurs de trafic avec l’option «**PolicyBasedTrafficSelectors**», périphériques VPN basée sur des stratégies tooconnect tooon local. Cette fonctionnalité vous permet de tooconnect à partir d’un réseau virtuel Azure et toomultiple de passerelle VPN locale basée sur des stratégies des appareils VPN/pare-feu, suppression de limite de connexion unique hello de hello actuelle Azure basée sur des stratégies les passerelles VPN.

> [!IMPORTANT]
> 1. tooenable cette connectivité, vos périphériques VPN basée sur des stratégies de local doivent prendre en charge **IKEv2** tooconnect toohello Azure passerelles VPN basée sur un itinéraire. Vérifiez les caractéristiques de votre périphérique VPN.
> 2. Hello sur des réseaux locaux qui se connectent via des appareils VPN basée sur des stratégies avec ce mécanisme ne peuvent se connecter toohello réseau virtuel Azure ; **qu’ils ne peuvent pas traversent tooother sur des réseaux locaux ou des réseaux virtuels via hello même passerelle VPN Azure**.
> 3. option de configuration Hello fait partie de la stratégie de connexion IPsec/IKE personnalisée hello. Si vous activez l’option de sélecteur hello du trafic basé sur une stratégie, vous devez spécifier la stratégie complète de hello (algorithmes de chiffrement et d’intégrité IPsec/IKE, atouts et durées de vie SA).

Hello suivant schéma montre pourquoi le routage de transit via la passerelle VPN Azure ne fonctionne pas avec l’option de hello basée sur des stratégies :

![transit basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Comme indiqué dans le diagramme de hello, passerelle VPN Azure de hello a sélecteurs de trafic à partir de tooeach de réseau virtuel hello des préfixes de réseau local hello, mais pas les préfixes de connexion croisée hello. Par exemple, le site local 2, 3 et 4 chacun peuvent communiquer tooVNet1 respectivement, mais ne peut pas se connecter via tooeach passerelle VPN Azure du hello autres. diagramme de Hello montre hello interconnexion sélecteurs de trafic qui ne sont pas disponibles dans une passerelle VPN Azure hello à cette configuration.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Configurer des sélecteurs de trafic basés sur des stratégies sur une connexion

Hello instructions de ce suivi de l’article hello même exemple, comme décrit dans [stratégie IPsec/IKE configurer pour les connexions S2S ou au réseau](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish une connexion VPN de S2S. Cela est illustré par hello suivant schéma :

![stratégie S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Hello tooenable de flux de travail cette connectivité :
1. Créer une passerelle de réseau local pour votre connexion intersite, réseau virtuel de hello et passerelle VPN
2. Créez une stratégie IPsec/IKE.
3. Appliquer la stratégie de hello lorsque vous créez une connexion S2S ou au réseau, et **activer les sélecteurs de trafic basé sur une stratégie hello** sur la connexion de hello
4. Si la connexion de hello existe déjà, vous pouvez appliquer ou mettre à jour la connexion à la stratégie hello tooan existante

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Activer des sélecteurs de trafic basés sur des stratégies sur une connexion

Vérifiez que vous avez effectué [partie 3 sur l’article de stratégie IPsec/IKE configurer hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) pour cette section. Hello suivant montre comment utiliser hello les mêmes paramètres et étapes :

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Étape 1 : créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Déclarez vos variables & connecter tooyour abonnement
Dans cet exercice, nous allons commencer par déclarer les variables. Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
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
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
toouse hello applets de commande Gestionnaire de ressources, veillez à basculer en mode de tooPowerShell. Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).

Ouvrez la console PowerShell et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local
Hello, l’exemple suivant crée un réseau virtuel hello, TestVNet1 avec trois sous-réseaux et de passerelle VPN de hello. Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ». Si vous le nommez autrement, la création de votre passerelle échoue.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Étape 2 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Créez une stratégie IPsec/IKE.

> [!IMPORTANT]
> Vous devez toocreate une stratégie IPsec/IKE dans l’ordre tooenable option « UsePolicyBasedTrafficSelectors » sur la connexion de hello.

Hello exemple suivant crée une stratégie IPsec/IKE avec ces algorithmes et les paramètres :
* IKEv2: AES256, SHA384, DHGroup24
* IPsec : AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Créer un réseau VPN S2S hello avec sélecteurs de trafic basé sur la stratégie et la stratégie IPsec/IKE
Créer un réseau VPN S2S et appliquer la stratégie IPsec/IKE de hello créé à l’étape précédente de hello. N’oubliez pas de paramètre supplémentaires hello »-UsePolicyBasedTrafficSelectors $True » qui permet des sélecteurs de trafic de basée sur la connexion de hello.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Après avoir effectué les étapes de hello, hello réseau VPN S2S utilise hello stratégie IPsec/IKE définie et activer les sélecteurs de trafic de basée sur la connexion de hello. Vous pouvez répéter hello même procédure tooadd plusieurs connexions tooadditional basée sur des stratégies VPN appareils locaux à partir de hello même passerelle VPN Azure.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Mettre à jour des sélecteurs de trafic basés sur des stratégies pour une connexion
dernière section de Hello vous montre comment les sélecteurs de trafic basé sur la stratégie tooupdate hello option pour une connexion VPN de S2S existante.

### <a name="1-get-hello-connection"></a>1. Obtenir la connexion de hello
Obtenir une ressource de connexion hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Hello du trafic basé sur la stratégie de sélecteurs option Vérifier
Hello ligne suivante indique si les sélecteurs de hello du trafic basé sur la stratégie sont utilisés pour la connexion de hello :

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Si la ligne de hello retourne «**True**», puis les sélecteurs de trafic basé sur la stratégie sont configurés sur la connexion de hello ; sinon, elle retourne «**False**. »

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Mettre à jour les sélecteurs de trafic basé sur une stratégie hello sur une connexion
Une fois que vous obtenez la ressource de connexion hello, vous pouvez activer ou désactiver l’option de hello.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Désactiver UsePolicyBasedTrafficSelectors
exemple Hello désactive option de sélecteurs hello du trafic basé sur la stratégie, mais laisse hello stratégie IPsec/IKE inchangé :

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Activer UsePolicyBasedTrafficSelectors
option de sélecteurs hello du trafic basé sur la stratégie active Hello exemple suivant, mais laisse hello stratégie IPsec/IKE inchangé :

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.

Pour en savoir plus sur les stratégies IPsec/IKE personnalisées, consultez [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuration d’une stratégie IPsec/IKE pour les connexions VPN S2S ou entre deux réseaux virtuels).
