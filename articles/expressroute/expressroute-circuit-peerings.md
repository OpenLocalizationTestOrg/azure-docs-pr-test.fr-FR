---
title: aaaAzure ExpressRoute circuits et domaines de routage | Documents Microsoft
description: "Cette page fournit une vue d’ensemble des circuits ExpressRoute et domaines de routage hello."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Circuits ExpressRoute et domaines de routage
 Vous devez commander un *circuit ExpressRoute* tooconnect votre tooMicrosoft d’infrastructure sur site via un fournisseur de connectivité. figure Hello ci-dessous fournit une représentation logique de la connectivité entre votre réseau étendu et de Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Circuits ExpressRoute
Un *circuit ExpressRoute* représente une connexion logique entre votre infrastructure local et les services de cloud Microsoft via un fournisseur de connectivité. Vous pouvez commander plusieurs circuits ExpressRoute. Chaque circuit peut être hello identiques ou différentes régions, et peut être local tooyour connectés via des fournisseurs de connectivité différents. 

Circuits ExpressRoute ne mappent pas tooany des entités physiques. Un circuit est identifié par un GUID standard appelé clé de service (s-key). clé du service Hello est hello uniquement les informations échangées entre Microsoft et vous fournisseur de connectivité hello. Hello s-key n’est pas un secret pour des raisons de sécurité. Il existe un mappage 1:1 entre un circuit ExpressRoute et le hello s-key.

Un circuit ExpressRoute peut avoir des homologations indépendant de toothree : Azure public, Azure privé et Microsoft. Chaque homologation est une paire de sessions BGP indépendantes, chacune configurée de manière redondante pour offrir une disponibilité optimale. Il existe un mappage 1:N (1 <= N <= 3) entre un circuit ExpressRoute et des domaines de routage. Un circuit ExpressRoute peut avoir une, deux ou trois homologations activées par circuit ExpressRoute.

Chaque circuit a une bande passante fixe (50 Mbits/s, 100 Mbits/s, 200 Mbits/s, 500 Mbits/s, 1 Gbits/s, 10 Gbits/s) et est le fournisseur de connectivité tooa mappé et un emplacement d’homologation. la bande passante Hello que vous sélectionnez est partagée entre tous les homologations hello pour le circuit de hello. 

### <a name="quotas-limits-and-limitations"></a>Quotas, limites et limitations
Des limites et quotas par défaut s'appliquent à chaque circuit ExpressRoute. Consultez toohello [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md) page pour obtenir des informations sur les quotas.

## <a name="expressroute-routing-domains"></a>Domaines de routage ExpressRoute
Un circuit ExpressRoute est associé à plusieurs domaines de routage : public Azure, privé Azure et Microsoft. Chacun des domaines de routage hello est configuré de façon identique sur une paire de routeurs (actif / actif ou partage de la charge configuration) pour la haute disponibilité. Services Azure sont classées comme étant *public Azure* et *privé Azure* toorepresent hello des modèles d’adressage IP.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Homologation privée
Services, à savoir les machines virtuelles (IaaS) de calcul Azure et des services de cloud (PaaS), qui sont déployés dans un réseau virtuel peuvent être connectés via le domaine d’homologation privée de hello. domaine d’homologation privée de Hello est considéré comme toobe une extension de confiance de votre réseau de base dans Microsoft Azure. Vous pouvez configurer une connectivité bidirectionnelle entre votre réseau de base et les réseaux virtuels Azure. Cette homologation vous permet de connecter des ordinateurs de toovirtual et services directement sur les adresses IP privées de cloud computing.  

Vous pouvez connecter plusieurs réseaux virtuels toohello d’homologation domaine privé. Hello de révision [page de FAQ](expressroute-faqs.md) pour plus d’informations sur les limites et limitations. Vous pouvez visiter hello [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md) page pour obtenir des informations sur les limites.  Consultez toohello [routage](expressroute-routing.md) page pour plus d’informations sur la configuration de routage.

### <a name="public-peering"></a>Homologation publique
Les services tels qu’Azure Storage, les bases de données SQL et Sites web sont proposés sur des adresses IP publiques. Vous pouvez connecter en privé de tooservices hébergés sur des adresses IP publiques, y compris les adresses IP virtuelles de vos services cloud, via le domaine de routage d’homologation publique hello. Vous pouvez connecter hello publics d’homologation domaine tooyour réseau de périmètre et se connecter tooall Azure services sur les adresses IP publiques à partir de votre réseau étendu sans avoir tooconnect via hello internet. 

