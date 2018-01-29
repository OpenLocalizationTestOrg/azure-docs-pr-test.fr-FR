---
title: "Vue d’ensemble du protocole IPv6 pour Azure Load Balancer | Microsoft Docs"
description: "Présentation de la prise en charge du protocole IPv6 par Azure Load Balancer et les machines virtuelles à charge équilibrée."
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
editor: 
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 1902475c81c4f83f8ba69a05f9564bc65a5de833
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Vue d’ensemble du protocole IPv6 pour Azure Load Balancer


[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

Des équilibrages de charge accessibles sur Internet peuvent être déployés avec une adresse IPv6. En plus d’une connectivité IPv4, les fonctionnalités suivantes sont activées :

* Une connectivité IPv6 de bout en bout native entre les clients Internet publics et les machines virtuelles Azure via l’équilibrage de charge
* Une connectivité IPv6 de bout en bout native sortante entre les machines virtuelles et les clients Internet publics compatibles IPv6.

L’image suivante illustre la fonctionnalité IPv6 pour Azure Load Balancer.

![Azure Load Balancer avec IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Une fois déployé, un client Internet compatible IPv4 ou IPv6 peut communiquer avec les adresses (ou noms d’hôte) IPv4 ou IPv6 publiques de l’équilibrage de charge accessible sur Internet d’Azure. L’équilibrage de charge achemine les paquets IPv6 vers les adresses IPv6 privées des machines virtuelles à l’aide de la traduction d’adresses réseau (NAT). Le client Internet IPv6 ne peut pas communiquer directement avec l’adresse IPv6 des machines virtuelles.

## <a name="features"></a>Caractéristiques

Une prise en charge IPv6 native pour les machines virtuelles déployées via Azure Resource Manager fournit :

1. Des services IPv6 à charge équilibrée pour les clients IPv6 sur Internet
2. Des points de terminaison IPv4 et IPv6 natifs sur les machines virtuelles (« à double pile »)
3. Des connexions IPv6 natives entrantes et sortantes
4. Les protocoles pris en charge tels que TCP, UDP et HTTP(S) permettent de bénéficier d’un large éventail d’architectures de service

## <a name="benefits"></a>Avantages

Cette fonctionnalité offre les avantages clés suivants :

* Elle garantit le respect des réglementations gouvernementales exigeant que les nouvelles applications soient accessibles aux clients IPv6 uniquement
* Elle permet aux développeurs mobiles et de l’Internet des objets (IoT) d’utiliser des machines virtuelles à double pile (IPv4 + IPv6) pour répondre à la demande des marchés croissants du mobile et de l’IoT

## <a name="details-and-limitations"></a>Détails et limitations

Détails

* Le service Azure DNS contient les enregistrements de nom IPv4 A et IPv6 AAAA et répond avec les deux enregistrements pour l’équilibrage de charge. Le client choisit l’adresse (IPv4 ou IPv6) avec laquelle communiquer.
* Lorsqu’une machine virtuelle amorce une connexion à un appareil IPv6 connecté à l’Internet public, le NAT fait correspondre l’adresse IPv6 source de la machine virtuelle à l’adresse IPv6 publique de l’équilibrage de charge.
* Les machines virtuelles exécutant le système d’exploitation Linux doivent être configurées pour recevoir une adresse IP IPv6 via DHCP. Un grand nombre des images Linux disponibles dans la galerie Azure sont déjà configurées pour prendre en charge IPv6 sans modification. Pour plus d’informations, consultez [Configuration de DHCPv6 pour les machines virtuelles Linux](load-balancer-ipv6-for-linux.md)
* Si vous choisissez d’utiliser une sonde d’intégrité avec votre équilibrage de charge, créez une sonde IPv4 et utilisez-la avec les points de terminaison IPv4 et IPv6. Si le service de votre machine virtuelle devient indisponible, les points de terminaison IPv4 et IPv6 sont mis hors service.

Limitations

* Vous ne pouvez pas ajouter de règles d’équilibrage de charge IPv6 dans le portail Azure. Les règles peuvent uniquement être créées via le modèle, l’interface CLI et PowerShell.
* Vous ne pouvez pas mettre à niveau des machines virtuelles existantes de sorte qu’elles utilisent des adresses IPv6. Vous devez déployer de nouvelles machines virtuelles.
* Une adresse IPv6 peut être affectée à une interface réseau unique dans chaque machine virtuelle.
* Les adresses IPv6 publiques ne peuvent être affectées à une machine virtuelle. Elles peuvent uniquement être affectées à un équilibrage de charge.
* Vous ne pouvez pas configurer la recherche DNS inversée pour les adresses IPv6 publiques.
* Les machines virtuelles dotées d’adresses IPv6 ne peuvent pas être membres d’un service cloud Azure. Elles peuvent être connectées à un réseau virtuel (VNet) Azure (VNet) et communiquer entre elles via leurs adresses IPv4.
* Des adresses IPv6 privées peuvent être déployées sur des machines virtuelles individuelles d’un groupe de ressources, mais ne peuvent pas être déployées dans un groupe de ressources via des jeux de mise à l’échelle.
* Les machines virtuelles Azure ne peuvent pas se connecter via IPv6 à d’autres machines virtuelles, d’autres services Azure ou des appareils locaux. Elles peuvent uniquement communiquer avec l’équilibrage de charge Azure via IPv6. Cependant, elles peuvent communiquer avec ces autres ressources à l’aide du protocole IPv4.
* La protection de groupe de sécurité réseau pour IPv4 est prise en charge dans les déploiements à double pile (IPv4 + IPv6). Les groupes de sécurité réseau ne s’appliquent pas aux points de terminaison IPv6.
* Le point de terminaison IPv6 sur la machine virtuelle n’est pas exposé directement à Internet. Il se trouve derrière un équilibreur de charge. Seuls les ports spécifiés dans les règles d’équilibrage de charge sont accessibles via IPv6.
* La modification du paramètre IdleTimeout pour IPv6 n’est **pas prise en charge pour le moment**. La valeur par défaut est de quatre minutes.
* La modification du paramètre loadDistributionMethod pour IPv6 n’est **pas prise en charge pour le moment**.
* Les adresses IP IPv6 réservées (où IPAllocationMethod = static) ne sont **pas prises en charge pour le moment**.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment déployer un équilibreur de charge avec IPv6.

* [Disponibilité du protocole IPv6 par région](https://go.microsoft.com/fwlink/?linkid=828357)
* [Déployer un équilibreur de charge avec IPv6 à l’aide d’un modèle](load-balancer-ipv6-internet-template.md)
* [Déployer un équilibreur de charge avec IPv6 à l’aide d’Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Déployer un équilibreur de charge avec IPv6 à l’aide de l’interface de ligne de commande Azure](load-balancer-ipv6-internet-cli.md)
