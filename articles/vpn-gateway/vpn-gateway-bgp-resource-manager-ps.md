---
title: "Configurer BGP sur des passerelles VPN Azure : Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de BGP avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Comment tooconfigure BGP sur les passerelles VPN Azure à l’aide de PowerShell
Cet article vous assiste hello étapes tooenable BGP sur une connexion de Site à Site (S2S) VPN intersite et une connexion au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.

## <a name="about-bgp"></a>À propos du protocole BGP
BGP est hello protocole de routage standard couramment utilisé dans hello Internet tooexchange routage et l’accessibilité des informations entre deux ou plusieurs réseaux. Protocole BGP permet les passerelles VPN Azure hello et vos périphériques VPN local, appelés homologues BGP ou voisins, tooexchange « itinéraires » informe les deux passerelles sur la disponibilité de hello et l’accessibilité pour les préfixes toogo via des passerelles de hello ou routeurs impliqués. Protocole BGP peut également activer le routage de transit entre plusieurs réseaux en propageant les itinéraires une passerelle BGP apprend à partir d’un tooall d’homologue BGP autres homologues BGP.

Consultez [vue d’ensemble du protocole BGP avec les passerelles VPN Azure](vpn-gateway-bgp-overview.md) pour plus d’informations sur les avantages du protocole BGP et toounderstand hello technique configuration requise et considérations relatives à l’aide du protocole BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Prise en main de BGP sur les passerelles VPN Azure

Cet article vous guide tout au long de hello de toodo étapes hello tâches suivantes :

