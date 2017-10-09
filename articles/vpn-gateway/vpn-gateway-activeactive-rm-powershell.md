---
title: "Configurer des connexions VPN S2S en mode actif/actif pour des passerelles VPN : Azure Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de connexions en mode actif/actif avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Configurer des connexions VPN S2S en mode actif/actif avec des passerelles VPN Azure

Cet article vous assiste hello étapes toocreate actif entre différents locaux et les connexions au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>À propos des connexions intersites hautement disponibles
tooachieve haute disponibilité pour intersite et la connectivité de réseau virtuel à réseau virtuel, vous devez déployer plusieurs passerelles VPN et établir plusieurs connexions parallèles entre les réseaux Azure. Pour une vue d’ensemble des options de connectivité et de la topologie, voir [Configuration haute disponibilité pour la connectivité entre réseaux locaux et entre réseaux virtuels](vpn-gateway-highlyavailable.md) .

Cet article fournit des instructions de hello tooset d’un actif entre différents locaux connexion VPN et connexion actif entre deux réseaux virtuels :

* [Partie 1 : créer et configurer votre passerelle VPN Azure en mode actif/actif](#aagateway)
* [Partie 2 : établir des connexions intersites en mode actif/actif](#aacrossprem)
* [Partie 3 : établir des connexions de réseau virtuel à réseau virtuel en mode actif/actif](#aav2v)
* [Partie 4 : mettre à jour une passerelle existante entre les modes actif/actif et actif/passif](#aaupdate)

Vous pouvez combiner ces toobuild ensemble une topologie de réseau plus complexe, hautement disponible qui répond à vos besoins.

> [!IMPORTANT]
> Notez que le mode actif / actif hello utilise hello uniquement après les références (SKU) : 
  * VpnGw1, VpnGw2, VpnGw3
  * HigPerformance (pour les anciennes références héritées)
> 
> 

## <a name ="aagateway"></a>Partie 1 : créer et configurer des passerelles VPN en mode actif/actif
Hello suit va configurer votre passerelle VPN Azure dans les modes actif / actif. Hello principales différences entre les passerelles hello actif-actif et de type actif / passif :

* Vous devez toocreate les deux configurations IP de la passerelle avec deux adresses IP publiques
* Vous devez définir indicateur EnableActiveActiveFeature de hello
* passerelle de Hello référence (SKU) doit être VpnGw1, VpnGw2, VpnGw3 ou hautes performances (hérité SKU).

Hello autres propriétés sont hello même en tant que passerelles d’actif-actif hello. 

### <a name="before-you-begin"></a>Avant de commencer
* Assurez-vous de disposer d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Vous aurez besoin des applets de commande Azure Resource Manager PowerShell tooinstall hello. Consultez [vue d’ensemble de Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.

### <a name="step-1---create-and-configure-vnet1"></a>Étape 1 – Créer et configurer le réseau virtuel VNet1
#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables
Dans cet exercice, nous allons commencer par déclarer les variables. exemple Hello ci-dessous déclare les variables de hello en utilisant les valeurs de hello pour cet exercice. Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production. Vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration. Modifier les variables de hello, puis copiez et collez dans votre console PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources
Veillez à que basculer hello de toouse mode tooPowerShell applets de commande Gestionnaire de ressources. Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).

Ouvrez la console PowerShell et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Créer TestVNet1
exemple Hello ci-dessous crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux, GatewaySubnet appelée un, un frontal appelée et un appelée back-end. Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ». Si vous le nommez autrement, la création de votre passerelle échoue.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Étape 2 : créer la passerelle VPN de hello pour TestVNet1 avec le mode actif / actif
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Créer des adresses IP publiques hello et des configurations IP de passerelle
Demande deux public adresses toobe toohello alloué passerelle IP que vous allez créer pour votre réseau virtuel. Vous allez également définir les sous-réseaux hello et les configurations IP requis.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Créer la passerelle VPN hello configuration actif-actif
Créer la passerelle de réseau virtuel hello pour TestVNet1. Notez qu’il existe deux entrées GatewayIpConfig et hello EnableActiveActiveFeature indicateur est défini. Création d’une passerelle peut prendre un certain temps (45 minutes ou plus toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Obtenir les adresses IP publiques hello passerelle et une adresse IP d’homologue BGP de hello
Une fois que la passerelle de hello est créée, vous devez tooobtain hello BGP homologue adresseIP sur hello passerelle VPN à Azure. Cette adresse est nécessaire tooconfigure hello passerelle VPN à Azure comme une paire BGP pour les appareils de votre VPN sur site.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Utilisez hello suivant d’applets de commande tooshow hello deux adresses IP publiques allouées pour la passerelle VPN et leurs adresses IP d’homologue BGP correspondantes pour chaque instance de passerelle :

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

commande Hello d’adresses IP publiques de hello pour les instances de passerelle de hello et hello les adresses d’homologation BGP correspondantes sont hello identiques. Dans cet exemple, la passerelle de hello machine virtuelle avec l’adresse IP publique de 40.112.190.5 utilisera 10.12.255.4 comme adresse d’homologation BGP, et passerelle hello avec 138.91.156.129 utilisera 10.12.255.5. Ces informations sont nécessaires lorsque vous configurez votre local de la connexion de passerelle d’actif-actif toohello les périphériques VPN. passerelle de Hello est illustré dans le diagramme de hello ci-dessous avec toutes les adresses :

![active-active-gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Une fois hello passerelle créée, vous pouvez utiliser cette actif tooestablish passerelle entre différents locaux ou un réseau à connexion. les sections suivantes de Hello guidera hello étapes toocomplete hello exercice.

## <a name ="aacrossprem"></a>Partie 2 : établir une connexion intersite en mode actif/actif
tooestablish une connexion intersite, vous devez toocreate une passerelle de réseau Local de toorepresent votre périphérique VPN sur site et la passerelle VPN Azure tooconnect hello connexion avec la passerelle de réseau local hello. Dans cet exemple, la passerelle VPN Azure de hello est en mode actif-actif. Par conséquent, même s’il n'existe qu’un seul localement le périphérique VPN (passerelle de réseau local) et les ressources d’une seule connexion, les deux instances de passerelle VPN Azure établir les tunnels VPN de S2S avec l’appareil local de hello.

Avant de poursuivre, vérifiez que vous avez terminé la [Partie 1](#aagateway) de cet exercice.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Étape 1 : créer et configurer la passerelle de réseau local hello
#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables
Cet exercice continue configuration de hello toobuild hello illustrée. Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Quelques toonote des opérations relatives aux paramètres de passerelle de réseau local hello :

* passerelle de réseau local Hello peut être dans hello identiques ou différents emplacements et les ressources de groupe en tant que passerelle VPN de hello. Cet exemple montre les différents groupes de ressources, mais dans hello même emplacement.
* S’il n'existe qu’une seule unité VPN locale comme indiqué ci-dessus, connexion d’actif-actif hello pouvez travailler avec ou sans protocole BGP. Cet exemple utilise le protocole BGP pour la connexion intersite de hello.
* Si le protocole BGP est activé, préfixe hello vous devez toodeclare pour la passerelle de réseau local hello est adresse d’hôte hello de votre adresse IP d’homologue BGP sur votre périphérique VPN. Dans ce cas, il s’agit d’un préfixe /32 de « 10.52.255.253/32 ».
* À titre de rappel, vous devez utiliser différents ASN BGP entre vos réseaux locaux et le réseau virtuel Azure. Si elles sont hello même, vous devez toochange votre ASN VNet si votre périphérique VPN sur site utilise déjà hello ASN toopeer avec d’autres voisins BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Créer la passerelle de réseau local hello pour Site5
Avant de continuer, vérifiez que vous êtes toujours connectée tooSubscription 1. Créer le groupe de ressources hello s’il n’est pas encore créé.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Étape 2 : connexion de réseau local et la passerelle de réseau virtuel hello
#### <a name="1-get-hello-two-gateways"></a>1. Obtenir hello deux passerelles

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Créer hello TestVNet1 tooSite5 connexion
Dans cette étape, vous allez créer des connexions de hello de TestVNet1 tooSite5_1 avec cette « propriété » définie trop$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Paramètres VPN et BGP pour votre périphérique VPN local
exemple Hello ci-dessous répertorie les paramètres de hello que vous devrez entrer dans hello section de configuration BGP sur l’appareil VPN local pour cet exercice :

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - Préfixes tooannounce : (par exemple) 10.51.0.0/16 et 10.52.0.0/16
    - Azure VNet ASN       : 65010
    - Azure réseau virtuel BGP IP 1 : 10.12.255.4 pour tunnel too40.112.190.5
    - IP de BGP réseau virtuel Azure 2 : 10.12.255.5 pour tunnel too138.91.156.129
    - Itinéraires statiques : Destination 10.12.255.4/32, saut suivant hello VPN tunnel interface too40.112.190.5 Destination 10.12.255.5/32, saut suivant hello VPN tunnel interface too138.91.156.129
    - eBGP sauts multiples : Vérifiez l’option de « sauts multiples » hello pour eBGP est activé sur votre appareil si nécessaire

connexion de Hello doit être établie après que quelques minutes, de la session d’homologation BGP de hello démarrera une fois établie hello connexion IPsec. Cet exemple a configuré jusqu'à présent pas qu’un périphérique VPN local, aboutissant à un diagramme hello indiqué ci-dessous :

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Étape 3 : deux local VPN des appareils toohello actif VPN passerelle de connexion
Si vous avez deux périphériques VPN au hello même local réseau, vous pouvez obtenir une redondance double en connexion hello Azure toohello deuxième VPN périphérique de passerelle VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Créer un deuxième passerelle de réseau local hello pour Site5
Notez qu’adresse d’homologation BGP pour la passerelle de réseau local hello deuxième adresse IP de passerelle hello et préfixe d’adresse doivent se chevauchent pas avec la passerelle de réseau local précédente hello pour hello même local réseau.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Se connecter hello réseau virtuel et la passerelle hello deuxième réseau local
Créer des connexions de hello à partir de TestVNet1 tooSite5_2 avec cette « propriété » définie trop$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Paramètres VPN et BGP pour votre deuxième périphérique VPN local
De même, paramètres de hello listes ci-dessous, vous devrez entrer dans périphérique VPN de la deuxième hello :

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Une fois la connexion de hello (tunnels) sont établies, vous aurez deux périphériques VPN redondant et tunnels de connexion de votre réseau local et le Azure :

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Partie 3 : établir une connexion de réseau virtuel à réseau virtuel en mode actif/actif
Cette section décrit comment créer une connexion de réseau virtuel à réseau virtuel en mode actif/actif avec le protocole BGP. 

instructions Hello ci-dessous continuent des étapes précédentes de hello répertoriés ci-dessus. Vous devez effectuer [partie 1](#aagateway) toocreate hello passerelle VPN avec protocole BGP et configurer TestVNet1. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Étape 1 - créer TestVNet2 et hello la passerelle VPN
Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet2, ne se chevauche pas avec les plages de votre réseau virtuel.

Dans cet exemple, les réseaux virtuels hello appartiennent toohello même abonnement. Vous pouvez configurer des connexions de réseau virtuel à réseau virtuel entre différents abonnements ; reportez-vous trop[configurer une connexion réseau à](vpn-gateway-vnet-vnet-rm-ps.md) toolearn plus en détail. Assurez-vous que vous ajoutez hello »-cette propriété $True » lorsque la création d’hello connexions tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables
Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Créer TestVNet2 hello nouveau groupe de ressources

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Créer de passerelle VPN d’actif hello pour TestVNet2
Demande deux public adresses toobe toohello alloué passerelle IP que vous allez créer pour votre réseau virtuel. Vous allez également définir les sous-réseaux hello et les configurations IP requis.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Créer la passerelle VPN de hello hello comme nombre et hello indicateur de « EnableActiveActiveFeature ». Notez que vous devez remplacer la valeur par défaut de hello ASN vos passerelles VPN Azure. Hello homologations pour hello connectés à des réseaux virtuels doivent être différents tooenable BGP et le routage de transit.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Étape 2 : se connecter les passerelles TestVNet1 et TestVNet2 hello
Dans cet exemple, les deux passerelles sont Bonjour même abonnement. Vous pouvez effectuer cette étape Bonjour même session PowerShell.

#### <a name="1-get-both-gateways"></a>1. Accéder aux deux passerelles
Assurez-vous de vous connecter et connectez tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Créer les deux connexions
Dans cette étape, vous allez créer une connexion hello de TestVNet1 tooTestVNet2, hello de TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Être tooenable que BGP pour les deux connexions.
> 
> 

Après avoir effectué ces étapes, les connexions hello établit dans quelques minutes et session d’homologation BGP de hello seront d’une fois la connexion de hello au réseau s’est terminée avec redondance double :

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Partie 4 : mettre à jour une passerelle existante entre les modes actif/actif et actif/passif
dernière section de Hello décrivent comment vous pouvez configurer une passerelle VPN Azure existante à partir du mode tooactive active de type actif / passif, ou vice versa.

> [!NOTE]
> Cette section inclut hello étapes tooresize une référence (SKU) hérité (ancienne version) d’une passerelle VPN déjà créée à partir de tooHighPerformance Standard. Ces étapes ne mettez pas à niveau un ancien tooone de référence (SKU) hérité de hello nouvelles références SKU.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Configurer une passerelle de tooactive-active de type actif / passif
#### <a name="1-gateway-parameters"></a>1. Paramètres de passerelle
Bonjour à l’exemple suivant convertit une passerelle de type actif / passif une passerelle d’actif-actif. Vous devez toocreate une autre adresse IP publique, puis ajoutez une deuxième configuration IP de la passerelle. Ci-dessous montre hello paramètres utilisés :

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Créer une adresse IP publique hello, puis ajouter hello deuxième passerelle IP configuration

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Activer la passerelle de hello de mise à jour et en mode actif / actif
Vous devez définir l’objet de passerelle hello dans la mise à jour réelle PowerShell tootrigger hello. Hello référence (SKU) de la passerelle de réseau virtuel hello doit également être modifié tooHighPerformance (redimensionnée), car il a été créé précédemment comme norme.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Cette mise à jour peut prendre 30 minutes too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Configurer une passerelle de secours tooactive actif-actif
#### <a name="1-gateway-parameters"></a>1. Paramètres de passerelle
Utilisez hello même paramètres comme indiqué ci-dessus, obtenir le nom de hello de hello IP configuration tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Supprimer la configuration IP de passerelle hello et désactiver le mode actif / actif hello
De même, vous devez définir objet de passerelle hello dans la mise à jour réelle PowerShell tootrigger hello.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Cette mise à jour peut prendre too30 trop 45 minutes.

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.
