---
title: "aaaOverview d’IPv6 pour l’équilibrage de charge Azure | Documents Microsoft"
description: "Présentation de la prise en charge du protocole IPv6 par Azure Load Balancer et les machines virtuelles à charge équilibrée."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Vue d’ensemble du protocole IPv6 pour Azure Load Balancer

Des équilibrages de charge accessibles sur Internet peuvent être déployés avec une adresse IPv6. En outre tooIPv4 connectivité, cela permet d’hello suivant de fonctionnalités :

* Bout en bout connectivité IPv6 native entre les clients Internet publics et des Machines virtuelles (VM) Azure via l’équilibrage de charge hello.
* Une connectivité IPv6 de bout en bout native sortante entre les machines virtuelles et les clients Internet publics compatibles IPv6.

Hello illustration suivante illustre les fonctionnalités de hello IPv6 pour l’équilibrage de charge Azure.

![Azure Load Balancer avec IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Une fois déployé, un client IPv4 ou IPv6 activé l’Internet peut communiquer avec hello public adresses IPv4 ou IPv6 ou les noms d’hôte de hello équilibrage de charge Azure-connecté à Internet. itinéraires de programme d’équilibrage de charge Hello hello IPv6 paquets toohello IPv6 des adresses privées des machines virtuelles de hello à l’aide de la traduction d’adresses réseau (NAT). client Internet IPv6 de Hello ne peut pas communiquer directement avec hello IPv6 de hello machines virtuelles.

## <a name="features"></a>Caractéristiques

Une prise en charge IPv6 native pour les machines virtuelles déployées via Azure Resource Manager fournit :

1. Équilibrage de la charge de services IPv6 pour les clients sur hello Internet IPv6
2. Des points de terminaison IPv4 et IPv6 natifs sur les machines virtuelles (« à double pile »)
3. Des connexions IPv6 natives entrantes et sortantes
4. Les protocoles pris en charge tels que TCP, UDP et HTTP(S) permettent de bénéficier d’un large éventail d’architectures de service

## <a name="benefits"></a>Avantages

Cette fonctionnalité permet de hello avantages clés suivants :

* Conformes aux réglementations exigent que les nouvelles applications soient des clients tooIPv6 uniquement accessibles
* Activer mobile et Internet des objets aux développeurs toouse double pile (IPv4 + IPv6) des Machines virtuelles Azure tooaddress hello mobile croissante & IOT marchés

## <a name="details-and-limitations"></a>Détails et limitations

Détails

* Hello service DNS Azure contient les enregistrements de nom A d’IPv4 et IPv6 AAAA et répond avec les deux enregistrements pour l’équilibrage de charge hello. client de Hello choisit l’adresse les toocommunicate (IPv4 ou IPv6) avec.
* Lorsqu’une machine virtuelle lance un périphérique de connexion Internet IPv6 public connexion tooa, adresse IPv6 de la source de machine virtuelle hello est la traduction d’adresses réseau (NAT) toohello adresse IPv6 publique d’équilibrage de charge hello.
* Machines virtuelles exécutant le système d’exploitation de Linux hello doivent être configuré tooreceive une adresse IP IPv6 via DHCP. Un grand nombre d’images de Linux hello Bonjour galerie Azure sont déjà configurées toosupport IPv6 sans modification. Pour plus d’informations, consultez [Configuration de DHCPv6 pour les machines virtuelles Linux](load-balancer-ipv6-for-linux.md)
* Si vous choisissez toouse une intégrité de la sonde avec votre équilibreur de charge, créer une sonde IPv4 et l’utiliser avec hello IPv4 et IPv6 de points de terminaison. Si le service hello sur votre machine virtuelle s’arrête, hello IPv4 et IPv6 de points de terminaison sont effectuées hors rotation.

Limites

* Impossible d’ajouter des règles d’équilibrage de charge IPv6 Bonjour portail Azure. Hello règles peuvent uniquement être créées via le modèle hello, CLI, PowerShell.
* Vous ne pouvez pas mettre à niveau des adresses IPv6 toouse machines virtuelles existantes. Vous devez déployer de nouvelles machines virtuelles.
* Tooa seule interface réseau sur chaque machine virtuelle peut être affectée à une seule adresse IPv6.
* Impossible d’attribuer les adresses IPv6 publiques Hello tooa machine virtuelle. Ils peuvent uniquement être affectés équilibrage de charge tooa.
* Vous ne pouvez pas configurer la recherche DNS inversée hello pour les adresses IPv6 votre publics.
* Hello machines virtuelles avec des adresses IPv6 de hello ne peut pas être membres d’un Service Cloud Azure. Ils peuvent être connecté tooan réseau virtuel Azure (VNet) et communiquent entre eux via leurs adresses IPv4.
* Des adresses IPv6 privées peuvent être déployées sur des machines virtuelles individuelles d’un groupe de ressources, mais ne peuvent pas être déployées dans un groupe de ressources via des jeux de mise à l’échelle.
* Machines virtuelles Azure ne peut pas se connecter via IPv6 tooother VMs, autres services Azure ou les appareils locaux. Ils peuvent uniquement communiquer avec équilibrage de charge Azure hello sur IPv6. Cependant, elles peuvent communiquer avec ces autres ressources à l’aide du protocole IPv4.
* La protection de groupe de sécurité réseau pour IPv4 est prise en charge dans les déploiements à double pile (IPv4 + IPv6). Groupes de sécurité réseau n’appliquent pas de points de terminaison toohello IPv6.
* point de terminaison Hello IPv6 sur hello VM n’est pas directement exposé toohello internet. Il se trouve derrière un équilibreur de charge. Seuls les ports hello spécifiés dans les règles d’équilibrage de charge de hello sont accessibles via IPv6.
* La modification de hello IdleTimeout paramètre IPv6 est **actuellement ne pas pris en charge**. valeur par défaut Hello est de quatre minutes.
* La modification de hello loadDistributionMethod paramètre IPv6 est **actuellement ne pas pris en charge**.
* Les adresses IP IPv6 réservées (où IPAllocationMethod = static) ne sont **pas prises en charge pour le moment**.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toodeploy un équilibreur de charge avec IPv6.

* [Disponibilité du protocole IPv6 par région](https://go.microsoft.com/fwlink/?linkid=828357)
* [Déployer un équilibreur de charge avec IPv6 à l’aide d’un modèle](load-balancer-ipv6-internet-template.md)
* [Déployer un équilibreur de charge avec IPv6 à l’aide d’Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Déployer un équilibreur de charge avec IPv6 à l’aide de l’interface de ligne de commande Azure](load-balancer-ipv6-internet-cli.md)