* [Partie 1 - Activer BGP sur votre passerelle VPN Azure](#enablebgp)
* [Partie 2 - Établir une connexion intersite avec BGP](#crossprembgp)
* [Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP](#v2vbgp)

Chaque partie d’instructions de hello constitue un bloc de construction de base pour activer BGP de la connectivité réseau. Si vous effectuez toutes les trois parties, vous créez une topologie de hello comme indiqué dans hello suivant schéma :

![Topologie BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Vous pouvez combiner des parties de toobuild ensemble un réseau de transit plus complexes, cascade, qui répond à vos besoins.

## <a name ="enablebgp"></a>Partie 1 : configurer le protocole BGP sur hello passerelle VPN à Azure
étapes de configuration Hello configurer hello paramètres BGP de la passerelle VPN Azure de hello comme indiqué dans hello suivant schéma :

![Passerelle BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Avant de commencer
* Assurez-vous de disposer d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Installer les applets de commande Azure Resource Manager PowerShell hello. Pour plus d’informations sur l’installation des applets de commande PowerShell hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Étape 1 – Créer et configurer le réseau virtuel VNet1
#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables
Dans cet exercice, nous allons commencer par déclarer les variables. Hello exemple suivant déclare les variables hello en utilisant les valeurs de hello pour cet exercice. Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production. Vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration. Modifier les variables de hello, puis copiez et collez dans votre console PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources
toouse hello applets de commande Gestionnaire de ressources, veillez à basculer en mode de tooPowerShell. Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).

Ouvrez la console PowerShell et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Créer TestVNet1
Hello exemple suivant crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux, GatewaySubnet appelée un, un frontal appelée et un appelée back-end. Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ». Si vous le nommez autrement, la création de votre passerelle échoue.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Étape 2 : créer hello passerelle VPN pour TestVNet1 avec des paramètres de protocole BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Créer des configurations IP et le sous-réseau hello
Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel. Vous allez également définir le sous-réseau de hello requis et les configurations IP.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Créer la passerelle VPN hello hello en tant que nombre
Créer la passerelle de réseau virtuel hello pour TestVNet1. BGP requiert une basée sur un itinéraire passerelle VPN et également hello Ajout paramètre, - Asn tooset hello ASN (en tant que nombre) pour TestVNet1. Si vous ne définissez pas de paramètre ASN hello, ASN 65515 est affecté. Création d’une passerelle peut prendre un certain temps (30 minutes ou plus toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Obtenir hello Azure BGP homologue IP adresse
Une fois que la passerelle de hello est créée, vous devez tooobtain hello BGP homologue adresseIP sur hello passerelle VPN à Azure. Cette adresse est nécessaire tooconfigure hello passerelle VPN à Azure comme une paire BGP pour les appareils de votre VPN sur site.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

la dernière commande Hello montre des configurations de protocole BGP correspondantes de hello sur hello passerelle VPN à Azure ; par exemple :

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Une fois que la passerelle de hello est créée, vous pouvez utiliser cette passerelle tooestablish entre différents locaux ou réseau à connexion avec BGP. Hello sections suivantes guident hello étapes toocomplete hello exercice.

## <a name ="crossprembbgp"></a>Partie 2 - Établir une connexion intersite avec BGP

tooestablish une connexion intersite, vous devez toocreate une passerelle de réseau Local de toorepresent votre périphérique VPN sur site et la passerelle VPN tooconnect hello connexion avec la passerelle de réseau local hello. Lorsqu’il existe des articles qui vous guident tout au long de ces étapes, cet article contient des paramètres de configuration hello des propriétés supplémentaires requis toospecify hello BGP.

![BGP pour une connexion intersite](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Avant de poursuivre, vérifiez que vous avez terminé la [Partie 1](#enablebgp) de cet exercice.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Étape 1 : créer et configurer la passerelle de réseau local hello

#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables

Cet exercice continue de configuration de hello toobuild hello illustrée. Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Quelques toonote des opérations relatives aux paramètres de passerelle de réseau local hello :

* passerelle de réseau local Hello peut être dans hello identiques ou différents emplacements et les ressources de groupe en tant que passerelle VPN de hello. Cet exemple les montre dans différents groupes de ressources situés dans différents emplacements.
* préfixe de minimale Hello nécessaire toodeclare pour la passerelle de réseau local hello est l’adresse d’hôte de hello de votre adresse IP d’homologue BGP sur votre périphérique VPN. Dans ce cas, c’est un préfixe /32 de « 10.52.255.254/32 ».
* À titre de rappel, vous devez utiliser différents ASN BGP entre vos réseaux locaux et le réseau virtuel Azure. Si elles sont hello même, vous devez toochange votre ASN VNet si votre périphérique VPN sur site utilise déjà hello ASN toopeer avec d’autres voisins BGP.

Avant de continuer, assurez-vous que vous êtes toujours connectée tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Créer la passerelle de réseau local hello pour Site5

Être sûr de groupe de ressources hello toocreate s’il n'est pas créé, avant de créer de passerelle de réseau local hello. Notez hello deux des paramètres supplémentaires pour la passerelle de réseau local hello : Asn et BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Étape 2 : connexion de réseau local et la passerelle de réseau virtuel hello

#### <a name="1-get-hello-two-gateways"></a>1. Obtenir hello deux passerelles

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Créer hello TestVNet1 tooSite5 connexion

Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooSite5. Vous devez spécifier «-cette propriété $True » tooenable BGP pour cette connexion. Comme indiqué précédemment, il est possible de toohave connexions BGP et non-BGP pour hello même passerelle VPN à Azure. À moins que le protocole BGP est activé dans la propriété de connexion hello, Azure n’active pas BGP pour cette connexion même si les paramètres BGP sont déjà configurés sur les deux passerelles.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Hello exemple suivant répertorie les paramètres de hello que vous entrez dans la section de configuration BGP de hello sur l’appareil VPN local pour cet exercice :

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Hello est établie après quelques minutes et le démarrage de session d’homologation hello BGP une fois établie hello connexion IPsec.

## <a name ="v2vbgp"></a>Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP

Cette section ajoute une connexion au réseau avec protocole BGP, comme indiqué dans hello suivant schéma :

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

continue de Hello suivant les instructions des étapes précédentes de hello. Vous devez effectuer [partie I](#enablebgp) toocreate hello passerelle VPN avec protocole BGP et configurer TestVNet1. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Étape 1 - créer TestVNet2 et hello la passerelle VPN

Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet2, ne se chevauche pas avec les plages de votre réseau virtuel.

Dans cet exemple, les réseaux virtuels hello appartiennent toohello même abonnement. Vous pouvez configurer les connexions de réseau virtuel à réseau virtuel entre différents abonnements. Pour plus d'informations, voir [Configurer une connexion de réseau virtuel à réseau virtuel](vpn-gateway-vnet-vnet-rm-ps.md). Assurez-vous que vous ajoutez hello »-cette propriété $True » lorsque la création d’hello connexions tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables

Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Créer la passerelle VPN de hello pour TestVNet2 avec des paramètres de protocole BGP

Demander une publique IP adresse toobe toohello alloué passerelle vous allez créer pour votre réseau virtuel et définissez le sous-réseau de hello requis et les configurations IP.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Créer la passerelle VPN hello hello en tant que nombre. Vous devez remplacer la valeur par défaut de hello ASN vos passerelles VPN Azure. Hello homologations pour hello connectés à des réseaux virtuels doivent être différents tooenable BGP et le routage de transit.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

Dans cette étape, vous créer connexion hello de TestVNet1 tooTestVNet2, hello de TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Être tooenable que BGP pour les deux connexions.
> 
> 

Après avoir effectué ces étapes, hello est établie après quelques minutes. session d’homologation BGP de Hello est une fois hello réseau à connexion terminée.

Une fois tous les trois parties de cet exercice, vous avez établi hello suivant la topologie du réseau :

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Étapes suivantes

Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.
