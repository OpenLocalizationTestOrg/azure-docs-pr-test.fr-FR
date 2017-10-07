---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : PowerShell | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell

Cet article explique comment toouse connexion de passerelle PowerShell toocreate un Site à Site VPN à partir de votre site réseau toohello réseau virtuel. étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portail Classic (classique)](vpn-gateway-site-to-site-create.md)
> 
>


Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe. Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Avant de commencer

Vérifiez que vous avez rempli hello suivant des critères avant de commencer votre configuration :

* Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il. Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).
* Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.
* Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous. Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour. Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.
* Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure. Applets de commande PowerShell sont fréquemment mis à jour et vous en aurez besoin tooupdate votre PowerShell applets de commande tooget hello dernières fonctionnalités. Si vous ne mettez à jour vos applets de commande PowerShell, les valeurs hello spécifiées peuvent échouer. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur le téléchargement et installation des applets de commande PowerShell.

### <a name="example"></a>Exemples de valeurs

exemples de Hello dans cet article utilisent hello valeurs suivantes. Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Se connecter tooyour abonnement

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Créer un réseau virtuel et un sous-réseau de passerelle

Si vous n’avez pas de réseau virtuel, créez-en un. Lorsque vous créez un réseau virtuel, assurez-vous que vous spécifiez des espaces d’adressage hello ne chevauchent pas hello d’espaces d’adressage que vous disposez sur votre réseau local.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate un réseau virtuel et un sous-réseau de passerelle

Cet exemple permet de créer un réseau virtuel et un sous-réseau de passerelle. Si vous disposez déjà d’un réseau virtuel que vous devez tooadd un sous-réseau de passerelle pour voir [tooadd un réseau virtuel tooa sous-réseau passerelle que vous avez déjà créé](#gatewaysubnet).

Créez un groupe de ressources :

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Créez votre réseau virtuel.

1. Définir les variables de hello.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Créer hello réseau virtuel.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd un réseau virtuel de tooa de sous-réseau de passerelle que vous avez déjà créé

1. Définir les variables de hello.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Créer un sous-réseau de passerelle hello.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Définir la configuration hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Créer une passerelle de réseau local hello

passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour. Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion. Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway. vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local. Si votre réseau local change, vous pouvez facilement mettre à jour les préfixes hello.

Utilisez hello valeurs suivantes :

* Hello *GatewayIPAddress* est l’adresse IP de hello de votre périphérique VPN sur site. Votre périphérique VPN ne peut pas se trouver derrière un NAT.
* Hello *AddressPrefix* est votre site sur l’espace d’adressage.

tooadd une passerelle de réseau local avec un préfixe d’adresse unique :

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd une passerelle de réseau local avec plusieurs préfixes d’adresses :

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify les préfixes d’adresse IP de la passerelle de réseau local :<br>
Parfois, les préfixes de votre passerelle de réseau local changent. Hello vous étapes toomodify votre adresse IP préfixes varient selon que vous avez créé une connexion de passerelle VPN. Consultez hello [modifier les préfixes d’adresse d’une passerelle de réseau local](#modify) section de cet article.

## <a name="PublicIP"></a>4. Demander une adresse IP publique

Une passerelle VPN doit avoir une adresse IP publique. Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel. adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello. Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*. Vous ne pouvez pas demander d’affectation d’adresse IP publique statique. Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour. Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé. Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.

Demander une adresse IP publique qui sera assignée tooyour de réseau virtuel passerelle VPN.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Créer la configuration d’adressage IP de la passerelle hello

configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello. Utilisez hello suivant exemple toocreate votre configuration de la passerelle :

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Créer une passerelle VPN de hello

Créer la passerelle VPN de réseau virtuel hello. Création d’une passerelle VPN peut prendre jusqu'à too45 minutes ou plus toocomplete.

Utilisez hello valeurs suivantes :

* Hello *- le type de passerelle* pour un Site à Site est configuration *Vpn*. type de passerelle Hello est toujours configuration toohello spécifique que vous implémentez. Par exemple, d’autres configurations de passerelle peuvent nécessiter GatewayType ExpressRoute.
* Hello *- VpnType* peut être *RouteBased* (appelée tooas une passerelle dynamique dans certains documents), ou *basée sur des stratégies* (appelée tooas une passerelle statique dans la documentation ). Pour plus d’informations sur les types de passerelles VPN, consultez [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).
* Sélectionnez hello SKU de passerelle que vous souhaitez toouse. Des limites de configuration s’appliquent à certaines références (SKU). Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Si vous obtenez une erreur lors de la création de passerelle VPN de hello concernant hello - GatewaySku, vérifiez que vous avez installé la version la plus récente des applets de commande PowerShell hello hello.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Configuration de votre périphérique VPN

Réseau local de tooan connexions site à Site requièrent un périphérique VPN. Dans cette étape, vous configurez votre périphérique VPN. Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :

- Une clé partagée. Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site. Dans nos exemples, nous utilisons une clé partagée basique. Nous conseillons de générer un toouse de clé plus complexe.
- Hello adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI. hello toofind adresse IP publique de votre passerelle de réseau virtuel à l’aide de PowerShell, hello d’utiliser l’exemple suivant :

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Créer la connexion VPN de hello

Ensuite, créez hello VPN de Site à Site connexion entre votre passerelle de réseau virtuel et votre périphérique VPN. Être des valeurs de hello tooreplace que par les vôtres. clé partagée de Hello doit correspondre à valeur hello que vous avez utilisé pour la configuration de votre périphérique VPN. Notez que hello '-ConnectionType' pour le Site à Site est *IPsec*.

1. Définir les variables de hello.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Créer la connexion de hello.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Après quelques instants, hello connexion sera établie.

## <a name="toverify"></a>9. Vérifiez la connexion VPN de hello

Il existe quelques façons tooverify votre connexion VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>machine virtuelle de tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modifier des préfixes d’adresses IP d’une passerelle de réseau local

Si vous changez de préfixes d’adresses IP hello souhaité routé emplacement local de tooyour, vous pouvez modifier la passerelle de réseau local hello. Deux ensembles d’instructions vous sont fournis : instructions Hello que vous choisissez dépendant de si vous avez déjà créé votre connexion de passerelle.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modifier l’adresse IP de passerelle hello pour une passerelle de réseau local

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Étapes suivantes

*  Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
