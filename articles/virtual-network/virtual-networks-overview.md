---
title: "aaaAzure réseau virtuel | Documents Microsoft"
description: "Découvrez les concepts et les fonctionnalités du réseau virtuel Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Réseau virtuel Azure

Bonjour permet de service de réseau virtuel Azure vous toosecurely connecter des ressources Azure tooeach autres avec des réseaux virtuels (réseaux virtuels). Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique de hello Azure cloud dédié tooyour abonnement. Vous pouvez également connecter le réseau local de tooyour des réseaux virtuels. Hello illustration suivante montre certaines fonctionnalités de hello des hello service de réseau virtuel Azure :

![Diagramme du réseau](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn en savoir plus sur hello suivant les fonctionnalités de réseau virtuel Azure, cliquez sur la fonctionnalité de hello :
- **[Isolement :](#isolation)** les réseaux virtuels sont isolés les uns des autres. Vous pouvez créer des réseaux virtuels distincts pour le développement, test et de production que hello utilisez mêmes blocs d’adresses CIDR. À l’inverse, vous pouvez créer plusieurs réseaux virtuels qui utilisent différents blocs d’adresses CIDR et connecter les réseaux entre eux. Vous pouvez segmenter un réseau virtuel en plusieurs sous-réseaux. Azure fournit la résolution de noms interne pour les machines virtuelles et instances de rôle Services de cloud computing connecté tooa réseau virtuel. Vous pouvez éventuellement configurer un réseau virtuel toouse vos propres serveurs DNS, au lieu d’utiliser la résolution de noms interne Azure.
- **[Connectivité Internet :](#internet)**  tous les Azure Machines virtuelles (VM) et les Services de cloud computing des instances de rôle tooa connecté réseau virtuel ont accèdent toohello Internet, par défaut. Vous pouvez également activer des ressources toospecific accès entrant, en fonction des besoins.
- **[Connectivité de la ressource Azure :](#within-vnet)**  ressources Azure telles que les Services de cloud computing et machines virtuelles peuvent être connecté toohello même réseau virtuel. ressources de Hello peuvent se connecter tooeach autres privé adresses IP, même si elles sont dans des sous-réseaux différents. Azure fournit par défaut le routage entre sous-réseaux, les réseaux virtuels et sur des réseaux locaux, afin que vous n’avez tooconfigure et gérer les itinéraires.
- **[Connectivité de réseau virtuel :](#connect-vnets)**  des réseaux virtuels peuvent être connectée tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooany avec n’importe quelle ressource sur n’importe quel autre réseau virtuel.
- **[Connectivité locale :](#connect-on-premises)**  des réseaux virtuels peuvent être connectés tooon des réseaux locaux par le biais des connexions de réseau privé entre votre réseau et Azure, ou via une connexion VPN de site à site sur Internet de hello.
- **[Filtrage du trafic :](#filtering)** le trafic réseau entrant et sortant des machines virtuelles et des instances de rôle Services cloud peut être filtré par adresse IP source et de port, adresse IP de destination et port, et protocole.
- **[Routage :](#routing)** vous pouvez également remplacer le routage Azure par défaut en configurant votre propre routage ou en utilisant des routes BGP via une passerelle réseau.

## <a name = "isolation"></a>Isolement et segmentation du réseau

Vous pouvez implémenter plusieurs réseaux virtuels au sein de chaque [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) Azure et de chaque [région](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region) Azure. Chaque réseau virtuel est isolé des autres réseaux virtuels. Pour chaque réseau virtuel, vous pouvez :
- Spécifier un espace d’adressage IP privé personnalisé à l’aide d’adresses (RFC 1918) publiques et privées. Azure attribue toohello connecté de ressources réseau virtuel d’une adresse IP privée à partir de l’espace d’adressage hello que vous attribuez.
- Segment hello réseau virtuel dans un ou plusieurs sous-réseaux et allouer une partie du sous-réseau tooeach d’espace d’adresses réseau virtuel de hello.
- Utiliser la résolution de noms fournie par Azure ou spécifier que votre propre serveur DNS pour une utilisation par les ressources connectées tooa réseau virtuel. toolearn plus sur la résolution de noms dans les réseaux virtuels, lire hello [la résolution de noms pour les ordinateurs virtuels et Services de cloud computing](virtual-networks-name-resolution-for-vms-and-role-instances.md) l’article.

## <a name = "internet"></a>Se connecter toohello Internet
Toutes les ressources de tooa connecté réseau virtuel ont connectivité sortante toohello Internet par défaut. Hello adresse IP privée de ressource de hello est l’adresse IP publique de (SNAT) tooa de traduction d’adresses de réseau source par hello infrastructure Azure. toolearn plus en détail la connectivité Internet sortante, lire hello [présentation des connexions sortantes dans Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) l’article. Vous pouvez modifier la connexion par défaut de hello en implémentant un routage personnalisé et un filtrage du trafic.

toocommunicate entrant tooAzure ressources hello Internet ou toocommunicate toohello sortant Internet sans SNAT, une ressource doit être affectée à une adresse IP publique. toolearn plus d’informations sur les adresses IP publiques, lire hello [des adresses IP publiques](virtual-network-public-ip-address.md) l’article.

## <a name="within-vnet"></a>Connecter des ressources Azure
Vous pouvez connecter plusieurs ressources Azure tooa réseau virtuel, telles que les Machines virtuelles (VM), les Services Cloud, les environnements de Service d’application et les machines virtuelles identiques. Machines virtuelles connectent sous-réseau tooa au sein d’un réseau virtuel via une interface réseau (NIC). toolearn plus d’informations sur les cartes réseau, lire hello [interfaces réseau](virtual-network-network-interface.md) l’article.

## <a name="connect-vnets"></a>Connecter des réseaux virtuels

Vous pouvez vous connecter à des réseaux virtuels tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooeither entre eux via des réseaux virtuels. Vous pouvez utiliser ou pour les deux hello suivant tooeach réseaux virtuels tooconnect du options autres :
- **Homologation :** permet aux ressources connecté toodifferent réseaux virtuels Azure dans hello même toocommunicate emplacement Azure entre eux. Hello la bande passante et latence pour hello des réseaux virtuels sont hello identique comme si les ressources hello ont été connecté toohello même réseau virtuel. toolearn en savoir plus sur l’homologation, lire hello [d’homologation de réseau virtuel](virtual-network-peering-overview.md) l’article.
- **Connexion de réseau virtuel à réseau virtuel :** permet aux ressources connecté toodifferent réseau virtuel Azure dans hello identiques ou différents emplacements Azure. Contrairement à l’homologation, la bande passante est limitée entre les réseaux virtuels car le trafic doit passer par une passerelle VPN Azure. toolearn plus d’informations sur la connexion de réseaux virtuels avec une connexion au réseau, lire hello [configurer une connexion réseau à](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.

## <a name="connect-on-premises"></a>Connecter le réseau local de tooan

Vous pouvez vous connecter votre tooa de réseau local virtuel à l’aide de n’importe quelle combinaison de hello options suivantes :
- **Réseau privé virtuel (VPN) Point-to-site :** établie entre un seul réseau d’ordinateurs connectés tooyour et hello réseau virtuel. Ce type de connexion est idéale si vous débutez avec Azure, ou pour les développeurs, car il requiert peu ou aucune modification tooyour réseau. connexion de Hello utilise communication via tooprovide chiffré le protocole SSTP hello sur hello Internet entre hello PC et hello réseau virtuel. latence Hello pour un réseau de point-to-site VPN est imprévisible, étant donné que le trafic de hello traverse hello Internet.
- **VPN de site à site :** connexion établie entre votre appareil VPN et une passerelle VPN Azure. Ce type de connexion permet de n’importe quelle ressource locale que vous autorisez tooaccess un réseau virtuel. connexion de Hello est un réseau VPN IPSec/IKE qui fournit une communication chiffrée sur hello Internet entre votre appareil local et une passerelle VPN Azure de hello. latence Hello pour une connexion site à site est imprévisible, étant donné que le trafic de hello traverse hello Internet.
- **Azure ExpressRoute :** connexion établie entre votre réseau et Azure via un partenaire ExpressRoute. Cette connexion est privée. Le trafic ne parcourt pas hello Internet. latence Hello pour une connexion ExpressRoute est prévisible, étant donné que le trafic ne traversent hello Internet.

toolearn plus d’informations sur tous les hello précédente options de connexion, lisez hello [diagrammes de topologie de connexion](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) l’article.

## <a name="filtering"></a>Filtrer le trafic réseau
Vous pouvez filtrer le trafic réseau entre les sous-réseaux à l’aide d’une ou les deux hello options suivantes :
- **Groupes de sécurité (NSG) réseau :** chaque groupe de sécurité réseau peut contenir plusieurs règles de sécurité entrante et sortante qui vous permettent de trafic toofilter par protocole, port et adresse IP source et de destination. Vous pouvez appliquer une tooeach de groupe de sécurité réseau NIC dans une machine virtuelle. Vous pouvez également appliquer un sous-réseau de toohello NSG une carte réseau, ou autres ressources Azure, est connecté à. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [groupes de sécurité réseau](virtual-networks-nsg.md) l’article.
- **Appliances de réseau virtuel (NVA) :** une appliance de réseau virtuel est une machine virtuelle exécutant un logiciel qui exécute une fonction de réseau, par exemple un pare-feu. Afficher la liste de NVAs disponibles dans hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Il existe également des appliances de réseau virtuel qui fournissent une optimisation du réseau étendu et d’autres fonctions de trafic réseau. Les appliances de réseau virtuel sont généralement utilisées avec des itinéraires définis par l’utilisateur ou des itinéraires BGP. Vous pouvez également utiliser un trafic de toofilter NVA entre des réseaux virtuels.

## <a name="routing"></a>Router le trafic réseau

Azure crée des tables d’itinéraires qui permettent de sous-réseau connecté tooany de ressources dans n’importe quel toocommunicate de réseau virtuel avec d’autres, par défaut. Vous pouvez implémenter une ou deux hello suivant options toooverride hello Azure crée les itinéraires par défaut :
- **Itinéraires définis par l’utilisateur :** vous pouvez créer des tables d’itinéraires personnalisés avec les itinéraires qui contrôlent où le trafic est routé toofor chaque sous-réseau. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.
- **Itinéraires BGP :** si vous vous connectez à votre réseau local de tooyour de réseau virtuel à l’aide d’une connexion de passerelle VPN à Azure ou ExpressRoute, vous pouvez les propager tooyour des itinéraires BGP des réseaux virtuels.

## <a name="pricing"></a>Tarification

Aucun frais n’est facturé pour les réseaux virtuels, les sous-réseaux, les tables de routage et les groupes de sécurité réseau. L’utilisation de la bande passante Internet sortante, les IP adresses publiques, l’homologation du réseau virtuel, les passerelles VPN et ExpressRoute possèdent leurs propres aux structures de tarification. Hello de vue [réseau virtuel](https://azure.microsoft.com/pricing/details/virtual-network), [passerelle VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), et [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) pages pour plus d’informations de tarification.

## <a name="faq"></a>Forum Aux Questions

tooreview Forum aux questions sur le réseau virtuel, consultez hello [FAQ sur les réseaux virtuels](virtual-networks-faq.md) l’article.


## <a name="next-steps"></a>Étapes suivantes

- Créer votre premier réseau et connecter plusieurs machines virtuelles tooit, en effectuant les étapes hello Bonjour [créer votre premier réseau virtuel](virtual-network-get-started-vnet-subnet.md) l’article.
- Créer un tooa de connexion de point-to-site réseau virtuel en procédant comme hello Bonjour [configurer une connexion de point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.
- En savoir plus sur certaines des hello autre clé [fonctionnalités réseau](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) de Azure.
