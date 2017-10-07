---
title: "passerelle de réseau virtuel Azure aaaLegacy références (SKU) | Documents Microsoft"
description: "Anciennes références SKU de passerelle de réseau virtuel."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Utilisation des références SKU de passerelle de réseau virtuel (anciennes références SKU)

Cet article contient des informations sur hello hérité (ancienne) passerelle de réseau virtuel références (SKU). hérité de Hello références (SKU) continueront de fonctionner dans les deux modèles de déploiement pour les passerelles VPN qui ont déjà été créés. Les passerelles VPN classiques continuer toouse hello hérité références (SKU), aussi bien pour les passerelles existantes et nouvelles passerelles. Lors de la création des passerelles VPN de nouveau gestionnaire de ressources, utilisez la passerelle hello références (SKU). Pour plus d’informations sur hello nouvelles références SKU, consultez [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>SKU de passerelle

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Débit agrégé estimé par SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Configurations prises en charge par référence SKU et type de VPN

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Redimensionner une passerelle (modifier la référence SKU d’une passerelle)

Vous pouvez redimensionner une référence (SKU) de passerelle dans hello même famille de référence (SKU). Par exemple, si vous avez une référence (SKU) Standard, vous pouvez redimensionner tooa HighPerformance SKU. Vous ne pouvez pas redimensionner votre VPN entre les passerelles hello anciennes références (SKU) et hello nouvelles familles de référence (SKU). Par exemple, vous ne peut pas accéder à partir d’un tooa de référence (SKU) Standard VpnGw2 référence (SKU). 

tooresize une passerelle référence (SKU) pour le modèle de déploiement classique de hello, hello utilisez commande suivante :

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize une référence (SKU) de la passerelle pour hello modèle de déploiement du Gestionnaire de ressources, utilisez hello de commande suivante :

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Migrer toohello nouvelle passerelle références (SKU)

Si vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello, vous pouvez migrer toohello nouvelle passerelle références (SKU). Si vous travaillez avec un modèle de déploiement classique de hello, vous ne pouvez pas migrer toohello nouvelles références SKU doivent continuer à la place de toouse hello références (SKU) hérité.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello nouvelles références SKU de passerelle, consultez [SKU de passerelle](vpn-gateway-about-vpngateways.md#gwsku).

Pour plus d’informations sur les paramètres de configuration, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).