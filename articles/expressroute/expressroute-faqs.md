---
title: aaaAzure FAQ sur ExpressRoute | Documents Microsoft
description: "Hello FAQ sur ExpressRoute contient des informations sur la prise en charge des Services Azure, coût, données et connexions, contrat SLA, fournisseurs et des emplacements, la bande passante et des informations techniques."
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
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Forum Aux Questions ExpressRoute

## <a name="what-is-expressroute"></a>Présentation d’ExpressRoute

ExpressRoute est un service Azure qui vous permet de créer des connexions privées entre les centres de données Microsoft et une infrastructure locale ou une installation de colocalisation. Les connexions ExpressRoute ne sont pas établies via hello Internet public et offre une sécurité accrue, la fiabilité et vitesses réduire des latences moindres par rapport aux connexions classiques sur Internet de hello.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Quels sont les avantages de hello de l’utilisation de connexions de réseau privé et ExpressRoute ?

Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ils offrent plus de sécurité, de fiabilité et de vitesses, avec une latence inférieure et cohérent qu’aux connexions classiques sur Internet de hello. Dans certains cas, à l’aide de données de tootransfer de connexions ExpressRoute entre des appareils locaux et Azure peut également avoir des avantages des coûts importants.

### <a name="where-is-hello-service-available"></a>Où est hello service disponibles ?

Consultez cette page pour connaître l’emplacement du service et la disponibilité : [Partenaires et emplacements ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Comment puis-je utiliser ExpressRoute tooconnect tooMicrosoft si je n’ai pas conclu de partenariat avec l’un des partenaires de transport ExpressRoute hello ?

Vous pouvez sélectionner un transporteur régional et terrestres tooone de connexions Ethernet d’exchange de hello pris en charge des emplacements du fournisseur. Vous pouvez ensuite homologue avec Microsoft à l’emplacement du fournisseur hello. Vérifiez la dernière section de hello de [ExpressRoute partenaires et des emplacements](expressroute-locations.md) toosee si votre fournisseur de services est présent dans un des emplacements d’exchange hello. Vous pouvez ensuite commander un circuit ExpressRoute via hello service fournisseur tooconnect tooAzure.

### <a name="how-much-does-expressroute-cost"></a>Combien coûte ExpressRoute ?

Pour plus d'informations sur la tarification, consultez la page [Tarification](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Si j’acquiers pour un circuit ExpressRoute d’une bande passante donnée, hello connexion VPN que j’achète auprès de mon fournisseur de services réseau ont toobe hello même vitesse ?

Non. Vous pouvez acheter une connexion VPN de n’importe quelle vitesse chez votre fournisseur de services. Toutefois, votre tooAzure de connexion est limitée toohello ExpressRoute bande passante du circuit que vous achetez.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Si j’acquiers un circuit ExpressRoute d’une bande passante donnée, ai-je tooburst de capacité hello des vitesses toohigher si nécessaire ?

Oui. Circuits ExpressRoute sont configuré tooallow vous tooburst des heures de tootwo hello limite de bande passante obtenue sans aucun coût supplémentaire. Vérifiez auprès de votre toosee de fournisseur de service si elles prennent en charge cette fonctionnalité.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Puis-je utiliser la fonctionnalité hello privée même la connexion réseau avec un réseau virtuel et les autres services Azure simultanément ?

Oui. Un circuit ExpressRoute, une fois configuré, vous permet de services tooaccess dans un réseau virtuel et autres services Azure simultanément. Vous vous connectez toovirtual réseaux sur le chemin d’accès d’homologation privée hello et tooother services sur le chemin d’accès d’homologation publique hello.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute offre-t-il un contrat de niveau de service (SLA) ?

Pour plus d’informations, consultez hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) page.

## <a name="supported-services"></a>Services pris en charge

ExpressRoute prend en charge [trois domaines de routage](expressroute-circuit-peerings.md) pour différents types de services.

### <a name="private-peering"></a>Homologation privée

* Réseaux virtuels, comprenant l’ensemble des machines virtuelles et des services cloud

### <a name="public-peering"></a>Homologation publique

