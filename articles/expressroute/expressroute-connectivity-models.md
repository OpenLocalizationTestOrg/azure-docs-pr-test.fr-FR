---
title: "Modèles de connectivité ExpressRoute : connexion tooMicrosoft Azure via des fournisseurs de services réseau, les échanges et les fournisseurs de Ethernet | Documents Microsoft"
description: "Cet article décrit les différents modes de hello de connectivité entre le réseau et les services Microsoft Azure, Office 365 et Dynamics 365 du client hello. Clients peuvent faire appel à des fournisseurs MPLS, des échanges de cloud et des fournisseurs Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Modèles de connectivité ExpressRoute
Vous pouvez créer une connexion entre votre réseau local et le hello cloud Microsoft de trois façons différentes, [colocalisation CloudExchange](#CloudExchange), [connexion Ethernet de point à point](#Ethernet)et [Pour tout (IPVPN) connexion](#IPVPN). Les fournisseurs de connectivité peuvent offrir un ou plusieurs modèles de connectivité. Vous pouvez travailler avec votre modèle hello toopick fournisseur connectivité qui vous convient le mieux.
<br><br>

![Schéma des modèles de connectivité ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Colocalisation avec un échange de cloud
Si vous sont colocalisés dans une fonction avec un échange de cloud computing, vous pouvez commander des interconnexions virtuel toohello cloud de Microsoft via Ethernet exchange du fournisseur de colocalisation hello. Les fournisseurs de colocalisation peuvent offrir de couche 2 interconnexions soit géré de couche 3 interconnexions entre votre infrastructure en fonction de la colocalisation hello et de cloud de Microsoft hello.

## <a name="Ethernet"></a>Connexions Ethernet point à point
Vous pouvez vous connecter à votre toohello de centres de données/bureaux locaux Microsoft cloud via des liens Ethernet de point à point. Fournisseurs de point à point Ethernet peuvent offrir des connexions de couche 2 ou géré les connexions de couche 3 entre votre site et vos hello cloud de Microsoft.

## <a name="IPVPN"></a>Réseaux universels (IPVPN)
Vous pouvez intégrer votre réseau étendu hello cloud de Microsoft. Les fournisseurs IPVPN (généralement des VPN MPLS) offrent une connectivité universelle entre vos succursales et vos centres de données. Hello Microsoft nuage peut être interconnectés tooyour toomake WAN elle recherchera simplement comme n’importe quel autre filiale. Les fournisseurs de réseaux étendus offrent généralement une connectivité de couche 3 gérée. Fonctionnalités et fonctions de ExpressRoute sont toutes identiques dans l’ensemble de hello au-dessus des modèles de connectivité. 

## <a name="next-steps"></a>Étapes suivantes
* Découvrez en détail les connexions ExpressRoute et les domaines de routage. Consultez la page [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).
* Découvrez en détail les fonctionnalités ExpressRoute. Consultez hello [présentation technique d’ExpressRoute](expressroute-introduction.md)
* Recherchez un fournisseur de services. Consultez la page [Partenaires ExpressRoute et emplacements d’homologation](expressroute-locations.md).
* Vérifiez que toutes les conditions préalables sont remplies. Consultez la page [Configuration requise pour ExpressRoute](expressroute-prerequisites.md).
* Consultez Configuration requise de toohello pour [routage](expressroute-routing.md), [NAT](expressroute-nat.md), et [QoS](expressroute-qos.md).
* Configurez votre connexion ExpressRoute.
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configuration du routage](expressroute-howto-routing-portal-resource-manager.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-portal-resource-manager.md)
