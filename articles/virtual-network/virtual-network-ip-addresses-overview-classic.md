---
title: "types d’adresses aaaIP dans Azure (classique) | Documents Microsoft"
description: "Découvrez plus en détail les adresses IP publiques et privées (Classic) dans Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Types d’adresses IP et méthodes d’allocation (classiques) dans Azure
Vous pouvez affecter IP adresses tooAzure ressources toocommunicate avec d’autres ressources Azure, votre réseau local et hello Internet. Les adresses IP que vous pouvez utiliser dans Azure sont de deux types : publiques et privées.

Les adresses IP publiques sont utilisées pour la communication avec hello Internet, y compris les services Azure publique.

Lorsque vous utilisez une passerelle VPN ou un tooextend de circuit ExpressRoute tooAzure de votre réseau, les adresses IP privées sont utilisées pour la communication au sein d’un réseau virtuel Azure (VNet), un service cloud et votre réseau local.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser Resource Manager. En savoir plus sur les adresses IP dans le Gestionnaire de ressources lors de la lecture de hello [des adresses IP](virtual-network-ip-addresses-overview-arm.md) l’article.

## <a name="public-ip-addresses"></a>Adresses IP publiques
Les adresses IP publiques permettent toocommunicate de ressources Azure avec les services publics Internet et Azure comme [Cache Redis Azure](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [bases de données SQL](../sql-database/sql-database-technical-overview.md), et [le stockage Azure](../storage/common/storage-introduction.md).

Une adresse IP publique est associée à hello les types de ressources suivants :

* Services cloud
* Machines virtuelles (VM) IaaS
* Instances de rôle PaaS
* Passerelles VPN
* Passerelles d’application

### <a name="allocation-method"></a>Méthode d’allocation
Lorsqu’une adresse IP publique doit toobe affecté tooan ressource Azure, il est *dynamiquement* alloué d’un pool d’adresse IP publique disponible, adresse au sein de la ressource de type hello emplacement hello est créé. Cette adresse IP est diffusée à la ressource de hello est arrêtée. En cas d’un service cloud, cela se produit lorsque toutes les instances de rôle hello sont arrêtés, qui peut être évité en utilisant un *statique* (réservé) adresse IP (consultez [Services de cloud computing](#Cloud-services)).

> [!NOTE]
> Hello la liste des plages d’adresses IP à partir de laquelle les adresses IP publiques tooAzure les ressources sont allouées est publiée à [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>Résolution de nom d’hôte DNS
Lorsque vous créez un service cloud ou un VM IaaS, vous devez tooprovide un nom DNS de service cloud qui est unique pour toutes les ressources dans Azure. Cette opération crée un mappage Bonjour serveurs gérés par Azure pour *dnsname*. cloudapp.net toohello adresse IP publique de ressource de hello. Par exemple, lorsque vous créez un service cloud avec un nom DNS du service cloud de **contoso**, nom de domaine complet de hello (FQDN) **contoso.cloudapp.net** résoudra tooa adresse IP publique (VIP) de service de cloud Hello. Vous pouvez utiliser cette toocreate de nom de domaine complet d’un enregistrement CNAME de domaine personnalisé pointant vers l’adresse IP toohello dans Azure.

### <a name="cloud-services"></a>Services cloud
Un service cloud a toujours une adresse IP publique adresse tooas auxquels une adresse IP virtuelle (VIP). Vous pouvez créer des points de terminaison dans un cloud service tooassociate des ports différents ports de toointernal VIP hello sur des machines virtuelles et instances de rôle au sein du service de cloud computing hello. 

Un service cloud peut contenir plusieurs IaaS machines virtuelles ou instances de rôle PaaS, tous exposés via hello la même adresse IP virtuelle de service cloud. Vous pouvez également affecter [service de cloud de plusieurs adresses IP virtuelles tooa](../load-balancer/load-balancer-multivip.md), ce qui permet des scénarios de plusieurs adresses IP virtuelles comme environnement mutualisé avec des sites Web SSL.

Vous pouvez garantir l’adresse IP publique de hello d’un service cloud reste hello identiques, même si tous les hello des instances de rôle sont arrêtés, à l’aide un *statique* adresse IP publique, auxquels tooas [adresse IP réservée](virtual-networks-reserved-public-ip.md). Vous pouvez créer une ressource IP (réservée) statique dans un emplacement spécifique et affecter le service de cloud computing tooany à cet emplacement. Vous ne pouvez pas spécifier l’adresse IP réelle de hello pour l’adresse IP réservée de hello, elle est allouée à partir du pool d’adresses IP disponibles dans l’emplacement hello qu'il est créé. Cette adresse IP n'est pas libérée jusqu'à ce que vous la supprimiez explicitement.

Statique des adresses IP publiques (réservés) sont couramment utilisés dans les scénarios de hello lorsqu’un service cloud :

* nécessite l’installation de toobe de règles de pare-feu par les utilisateurs finaux.
* varie selon la résolution de noms DNS externe (une adresse IP dynamique nécessite la mise à jour des enregistrements A) ;
* consomme les services web externes qui utilisent le modèle de sécurité basé sur IP ;
* utilise l’adresse tooan lié de certificats SSL.

> [!NOTE]
> Quand vous créez une machine virtuelle classique, un *service cloud* conteneur est créé par Azure, qui a une adresse IP virtuelle (VIP). Lorsque la création de hello est effectuée via le portail, la valeur par défaut RDP ou SSH *point de terminaison* est configurée par le portail de hello pour vous connecter via l’adresse IP virtuelle de service de cloud hello toohello machine virtuelle. Cette adresse IP virtuelle du service cloud peut être réservée, qui fournit un toohello de tooconnect adresse IP réservée machine virtuelle. Vous pouvez ouvrir des ports supplémentaires en configurant d’autres points de terminaison.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>Instances de rôle des machines virtuelles IaaS et PaaS
Vous pouvez affecter un public d’adresses IP directement tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou instance de rôle PaaS dans un service cloud. Il s’agit de tooas auxquels une adresse IP publique de niveau de l’instance ([ILPIP](virtual-networks-instance-level-public-ip.md)). Cette adresse IP publique peut uniquement être dynamique.

> [!NOTE]
> Cela est différent de hello adresse IP virtuelle du service de cloud hello, qui est un conteneur pour les instances de rôle des machines virtuelles IaaS ou PaaS, car un service cloud peut contenir plusieurs machines virtuelles IaaS ou des instances de rôle PaaS, tous exposés via hello même adresse IP virtuelle du service de cloud.
> 
> 

### <a name="vpn-gateways"></a>Passerelles VPN
A [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) peut être utilisé tooconnect un tooother de réseau virtuel Azure réseaux réseaux virtuels Azure ou localement. Une passerelle VPN est affectée une adresse IP publique *dynamiquement*, ce qui permet la communication avec le réseau distant de hello.

### <a name="application-gateways"></a>Passerelles d’application
Azure [passerelle d’Application](../application-gateway/application-gateway-introduction.md) peut être utilisé pour Layer7 trafic de réseau tooroute de l’équilibrage de charge basé sur HTTP. Passerelle d’application est affectée à une adresse IP publique *dynamiquement*, qui sert de hello VIP d’équilibrage de la charge.

### <a name="at-a-glance"></a>Aperçu
tableau Hello ci-dessous montre chaque type de ressource avec des méthodes d’allocation possible hello (dynamique/statique) et capacité tooassign plusieurs adresses IP publiques.

| Ressource | Dynamique | statique | Plusieurs adresses IP |
| --- | --- | --- | --- |
| service cloud |Oui |Oui |Oui |
| Instance de rôle PaaS ou VM IaaS |Oui |Non |Non |
| passerelle VPN |Oui |Non |Non |
| passerelle d’application |Oui |Non |Non |

## <a name="private-ip-addresses"></a>Adresses IP privées
Les adresses IP privées autoriser toocommunicate de ressources Azure avec d’autres ressources dans un service cloud ou un [réseau virtuel](virtual-networks-overview.md)(VNet), ou de réseau local tooon (via une passerelle VPN ou un circuit ExpressRoute) sans utiliser un Chaque adresse IP accessible à l’Internet.

Dans le modèle de déploiement classique Azure, une adresse IP privée peut être attribuée toohello suivant des ressources Azure :

* Instances de rôle des machines virtuelles IaaS et PaaS
* Équilibreur de charge interne
* passerelle d’application

### <a name="iaas-vms-and-paas-role-instances"></a>Instances de rôle des machines virtuelles IaaS et PaaS
Machines virtuelles (VM) créés avec le modèle de déploiement classique de hello sont toujours placées dans un service cloud, les instances de rôle tooPaaS similaire. comportement de Hello d’adresses IP privées sont donc similaires pour ces ressources.

Il est important toonote un service cloud pouvant être déployées de deux manières :

* en tant que service cloud *autonome* , en dehors d’un réseau virtuel ;
* déployé dans un réseau virtuel.

#### <a name="allocation-method"></a>Méthode d’allocation
Dans le cas d’un *autonome* service cloud, obtenir des ressources d’allouer une adresse IP privée *dynamiquement* plage d’adresses de l’IP privé du centre de données Azure hello. Il peut être utilisé uniquement pour la communication avec les autres ordinateurs virtuels au sein de hello même service cloud. Cette adresse IP peut changer lors de la ressource de hello est arrêté et démarré.

En cas d’un service cloud déployé dans un réseau virtuel, les ressources obtenir privés ou les adresses IP allouées à partir de la plage d’adresses hello Hello associées trouvées (comme spécifié dans sa configuration de réseau). Cette adresse IP privée utilisable pour la communication entre tous les ordinateurs virtuels au sein de hello réseau virtuel.

Par ailleurs, en cas de services cloud au sein d'un VNet, une adresse IP privée est allouée *dynamiquement* (à l'aide de DHCP) par défaut. Il peut changer lors de la ressource de hello est arrêté et démarré. tooensure hello IP adresse reste hello même, vous devez méthode d’allocation tooset hello trop*statique*et fournir une adresse IP valide au sein de la plage d’adresses hello correspondante.

Les adresses IP privées statiques sont couramment utilisées pour :

* les machines virtuelles qui agissent en tant que contrôleurs de domaine ou serveurs DNS ;
* les machines virtuelles qui nécessitent des règles de pare-feu utilisant des adresses IP ;
* les machines virtuelles auxquelles d’autres applications accèdent via une adresse IP.

#### <a name="internal-dns-hostname-resolution"></a>Résolution du nom d’hôte DNS interne
Toutes instances de rôle PaaS et les machines virtuelles Azure sont configurées avec des [serveurs DNS gérés par Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) par défaut, sauf si vous configurez explicitement des serveurs DNS personnalisés. Ces serveurs DNS fournissent la résolution de noms interne pour les machines virtuelles et instances de rôle qui résident dans hello même réseau virtuel ou un service cloud.

Lorsque vous créez une machine virtuelle, un mappage d’adresse IP privée de hello nom d’hôte tooits est ajouté toohello géré par Azure serveurs. En cas d’une machine virtuelle multi-NIC, nom d’hôte hello est mappé toohello une adresse IP privée de la carte réseau principale de hello. Toutefois, ces informations de mappage sont restreint tooresources dans hello même service cloud ou réseau virtuel.

Dans le cas d’un *autonome* service cloud, vous serez en mesure de tooresolve les noms d’hôte de toutes les instances de machines virtuelles/rôle au sein de hello même service de cloud computing uniquement. En cas d’un service cloud dans un réseau virtuel, vous serez en mesure de tooresolve les noms d’hôtes de toutes les instances de machines virtuelles/rôle hello dans hello réseau virtuel.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Équilibreurs de charge internes (ILB) et passerelles d’application
Vous pouvez affecter un toohello d’adresse IP privée **frontal** configuration d’un [équilibrage de charge interne Azure](../load-balancer/load-balancer-internal-overview.md) (équilibrage de charge interne) ou un [passerelle d’Application Azure](../application-gateway/application-gateway-introduction.md). Cette adresse IP privée sert de point de terminaison interne, les ressources accessibles toohello uniquement au sein de son réseau virtuel (VNet) et les réseaux distants de hello connecté toohello réseau virtuel. Vous pouvez attribuer soit une dynamique ou statique privées toohello frontal configuration d’adresse IP. Vous pouvez également affecter plusieurs scénarios de plusieurs adresses IP virtuelles IP adresses tooenable privé.

### <a name="at-a-glance"></a>Aperçu
tableau Hello ci-dessous montre chaque type de ressource avec des méthodes d’allocation possible hello (dynamique/statique) et capacité tooassign plusieurs adresses IP privées.

| Ressource | Dynamique | statique | Plusieurs adresses IP |
| --- | --- | --- | --- |
| Machine virtuelle (dans un service cloud *autonome* ) |Oui |Oui |Oui |
| Instance de rôle PaaS (dans un service cloud *autonome* ) |Oui |Non |Oui |
| Instance de rôle PaaS ou VM (dans un VNet) |Oui |Oui |Oui |
| Équilibreur de charge interne frontal |Oui |Oui |Oui |
| Passerelle d’application frontale |Oui |Oui |Oui |

## <a name="limits"></a>limites
tableau Hello ci-dessous indique les limites de hello imposées IP de l’adressage dans Azure par abonnement. Vous pouvez [contactez le support technique](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) limites par défaut du hello tooincrease des limites maximales de toohello selon les besoins de votre entreprise.

|  | Limite par défaut | Limite maximale |
| --- | --- | --- |
| Adresses IP publiques (dynamiques) |5 |contacter le support |
| Adresses IP publiques réservées |20 |contacter le support |
| Adresse IP virtuelle publique par déploiement (service cloud) |5 |contacter le support |
| Adresse IP virtuelle privée (ILB) par déploiement (service cloud) |1 |1 |

Assurez-vous de lire le jeu complet de hello de [limite de mise en réseau](../azure-subscription-service-limits.md#networking-limits) dans Azure.

## <a name="pricing"></a>Tarification
Dans la plupart des cas, les adresses IP publiques sont gratuites. Il existe un coût nominal toouse supplémentaires et/ou statiques des adresses IP publiques. Assurez-vous que vous comprenez hello [structure de prix pour des adresses IP publiques](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Différences entre les déploiements Resource Manager et Classic
Voici une comparaison des fonctionnalités d’adressage IP dans le Gestionnaire de ressources et le modèle de déploiement classique hello.

|  | Ressource | Classique | Gestionnaire de ressources |
| --- | --- | --- | --- |
| **Adresse IP publique** |***Machine virtuelle*** |Tooas auxquels un ILPIP (dynamique uniquement) |Visés tooas une adresse IP publique (dynamique ou statique) |
|  ||Tooan attribué IaaS VM ou une instance de rôle PaaS |Carte réseau de l’ordinateur virtuel toohello associé | |
|  |***Équilibreur de charge accessible sur Internet*** |Visés tooas VIP (dynamique) ou l’adresse IP réservée (statique) |Visés tooas une adresse IP publique (dynamique ou statique) | |
|  ||Service de cloud computing tooa attribué |Toohello associé charger la configuration de serveur frontal d’équilibrage | |
|  | | | |
| **Adresse IP privée** |***Machine virtuelle*** |Tooas auxquels une adresse DIP |Visés tooas une adresse IP privée |
|  ||Tooan attribué IaaS VM ou une instance de rôle PaaS |Carte réseau de l’ordinateur virtuel toohello attribué | |
|  |***Équilibreur de charge interne*** |Toohello attribué équilibrage de charge interne (dynamique ou statique) |Configuration de frontal d’équilibrage de charge toohello attribué (dynamique ou statique) | |

## <a name="next-steps"></a>Étapes suivantes
* [Déployer un ordinateur virtuel avec une adresse IP privée statique](virtual-networks-static-private-ip-classic-pportal.md) à l’aide de hello portail Azure.

