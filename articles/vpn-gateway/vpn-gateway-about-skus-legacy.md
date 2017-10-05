---
title: "Références SKU héritées de passerelle de réseau virtuel Azure | Microsoft Docs"
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
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="2d29d-103">Utilisation des références SKU de passerelle de réseau virtuel (anciennes références SKU)</span><span class="sxs-lookup"><span data-stu-id="2d29d-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="2d29d-104">Cet article contient des informations sur les anciennes références SKU de passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2d29d-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="2d29d-105">Les anciennes références SKU continuent de fonctionner dans les deux modèles de déploiement pour les passerelles VPN qui ont déjà été créés.</span><span class="sxs-lookup"><span data-stu-id="2d29d-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="2d29d-106">Les passerelles VPN classiques continuent à utiliser d’anciennes références SKU, aussi bien pour les passerelles existantes que pour les nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="2d29d-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="2d29d-107">Lorsque vous créez de nouvelles passerelles VPN de gestionnaire de ressources, utilisez les références SKU des nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="2d29d-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="2d29d-108">Pour plus d’informations sur les nouvelles références SKU, reportez-vous à la rubrique [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="2d29d-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="2d29d-109"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="2d29d-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="2d29d-110"><a name="agg"></a>Débit agrégé estimé par SKU</span><span class="sxs-lookup"><span data-stu-id="2d29d-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="2d29d-111"><a name="config"></a>Configurations prises en charge par référence SKU et type de VPN</span><span class="sxs-lookup"><span data-stu-id="2d29d-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="2d29d-112"><a name="resize"></a>Redimensionner une passerelle (modifier la référence SKU d’une passerelle)</span><span class="sxs-lookup"><span data-stu-id="2d29d-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="2d29d-113">Vous pouvez redimensionner la référence SKU d’une passerelle au sein de la même famille de références SKU.</span><span class="sxs-lookup"><span data-stu-id="2d29d-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="2d29d-114">Par exemple, si vous avez une référence SKU standard, vous pouvez redimensionner selon une référence SKU HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="2d29d-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="2d29d-115">Vous ne pouvez pas redimensionner vos passerelles VPN entre d’anciennes références SKU est de nouvelles familles de références SKU.</span><span class="sxs-lookup"><span data-stu-id="2d29d-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="2d29d-116">Par exemple, vous ne pouvez pas aller d’une référence SKU standard à une référence SKU VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="2d29d-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="2d29d-117">Pour redimensionner une référence SKU de passerelle pour le modèle de déploiement classique, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d29d-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="2d29d-118">Pour redimensionner une référence SKU de passerelle pour le modèle de déploiement du Gestionnaire de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d29d-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="2d29d-119"><a name="migrate"></a>Migration vers les nouvelles références SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="2d29d-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="2d29d-120">Si vous utilisez le modèle de déploiement du Gestionnaire de ressources, vous pouvez migrer vers les nouvelles références SKU de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2d29d-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="2d29d-121">Si vous utilisez le modèle de déploiement classique, vous ne pouvez pas migrer vers les nouvelles références SKU et devez continuer à utiliser les anciennes références SKU.</span><span class="sxs-lookup"><span data-stu-id="2d29d-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2d29d-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d29d-122">Next steps</span></span>

<span data-ttu-id="2d29d-123">Pour plus d’informations sur les nouvelles références SKU de passerelle, voir [Références (SKU) de passerelle](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="2d29d-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="2d29d-124">Pour plus d’informations sur les paramètres de configuration, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2d29d-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>