Connectivité est toujours lancée à partir de votre réseau étendu tooMicrosoft Azure services. Services Microsoft Azure ne sera pas en mesure de tooinitiate des connexions à votre réseau via ce domaine de routage. Une fois que l’homologation publique est activée, vous serez en mesure de tooconnect tooall Azure services. Nous ne vous permettent pas les services de prélèvement tooselectively pour lequel nous publier d’itinéraires sur. Vous pouvez consulter la liste de hello des préfixes nous publier tooyou via cette homologation sur hello [plages d’adresses IP Microsoft Azure Datacenter](http://www.microsoft.com/download/details.aspx?id=41653) page. page de Hello est mise à jour chaque semaine.

Vous pouvez définir des filtres de routage personnalisées au sein de votre réseau tooconsume uniquement hello itinéraires que vous avez besoin. Consultez toohello [routage](expressroute-routing.md) page pour plus d’informations sur la configuration de routage. 

Consultez hello [page de FAQ](expressroute-faqs.md) pour plus d’informations sur les services pris en charge par le domaine de routage d’homologation publique hello. 

### <a name="microsoft-peering"></a>Homologation Microsoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Connectivité tooall autres services en ligne Microsoft (par exemple, les services Office 365) sera via l’homologation de Microsoft hello. Nous allons activer une connectivité bidirectionnelle entre vos services cloud Microsoft et de réseau étendu via le domaine de routage d’homologation hello Microsoft. Vous devez vous connecter à des services de cloud computing tooMicrosoft uniquement sur les adresses IP publiques qui sont détenus par vous ou votre fournisseur de connectivité, et vous devez respecter les règles tooall hello défini. Consultez hello [conditions préalables d’ExpressRoute](expressroute-prerequisites.md) page pour plus d’informations.

Consultez hello [page de FAQ](expressroute-faqs.md) pour plus d’informations sur les services pris en charge, les coûts et les détails de configuration. Consultez hello [ExpressRoute emplacements](expressroute-locations.md) page pour plus d’informations sur la liste de hello de fournisseurs de connectivité offre la prise en charge d’homologation de Microsoft.

## <a name="routing-domain-comparison"></a>Comparaison des domaines de routage
tableau Hello ci-dessous compare les trois domaines de routage hello.

|  | **Homologation privée** | **Homologation publique** | **Homologation Microsoft** |
| --- | --- | --- | --- |
| **Nb max. de préfixes pris en charge par homologation** |4 000 par défaut, 10 000 avec ExpressRoute Premium |200 |200 |
| **Plages d’adresses IP prises en charge** |Toute adresse IPv4 valide au sein de votre réseau étendu. |Adresses IPv4 publiques détenues par vous ou par votre fournisseur de connectivité. |Adresses IPv4 publiques détenues par vous ou par votre fournisseur de connectivité. |
| **Exigences en matière de numéros AS** |Numéros AS publics et privés Vous devez posséder hello publique en tant que nombre si vous choisissez toouse une. |Numéros AS publics et privés Cependant, vous devez prouver la propriété des adresses IP publiques. |Numéros AS publics et privés Cependant, vous devez prouver la propriété des adresses IP publiques. |
| **Adresses IP de l’interface de routage** |RFC1918 et adresses IP publiques |Tooyou inscrit dans les registres de routage d’adresses IP publiques. |Tooyou inscrit dans les registres de routage d’adresses IP publiques. |
| **Prise en charge du hachage MD5** |Oui |Oui |Oui |

Vous pouvez choisir tooenable un ou plusieurs des domaines de routage hello dans le cadre de votre circuit ExpressRoute. Vous pouvez choisir toohave tous les domaines de routage hello placés hello VPN même si vous souhaitez toocombine dans un domaine de routage unique. Vous pouvez également les placer sur différents domaines de routage, diagramme de toohello similaire. Hello recommandé de configuration est cette homologation privée est connecté directement le réseau de base toohello et hello public et des liens d’homologation Microsoft sont connectés tooyour le réseau de périmètre.

Si vous choisissez toohave toutes les sessions d’homologation trois, vous devez disposer de trois paires de sessions BGP pour (une paire pour chaque type d’homologation). paires de session BGP Hello fournissent un lien hautement disponible. Si vous vous connectez via des fournisseurs de couche 2, il vous incombe de configurer et de gérer le routage. Vous trouverez plus en consultant hello [workflows](expressroute-workflows.md) pour la configuration d’ExpressRoute.

## <a name="next-steps"></a>Étapes suivantes
* Recherchez un fournisseur de services. Consultez la rubrique [Emplacements et fournisseurs de services ExpressRoute](expressroute-locations.md).
* Vérifiez que toutes les conditions préalables sont remplies. Consultez la page [Configuration requise pour ExpressRoute](expressroute-prerequisites.md).
* Configurez votre connexion ExpressRoute.
  * [Créer et gérer des circuits ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurer l’acheminement (homologation) pour les circuits ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)

