---
title: "l’homologation de réseau virtuel aaaAzure | Documents Microsoft"
description: "En savoir plus sur l’homologation de réseaux virtuels dans Azure."
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Homologation de réseaux virtuels
Permet d’homologation de réseau virtuel vous tooconnect deux réseaux virtuels dans hello même région via hello réseau principal Azure. Une fois homologuer, les réseaux virtuels deux hello apparaissent comme un seul, à des fins de connectivité. les réseaux virtuels Hello deux sont toujours gérés comme des ressources distinctes, mais les machines virtuelles dans hello ressources des réseaux virtuels peuvent communiquer directement avec les uns des autres, à l’aide des adresses IP privées.

trafic Hello entre les machines virtuelles dans hello homologuer les réseaux virtuels est routé via hello infrastructure Azure, de la même manière que le trafic est acheminé entre les machines virtuelles dans hello même réseau virtuel. Voici quelques-uns des avantages hello de réseau virtuel d’homologation :

* Connexion à latence faible et haut débit entre les ressources de différents réseaux virtuels.
* Hello capacité toouse les ressources telles que les dispositifs réseau et les passerelles VPN en tant que points de transit dans un réseau virtuel de ressources.
* Hello capacité toopeer deux réseaux virtuels créés via le modèle de déploiement du Gestionnaire de ressources Azure hello ou toopeer un réseau virtuel créé via le Gestionnaire de ressources tooa réseau virtuel créé via le modèle de déploiement classique hello. Hello de lecture [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) toolearn article plus d’informations sur les différences de hello entre les modèles de déploiement Azure hello deux.

## <a name="requirements-constraints"></a>Exigences et contraintes

