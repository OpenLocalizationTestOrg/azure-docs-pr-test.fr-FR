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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="4108b-103">Utilisation des références SKU de passerelle de réseau virtuel (anciennes références SKU)</span><span class="sxs-lookup"><span data-stu-id="4108b-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="4108b-104">Cet article contient des informations sur hello hérité (ancienne) passerelle de réseau virtuel références (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="4108b-105">hérité de Hello références (SKU) continueront de fonctionner dans les deux modèles de déploiement pour les passerelles VPN qui ont déjà été créés.</span><span class="sxs-lookup"><span data-stu-id="4108b-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="4108b-106">Les passerelles VPN classiques continuer toouse hello hérité références (SKU), aussi bien pour les passerelles existantes et nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="4108b-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="4108b-107">Lors de la création des passerelles VPN de nouveau gestionnaire de ressources, utilisez la passerelle hello références (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="4108b-108">Pour plus d’informations sur hello nouvelles références SKU, consultez [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="4108b-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="4108b-109"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="4108b-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="4108b-110"><a name="agg"></a>Débit agrégé estimé par SKU</span><span class="sxs-lookup"><span data-stu-id="4108b-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="4108b-111"><a name="config"></a>Configurations prises en charge par référence SKU et type de VPN</span><span class="sxs-lookup"><span data-stu-id="4108b-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="4108b-112"><a name="resize"></a>Redimensionner une passerelle (modifier la référence SKU d’une passerelle)</span><span class="sxs-lookup"><span data-stu-id="4108b-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="4108b-113">Vous pouvez redimensionner une référence (SKU) de passerelle dans hello même famille de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="4108b-114">Par exemple, si vous avez une référence (SKU) Standard, vous pouvez redimensionner tooa HighPerformance SKU.</span><span class="sxs-lookup"><span data-stu-id="4108b-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="4108b-115">Vous ne pouvez pas redimensionner votre VPN entre les passerelles hello anciennes références (SKU) et hello nouvelles familles de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="4108b-116">Par exemple, vous ne peut pas accéder à partir d’un tooa de référence (SKU) Standard VpnGw2 référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="4108b-117">tooresize une passerelle référence (SKU) pour le modèle de déploiement classique de hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4108b-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="4108b-118">tooresize une référence (SKU) de la passerelle pour hello modèle de déploiement du Gestionnaire de ressources, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4108b-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="4108b-119"><a name="migrate"></a>Migrer toohello nouvelle passerelle références (SKU)</span><span class="sxs-lookup"><span data-stu-id="4108b-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="4108b-120">Si vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello, vous pouvez migrer toohello nouvelle passerelle références (SKU).</span><span class="sxs-lookup"><span data-stu-id="4108b-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="4108b-121">Si vous travaillez avec un modèle de déploiement classique de hello, vous ne pouvez pas migrer toohello nouvelles références SKU doivent continuer à la place de toouse hello références (SKU) hérité.</span><span class="sxs-lookup"><span data-stu-id="4108b-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4108b-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4108b-122">Next steps</span></span>

<span data-ttu-id="4108b-123">Pour plus d’informations sur hello nouvelles références SKU de passerelle, consultez [SKU de passerelle](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="4108b-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="4108b-124">Pour plus d’informations sur les paramètres de configuration, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4108b-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>