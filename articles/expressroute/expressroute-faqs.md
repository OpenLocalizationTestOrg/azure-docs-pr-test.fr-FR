---
title: Forum Aux Questions Azure ExpressRoute | Microsoft Docs
description: "Le Forum aux questions ExpressRoute contient des informations sur les services Azure pris en charge, le coût, les données et connexions, le contrat de niveau de service, les fournisseurs et les emplacements, la bande passante et les détails techniques."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 39b79dce555ba1b57f48ca2b431c13b1c1e4d90b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-faq"></a>Forum Aux Questions ExpressRoute

## <a name="what-is-expressroute"></a>Présentation d’ExpressRoute

ExpressRoute est un service Azure qui vous permet de créer des connexions privées entre les centres de données Microsoft et une infrastructure locale ou une installation de colocalisation. Les connexions ExpressRoute ne sont pas établies via le réseau public Internet et offrent plus de sécurité, de fiabilité et de rapidité, ainsi que moins de latences que les connexions classiques sur Internet.

### <a name="what-are-the-benefits-of-using-expressroute-and-private-network-connections"></a>Quels avantages présentent l’utilisation d’ExpressRoute et les connexions de réseau privé ?

Les connexions ExpressRoute ne sont pas établies par le biais de l'Internet public. Elles offrent plus de sécurité, de fiabilité et de rapidité, ainsi que des latences inférieures et cohérentes par rapport aux connexions classiques sur Internet. Dans certains cas, l’utilisation de connexions ExpressRoute pour transférer des données entre les appareils locaux et Azure peut générer des économies significatives.

### <a name="where-is-the-service-available"></a>Où le service est-il disponible ?