* Hello ressources des réseaux virtuels doivent exister dans hello même région Azure. Vous pouvez vous connecter à des réseaux virtuels dans différentes régions Azure à l’aide d’une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Hello ressources des réseaux virtuels doivent avoir espaces d’adressage IP sans chevauchement.
* Il n’est pas possible d’ajouter ni de supprimer des espaces d’adressage dans un réseau virtuel une fois que celui-ci est homologué avec un autre réseau virtuel.
* L’homologation se fait entre deux réseaux virtuels. Il n’y a aucune relation transitive entre homologations. Par exemple, si virtualNetworkA est homologué avec virtualNetworkB et virtualNetworkB est homologué avec virtualNetworkC, virtualNetworkA est *pas* toovirtualNetworkC de ressources.
* Vous pouvez d’homologues des réseaux virtuels qui existent dans les deux abonnements différents, comme la durée pendant laquelle un utilisateur doté de privilèges (consultez [des autorisations spécifiques](create-peering-different-deployment-models-subscriptions.md#permissions)) des deux hello d’homologation autorise les abonnements et les abonnements hello sont toohello associé même Client de Azure Active Directory. Vous pouvez utiliser un [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect des réseaux virtuels dans les abonnements associés toodifferent les clients Active Directory.
* Peuvent être homologuer les réseaux virtuels sont créés via le modèle de déploiement du Gestionnaire de ressources hello ou si un réseau virtuel est créé via le modèle de déploiement du Gestionnaire de ressources hello et hello autres est créé via le modèle de déploiement classique hello. Deux réseaux virtuels créés via le modèle de déploiement classique hello ne peut pas être des ressources tooeach autre, cependant. Vous pouvez utiliser un [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect deux des réseaux virtuels créés via le modèle de déploiement classique hello.
* Si la communication hello entre les machines virtuelles dans des réseaux virtuels ressources n’a aucune restriction de la bande passante supplémentaire, il existe une bande passante maximale en fonction de la taille de machine virtuelle hello qui s’appliquent toujours. toolearn plus d’informations sur la bande passante réseau maximale pour les tailles de machine virtuelle différente, lire hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle.
* La résolution de noms DNS internes fournie par Azure pour les machines virtuelles ne fonctionne pas entre des réseaux virtuels homologués. Machines virtuelles ont des noms DNS internes qui peuvent être résolus uniquement dans le réseau virtuel local de hello. Toutefois, vous pouvez configurer des réseaux virtuels de machines virtuelles connectées toopeered en tant que serveurs DNS pour un réseau virtuel. Pour plus d’informations, consultez hello [résolution de noms à l’aide de votre propre serveur DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) l’article.

![Homologation de réseaux virtuels de base](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Connectivité
Une fois que les deux réseaux virtuels sont appariés, ressources dans un réseau virtuel peuvent se connecter directement des ressources dans un réseau virtuel de hello ressources. les réseaux virtuels Hello deux ont le niveau IP complète connectivité.

latence du réseau Hello pour un aller-retour entre deux ordinateurs virtuels dans des réseaux virtuels ressources est hello même que pour un aller-retour au sein d’un seul réseau virtuel. débit du réseau Hello est basé sur la bande passante hello qui est autorisée pour l’ordinateur virtuel de hello, proportionnées tooits taille. Il n’existe pas de n’importe quel restriction supplémentaire sur la bande passante dans hello d’homologation.

le trafic de Hello entre les machines virtuelles dans des réseaux virtuels ressources est acheminé directement par le biais de hello Azure infrastructure principale, pas par le biais d’une passerelle.

Réseau virtuel de machines virtuelles tooa connecté peut accéder hello équilibrés en charge points de terminaison internes dans le réseau virtuel de hello ressources. Groupes de sécurité réseau peuvent être appliquées dans les réseaux virtuels de réseau virtuel tooblock accès tooother ou sous-réseaux, si vous le souhaitez.

Lors de la configuration d’homologation de réseau virtuel, vous pouvez ouvrir ou fermer des règles de groupe de sécurité de réseau hello entre les réseaux virtuels hello. Si vous ouvrez une connectivité totale entre les ressources réseaux virtuels (qui est l’option par défaut de hello), vous pouvez appliquer le réseau sécurité groupes toospecific sous-réseaux ou des machines virtuelles tooblock ou refuser l’accès spécifique. toolearn en savoir plus sur les groupes de sécurité du réseau de lire hello [présentation des groupes de sécurité réseau](virtual-networks-nsg.md) l’article.

## <a name="service-chaining"></a>Chaînage de services
Vous pouvez configurer des itinéraires définis par l’utilisateur qui point toovirtual des ordinateurs dans des réseaux virtuels ressources comme hello « de tronçon suivant » IP adresse tooenable chaînage de services. Chaînage de service permet de vous toodirect le trafic à partir d’une appliance virtuelle tooa de réseau virtuel dans un réseau virtuel ressources via les itinéraires définis par l’utilisateur.

Vous pouvez également créer des environnements de type de hub and spoke, où les hub hello peut héberger des composants d’infrastructure comme un réseau virtuel. Tous les réseaux virtuels spoke de hello peuvent ensuite homologue avec le réseau virtuel du concentrateur hello. Le trafic peut passer par dispositifs réseau virtuel qui sont exécutent dans le réseau virtuel du concentrateur hello. En bref, réseau virtuel d’homologation permet hello IP adresse du tronçon suivant sur hello défini par l’utilisateur itinéraire toobe hello adresse d’un ordinateur virtuel dans le réseau virtuel de hello ressources. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [vue d’ensemble des itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.

## <a name="gateways-and-on-premises-connectivity"></a>Passerelles et connectivité locale
Chaque réseau virtuel, indépendamment de si elle est homologué avec un autre réseau virtuel, peut encore avoir sa propre passerelle et utilisez-la tooconnect tooan sur réseau local. Vous pouvez également configurer [les connexions réseau-à-virtuel virtuel](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) à l’aide des passerelles, même si les réseaux virtuels hello sont appariés.

Lorsque les deux options pour l’interconnexion de réseau virtuel sont configurées, hello le trafic entre les réseaux virtuels hello acheminé via la configuration d’homologation de hello (autrement dit, via hello backbone Azure).

Lorsque les réseaux virtuels sont appariés, vous pouvez également configurer la passerelle de hello dans le réseau virtuel de hello ressources comme un réseau local de tooan de point de transit. Dans ce cas, le réseau virtuel hello qui utilise une passerelle à distance ne peut pas avoir sa propre passerelle. Un réseau virtuel ne peut posséder qu’une seule passerelle. passerelle de Hello peut avoir une passerelle locale ou distante (hello ressources réseau virtuel), comme indiqué dans hello illustration suivante :

![Transit entre des réseaux virtuels homologués](./media/virtual-networks-peering-overview/figure02.png)

Transit de la passerelle n’est pas prise en charge de la relation d’homologation de hello entre réseaux virtuels créés par le biais des modèles de déploiement différentes. Les deux réseaux virtuels dans une relation d’homologation hello doit avoir été créé par le biais du Gestionnaire de ressources pour un toowork de transit de passerelle.

Lorsque les réseaux virtuels hello qui partagent une seule connexion d’Azure ExpressRoute sont appariés, trafic de hello entre eux est envoyé via la relation d’homologation hello (autrement dit, via hello réseau Azure principal). Vous pouvez toujours utiliser des passerelles locales dans chaque circuit de réseau virtuel tooconnect toohello local. Vous pouvez également utiliser une passerelle partagée et configurer le transit pour la connectivité locale.

## <a name="provisioning"></a>Approvisionnement
L’homologation de réseaux virtuels est une opération nécessitant des privilèges. Il est une fonction distincte sous l’espace de noms VirtualNetworks hello. Un utilisateur peut recevoir d’homologation de tooauthorize des droits spécifiques. Un utilisateur disposant de réseau virtuel de l’accès en lecture / écriture toohello hérite automatiquement de ces droits.

Un utilisateur qui est un administrateur ou un utilisateur doté de privilèges de capacité d’homologation de hello peut lancer une opération d’homologation sur un autre réseau virtuel. S’il existe une requête correspondante pour l’homologation sur hello autre côté, et si d’autres conditions sont remplies, hello d’homologation est établie.

## <a name="limits"></a>limites
Il existe des limites sur le nombre hello des homologations qui sont autorisées pour un seul réseau virtuel. Pour plus d’informations, consultez hello [limite de mise en réseau Azure](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Tarification
Un coût nominal s’applique pour le trafic entrant et sortant qui utilise une homologation de réseau virtuel. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Étapes suivantes

* Suivez un didacticiel d’homologation de réseaux virtuels. Une homologation de réseau virtuel est créée entre les réseaux virtuels créés via hello même, ou des modèles de déploiement différentes qui existent dans hello identiques ou différents abonnements. Suivre un didacticiel pour l’une des hello les scénarios suivants :
 
    |Modèle de déploiement Azure  | Abonnement  |
    |---------|---------|
    |Les deux modèles Resource Manager |[Identique](virtual-network-create-peering.md)|
    | |[Différent](create-peering-different-subscriptions.md)|
    |Un modèle Resource Manager, un modèle classique     |[Identique](create-peering-different-deployment-models.md)|
    | |[Différent](create-peering-different-deployment-models-subscriptions.md)|

* Découvrez comment toocreate un [topologie de réseau hub and spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* En savoir plus sur tous les [paramètres d’homologation de réseau virtuel et comment toochange les](virtual-network-manage-peering.md)
