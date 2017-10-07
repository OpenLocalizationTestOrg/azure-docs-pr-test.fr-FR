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
# <a name="about-vpn-gateway-configuration-settings"></a>À propos des paramètres de configuration de la passerelle VPN

Une passerelle VPN est un type de passerelle de réseau virtuel qui envoie le trafic chiffré entre votre réseau virtuel et votre emplacement local à travers une connexion publique. Vous pouvez également utiliser un trafic de toosend de passerelle VPN entre les réseaux virtuels entre hello backbone Azure.

Une connexion de passerelle VPN s’appuie sur la configuration hello de ressources, chacune contenant des paramètres configurables. sections de Hello dans cet article décrivent les ressources hello et les paramètres qui concernent la passerelle VPN de tooa pour un réseau virtuel créé dans le modèle de déploiement de gestionnaire de ressources. Vous pouvez trouver des descriptions et des diagrammes de topologie pour chaque solution connexion Bonjour [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) l’article.

## <a name="gwtype"></a>Types de passerelle

Chaque réseau virtuel ne peut posséder qu’une seule passerelle de réseau virtuel de chaque type. Lorsque vous créez une passerelle de réseau virtuel, il se peut que vous devez vous assurer que le type de passerelle hello est correcte pour votre configuration.

Hello les valeurs disponibles pour le type de passerelle - sont :

* Vpn
* ExpressRoute

Une passerelle VPN requiert hello `-GatewayType` *Vpn*.

Exemple :

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKU de passerelle

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Configurer la passerelle de hello référence (SKU)

#### <a name="azure-portal"></a>Portail Azure

Si vous utilisez hello toocreate portail Azure une passerelle de réseau virtuel du Gestionnaire de ressources, vous pouvez sélectionner la passerelle de hello référence (SKU) à l’aide du menu déroulant de hello. options de Hello avec que vous sont présentées correspondent toohello type de la passerelle et le type VPN que vous sélectionnez.

#### <a name="powershell"></a>PowerShell

exemple PowerShell suivant Hello spécifie hello `-GatewaySku` comme VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Modifier (redimensionner) une référence SKU de passerelle

Si vous souhaitez tooupgrade votre tooa de référence (SKU) de passerelle SKU plus puissant, vous pouvez utiliser hello `Resize-AzureRmVirtualNetworkGateway` applet de commande PowerShell. Vous pouvez également rétrograder taille hello de référence (SKU) de passerelle à l’aide de cette applet de commande.

Hello PowerShell l’exemple suivant montre qu'une passerelle SKU redimensionnée tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Types de connexion

Dans le modèle de déploiement du Gestionnaire de ressources hello, chaque configuration nécessite un type de connexion de passerelle de réseau virtuel spécifique. Hello PowerShell Gestionnaire de ressources disponibles les valeurs pour `-ConnectionType` sont :

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

Bonjour PowerShell l’exemple suivant, nous créer une connexion de S2S qui requiert le type de connexion hello *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Types de VPN

Lorsque vous créez la passerelle de réseau virtuel hello pour une configuration de passerelle VPN, vous devez spécifier un type VPN. Hello type VPN que vous choisissez dépend de la topologie de connexion hello que vous souhaitez toocreate. Par exemple, une connexion P2S nécessite un VPN de type basé sur un itinéraire. Un type VPN peut également dépendre de matériel hello que vous utilisez. Les configurations S2S nécessitent un périphérique VPN. Certains périphériques VPN seront ne prennent en charge qu’un certain type de VPN.

Hello type VPN que vous sélectionnez doit satisfaire toutes les exigences de connexion hello pour les solutions hello souhaité toocreate. Par exemple, si vous souhaitez toocreate une connexion de passerelle S2S VPN et une connexion de passerelle VPN de P2S pour hello même réseau virtuel, vous utiliseriez le type de VPN *RouteBased* car P2S nécessite un type RouteBased VPN. Vous devez également tooverify que votre périphérique VPN pris en charge une connexion VPN de RouteBased. 

Une fois qu’une passerelle de réseau virtuel a été créée, vous ne pouvez pas modifier le type de VPN hello. Vous avez toodelete hello passerelle de réseau virtuel et créez-en un nouveau. Il existe deux types de VPN :

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