Consultez cette page pour connaître l’emplacement du service et la disponibilité : [Partenaires et emplacements ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-to-connect-to-microsoft-if-i-dont-have-partnerships-with-one-of-the-expressroute-carrier-partners"></a>Comment puis-je utiliser ExpressRoute pour me connecter à Microsoft si je n’ai pas conclu de partenariat avec l’un des partenaires opérateurs d’ExpressRoute ?

Vous pouvez sélectionner un opérateur régional et accéder à des connexions Ethernet établies avec l’un des emplacements de fournisseur Exchange pris en charge. Vous pouvez ensuite vous apparier avec Microsoft à l’emplacement du fournisseur. Vérifiez la dernière section de la rubrique [Partenaires et emplacements ExpressRoute](expressroute-locations.md) pour voir si votre fournisseur de services est présent dans l’un des emplacements Exchange. Vous pouvez ensuite commander un circuit ExpressRoute via le fournisseur de services pour vous connecter à Azure.

### <a name="how-much-does-expressroute-cost"></a>Combien coûte ExpressRoute ?

Pour plus d'informations sur la tarification, consultez la page [Tarification](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-the-vpn-connection-i-purchase-from-my-network-service-provider-have-to-be-the-same-speed"></a>Si j’achète un circuit ExpressRoute d’une bande passante donnée, la connexion VPN que j’achète auprès de mon fournisseur de services réseau doit-elle être de la même vitesse ?

Non. Vous pouvez acheter une connexion VPN de n’importe quelle vitesse chez votre fournisseur de services. Toutefois, votre connexion à Azure est limitée à la bande passante du circuit ExpressRoute que vous achetez.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-the-ability-to-burst-up-to-higher-speeds-if-necessary"></a>Si j’achète un circuit ExpressRoute présentant une bande passante donnée, puis-je augmenter sa vitesse en cas de nécessité ?

Oui. La configuration des circuits ExpressRoute vous permet d’augmenter jusqu’à deux fois la limite de la bande passante obtenue sans frais supplémentaire. Consultez votre fournisseur de services pour savoir si cette capacité est prise en charge.

### <a name="can-i-use-the-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Puis-je utiliser la même connexion réseau privée avec un réseau virtuel et d’autres services Azure simultanément ?

Oui. Un circuit ExpressRoute, une fois configuré, vous permet d’accéder simultanément aux services au sein d’un réseau virtuel et aux autres services Azure. Vous vous connectez à des réseaux virtuels sur le chemin d’accès d’homologation privée et à d’autres services sur le chemin d’accès d’homologation publique.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute offre-t-il un contrat de niveau de service (SLA) ?

Pour plus d’informations, consultez la page [SLA ExpressRoute](https://azure.microsoft.com/support/legal/sla/) .

## <a name="supported-services"></a>Services pris en charge

ExpressRoute prend en charge [trois domaines de routage](expressroute-circuit-peerings.md) pour différents types de services.

### <a name="private-peering"></a>Homologation privée

* Réseaux virtuels, comprenant l’ensemble des machines virtuelles et des services cloud

### <a name="public-peering"></a>Homologation publique

* Power BI
* Dynamics 365 for Finance and Operations (anciennement Dynamics AX Online)
* La plupart des services Azure, avec quelques exceptions ci-dessous :
  * CDN
  * Test de charge Visual Studio Team Services
  * Multi-Factor Authentication
  * Traffic Manager

### <a name="microsoft-peering"></a>Homologation Microsoft

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Applications d’Engagement client Dynamics 365 (anciennement CRM Online)
  * Dynamics 365 pour les ventes
  * Dynamics 365 pour le service client
  * Dynamics 365 pour le service après-vente
  * Dynamics 365 pour le service de projet

## <a name="data-and-connections"></a>Données et connexions

### <a name="are-there-limits-on-the-amount-of-data-that-i-can-transfer-using-expressroute"></a>Existe-t-il des limites sur la quantité de données que je peux transférer avec ExpressRoute ?

Nous ne définissons aucune limite sur la quantité de transfert de données. Pour plus d'informations sur les tarifs de bande passante, consultez la page de [tarification](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Quelles vitesses de connexion sont prises en charge par ExpressRoute ?

Offres relatives à la bande passante prise en charge :

50 Mbit/s, 100 Mbit/s, 200 Mbit/s, 500 Mbit/s, 1 Gbit/s, 2 Gbit/s, 5 Gbit/s, 10 Gbit/s

### <a name="which-service-providers-are-available"></a>Quels fournisseurs de services sont disponibles ?

Pour obtenir la liste des fournisseurs de services et des emplacements, consultez la page [Partenaires et emplacements ExpressRoute](expressroute-locations.md) .

## <a name="technical-details"></a>Détails techniques

### <a name="what-are-the-technical-requirements-for-connecting-my-on-premises-location-to-azure"></a>Quelles sont les exigences techniques pour connecter mon emplacement local à Azure ?

Consultez [la page conditions préalables d’ExpressRoute](expressroute-prerequisites.md) pour la configuration requise.

### <a name="are-connections-to-expressroute-redundant"></a>Les connexions à ExpressRoute sont-elles redondantes ?

Oui. Chaque circuit ExpressRoute dispose d’une paire redondante de connexions croisées configurées pour fournir une haute disponibilité.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Vais-je perdre ma connectivité en cas d’échec de l’un de mes liens ExpressRoute ?

Vous ne perdez pas votre connectivité si une des connexions croisées échoue. Une connexion redondante est disponible pour prendre en charge la charge de votre réseau. Vous pouvez également créer plusieurs circuits dans un autre emplacement d’homologation pour bénéficier de la tolérance de panne.

### <a name="onep2plink"></a>Si je ne suis pas colocalisé au niveau d’un échange de cloud et que mon fournisseur de services offre une connexion point à point, dois-je commander deux connexions physiques entre mon réseau local et Microsoft ?

Vous n’avez besoin que d’une seule connexion physique si votre fournisseur de services peut établir deux circuits virtuels Ethernet via la connexion physique. La connexion physique (par exemple, une fibre optique) se termine sur un appareil de couche 1 (L1) (voir l’image). Les deux circuits virtuels Ethernet sont marqués avec des ID de VLAN différents, l’un pour le circuit principal et l’autre pour le circuit secondaire. Ces ID de VLAN se trouvent dans l’en-tête Ethernet 802.1Q externe. L’en-tête Ethernet 802.1Q interne (non illustré) est mappé à un [domaine de routage ExpressRoute](expressroute-circuit-peerings.md)spécifique.

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-to-azure-using-expressroute"></a>Puis-je étendre l’un de mes réseaux locaux virtuels vers Azure avec ExpressRoute ?

Non. Nous ne prenons pas en charge les extensions de connectivité de couche 2 dans Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Puis-je avoir plusieurs circuits ExpressRoute dans mon abonnement ?

Oui. Vous pouvez avoir plusieurs circuits ExpressRoute dans votre abonnement. La limite par défaut est définie sur 10. Vous pouvez contacter le support technique de Microsoft pour augmenter la limite, si nécessaire.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Puis-je avoir des circuits ExpressRoute de différents fournisseurs de services ?

Oui. Vous pouvez avoir des circuits ExpressRoute de nombreux fournisseurs de services. Chaque circuit ExpressRoute est associé uniquement à un fournisseur de services. 

### <a name="can-i-have-multiple-expressroute-circuits-in-the-same-location"></a>Puis-je avoir plusieurs circuits ExpressRoute dans le même emplacement ?

Oui. Vous pouvez avoir plusieurs circuits ExpressRoute, avec des fournisseurs de services identiques ou différents, dans le même emplacement. Vous ne pouvez toutefois pas lier plusieurs circuits ExpressRoute au même réseau virtuel à partir du même emplacement.

### <a name="how-do-i-connect-my-virtual-networks-to-an-expressroute-circuit"></a>Comment connecter mes réseaux virtuels à un circuit ExpressRoute ?

Étapes élémentaires :

* Établissez un circuit ExpressRoute et faites-le activer par le fournisseur de services.
* Vous, ou le fournisseur, devez configurer les homologations BGP.
* Liez le réseau virtuel au circuit ExpressRoute.

Pour plus d’informations, consultez [flux de travail ExpressRoute pour la configuration de circuits et les états des circuits](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Existe-t-il des limites de connectivité pour le circuit ExpressRoute ?

Oui. L’article [partenaires et emplacements ExpressRoute](expressroute-locations.md) offre une vue d’ensemble des limites de connectivité d’un circuit ExpressRoute. La connectivité d’un circuit ExpressRoute est limitée à une seule région géopolitique. La connectivité peut être étendue pour traverser des régions géopolitiques en activant la fonctionnalité Premium d’ExpressRoute.

### <a name="can-i-link-to-more-than-one-virtual-network-to-an-expressroute-circuit"></a>Puis-je lier plusieurs réseaux virtuels à un circuit ExpressRoute ?

Oui. Vous pouvez avoir jusqu’à 10 connexions réseaux virtuels sur un circuit ExpressRoute standard et jusqu’à 100 sur un [circuit ExpressRoute premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-to-a-single-expressroute-circuit"></a>Je possède plusieurs abonnements Azure qui contiennent des réseaux virtuels. Puis-je connecter des réseaux virtuels qui figurent dans des abonnements distincts à un circuit ExpressRoute ?

Oui. Vous pouvez autoriser jusqu’à 10 autres abonnements Azure à utiliser un même circuit ExpressRoute. Cette limite peut être augmentée en activant la fonctionnalité Premium d’ExpressRoute.

Pour plus d'informations, consultez la page [Partage d'un circuit ExpressRoute entre plusieurs abonnements](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-to-the-same-circuit-isolated-from-each-other"></a>Les réseaux virtuels sont-ils connectés à un même circuit en étant isolés les uns des autres ?

Non. Dans une perspective de routage, l’ensemble des réseaux virtuels liés au même circuit ExpressRoute fait partie du même domaine de routage et ne sont pas isolés les un des autres. Si vous devez isoler des itinéraires, vous devez créer un circuit ExpressRoute distinct.

### <a name="can-i-have-one-virtual-network-connected-to-more-than-one-expressroute-circuit"></a>Puis-je avoir un seul réseau virtuel connecté à plusieurs circuits ExpressRoute ?

Oui. Vous pouvez lier un réseau virtuel avec quatre circuits ExpressRoute au maximum. Ils doivent être ordonnés par le biais de quatre [emplacements ExpressRoute](expressroute-locations.md)différents.

### <a name="can-i-access-the-internet-from-my-virtual-networks-connected-to-expressroute-circuits"></a>Puis-je accéder à Internet à partir de mes réseaux virtuels connectés à des circuits ExpressRoute ?

Oui. Si vous n’avez pas publié les itinéraires par défaut (0.0.0.0/0) ou les préfixes d’itinéraire Internet via la session BGP, vous pouvez vous connecter à Internet à partir d’un réseau virtuel lié à un circuit ExpressRoute.

### <a name="can-i-block-internet-connectivity-to-virtual-networks-connected-to-expressroute-circuits"></a>Puis-je bloquer connectivité Internet pour les réseaux virtuels connectés à des circuits ExpressRoute ?

Oui. Vous pouvez publier des itinéraires par défaut (0.0.0.0/0) pour bloquer la connectivité Internet de toutes les machines virtuelles qui sont déployées au sein d’un réseau virtuel et qui acheminent tout le trafic sortant via le circuit ExpressRoute.

Si vous publiez des itinéraires par défaut, nous forçons le trafic en direction des services offerts via l’homologation publique (tels que le stockage Azure et base de données SQL) vers votre environnement local. Vous devrez configurer votre routeur pour retourner le trafic vers Azure via le chemin d’accès d’homologation publique ou via Internet.

### <a name="can-virtual-networks-linked-to-the-same-expressroute-circuit-talk-to-each-other"></a>Les réseaux virtuels liés à un même circuit ExpressRoute peuvent-ils communiquer entre eux ?

Oui. Les machines virtuelles qui sont déployées dans des réseaux virtuels connectés à un même circuit ExpressRoute peuvent communiquer entre elles.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Puis-je utiliser une connectivité de site à site pour les réseaux virtuels conjointement avec ExpressRoute ?

Oui. ExpressRoute peut coexister avec des réseaux VPN de site à site.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-to-use-expressroute"></a>Puis-je déplacer un réseau virtuel à partir de la configuration de site à site/point à site pour utiliser ExpressRoute ?

Oui. Vous devez créer une passerelle ExpressRoute dans votre réseau virtuel. Le processus entraîne un léger temps d’arrêt.

### <a name="why-is-there-a-public-ip-address-associated-with-the-expressroute-gateway-on-a-virtual-network"></a>Pourquoi une adresse IP publique est-elle associée à la passerelle ExpressRoute sur un réseau virtuel ?

L’adresse IP publique est utilisée pour la gestion interne uniquement. Cette adresse IP publique n’est pas exposée à Internet et ne constitue pas un risque pour la sécurité de votre réseau virtuel.

### <a name="what-do-i-need-to-connect-to-azure-storage-over-expressroute"></a>De quoi ai-je besoin pour me connecter au stockage Azure via ExpressRoute ?

Vous devez établir un circuit ExpressRoute et configurer des itinéraires pour l’homologation publique.

### <a name="are-there-limits-on-the-number-of-routes-i-can-advertise"></a>Existe-t-il des limites sur le nombre d’itinéraires que je peux publier ?

Oui. Nous acceptons jusqu’à 4000 préfixes d’itinéraires pour l’homologation privée et 200 pour l’homologation publique et l’homologation Microsoft. Vous pouvez augmenter ce nombre jusqu’à 10 000 itinéraires par homologation privée si vous activez la fonctionnalité Premium d’ExpressRoute.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-the-bgp-session"></a>Existe-t-il des restrictions de plages d’adresses IP que je peux publier sur la session BGP ?

Nous n’acceptons pas les préfixes privés (RFC1918) dans la session BGP d’homologation publique et dans la session BGP d’homologation Microsoft.

### <a name="what-happens-if-i-exceed-the-bgp-limits"></a>Que se passe-t-il si je dépasse les limites du protocole BGP ?

Les sessions BGP sont supprimées. Elles sont ensuite réinitialisées lorsque le nombre de préfixes tombe en dessous de la limite.

### <a name="what-is-the-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Quelle est la durée de conservation BGP d'ExpressRoute ? Peut-elle être ajustée ?

La durée de conservation est de 180. Les messages persistants sont envoyés toutes les 60 secondes. Il s'agit de paramètres fixes de Microsoft qui ne peuvent pas être modifiés. Vous pouvez configurer différents minuteurs et les paramètres de la session BGP seront négociés en conséquence.

### <a name="after-i-advertise-the-default-route-00000-to-my-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-to-i-fix-this"></a>Une fois que je publie l’itinéraire par défaut (0.0.0.0/0) sur mes réseaux virtuels, je ne peux pas activer Windows qui est en cours d’exécution sur mes machines virtuelles Azure. Comment faire pour résoudre ce problème ?

Les étapes suivantes aident Azure à reconnaître la demande d’activation :

1. Établissez l’homologation publique pour votre circuit ExpressRoute.
2. Effectuez une recherche DNS et recherchez l’adresse IP de **kms.core.windows.net**
3. Le Service de gestion de clés doit reconnaître que la demande d’activation provient d’Azure et honorer la demande. Effectuez l’une des trois tâches suivantes :

   * Sur votre réseau local, réacheminez le trafic destiné à l’adresse IP que vous avez obtenu à l’étape 2 vers Azure via l’homologation publique.
   * Faites en sorte que votre fournisseur de services réseau renvoie le trafic vers Azure via l’homologation publique.
   * Créez un itinéraire défini par l’utilisateur qui pointe sur l’adresse IP ayant Internet en tant que tronçon suivant et appliquez-le au(x) sous-réseau(x) où sont situées ces machines virtuelles.

### <a name="can-i-change-the-bandwidth-of-an-expressroute-circuit"></a>Puis-je modifier la bande passante d’un circuit ExpressRoute ?

Oui, vous pouvez tenter d’augmenter la bande passante de votre circuit ExpressRoute dans le portail Azure, ou à l’aide de PowerShell. Si il y a de la capacité disponible sur le port physique sur lequel votre circuit a été créé, votre modification a réussi. 

Si votre modification échoue, cela signifie peut signifier qu’il ne reste pas suffisamment de capacité sur le port actuel et que vous devez créer un nouveau circuit ExpressRoute avec une plus grande bande passante, ou qu’il n’y a pas de capacité supplémentaire à cet emplacement. Dans ce cas vous ne pourrez pas augmenter la bande passante. 

Vous devez également effectuer un suivi avec votre fournisseur de connectivité pour vous assurer qu’il met à jour les limitations dans ses réseaux pour prendre en charge l’augmentation de la bande passante. Vous ne pouvez toutefois pas réduire la bande passante de votre circuit ExpressRoute. Vous devez créer un nouveau circuit ExpressRoute avec une bande passante inférieure et supprimer l’ancien circuit.

### <a name="how-do-i-change-the-bandwidth-of-an-expressroute-circuit"></a>Comment modifier la bande passante d’un circuit ExpressRoute ?

Vous pouvez mettre à jour de la bande passante du circuit ExpressRoute à l’aide de l’API REST ou l’applet de commande PowerShell.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>En quoi consiste ExpressRoute Premium ?

ExpressRoute Premium est un ensemble de fonctionnalités répertoriées ci-dessous.

* Augmentation de la limite de la table d’itinéraires de 4 000 à 10 000 itinéraires pour l’homologation privée.
* Augmentation du nombre de réseaux virtuels qui peuvent être connectés à un circuit ExpressRoute (la valeur par défaut est 10). Pour plus d’informations, consultez le tableau [Limites d’ExpressRoute](#limits).
* Connectivité à Office 365 et Dynamics 365.
* Connectivité globale sur le réseau principal Microsoft. Vous pouvez désormais lier un réseau virtuel dans une région géopolitique à un circuit ExpressRoute d’une autre région.<br>
    **Exemples :**

    *  Vous pouvez lier un réseau virtuel créé en Europe de l’ouest à un circuit créé dans la Silicon Valley. 
    *  Sur l’homologation publique, les préfixes d’autres régions géopolitiques sont publiés de sorte que vous pouvez vous connecter à SQL Azure en Europe de l’ouest à partir d’un circuit dans la Silicon Valley, par exemple.


### <a name="limits"></a>Combien de réseaux virtuels puis-je lier à un circuit ExpressRoute si j’ai activé ExpressRoute Premium ?

Les tableaux suivants indiquent les limites d’ExpressRoute et le nombre de réseaux virtuels par circuit ExpressRoute.

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Comment activer ExpressRoute Premium ?

Les fonctionnalités premium ExpressRoute peuvent être activées lorsque la fonctionnalité est activée et peuvent être arrêtées en mettant à jour l’état du circuit. Vous pouvez activer ExpressRoute Premium quand vous créez le circuit ou vous pouvez appeler l’API REST/l’applet de commande PowerShell pour activer ExpressRoute Premium.

### <a name="how-do-i-disable-expressroute-premium"></a>Comment désactiver ExpressRoute Premium ?

Vous pouvez désactiver ExpressRoute Premium en appelant l’API REST/l’applet de commande PowerShell. Vous devez vous assurer que vous avez redimensionné vos besoins en connectivité afin de respecter les limites par défaut avant de désactiver ExpressRoute Premium. Si votre utilisation met à l’échelle au-delà des limites par défaut, la requête de désactivation d’ExpressRoute Premium échoue.

### <a name="can-i-pick-and-choose-the-features-i-want-from-the-premium-feature-set"></a>Puis-je choisir les fonctionnalités parmi l’ensemble des fonctionnalités Premium ?

Non. Vous ne pouvez pas sélectionner les fonctionnalités. Nous activons toutes les fonctionnalités lorsque vous activez ExpressRoute Premium.

### <a name="how-much-does-expressroute-premium-cost"></a>Combien coûte ExpressRoute Premium ?

Consultez la page de [tarification](https://azure.microsoft.com/pricing/details/expressroute/) pour connaître les coûts.

### <a name="do-i-pay-for-expressroute-premium-in-addition-to-standard-expressroute-charges"></a>Dois-je payer pour ExpressRoute Premium en plus des frais ExpressRoute standard ?

Oui. Les frais d’ExpressRoute Premium s’ajoutent aux frais de circuit ExpressRoute et aux frais du fournisseur de connectivité.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute pour Office 365 et Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-to-connect-to-office-365-services-and-dynamics-365"></a>Comment créer un circuit ExpressRoute pour se connecter à des services Office 365 et Dynamics 365 ?

1. Consultez la [page des conditions préalables d’ExpressRoute](expressroute-prerequisites.md) pour vérifier que vous avez respecté les conditions.
2. Pour vous assurer que vos besoins de connectivité sont satisfaisants, examinez la liste des fournisseurs de services et les emplacements dans l’article [Partenaires d’ExpressRoute partenaires et emplacements](expressroute-locations.md).
3. Planifiez vos besoins en capacité en consultant la page [Planification réseau et optimisation des performances pour Office 365](http://aka.ms/tune/).
4. Suivez les étapes répertoriées dans les flux de travail pour configurer la connectivité aux [flux de travail ExpressRoute pour l’approvisionnement et les états du circuit](expressroute-workflows.md).

> [!IMPORTANT]
> Assurez-vous d’avoir activé le module complémentaire ExpressRoute lors de la configuration de la connectivité aux services Office 365 et Dynamics 365.
> 
> 

### <a name="do-i-need-to-enable-azure-public-peering-to-connect-to-office-365-services-and-dynamics-365"></a>Dois-je activer l’homologation publique Azure pour me connecter aux services Office 365 et Dynamics 365 ?

Non, vous devez uniquement activer l’homologation Microsoft. Le trafic d'authentification vers Azure AD est envoyé via l’homologation Microsoft. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-to-office-365-services-and-dynamics-365"></a>Mes circuits ExpressRoute existants peuvent-ils prendre en charge la connectivité aux services Office 365 et Dynamics 365 ?

Oui. Votre circuit ExpressRoute existant peut être configuré pour prendre en charge la connectivité aux services Office 365. Assurez-vous d'avoir une capacité suffisante pour vous connecter aux services Office 365 et d’avoir activé le module complémentaire premium. [Planification réseau et optimisation des performances pour Office 365](http://aka.ms/tune/) vous aide à prévoir vos besoins de connectivité. Voir également [Création et modification d’un circuit ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Quels services Office 365 sont accessibles via une connexion ExpressRoute ?

Reportez-vous à la page [URL et plages d’adresses IP Office 365](http://aka.ms/o365endpoints) pour obtenir une liste à jour des services pris en charge par le biais d’ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Combien coûte ExpressRoute pour les services Office 365 et Dynamics 365 ?

Les services Office 365 et Dynamics 365 nécessitent l'activation d'un module premium complémentaire. Consultez la [page de détails des prix appliqués](https://azure.microsoft.com/pricing/details/expressroute/) pour les coûts.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Quelles régions sont prises en charge dans ExpressRoute pour Office 365 ?

Consultez [Partenaires et emplacements ExpressRoute ](expressroute-locations.md) pour plus d’informations.

### <a name="can-i-access-office-365-over-the-internet-even-if-expressroute-was-configured-for-my-organization"></a>Puis-je accéder à Office 365 via Internet même si ExpressRoute a été configuré pour mon organisation ?

Oui. Les points de terminaison du service Office 365 sont accessibles via Internet, même si ExpressRoute a été configuré pour votre réseau. Si votre emplacement est configuré pour vous connecter aux services Office 365 via ExpressRoute, vous vous connectez via ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Puis-je accéder aux services Office 365 US Government Community (GCC) sur un circuit Azure US Government ExpressRoute ?

Oui. Les points de terminaison du service Office 365 GCC sont accessibles via Azure US Government ExpressRoute. Toutefois, vous devez d’abord ouvrir un ticket de support sur le portail Azure pour fournir à Microsoft les préfixes que vous avez l’intention de publier. La connectivité aux services Office 365 GCC sera établie une fois le ticket de support résolu. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Dynamics 365 for Operations (précédemment appelé Dynamics AX Online) est-il accessible par le biais d’une connexion ExpressRoute ?

Oui. [Dynamics 365 pour les opérations](https://www.microsoft.com/dynamics365/operations) est hébergé sur Azure. Vous pouvez activer l’homologation publique Azure sur votre circuit ExpressRoute pour vous y connecter.

## <a name="route-filters-for-microsoft-peering"></a>Filtres de routage pour l’homologation Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-the-first-time-what-routes-will-i-see"></a>J’active l’homologation Microsoft pour la première fois, quels itinéraires s’afficheront ?

Aucun itinéraire ne s’affichera. Vous devez joindre un filtre de routage à votre circuit pour démarrer des publications de préfixe. Consultez [Configurer des filtres de routage pour l’homologation Microsoft](how-to-routefilter-powershell.md)pour obtenir des instructions.

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-to-select-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-to-do-it"></a>J’ai activé l’homologation Microsoft et maintenant j’essaie de sélectionner Exchange Online, mais il affiche une erreur m’indiquant que je ne suis pas autorisé à le faire.

Lorsque vous utilisez des filtres de routage, n’importe quel client peut activer homologation Microsoft. Toutefois, pour utiliser les services Office 365, vous devez toujours obtenir l’autorisation de la part de Office 365.

### <a name="do-i-need-to-get-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Ai-je besoin d’obtenir une autorisation pour activer Dynamics 365 via l’homologation Microsoft ?

Non, vous n’avez pas besoin d’autorisation pour Dynamics 365. Vous pouvez créer une règle et sélectionner la Communauté Dynamics 365 sans autorisation.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>J’ai déjà homologation Microsoft, comment puis-je tirer parti des filtres de routage ?

Vous pouvez créer un filtre de routage, sélectionnez les services que vous souhaitez utiliser et joindre le filtre à votre homologation Microsoft. Consultez [Configurer des filtres de routage pour l’homologation Microsoft](how-to-routefilter-powershell.md)pour obtenir des instructions.

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-to-enable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Je dispose de l’homologation Microsoft à un emplacement, maintenant j’essaie de l’activer à un autre emplacement et aucun préfixe ne s’affiche.

* L’homologation Microsoft des circuits ExpressRoute ayant été configurés avant le 1er août 2017 entraînera la publication de tous les préfixes de service via l’homologation Microsoft, même si les filtres d’itinéraire ne sont pas définis.

* L’homologation Microsoft des circuits ExpressRoute configurés à partir du 1er août 2017 n’entraînera la publication d’aucun préfixe tant qu’un filtre de routage sera joint au circuit. Aucun préfixe par défaut ne s’affichera.