* Power BI
* Dynamics 365 for Finance and Operations (anciennement Dynamics AX Online)
* Les services de la plupart des hello Azure avec hello suivant quelques exceptions près :
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

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Existe-t-il des limites sur la quantité de hello de données que je peux transférer à l’aide d’ExpressRoute ?

Nous ne définissez pas une limite de quantité hello de transfert de données. Consultez trop[tarification](https://azure.microsoft.com/pricing/details/expressroute/) pour plus d’informations sur les taux de bande passante.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Quelles vitesses de connexion sont prises en charge par ExpressRoute ?

Offres relatives à la bande passante prise en charge :

50 Mbit/s, 100 Mbit/s, 200 Mbit/s, 500 Mbit/s, 1 Gbit/s, 2 Gbit/s, 5 Gbit/s, 10 Gbit/s

### <a name="which-service-providers-are-available"></a>Quels fournisseurs de services sont disponibles ?

Consultez [ExpressRoute partenaires et des emplacements](expressroute-locations.md) pour la liste de fournisseurs de services et emplacements hello.

## <a name="technical-details"></a>Détails techniques

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Quelles sont les exigences techniques de hello pour se connecter à mon tooAzure d’emplacement local ?

Consultez [la page conditions préalables d’ExpressRoute](expressroute-prerequisites.md) pour la configuration requise.

### <a name="are-connections-tooexpressroute-redundant"></a>Sont tooExpressRoute des connexions redondantes ?

Oui. Chaque circuit ExpressRoute dispose d’une paire de cross-connexions configurées tooprovide haute disponibilité.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Vais-je perdre ma connectivité en cas d’échec de l’un de mes liens ExpressRoute ?

Vous ne perdez pas de connectivité si une de hello Cross-connexions échoue. Une connexion redondante est la charge de hello toosupport disponible de votre réseau. Vous pouvez également créer plusieurs circuits dans une autre homologation emplacement tooachieve tolérance aux défaillances.

### <a name="onep2plink"></a>Si je ne suis pas situé au niveau d’un échange de cloud et mon fournisseur de services offre connexion point à point, dois-je tooorder deux connexions physiques entre Microsoft et de mon réseau local ?

Si votre fournisseur de services d’établir deux circuits virtuels Ethernet via hello physique, vous devez uniquement une connexion physique. Hello connexion physique (par exemple, une fibre optique) est terminée sur une couche 1 (L1) appareil (voir l’image de hello). circuits virtuels de Hello deux Ethernet sont balisés avec différents ID de réseau local virtuel, un pour hello principal, un circuit et l’autre pour hello secondaire. Ces ID de VLAN sont dans l’en-tête de Ethernet hello 802. 1 q externe. en-tête de Ethernet Hello 802. 1 q interne (non affiché) est mappé tooa spécifique [domaine de routage ExpressRoute](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>Puis-je étendre l’un de me tooAzure de réseaux locaux virtuels à l’aide d’ExpressRoute ?

Non. Nous ne prenons pas en charge les extensions de connectivité de couche 2 dans Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Puis-je avoir plusieurs circuits ExpressRoute dans mon abonnement ?

Oui. Vous pouvez avoir plusieurs circuits ExpressRoute dans votre abonnement. la limite par défaut Hello a la valeur too10. Vous pouvez contacter la limite de Support technique de Microsoft tooincrease hello, si nécessaire.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Puis-je avoir des circuits ExpressRoute de différents fournisseurs de services ?

Oui. Vous pouvez avoir des circuits ExpressRoute de nombreux fournisseurs de services. Chaque circuit ExpressRoute est associé uniquement à un fournisseur de services. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Puis-je avoir plusieurs circuits ExpressRoute dans hello même emplacement ?

Oui. Vous pouvez avoir plusieurs circuits ExpressRoute, avec hello identiques ou différents fournisseurs de services dans hello même emplacement. Toutefois, vous ne pouvez pas lier plusieurs toohello de circuit ExpressRoute même virtuel réseau à partir de hello, ce même emplacement.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Comment se connecter mon tooan de réseaux virtuels circuit ExpressRoute

les étapes de base Hello sont :

* Mettre en place un circuit ExpressRoute et avez prestataire hello l’activer.
* Vous ou le fournisseur hello, doit configurer hello BGP d’homologation (s).
* Lier un circuit ExpressRoute de hello réseau virtuel toohello.

Pour plus d’informations, consultez [flux de travail ExpressRoute pour la configuration de circuits et les états des circuits](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Existe-t-il des limites de connectivité pour le circuit ExpressRoute ?

Oui. Hello [ExpressRoute partenaires et des emplacements](expressroute-locations.md) article fournit une vue d’ensemble des limites de connectivité hello pour un circuit ExpressRoute. Connectivité pour un circuit ExpressRoute est région géopolitiques tooa limité. Connectivité peut être développé toocross des régions géopolitiques en activant la fonctionnalité de hello ExpressRoute premium.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Puis-je lier toomore à un réseau virtuel tooan circuit ExpressRoute ?

Oui. Vous pouvez avoir too10 les connexions de réseaux virtuels sur un circuit ExpressRoute standard et too100 sur un [circuit ExpressRoute de premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Je possède plusieurs abonnements Azure qui contiennent des réseaux virtuels. Puis-je connecter des réseaux virtuels qui se trouvent dans des abonnements distincts tooa même circuit ExpressRoute ?

Oui. Vous pouvez autoriser des too10 autres toouse abonnements Azure un même circuit ExpressRoute. Cette limite peut être augmentée en activant la fonctionnalité de hello ExpressRoute premium.

Pour plus d'informations, consultez la page [Partage d'un circuit ExpressRoute entre plusieurs abonnements](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Sont toohello connectés à des réseaux virtuels même circuit isolé de l’autre ?

Non. À partir d’un routage toohello lié de perspective, tout des réseaux virtuels même circuit ExpressRoute font partie du même domaine de routage de hello et ne sont pas isolées des autres. Si vous avez besoin de router d’isolation, vous devez toocreate un circuit ExpressRoute distinct.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Puis-je avoir un toomore de réseau virtuel connecté à un circuit ExpressRoute ?

Oui. Vous pouvez lier un seul réseau virtuel avec des circuits ExpressRoute de toofour. Ils doivent être ordonnés par le biais de quatre [emplacements ExpressRoute](expressroute-locations.md)différents.

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>Puis-je accéder à hello Internet à partir de mes réseaux virtuels des circuits tooExpressRoute connectés ?

Oui. Si vous n’avez pas publié les itinéraires par défaut (0.0.0.0/0) ou le préfixe d’itinéraire Internet via une session de hello BGP, vous pouvez vous connecter à toohello Internet à partir d’un circuit ExpressRoute de tooan réseau virtuel lié.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Puis-je bloquer Internet connectivité toovirtual réseaux connectés tooExpressRoute circuits ?

Oui. Vous pouvez publier tooblock d’itinéraires (0.0.0.0/0) par défaut toutes les machines de toovirtual de connectivité Internet déploiement au sein d’un réseau virtuel et acheminer tout le trafic sortant via le circuit ExpressRoute de hello.

Si vous publiez les itinéraires par défaut, nous forcer tooservices trafic proposés sur public local tooyour arrière d’homologation (par exemple, le stockage Azure et base de données SQL). Vous devez tooconfigure votre tooAzure de trafic tooreturn routeurs via le chemin d’accès d’homologation publique hello ou via hello Internet.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Peut toohello lié de réseaux virtuels même circuit ExpressRoute parler tooeach autres ?

Oui. Ordinateurs virtuels déployés dans des réseaux virtuels connectés toohello est même circuit ExpressRoute permettre communiquer entre eux.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Puis-je utiliser une connectivité de site à site pour les réseaux virtuels conjointement avec ExpressRoute ?

Oui. ExpressRoute peut coexister avec des réseaux VPN de site à site.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Puis-je déplacer un réseau virtuel à partir de la configuration de site à site / point-to-site toouse ExpressRoute ?

Oui. Vous devez toocreate une passerelle ExpressRoute au sein de votre réseau virtuel. Il existe un bref temps d’arrêt liés au processus de hello.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Pourquoi existe-t-il une adresse IP publique associée à la passerelle ExpressRoute hello un réseau virtuel ?

adresse IP publique de Hello est utilisé pour la gestion interne uniquement. Cette adresse IP publique n’est pas exposé toohello Internet et ne constitue pas un risque pour la sécurité de votre réseau virtuel.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Comment dois-je tooconnect tooAzure stockage via ExpressRoute ?

Vous devez établir un circuit ExpressRoute et configurer des itinéraires pour l’homologation publique.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Existe-t-il des limites sur le nombre de hello d’itinéraires que je peux publier ?

Oui. Nous acceptons les préfixes d’itinéraire too4000 pour l’homologation privée et 200 pour l’homologation publique et d’homologation Microsoft. Vous pouvez augmenter cette too10, 000 itinéraires pour l’homologation privée si vous activez la fonctionnalité de hello ExpressRoute premium.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Existe-t-il des restrictions sur les plages d’adresses IP que je peux publier sur la session de hello BGP ?

Nous n’acceptent pas les préfixes privés (plage RFC1918) Bonjour publique et la session BGP d’homologation de Microsoft.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Que se passe-t-il si je dépasse les limites BGP hello ?

Les sessions BGP sont supprimées. Une fois que le nombre de préfixes hello tombe en dessous de limite de hello, elles seront réinitialisées.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Qu’est hello BGP ExpressRoute contiennent les temps ? Peut-elle être ajustée ?

Durée Hello est 180. Hello KeepAlive sont envoyés toutes les 60 secondes. Ceux-ci sont fixes paramètres sur hello côté Microsoft qui ne peut pas être modifiée. Il est possible que vous tooconfigure les minuteurs différents et paramètres de la session BGP hello seront négociées en conséquence.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Une fois que j’ai publier des réseaux virtuels du toomy itinéraire (0.0.0.0/0) par défaut hello, ne puis-je pas activer Windows en cours d’exécution sur mes machines virtuelles Azure. Comment tooI résoudre ce problème ?

Hello suit aider à Azure de reconnaître la demande d’activation de hello :

1. Établir hello pour l’homologation publique pour votre circuit ExpressRoute.
2. Effectuer une recherche DNS et adresse IP de hello de **kms.core.windows.net**
3. Hello Service de gestion de clés doit reconnaître cette demande d’activation hello proviennent d’Azure et honorer hello demande. Effectuez l’une des hello trois tâches suivantes :

   * Sur votre réseau local, acheminer le trafic de hello destinés à hello adresse IP que vous avez obtenue dans l’étape 2 de tooAzure arrière via l’homologation publique hello.
   * Avoir votre NSP fournisseur cheveux broches hello trafic arrière tooAzure via l’homologation publique hello.
   * Créer un itinéraire défini par l’utilisateur qui IP hello points ayant Internet comme un tronçon suivant et l’appliquer ou toohello où ces machines virtuelles sont les sous-réseaux.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Puis-je modifier la bande passante hello d’un circuit ExpressRoute ?

Oui, vous pouvez tenter de la bande passante de hello tooincrease de votre circuit ExpressRoute Bonjour portail Azure, ou à l’aide de PowerShell. Si la capacité est disponible sur le port physique hello sur lequel votre circuit a été créé, votre modification réussit. 

Si votre modification échoue, cela signifie que soit la capacité est insuffisante restant sur le port actif de hello et que vous devez toocreate un circuit ExpressRoute de nouveau avec hello beaucoup de bande passante, ou qu’il n’existe aucune capacité supplémentaire à cet emplacement, auquel cas vous ne pourrez bande passante de tooincrease hello. 

Vous devez également toofollow avec votre tooensure de fournisseur de connectivité qu’ils mettent à jour les accélérateurs hello dans leur augmentation de la bande passante des réseaux toosupport hello. Vous ne peut pas, toutefois, réduire la bande passante hello de votre circuit ExpressRoute. Avoir toocreate un circuit ExpressRoute de nouveau avec une faible bande passante et supprimer le circuit d’ancien hello.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Comment modifier la bande passante hello d’un circuit ExpressRoute ?

Vous pouvez mettre à jour de la bande passante hello du circuit ExpressRoute de hello à l’aide d’applet de commande hello API REST ou PowerShell.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>En quoi consiste ExpressRoute Premium ?

ExpressRoute premium est une collection de hello suivant de fonctionnalités :

* Augmentation de la limite de table routage de 4000 itinéraires too10, 000 itinéraires pour l’homologation privée.
* Augmente le nombre de réseaux virtuels qui peuvent être connecté toohello circuit ExpressRoute (valeur par défaut est 10). Pour plus d’informations, consultez hello [ExpressRoute limites](#limits) table.
* Connectivité tooOffice 365 et Dynamics 365.
* Connectivité globale sur le réseau de base Microsoft hello. Vous pouvez désormais lier un réseau virtuel dans une région géopolitique à un circuit ExpressRoute d’une autre région.<br>
    **Exemples :**

    *  Vous pouvez lier un réseau virtuel créé à l’Europe de l’ouest tooan circuit ExpressRoute créé dans la Silicon Valley. 
    *  Sur l’homologation publique hello, les préfixes d’autres régions géopolitiques sont publiés telles que vous pouvez vous connecter à, par exemple, SQL Azure en Europe de l’ouest à partir d’un circuit dans la Silicon Valley.


### <a name="limits"></a>Le nombre de réseaux virtuels puis-je lier circuit ExpressRoute de tooan si j’ai activé ExpressRoute premium ?

Hello tableaux suivants indiquent les limites d’ExpressRoute hello et nombre de hello de réseaux virtuels par circuit ExpressRoute :

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Comment activer ExpressRoute Premium ?

Des fonctionnalités premium ExpressRoute peuvent être activées lors de la fonctionnalité de hello est activée et peuvent être arrêtées en mettant à jour d’état du circuit hello. Vous pouvez activer ExpressRoute premium au moment de la création du circuit, ou peut appeler l’API REST de hello / applet de commande PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>Comment désactiver ExpressRoute Premium ?

Vous pouvez désactiver ExpressRoute premium en appelant l’applet de commande hello API REST ou PowerShell. Il se peut que vous devez vous assurer que vous avez mis à l’échelle vos besoins toomeet hello par défaut des limites de connectivité avant de désactiver ExpressRoute premium. Si votre utilisation des échelles au-delà des limites par défaut de hello, premium de ExpressRoute toodisable hello demande échoue.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>Puis-je puis-je choisir les fonctions hello souhaitée à partir de l’ensemble des fonctionnalités premium hello ?

Non. Vous ne pouvez pas sélectionner les fonctions hello. Nous activons toutes les fonctionnalités lorsque vous activez ExpressRoute Premium.

### <a name="how-much-does-expressroute-premium-cost"></a>Combien coûte ExpressRoute Premium ?

Consultez trop[tarification](https://azure.microsoft.com/pricing/details/expressroute/) coût.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Dois-je payer pour ExpressRoute premium en outre toostandard frais d’ExpressRoute ?

Oui. Frais de premium ExpressRoute s’appliquent en plus des frais de circuit ExpressRoute et requis par le fournisseur de connectivité hello.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute pour Office 365 et Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Comment créer un tooconnect de circuit ExpressRoute des services tooOffice 365 et Dynamics 365 ?

1. Hello de révision [page conditions préalables d’ExpressRoute](expressroute-prerequisites.md) toomake respecter les exigences de hello.
2. tooensure a besoin de la connectivité sont remplies, passez en revue la liste hello de fournisseurs de services et des emplacements hello [ExpressRoute partenaires et des emplacements](expressroute-locations.md) l’article.
3. Planifiez vos besoins en capacité en consultant la page [Planification réseau et optimisation des performances pour Office 365](http://aka.ms/tune/).
4. Suivez les étapes de hello répertoriées dans tooset de flux de travail hello la connectivité [flux de travail pour l’approvisionnement et les États du circuit ExpressRoute](expressroute-workflows.md).

> [!IMPORTANT]
> Assurez-vous que vous avez activé complémentaire ExpressRoute lors de la configuration des services de connectivité de tooOffice 365 et Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>Ai-je besoin tooenable Azure publics d’homologation de services de tooconnect tooOffice 365 et Dynamics 365 ?

Non, vous ne devez tooenable Microsoft Peering. L’authentification du trafic tooAzure AD est envoyé via Microsoft Peering. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>Peuvent mon circuits ExpressRoute existants prend en charge les services de connectivité tooOffice 365 et Dynamics 365 ?

Oui. Votre circuit ExpressRoute existant peut être configuré toosupport connectivité tooOffice 365 services. Assurez-vous que vous avez les services tooOffice 365 tooconnect capacité suffisante et que vous avez activé un module complémentaire premium. [Planification réseau et optimisation des performances pour Office 365](http://aka.ms/tune/) vous aide à prévoir vos besoins de connectivité. Voir également [Création et modification d’un circuit ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Quels services Office 365 sont accessibles via une connexion ExpressRoute ?

Consultez trop[plages d’adresses IP et des URL d’Office 365](http://aka.ms/o365endpoints) page pour obtenir une liste des services pris en charge via ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Combien coûte ExpressRoute pour les services Office 365 et Dynamics 365 ?

Les services Office 365 et Dynamics 365 nécessitent toobe du module complémentaire premium activée. Consultez hello [page de détails de tarification](https://azure.microsoft.com/pricing/details/expressroute/) pour les coûts.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Quelles régions sont prises en charge dans ExpressRoute pour Office 365 ?

Consultez [Partenaires et emplacements ExpressRoute ](expressroute-locations.md) pour plus d’informations.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>Puis-je accéder à Office 365 sur hello Internet, même si ExpressRoute a été configuré pour mon organisation ?

Oui. Points de terminaison de service 365 Office sont accessibles via hello Internet, même si ExpressRoute a été configuré pour votre réseau. Si vous êtes dans un emplacement qui est configuré tooconnect tooOffice 365 des services via ExpressRoute, vous vous connectez via ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Puis-je accéder aux services Office 365 US Government Community (GCC) sur un circuit Azure US Government ExpressRoute ?

Oui. Points de terminaison de service Office 365 GCC sont accessibles via hello Azure US Government ExpressRoute. Toutefois, vous première nécessité tooopen prise en charge un ticket sur hello préfixes de hello tooprovide portail Azure vous avez l’intention de tooadvertise tooMicrosoft. Votre tooOffice 365 GCC les services de connectivité seront établies une fois le ticket de support hello est résolu. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Dynamics 365 for Operations (précédemment appelé Dynamics AX Online) est-il accessible par le biais d’une connexion ExpressRoute ?

Oui. [Dynamics 365 pour les opérations](https://www.microsoft.com/dynamics365/operations) est hébergé sur Azure. Vous pouvez activer l’homologation publique Azure sur votre tooit tooconnect du circuit ExpressRoute.

## <a name="route-filters-for-microsoft-peering"></a>Filtres de routage pour l’homologation Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Je suis sous tension homologation Microsoft pour hello première fois, les itinéraires s’affiche ?

Aucun itinéraire ne s’affichera. Vous avez tooattach un filtre tooyour circuit toostart préfixe les annonces de routage. Consultez [Configurer des filtres de routage pour l’homologation Microsoft](how-to-routefilter-powershell.md)pour obtenir des instructions.

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>J’ai activé sur l’homologation, Microsoft et je suis tooselect lors de la tentative Exchange Online, mais il me donne une erreur que je ne suis pas toodo autorisé il.

Lorsque vous utilisez des filtres de routage, n’importe quel client peut activer homologation Microsoft. Toutefois, pour la consommation des services Office 365, vous devez encore tooget autorisé par Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Ai-je besoin d’autorisation de tooget d’activation sur l’homologation Microsoft Dynamics 365 ?

Non, vous n’avez pas besoin d’autorisation pour Dynamics 365. Vous pouvez créer une règle et sélectionner la Communauté Dynamics 365 sans autorisation.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>J’ai déjà homologation Microsoft, comment puis-je tirer parti des filtres de routage ?

Vous pouvez créer un filtre de routage, services hello sélectionnez souhaité toouse, attacher hello filtre tooyour Microsoft homologation. Consultez [Configurer des filtres de routage pour l’homologation Microsoft](how-to-routefilter-powershell.md)pour obtenir des instructions.

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>J’ai Microsoft d’homologation à un emplacement, maintenant j’essaie de tooenable à un autre emplacement et je ne vois pas tous les préfixes.

* Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés via l’homologation Microsoft, même si les filtres de routage ne sont pas définis.

* Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit. Aucun préfixe par défaut ne s’affichera.
