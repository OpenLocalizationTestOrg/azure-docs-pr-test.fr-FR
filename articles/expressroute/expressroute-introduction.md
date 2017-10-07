---
title: "Vue d’ensemble de ExpressRoute : Étendre votre tooAzure de réseau local via une connexion privée | Documents Microsoft"
description: "Cette présentation technique d’ExpressRoute explique comment une connexion ExpressRoute fonctionne tooextend votre tooAzure de réseau local via une connexion privée."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Présentation d’ExpressRoute
Microsoft Azure ExpressRoute vous permet d’étendre vos réseaux locaux dans hello cloud de Microsoft via une connexion privée facilitée par un fournisseur de connectivité. Grâce à ExpressRoute, vous pouvez établir des services de cloud computing tooMicrosoft de connexions, telles que Microsoft Azure, Office 365 et Dynamics 365.

La connectivité peut provenir d'un réseau universel (IP VPN), d’un réseau Ethernet point à point ou d’une interconnexion virtuelle via un fournisseur de connectivité dans un centre de colocalisation. Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ainsi, toooffer de connexions ExpressRoute plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello. Pour plus d’informations sur la façon de tooconnect votre tooMicrosoft réseau à l’aide d’ExpressRoute, consultez [ExpressRoute des modèles de connectivité](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Principaux avantages

