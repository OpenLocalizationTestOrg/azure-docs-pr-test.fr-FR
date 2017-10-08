---
title: "passerelles de réseau virtuel aaaAbout ExpressRoute | Documents Microsoft"
description: "En savoir plus sur les passerelles de réseau virtuel pour ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="b0976-103">À propos des passerelles de réseau virtuel pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b0976-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="b0976-104">Sert de passerelle de réseau virtuel toosend le trafic de réseau entre les réseaux virtuels Azure et les emplacements sur site.</span><span class="sxs-lookup"><span data-stu-id="b0976-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="b0976-105">Lorsque vous configurez une connexion ExpressRoute, vous devez créer et configurer une passerelle de réseau virtuel et une connexion à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0976-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="b0976-106">Lorsque vous créez une passerelle de réseau virtuel, vous spécifiez plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="b0976-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="b0976-107">Un des paramètres de hello requis spécifie si la passerelle de hello doit être utilisé pour le trafic ExpressRoute ou VPN de Site à Site.</span><span class="sxs-lookup"><span data-stu-id="b0976-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="b0976-108">Dans le modèle de déploiement du Gestionnaire de ressources hello, paramètre de hello est '-le type de passerelle ».</span><span class="sxs-lookup"><span data-stu-id="b0976-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="b0976-109">Lorsque le trafic réseau est envoyé sur une connexion privée, vous utilisez le type de passerelle hello « ExpressRoute ».</span><span class="sxs-lookup"><span data-stu-id="b0976-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="b0976-110">Il s’agit également tooas auxquels une passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b0976-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="b0976-111">Lorsque le trafic réseau est envoyé chiffré entre hello Internet public, vous utilisez le type de passerelle hello « Vpn ».</span><span class="sxs-lookup"><span data-stu-id="b0976-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="b0976-112">Il s’agit de tooas auxquels une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="b0976-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="b0976-113">Les connexions site à site, point à site et réseau virtuel à réseau virtuel utilisent toutes une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="b0976-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="b0976-114">Chaque réseau virtuel ne peut posséder qu’une seule passerelle de réseau virtuel par type de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b0976-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="b0976-115">Par exemple, une passerelle de réseau virtuel peut utiliser le type de passerelle VPN et une autre le type de passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b0976-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="b0976-116">Cet article se concentre sur la passerelle de réseau virtuel hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b0976-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="b0976-117"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="b0976-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="b0976-118">Si vous souhaitez tooupgrade votre tooa passerelle plus puissante passerelle référence (SKU), dans la plupart des cas, vous pouvez utiliser hello applet de commande PowerShell de « Resize-AzureRmVirtualNetworkGateway ».</span><span class="sxs-lookup"><span data-stu-id="b0976-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="b0976-119">Cela fonctionne pour les mises à niveau tooStandard et références (SKU) hautes performances.</span><span class="sxs-lookup"><span data-stu-id="b0976-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="b0976-120">Toutefois, tooupgrade toohello UltraPerformance SKU, vous devrez passerelle de hello toorecreate.</span><span class="sxs-lookup"><span data-stu-id="b0976-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="b0976-121"><a name="aggthroughput"></a>Débit agrégé estimé par SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="b0976-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="b0976-122">Hello tableau suivant répertorie les types de passerelles hello et débit estimé hello.</span><span class="sxs-lookup"><span data-stu-id="b0976-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="b0976-123">Ce tableau s’applique tooboth hello Gestionnaire de ressources et les modèles de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="b0976-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b0976-124">Débit de l’application dépend de plusieurs facteurs, tels que de latence de bout en bout hello, et nombre de hello du trafic flux hello application ouvre.</span><span class="sxs-lookup"><span data-stu-id="b0976-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="b0976-125">nombres de Hello dans hello table représentent hello limite supérieure qu’application hello peut theorectically atteindre dans un environnement idéal.</span><span class="sxs-lookup"><span data-stu-id="b0976-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="b0976-126"><a name="resources"></a>API REST et applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0976-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="b0976-127">Pour les ressources techniques supplémentaires en matière de syntaxe spécifique lors de l’utilisation des API REST et les applets de commande PowerShell pour les configurations de passerelle de réseau virtuel, consultez hello suivant pages :</span><span class="sxs-lookup"><span data-stu-id="b0976-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="b0976-128">**Classique**</span><span class="sxs-lookup"><span data-stu-id="b0976-128">**Classic**</span></span> | <span data-ttu-id="b0976-129">**Gestionnaire de ressources**</span><span class="sxs-lookup"><span data-stu-id="b0976-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="b0976-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0976-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="b0976-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0976-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="b0976-132">API REST</span><span class="sxs-lookup"><span data-stu-id="b0976-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="b0976-133">API REST</span><span class="sxs-lookup"><span data-stu-id="b0976-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="b0976-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0976-134">Next steps</span></span>
<span data-ttu-id="b0976-135">Pour plus d’informations sur les configurations de connexion disponibles, consultez la rubrique [Vue d’ensemble d’ExpressRoute](expressroute-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="b0976-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

