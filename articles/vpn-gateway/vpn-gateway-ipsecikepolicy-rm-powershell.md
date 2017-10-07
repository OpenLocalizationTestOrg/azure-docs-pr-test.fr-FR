---
title: "Configurer la stratégie IPSec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel : Azure Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de stratégie IPSec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel

Cet article vous guide tout au long des étapes de hello tooconfigure stratégie IPsec/IKE pour les connexions VPN de Site à Site ou au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.

## <a name="about"></a>À propos des paramètres de stratégie IPsec et IKE pour les passerelles VPN Azure
La norme de protocole IPsec et IKE standard prend en charge un vaste éventail d’algorithmes de chiffrement dans différentes combinaisons. Consultez trop[sur les exigences de chiffrement et les passerelles VPN Azure](vpn-gateway-about-compliance-crypto.md) toosee comment cela peut aider à s’assurer qu’entre différents locaux et connectivité de réseau pour satisfaire vos exigences de conformité ou la sécurité.

Cet article fournit des instructions toocreate et configurer une stratégie IPsec/IKE et appliquer la connexion existante ou nouvelle de tooa :

* [Partie 1 - toocreate de flux de travail et de définir la stratégie IPsec/IKE](#workflow)
* [Partie 2 : algorithmes de chiffrement pris en charge et avantages clés](#params)
* [Partie 3 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE](#crossprem)
* [Partie 4 : création d’une connexion de réseau virtuel à réseau virtuel avec une stratégie IPsec/IKE](#vnet2vnet)
* [Partie 5 : gestion (créer, ajouter, supprimer) de la stratégie IPsec/IKE pour une connexion](#managepolicy)

> [!IMPORTANT]
> 1. Notez que les stratégies IPsec/IKE ne fonctionnement que sur hello suivant SKU de passerelle :
>    * ***VpnGw1, VpnGw2, VpnGw3*** (basée sur le routage)
>    * ***Standard*** et ***HighPerformance*** (basée sur le routage)
> 2. Vous pouvez uniquement spécifier ***une*** combinaison de stratégie pour une connexion donnée.
> 3. Vous devez spécifier tous les algorithmes et paramètres pour IKE (mode principal) et IPsec (mode rapide). Vous n’êtes pas en droit de spécifier de stratégie partielle.
> 4. Consultez vos spécifications de fournisseur de périphérique VPN stratégie de hello tooensure est pris en charge sur les appareils de votre VPN sur site. S2S ou des connexions de réseau virtuel à réseau virtuel ne peut pas établir si les stratégies hello ne sont pas compatibles.

## <a name ="workflow"></a>Partie 1 - toocreate de flux de travail et de définir la stratégie IPsec/IKE
Cette section souligne hello toocreate et mise à jour IPsec/IKE stratégie de workflow sur une connexion VPN de S2S ou de réseau virtuel à réseau virtuel :
1. créer un réseau virtuel et une passerelle VPN ;
2. créer une passerelle de réseau local pour une connexion entre sites locaux, ou un autre réseau virtuel et une passerelle pour une connexion de réseau virtuel à réseau virtuel ;
3. créer une stratégie IPsec/IKE avec des algorithmes et paramètres sélectionnés ;
4. Créer une connexion (IPsec ou VNet2VNet) avec la stratégie IPsec/IKE de hello
5. ajouter/mettre à jour/supprimer une stratégie IPsec/IKE pour une connexion existante.

instructions Hello dans cet article vous aide à installer et configurer des stratégies IPsec/IKE comme indiqué dans le diagramme de hello :

![stratégie IPSec/IKE](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Partie 2 : algorithmes de chiffrement pris en charge et avantages clés

Hello tableau suivant répertorie les algorithmes de chiffrement pris en charge de hello et atouts configurables par les clients de hello :

| **IPsec/IKEv2**  | **Options**    |
| ---  | --- 
| Chiffrement IKEv2 | AES256, AES192, AES128, DES3, DES  
| Intégrité IKEv2  | SHA384, SHA256, SHA1, MD5  |
| Groupe DH         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, Aucun |
| Chiffrement IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Aucun    |
| Intégrité IPsec  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| Groupe PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Aucun 
| Durée de vie de l’AS en mode rapide   | (**Facultatif** : les valeurs par défaut sont utilisées si aucun valeur n’est indiquée)<br>Secondes (entier ; **min 300**  /par défaut 27 000 secondes)<br>Kilo-octets (entier ; **min 1 024**  /par défaut 102 400 000 Ko)   |
| Sélecteur de trafic | UsePolicyBasedTrafficSelectors** ($True/$False ; **facultatif**, $False par défaut si aucune valeur n’est indiquée)    |
|  |  |

> [!IMPORTANT]
> 1. **Si GCMAES est utilisé pour l’algorithme de chiffrement d’IPsec, vous devez sélectionner hello même algorithme GCMAES et la longueur de clé pour l’intégrité IPsec ; par exemple, à l’aide de GCMAES128 pour les deux**
> 2. Durée de vie de SA de Mode principal IKEv2 est fixée à 28 800 secondes sur les passerelles VPN Azure hello
> 3. Définition de « UsePolicyBasedTrafficSelectors » trop$ True sur une connexion configurera hello VPN Azure passerelle tooconnect toopolicy pare-feu basé sur VPN sur site. Si vous activez PolicyBasedTrafficSelectors, vous devez tooensure que votre périphérique VPN a défini toutes les combinaisons de vos préfixes de (passerelle de réseau local) de réseau local à partir de préfixes de réseau virtuel Azure hello, les sélecteurs le trafic correspondant hello au lieu de tout. Par exemple, si les préfixes de votre réseau local sont 10.1.0.0/16 et 10.2.0.0/16, et les préfixes de votre réseau virtuel sont 192.168.0.0/16 et 172.16.0.0/16, vous devez hello toospecify suivant des sélecteurs de trafic :
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

Pour plus d’informations sur les sélecteurs de trafic basés sur une stratégie, voir [Connecter plusieurs périphériques VPN basés sur une stratégie locale](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Hello tableau ci-dessous répertorie hello groupes Diffie-Hellman correspondants pris en charge par la stratégie personnalisée de hello :

| **Groupe Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Longueur de clé** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | MODP 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP 1 024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP 2 048 bits  |
| 19                        | ECP256                   | ECP256       | ECP 256 bits    |
| 20                        | ECP384                   | ECP284       | ECP 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP 2 048 bits  |

Consultez trop[RFC3526](https://tools.ietf.org/html/rfc3526) et [RFC5114](https://tools.ietf.org/html/rfc5114) pour plus d’informations.

## <a name ="crossprem"></a>Partie 3 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE

Cette section vous guide tout au long des étapes de création d’une connexion VPN de S2S avec une stratégie IPsec/IKE de hello. Hello suit crée hello connexion comme indiqué dans le diagramme de hello :

![stratégie S2S](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Pour des instructions détaillées concernant la création d’une connexion VPN S2S, voir [Créer une connexion VPN S2S](vpn-gateway-create-site-to-site-rm-powershell.md).

### <a name="before"></a>Avant de commencer

* Assurez-vous de disposer d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Installer les applets de commande Azure Resource Manager PowerShell hello. Consultez [vue d’ensemble de Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.

### <a name="createvnet1"></a>Étape 1 : créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local

#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources

Veillez à que basculer hello de toouse mode tooPowerShell applets de commande Gestionnaire de ressources. Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).

Ouvrez la console PowerShell et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local

Hello suivant l’exemple crée un réseau virtuel hello, TestVNet1, avec trois sous-réseaux et de passerelle VPN de hello. Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ». Si vous le nommez autrement, la création de votre passerelle échoue.

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

### <a name="s2sconnection"></a>Étape 2 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Créez une stratégie IPsec/IKE.

Hello script de l’exemple suivant crée une stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Si vous utilisez GCMAES pour IPsec, vous devez utiliser hello le même algorithme GCMAES et la longueur de clé de chiffrement de sécurité IPsec et l’intégrité, par exemple :

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Créer un réseau VPN S2S hello avec hello stratégie IPsec/IKE

Créer un réseau VPN S2S et appliquer la stratégie IPsec/IKE de hello créé précédemment.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Vous pouvez éventuellement ajouter «-UsePolicyBasedTrafficSelectors $True » toohello créer connexion applet de commande tooenable VPN Azure passerelle tooconnect toopolicy VPN périphériques basés sur local, comme décrit ci-dessus.

> [!IMPORTANT]
> Une fois qu’une stratégie IPsec/IKE est spécifiée sur une connexion, passerelle VPN Azure de hello sera uniquement envoyer ou accepter hello IPsec/IKE avec les algorithmes de chiffrement spécifiés et des avantages clés sur cette connexion particulière. Assurez-vous que votre appareil VPN locaux pour la connexion de hello utilise ou accepte une combinaison de stratégie exacte hello, sinon tunnel de VPN de S2S hello établira pas.


## <a name ="vnet2vnet"></a>Partie 4 : création d’une connexion de réseau virtuel à réseau virtuel avec une stratégie IPsec/IKE

étapes de Hello de création d’une connexion au réseau avec une stratégie IPsec/IKE sont similaires toothat d’une connexion VPN de S2S. Hello exemples de scripts suivants créent hello connexion comme indiqué dans le diagramme de hello :

![Stratégie de réseau virtuel à réseau virtuel](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Pour plus d’informations sur les étapes de création d’une connexion de réseau virtuel à réseau virtuel, voir [Créer une connexion de réseau virtuel à réseau virtuel](vpn-gateway-vnet-vnet-rm-ps.md). Vous devez effectuer [partie 3](#crossprem) toocreate hello passerelle VPN et configurer TestVNet1.

### <a name="createvnet2"></a>Étape 1 : créer le réseau virtuel deuxième de hello et passerelle VPN

#### <a name="1-declare-your-variables"></a>1. Déclarer vos variables

Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Créer des réseaux deuxième hello et passerelle VPN dans le nouveau groupe de ressources hello

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Étape 2 : créer une connexion de réseau virtuel-toVNet avec hello stratégie IPsec/IKE

Toohello similaire réseau VPN S2S, créer une stratégie IPsec/IKE, puis appliquer les toopolicy toohello nouvelle connexion.

#### <a name="1-create-an-ipsecike-policy"></a>1. Créez une stratégie IPsec/IKE.

Hello script de l’exemple suivant crée une autre stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. Créer des connexions de réseau virtuel à réseau virtuel avec hello stratégie IPsec/IKE

Créer une connexion au réseau et appliquer la stratégie IPsec/IKE de hello que vous avez créé. Dans cet exemple, les deux passerelles sont Bonjour même abonnement. Il est donc possible toocreate et configurez les deux connexions avec hello même stratégie IPsec/IKE Bonjour même session PowerShell.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Une fois qu’une stratégie IPsec/IKE est spécifiée sur une connexion, passerelle VPN Azure de hello sera uniquement envoyer ou accepter hello IPsec/IKE avec les algorithmes de chiffrement spécifiés et des avantages clés sur cette connexion particulière. Vérifiez que hello stratégies IPsec pour les deux connexions sont hello identiques, sinon établit pas la connexion au réseau.

Après avoir effectué ces étapes, hello est établie dans quelques minutes, et vous aurez hello suivant la topologie du réseau comme indiqué dans le début de hello :

![stratégie IPSec/IKE](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Partie 5 : mise à jour de la stratégie IPsec/IKE pour une connexion

dernière section de Hello vous montre comment toomanage stratégie IPsec/IKE pour une connexion existante de S2S ou au réseau. exercice Hello ci-dessous vous guide tout au long de hello opérations sur une connexion suivantes :

1. Afficher la stratégie IPsec/IKE de hello d’une connexion
2. Ajouter ou mettre à jour hello IPsec/IKE stratégie tooa connexion
3. Supprimer la stratégie IPsec/IKE de hello à partir d’une connexion

Hello même procédure s’applique tooboth S2S et les connexions de réseau virtuel à réseau virtuel.

> [!IMPORTANT]
> Une stratégie IPsec/IKE est prise en charge uniquement sur des passerelles VPN *Standard* et *HighPerformance* basées sur itinéraires. Il ne fonctionne pas sur la passerelle de base hello référence (SKU) ou une passerelle VPN basée sur des stratégies hello.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Afficher la stratégie IPsec/IKE de hello d’une connexion

Bonjour à l’exemple suivant montre comment tooget hello stratégie IPsec/IKE configuré sur une connexion. les scripts Hello également continuent à partir des exercices hello ci-dessus.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

la dernière commande Hello répertorie la stratégie IPsec/IKE actuelle hello configuré sur la connexion de hello, s’il en existe une. Hello suivant le résultat de l’exemple est pour la connexion de hello :

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

S’il n’existe aucune stratégie IPsec/IKE configuré, hello commande (PS > $connection6.policy) Obtient vide retour. Cela ne signifie pas IPsec/IKE n’est pas configuré sur la connexion de hello, mais qu’il n’existe aucune stratégie IPsec/IKE personnalisée. connexion réelle de Hello utilise une stratégie de valeur par défaut hello négocié entre votre périphérique VPN sur site et la passerelle VPN Azure de hello.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Ajouter ou mettre à jour une stratégie IPsec/IKE pour une connexion

les étapes Hello tooadd une nouvelle stratégie ou mise à jour une stratégie existante sur une connexion sont hello même : créer une nouvelle stratégie, puis appliquer la nouvelle connexion de toohello stratégie hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable « UsePolicyBasedTrafficSelectors » lors de la connexion tooan basée sur des stratégies VPN appareil local, ajoutez hello »-UsePolicyBaseTrafficSelectors « paramètre toohello applet de commande, ou définissez-la trop option de hello $False toodisable :

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Vous pouvez obtenir la connexion de hello toocheck à nouveau si la mise à jour de stratégie de hello.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Vous devez voir la sortie hello à partir de la dernière ligne de hello, comme indiqué dans hello l’exemple suivant :

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Supprimer une stratégie IPsec/IKE d’une connexion

Lorsque vous supprimez une connexion de stratégie personnalisée de hello, passerelle VPN Azure de hello revient arrière toohello [liste par défaut des propositions de IPsec/IKE](vpn-gateway-about-vpn-devices.md) et renégocie à nouveau avec votre périphérique VPN sur site.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

Vous pouvez utiliser hello toocheck de script même si la stratégie de hello a été supprimée à partir de la connexion de hello.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les sélecteurs de trafic basés sur une stratégie, voir [Connecter plusieurs périphériques VPN basés sur un stratégie locale](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.