exemple PowerShell suivant Hello spécifie hello `-VpnType` en tant que *RouteBased*. Lorsque vous créez une passerelle, vous devez vous assurer que hello - VpnType est correcte pour votre configuration.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Conditions requises de la passerelle

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Sous-réseau de passerelle

Avant de créer votre passerelle VPN, vous devez d’abord créer un sous-réseau de passerelle. sous-réseau de passerelle Hello contient des adresses IP hello cette passerelle de réseau virtuel hello machines virtuelles et services utilisent. Lorsque vous créez votre passerelle de réseau virtuel, lors passerelle machines virtuelles sont sous-réseau de passerelle toohello déployé et configuré avec les paramètres de la passerelle VPN hello requis. Vous ne devez jamais déployer sous-réseau de passerelle toohello n’importe quel autre (par exemple, les machines virtuelles supplémentaires). sous-réseau de passerelle Hello doit être nommé « GatewaySubnet » toowork correctement. Sous-réseau de passerelle hello d’affectation de noms « GatewaySubnet » permet Azure savoir qu’il est la passerelle de réseau virtuel hello hello sous-réseau toodeploy machines virtuelles et services.

Lorsque vous créez le sous-réseau de passerelle hello, vous spécifiez hello d’adresses IP qui hello sous-réseau contient. adresses IP de Hello dans le sous-réseau de passerelle hello sont des ordinateurs virtuels de passerelle toohello alloué et les services de la passerelle. Certaines configurations nécessitent plus d’adresses IP que d’autres. Consulter les instructions hello pour configuration hello que vous souhaitez toocreate et vérifiez que vous souhaitez toocreate le sous-réseau passerelle hello répondait à ces critères. En outre, vous souhaiterez toomake que votre sous-réseau de passerelle contient suffisamment IP adresses tooaccommodate possibles futures des configurations supplémentaires. Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau de passerelle de taille /28 ou supérieure (/28, /27, /26, etc.). De cette façon, si vous ajoutez des fonctionnalités Bonjour futures, vous n’ont tootear votre passerelle, puis supprimez et recréez tooallow de sous-réseau de passerelle hello pour plus d’adresses IP.

Hello exemple de gestionnaire de ressources PowerShell suivant montre un sous-réseau de passerelle nommé GatewaySubnet. Vous pouvez voir la notation CIDR hello spécifie un /27, ce qui permet de suffisamment d’adresses IP pour la plupart des configurations qui existent actuellement.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Passerelles de réseau local

Lorsque vous créez une configuration de passerelle VPN, passerelle de réseau local hello représente souvent votre emplacement local. Dans le modèle de déploiement classique de hello, passerelle de réseau local hello a tooas auxquels un Site Local. 

Vous donnez un nom à passerelle de réseau local hello hello adresse IP publique de l’appareil VPN local hello et spécifiez les préfixes d’adresse hello qui sont trouvent sur un emplacement local de hello. Azure examine les préfixes d’adresse de destination hello pour le trafic réseau, consulte configuration hello que vous avez spécifiées pour votre passerelle de réseau local et route les paquets en conséquence. Vous spécifiez également des passerelles de réseau local pour les configurations avec interconnexion de réseaux virtuels qui utilisent une connexion de passerelle VPN.

Hello l’exemple PowerShell suivant crée une nouvelle passerelle de réseau local :

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Vous avez parfois besoin de paramètres de passerelle du réseau local toomodify hello. Par exemple, lorsque vous ajoutez ou modifiez la plage d’adresses hello, ou si hello adresseIP du périphérique VPN de hello change. Pour un réseau virtuel classique, vous pouvez modifier ces paramètres dans le portail classique de hello sur la page de réseaux locaux hello. Pour Resource Manager, voir [Modification des paramètres de passerelle de réseau local à l’aide de PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>API REST et applets de commande PowerShell

Pour les ressources techniques supplémentaires en matière de syntaxe spécifique lors de l’utilisation des API REST, les applets de commande PowerShell ou CLI d’Azure pour les configurations de passerelle VPN, consultez hello suivant pages :

| **Classique** | **Gestionnaire de ressources** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [API REST](https://msdn.microsoft.com/library/jj154113) |[API REST](/rest/api/network/virtualnetworkgateways) |
| Non pris en charge | [Interface de ligne de commande Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les configurations de connexion disponible, consultez la rubrique [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).