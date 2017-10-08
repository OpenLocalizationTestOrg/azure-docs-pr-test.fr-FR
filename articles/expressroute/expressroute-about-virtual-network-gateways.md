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
# <a name="about-virtual-network-gateways-for-expressroute"></a>À propos des passerelles de réseau virtuel pour ExpressRoute
Sert de passerelle de réseau virtuel toosend le trafic de réseau entre les réseaux virtuels Azure et les emplacements sur site. Lorsque vous configurez une connexion ExpressRoute, vous devez créer et configurer une passerelle de réseau virtuel et une connexion à la passerelle de réseau virtuel.

Lorsque vous créez une passerelle de réseau virtuel, vous spécifiez plusieurs paramètres. Un des paramètres de hello requis spécifie si la passerelle de hello doit être utilisé pour le trafic ExpressRoute ou VPN de Site à Site. Dans le modèle de déploiement du Gestionnaire de ressources hello, paramètre de hello est '-le type de passerelle ».

Lorsque le trafic réseau est envoyé sur une connexion privée, vous utilisez le type de passerelle hello « ExpressRoute ». Il s’agit également tooas auxquels une passerelle ExpressRoute. Lorsque le trafic réseau est envoyé chiffré entre hello Internet public, vous utilisez le type de passerelle hello « Vpn ». Il s’agit de tooas auxquels une passerelle VPN. Les connexions site à site, point à site et réseau virtuel à réseau virtuel utilisent toutes une passerelle VPN.

Chaque réseau virtuel ne peut posséder qu’une seule passerelle de réseau virtuel par type de passerelle. Par exemple, une passerelle de réseau virtuel peut utiliser le type de passerelle VPN et une autre le type de passerelle ExpressRoute. Cet article se concentre sur la passerelle de réseau virtuel hello ExpressRoute.

## <a name="gwsku"></a>SKU de passerelle
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Si vous souhaitez tooupgrade votre tooa passerelle plus puissante passerelle référence (SKU), dans la plupart des cas, vous pouvez utiliser hello applet de commande PowerShell de « Resize-AzureRmVirtualNetworkGateway ». Cela fonctionne pour les mises à niveau tooStandard et références (SKU) hautes performances. Toutefois, tooupgrade toohello UltraPerformance SKU, vous devrez passerelle de hello toorecreate.

### <a name="aggthroughput"></a>Débit agrégé estimé par SKU de passerelle
Hello tableau suivant répertorie les types de passerelles hello et débit estimé hello. Ce tableau s’applique tooboth hello Gestionnaire de ressources et les modèles de déploiement classique.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Débit de l’application dépend de plusieurs facteurs, tels que de latence de bout en bout hello, et nombre de hello du trafic flux hello application ouvre. nombres de Hello dans hello table représentent hello limite supérieure qu’application hello peut theorectically atteindre dans un environnement idéal. 
> 
>

## <a name="resources"></a>API REST et applets de commande PowerShell
Pour les ressources techniques supplémentaires en matière de syntaxe spécifique lors de l’utilisation des API REST et les applets de commande PowerShell pour les configurations de passerelle de réseau virtuel, consultez hello suivant pages :

| **Classique** | **Gestionnaire de ressources** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [API REST](https://msdn.microsoft.com/library/jj154113.aspx) |[API REST](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les configurations de connexion disponibles, consultez la rubrique [Vue d’ensemble d’ExpressRoute](expressroute-introduction.md) . 

