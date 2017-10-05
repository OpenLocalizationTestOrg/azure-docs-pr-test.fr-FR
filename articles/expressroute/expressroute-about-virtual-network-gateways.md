---
title: "À propos des passerelles de réseau virtuel pour ExpressRoute | Microsoft Docs"
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
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="026b9-103">À propos des passerelles de réseau virtuel pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="026b9-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="026b9-104">Une passerelle de réseau virtuel est conçue pour faire circuler le trafic réseau entre les réseaux virtuels Azure et les emplacements locaux.</span><span class="sxs-lookup"><span data-stu-id="026b9-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="026b9-105">Lorsque vous configurez une connexion ExpressRoute, vous devez créer et configurer une passerelle de réseau virtuel et une connexion à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="026b9-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="026b9-106">Lorsque vous créez une passerelle de réseau virtuel, vous spécifiez plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="026b9-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="026b9-107">L’un des paramètres requis spécifie si la passerelle sera utilisée pour le trafic ExpressRoute ou le trafic VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="026b9-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="026b9-108">Dans le modèle de déploiement de Resource Manager, le paramètre est « -GatewayType ».</span><span class="sxs-lookup"><span data-stu-id="026b9-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="026b9-109">Lorsque le trafic réseau est envoyé sur une connexion privée, vous utilisez le type de passerelle « ExpressRoute ».</span><span class="sxs-lookup"><span data-stu-id="026b9-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="026b9-110">C’est ce que l’on appelle une passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="026b9-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="026b9-111">Lorsque le trafic réseau est transmis chiffré sur l’Internet public, vous utilisez le type de passerelle « Vpn ».</span><span class="sxs-lookup"><span data-stu-id="026b9-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="026b9-112">Il s’agit alors d’une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="026b9-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="026b9-113">Les connexions site à site, point à site et réseau virtuel à réseau virtuel utilisent toutes une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="026b9-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="026b9-114">Chaque réseau virtuel ne peut posséder qu’une seule passerelle de réseau virtuel par type de passerelle.</span><span class="sxs-lookup"><span data-stu-id="026b9-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="026b9-115">Par exemple, une passerelle de réseau virtuel peut utiliser le type de passerelle VPN et une autre le type de passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="026b9-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="026b9-116">Cet article décrit la passerelle de réseau virtuel ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="026b9-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="026b9-117"><a name="gwsku"></a>SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="026b9-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="026b9-118">Si vous souhaitez mettre à niveau votre passerelle vers une référence (SKU) de passerelle plus puissante, dans la plupart des cas, vous pouvez utiliser l’applet de commande PowerShell « Resize-AzureRmVirtualNetworkGateway ».</span><span class="sxs-lookup"><span data-stu-id="026b9-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="026b9-119">Cela fonctionne pour les mises à niveau vers les références (SKU) Standard HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="026b9-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="026b9-120">Toutefois, pour mettre à niveau vers la référence (SKU) UltraPerformance, vous devez recréer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="026b9-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="026b9-121"><a name="aggthroughput"></a>Débit agrégé estimé par SKU de passerelle</span><span class="sxs-lookup"><span data-stu-id="026b9-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="026b9-122">Le tableau ci-dessous présente les types de passerelle et le débit total estimé.</span><span class="sxs-lookup"><span data-stu-id="026b9-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="026b9-123">Cette table s’applique aux modèles de déploiement classique et Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="026b9-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="026b9-124">Le débit de l’application dépend de plusieurs facteurs, tels que la latence de bout en bout et le nombre de flux de trafic que l’application ouvre.</span><span class="sxs-lookup"><span data-stu-id="026b9-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="026b9-125">Les numéros indiqués dans le tableau représentent la limite supérieure que l’application peut théoriquement atteindre dans un environnement idéal.</span><span class="sxs-lookup"><span data-stu-id="026b9-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="026b9-126"><a name="resources"></a>API REST et applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="026b9-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="026b9-127">Pour accéder à des ressources techniques supplémentaires et connaître les exigences spécifiques en matière de syntaxe lors de l’utilisation d’API REST et d’applets de commande PowerShell pour les configurations de passerelles de réseau virtuel, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="026b9-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="026b9-128">**Classique**</span><span class="sxs-lookup"><span data-stu-id="026b9-128">**Classic**</span></span> | <span data-ttu-id="026b9-129">**Gestionnaire de ressources**</span><span class="sxs-lookup"><span data-stu-id="026b9-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="026b9-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="026b9-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="026b9-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="026b9-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="026b9-132">API REST</span><span class="sxs-lookup"><span data-stu-id="026b9-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="026b9-133">API REST</span><span class="sxs-lookup"><span data-stu-id="026b9-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="026b9-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="026b9-134">Next steps</span></span>
<span data-ttu-id="026b9-135">Pour plus d’informations sur les configurations de connexion disponibles, consultez la rubrique [Vue d’ensemble d’ExpressRoute](expressroute-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="026b9-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