* Connectivité de couche 3 entre votre réseau local et le hello Microsoft Cloud via un fournisseur de connectivité. La connectivité peut provenir d'un réseau universel (IPVPN), d’une connexion Ethernet point à point, ou d’une interconnexion virtuelle via un échange Ethernet.
* Services de cloud computing connectivité tooMicrosoft toutes les régions dans la région de hello géopolitiques.
* Services tooMicrosoft de connectivité globale de toutes les régions avec ExpressRoute complémentaire.
* Routage dynamique entre votre réseau et Microsoft via des protocoles standard (BGP).
* Redondance intégrée dans chaque emplacement d'homologation pour une plus grande fiabilité.
* [SLA](https://azure.microsoft.com/support/legal/sla/)de disponibilité de la connexion.
* Support de la qualité de service pour Skype Entreprise.

Pour plus d’informations, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Caractéristiques

### <a name="layer-3-connectivity"></a>Connectivité de couche 3
Microsoft utilise industry standard dynamique routage protocole (BGP Border) tooexchange achemine entre votre réseau local, vos instances dans Azure et Microsoft adresses publiques.  Nous établissons plusieurs sessions BGP avec votre réseau pour tester différents profils de trafic. Vous trouverez plus de détails dans hello [ExpressRoute circuit et domaines de routage](expressroute-circuit-peerings.md) l’article.

### <a name="redundancy"></a>Redondance
Chaque circuit ExpressRoute se compose de deux connexions tootwo Microsoft Enterprise routeurs de bord (MSEEs) à partir du fournisseur de connectivité hello / votre réseau de périmètre. Microsoft requiert deux connexions BGP à partir du fournisseur de connectivité hello / votre côté – un tooeach MSEE. Vous pouvez choisir pas toodeploy périphériques redondant / Ethernet circuits à votre fin. Toutefois, les fournisseurs de connectivité utilisent tooensure périphériques redondant qui tooMicrosoft vos connexions sont transmises de manière redondante. Une configuration de la connectivité de couche 3 redondant est nécessaire pour notre [SLA](https://azure.microsoft.com/support/legal/sla/) toobe valide.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Services de cloud computing tooMicrosoft de connectivité
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Les connexions ExpressRoute activer toohello accès suivant de services :

* Services Microsoft Azure
* Services Microsoft Office 365
* Microsoft Dynamics 365

Vous pouvez visiter hello [FAQ sur ExpressRoute](expressroute-faqs.md) page pour une liste détaillée des services pris en charge via ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Régions tooall de connectivité dans une région géopolitique
Vous pouvez vous connecter tooMicrosoft dans un de nos [emplacements d’homologation](expressroute-locations.md) et ont accès tooall au sein de la région de hello géopolitiques. 

Par exemple, si vous connecté tooMicrosoft à Amsterdam via ExpressRoute, vous avez accès tooall Microsoft cloud services hébergés dans Europe du Nord et Europe occidentale. Consultez hello [ExpressRoute partenaires et les emplacements d’homologation](expressroute-locations.md) article pour une vue d’ensemble des régions de géopolitiques hello, régions de cloud Microsoft associées et les emplacements d’homologation ExpressRoute correspondants.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Connectivité globale avec le module complémentaire ExpressRoute premium
Vous pouvez activer la connectivité du module complémentaire fonctionnalité tooextend pour hello ExpressRoute premium au-delà des limites géopolitiques. Par exemple, si vous êtes connecté tooMicrosoft à Amsterdam via ExpressRoute, vous aurez accès tooall Microsoft cloud services hébergés dans toutes les régions sur Bonjour (clouds nationales sont exclus). Vous pouvez accéder à des services déployées en Amérique du Sud ou Australie hello comme vous hello Nord et des régions d’Europe de l’ouest.

### <a name="rich-connectivity-partner-ecosystem"></a>Riche écosystème de partenaires de connectivité
ExpressRoute offre un écosystème sans cesse croissant de fournisseurs de connectivité et de partenaires intégrateurs de systèmes. Vous pouvez faire référence toohello [ExpressRoute fournisseurs et des emplacements](expressroute-locations.md) article pour les informations les plus récentes hello.

### <a name="connectivity-toonational-clouds"></a>Clouds toonational de connectivité
Microsoft gère des environnements de cloud isolés dans des régions géopolitiques et des segments de clientèle spécifiques. Consultez toohello [ExpressRoute fournisseurs et des emplacements](expressroute-locations.md) page pour obtenir la liste des fournisseurs et des clouds nationales.

### <a name="bandwidth-options"></a>Options de bande passante
Vous pouvez acheter des circuits ExpressRoute pour un large éventail de bandes passantes. Les bandes passantes prises en charge sont répertoriées ci-dessous. Être toocheck que votre connectivité fournisseur toodetermine hello parmi des bandes passantes prises en charge, qu'ils fournissent.

* 50 Mbits/s
* 100 Mbits/s
* 200 Mbits/s
* 500 Mbits/s
* 1 Gbit/s
* 2 Gbit/s
* 5 Gbit/s
* 10 Gbits/s

### <a name="dynamic-scaling-of-bandwidth"></a>Mise à l'échelle dynamique de la bande passante
Vous pouvez augmenter la bande passante du circuit ExpressRoute hello (sur le plus tôt) sans avoir tootear vos connexions vers le bas. 

### <a name="flexible-billing-models"></a>Modèles de facturation flexibles
Vous pouvez choisir le modèle de facturation qui vous convient le mieux. Choisissez entre les modèles de facturation hello répertoriées ci-dessous. Pour plus d’informations, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).

* **Données illimitées**. Hello circuit ExpressRoute est facturé en fonction des frais mensuels et tous les transferts de données entrant et sortant sont inclus gratuitement. 
* **Données limitées**. Hello circuit ExpressRoute est facturé en fonction des frais mensuels. Tous les transferts de données entrants sont gratuits. Chaque transfert de données sortant est facturé par Go de données transférées. Les taux de transfert de données varient selon la région.
* **Module complémentaire ExpressRoute premium**. premium d’ExpressRoute Hello est un module complémentaire sur hello circuit ExpressRoute. module complémentaire de Hello ExpressRoute premium fournit hello suivant de fonctionnalités : 
  * Limites d’itinéraire accrue pour Azure publics et Azure homologation privée à partir de 4 000 itinéraires too10, 000 itinéraires.
  * Connectivité globale des services. Un circuit ExpressRoute créé dans n’importe quelle région (à l’exclusion des clouds nationales) auront accès tooresources sur n’importe quelle autre région Bonjour. Par exemple, un réseau virtuel créé en l'Europe occidentale est accessible via un circuit ExpressRoute configuré dans la Silicon Valley.
  * Nombre accru de liens de réseau virtuel par circuit ExpressRoute de 10 tooa supérieure de la limite, en fonction de la bande passante hello du circuit de hello.

## <a name="faq"></a>Forum Aux Questions

Pour les questions fréquemment posées sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Étapes suivantes

* Consultez des informations supplémentaires sur les [modèles de connectivité ExpressRoute](expressroute-connectivity-models.md).
* Découvrez en détail les connexions ExpressRoute et les domaines de routage. Consultez la page [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).
* Recherchez un fournisseur de services. Consultez la page [Partenaires ExpressRoute et emplacements d’homologation](expressroute-locations.md).
* Vérifiez que toutes les conditions préalables sont remplies. Consultez la page [Configuration requise pour ExpressRoute](expressroute-prerequisites.md).
* Consultez Configuration requise de toohello pour [routage](expressroute-routing.md), [NAT](expressroute-nat.md), et [QoS](expressroute-qos.md).
* Configurez votre connexion ExpressRoute.
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configuration de l’homologation pour un circuit ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Se connecter à un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-portal-resource-manager.md)
* En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.
