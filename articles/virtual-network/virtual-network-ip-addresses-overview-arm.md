---
title: "types d’adresses aaaIP dans Azure | Documents Microsoft"
description: "Apprenez-en plus sur les adresses IP publiques et privées dans Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Types d’adresses IP et méthodes d’allocation dans Azure
Vous pouvez affecter IP adresses tooAzure ressources toocommunicate avec d’autres ressources Azure, votre réseau local et hello Internet. Les adresses IP que vous pouvez utiliser dans Azure sont de deux types :

* **Les adresses IP publiques**: utilisé pour la communication avec hello Internet, y compris les services publics Azure
* **Adresses IP privées**: utilisé pour la communication au sein d’un réseau virtuel Azure (VNet), et votre site réseau lorsque vous utilisez une passerelle VPN ou un tooextend de circuit ExpressRoute tooAzure de votre réseau.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-ip-addresses-overview-classic.md).
> 

Si vous êtes familiarisé avec le modèle de déploiement classique de hello, vérifiez hello [différences entre classique d’adressage IP et le Gestionnaire de ressources](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Adresses IP publiques
Les adresses IP publiques permettent toocommunicate de ressources Azure avec les services publics Internet et Azure comme [Cache Redis Azure](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [bases de données SQL](../sql-database/sql-database-technical-overview.md), et [le stockage Azure](../storage/common/storage-introduction.md).

Dans Azure Resource Manager, une [adresse IP publique](resource-groups-networking.md#public-ip-address) est une ressource ayant ses propres propriétés. Vous pouvez associer une ressource d’adresse IP publique avec les hello suivant des ressources :

* Machines virtuelles
* Équilibreurs de charge accessibles sur Internet
* Passerelles VPN
* Passerelles d’application

### <a name="allocation-method"></a>Méthode d’allocation
Il existe deux méthodes dans lesquelles une adresse IP est allouée tooa *public* ressource IP - *dynamique* ou *statique*. méthode d’allocation Hello par défaut est *dynamique*, où une adresse IP est **pas** alloué au moment de hello de sa création. Au lieu de cela, adresse IP publique de hello est allouée lorsque vous démarrez (ou créez) ressource hello associé (par exemple, un ordinateur virtuel ou un équilibrage). adresse IP de Hello est libérée lorsque vous arrêtez (ou supprimez) des ressources de hello. Cela provoque une hello IP adresse toochange quand vous arrêter et démarrer une ressource.

adresse IP de hello tooensure de hello ressources associés sont conservées même hello, vous pouvez définir méthode d’allocation de hello explicitement trop*statique*. Dans ce cas, une adresse IP est affectée immédiatement. Elle est libérée uniquement lorsque vous supprimez la ressource de hello ou modifiez sa méthode d’allocation trop*dynamique*.

> [!NOTE]
> Même lorsque vous définissez méthode d’allocation de hello trop*statique*, vous ne pouvez pas spécifier hello réel IP adresse affectée toohello *ressource IP publique*. Au lieu de cela, il est alloué d’un pool d’adresses IP disponibles dans hello emplacement Azure, les ressources hello sont créé dans.
>

Les adresses IP publiques statiques sont couramment utilisées dans hello les scénarios suivants :

* Les utilisateurs finaux doivent toocommunicate de règles de pare-feu tooupdate avec vos ressources Azure.
* La résolution de noms DNS est telle qu’une modification de l’adresse IP nécessiterait une mise à jour des enregistrements A.
* Vos ressources Azure communiquent avec d’autres applications ou services qui utilisent un modèle de sécurité basé sur une adresse IP.
* Vous utilisez adresse tooan lié de certificats SSL.

> [!NOTE]
> Hello la liste des plages d’adresses IP à partir de laquelle les adresses IP publiques (dynamique/statique) tooAzure les ressources sont allouées est publiée à [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Résolution de nom d’hôte DNS
Vous pouvez spécifier une étiquette de nom de domaine DNS pour une ressource IP publique, qui crée un mappage pour *domainnamelabel*. *emplacement*. cloudapp.azure.com toohello adresse IP publique dans les serveurs DNS de Azure-gérés hello. Par exemple, si vous créez une ressource IP publique avec **contoso** comme un *domainnamelabel* Bonjour **ouest des États-Unis** Azure *emplacement*, hello nom de domaine complet (FQDN) **contoso.westus.cloudapp.azure.com** résoudra toohello une adresse IP publique de ressource de hello. Vous pouvez utiliser cette toocreate de nom de domaine complet d’un enregistrement CNAME de domaine personnalisé pointant vers l’adresse IP toohello dans Azure.

> [!IMPORTANT]
> Chaque étiquette de nom de domaine créée doit être unique dans son emplacement Azure.  
>

### <a name="virtual-machines"></a>Machines virtuelles
Vous pouvez associer une adresse IP publique avec une [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) machine virtuelle en lui assignant tooits **interface réseau**. Dans le cas de hello d’une machine virtuelle avec plusieurs interfaces réseau, vous pouvez l’affecter toohello *principal* interface réseau uniquement. Vous pouvez affecter un dynamique ou un tooa d’adresse IP publique statique machine virtuelle.

### <a name="internet-facing-load-balancers"></a>Équilibreurs de charge accessibles sur Internet
Vous pouvez associer une adresse IP publique avec une [équilibrage de charge Azure](../load-balancer/load-balancer-overview.md), en lui assignant toohello l’équilibrage de charge **frontal** configuration. Cette adresse IP publique sert d’adresse IP virtuelle (VIP) à charge équilibrée. Vous pouvez affecter un dynamique ou statique publique IP adresse tooa équilibrage de charge frontal. Vous pouvez également assigner plusieurs publique IP adresses tooa équilibrage de charge frontal, qui permet de [multi-VIP](../load-balancer/load-balancer-multivip.md) scénarios comme une architecture mutualisée avec des sites Web SSL.

### <a name="vpn-gateways"></a>Passerelles VPN
[Passerelle VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md) est tooconnect utilisé un réseau virtuel Azure (VNet) tooother réseaux virtuels Azure ou tooan sur réseau local. Vous devez tooassign une tooits d’adresse IP publique **configuration IP** tooenable il toocommunicate avec un réseau distant hello. Actuellement, vous pouvez uniquement affecter un *dynamique* passerelle du VPN tooa à adresse IP publique.

### <a name="application-gateways"></a>Passerelles d’application
Vous pouvez associer une adresse IP publique Azure [Application Gateway](../application-gateway/application-gateway-introduction.md), en lui assignant la passerelle toohello **frontal** configuration. Cette adresse IP publique sert d’adresse IP virtuelle à équilibrage de charge. Actuellement, vous pouvez uniquement affecter un *dynamique* public tooan application passerelle frontale configuration d’adresse IP.

### <a name="at-a-glance"></a>Aperçu
tableau Hello ci-dessous montre la propriété spécifique de hello qui peut être une adresse IP publique tooa associé les ressources de niveau supérieur et hello possible de méthodes d’allocation (dynamiques ou statiques) qui peuvent être utilisés.

| Ressources de niveau supérieur | Association d’adresse IP | dynamique | statique |
| --- | --- | --- | --- |
| Machine virtuelle |interface réseau |Oui |Oui |
| Équilibrage de charge |Configuration frontale |Oui |Oui |
| Passerelle VPN |Configuration IP de la passerelle |Oui |Non |
| Application Gateway |Configuration frontale |Oui |Non |

## <a name="private-ip-addresses"></a>Adresses IP privées
Autoriser les adresses IP privées toocommunicate de ressources Azure avec d’autres ressources dans un [réseau virtuel](virtual-networks-overview.md) ou un réseau local via une passerelle VPN ou un circuit ExpressRoute, sans utiliser une adresse IP accessible à l’Internet.

Dans le modèle de déploiement du Gestionnaire de ressources Azure hello, une adresse IP privée est toohello associé, les types de ressources Azure suivants :

* Machines virtuelles
* Équilibreurs de charge interne (ILB)
* Passerelles d’application

### <a name="allocation-method"></a>Méthode d’allocation
Une adresse IP privée est allouée à partir de l’adresse de hello plage de ressource de hello sous-réseau toowhich hello est attaché. plage d’adresses Hello du sous-réseau hello lui-même fait partie de la plage d’adresses de réseau virtuel hello.

Il existe deux méthodes d’allocation d’adresses IP : *dynamique* ou *statique*. méthode d’allocation Hello par défaut est *dynamique*, où l’adresse IP de hello est alloué automatiquement à partir du sous-réseau de la ressource hello (à l’aide de DHCP). Cette adresse IP permettre changer lorsque vous arrêter et démarrer les ressources hello.

Vous pouvez définir des méthode d’allocation de hello trop*statique* tooensure hello IP adresse reste hello identiques. Dans ce cas, vous devez également tooprovide une adresse IP valide qui fait partie du sous-réseau de la ressource hello.

Les adresses IP privées statiques sont couramment utilisées pour :

* les ordinateurs virtuels qui agissent en tant que contrôleurs de domaine ou serveurs DNS ;
* les ressources qui nécessitent des règles de pare-feu utilisant des adresses IP ;
* des ressources auxquelles d’autres applications/ressources accèdent via une adresse IP.

### <a name="virtual-machines"></a>Machines virtuelles
Une adresse IP privée est affectée toohello **interface réseau** d’un [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) machine virtuelle. Dans le cas d’une machine virtuelle comportant plusieurs interfaces réseau, une adresse IP privée est affectée à chacune d’elles. Vous pouvez spécifier la méthode d’allocation de hello en tant que dynamique ou statique pour une interface réseau.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Résolution de nom d’hôte DNS interne (pour les machines virtuelles)
Toutes les machines virtuelles Azure sont configurées avec des [serveurs DNS gérés par Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) par défaut, sauf si vous configurez explicitement des serveurs DNS personnalisés. Ces serveurs DNS fournissent la résolution de noms interne pour les machines virtuelles qui résident dans hello même réseau virtuel.

Lorsque vous créez une machine virtuelle, un mappage d’adresse IP privée de hello nom d’hôte tooits est ajouté toohello géré par Azure serveurs. En cas d’une interface réseau multiples machine virtuelle, nom d’hôte hello est mappé toohello une adresse IP privée de l’interface réseau principale de hello.

Machines virtuelles configurées avec des serveurs DNS de Azure-géré sera en mesure de tooresolve hello les noms d’hôte de tous les ordinateurs virtuels au sein de leurs réseau virtuel tootheir des adresses IP privées.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Équilibreurs de charge internes (ILB) et passerelles d’application
Vous pouvez affecter un toohello d’adresse IP privée **frontal** configuration d’un [équilibrage de charge interne Azure](../load-balancer/load-balancer-internal-overview.md) (équilibrage de charge interne) ou un [passerelle d’Application Azure](../application-gateway/application-gateway-introduction.md). Cette adresse IP privée sert de point de terminaison interne, les ressources accessibles toohello uniquement au sein de son réseau virtuel (VNet) et les réseaux distants de hello connecté toohello réseau virtuel. Vous pouvez attribuer soit une dynamique ou statique privées toohello frontal configuration d’adresse IP.

### <a name="at-a-glance"></a>Aperçu
tableau Hello ci-dessous montre la propriété spécifique de hello qui peut être une adresse IP privée tooa associé les ressources de niveau supérieur et hello possible de méthodes d’allocation (dynamiques ou statiques) qui peuvent être utilisés.

| Ressources de niveau supérieur | Association d’adresse IP | dynamique | statique |
| --- | --- | --- | --- |
| Machine virtuelle |interface réseau |Oui |Oui |
| Équilibrage de charge |Configuration frontale |Oui |Oui |
| Application Gateway |Configuration frontale |Oui |Oui |

## <a name="limits"></a>limites
Hello limite imposée sur l’adressage IP est indiqués dans le jeu complet de hello de [limite de mise en réseau](../azure-subscription-service-limits.md#networking-limits) dans Azure. Ces limites sont exprimées par région et par abonnement. Vous pouvez [contactez le support technique](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) limites par défaut du hello tooincrease des limites maximales de toohello selon les besoins de votre entreprise.

## <a name="pricing"></a>Tarification
Les adresses IP publiques peuvent avoir un coût nominal. toolearn savoir plus sur IP adresse tarification dans Azure, consultez hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.

## <a name="next-steps"></a>Étapes suivantes
* [Déployer un ordinateur virtuel avec une adresse IP publique statique à l’aide de hello portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Déployer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle](virtual-network-deploy-static-pip-arm-template.md)
* [Déployer un ordinateur virtuel avec une adresse IP privée statique à l’aide de hello portail Azure](virtual-networks-static-private-ip-arm-pportal.md)
