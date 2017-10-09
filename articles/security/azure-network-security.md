---
title: "Sécurité du réseau d’aaaAzure | Documents Microsoft"
description: "En savoir plus sur les services informatiques en nuage qui incluent une large sélection des instances de calcul et de services qui peuvent mettre à l’échelle haut et bas automatiquement toomeet hello aux besoins de votre application ou votre entreprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure Network Security

Nous savons que la sécurité est une tâche dans le cloud de hello et combien il est important que vous trouvez des informations précises et actuelles sur la sécurité Azure. Un des hello meilleures raisons toouse Azure pour vos applications et services est parti tootake de large gamme d’Azure d’outils de sécurité et des fonctions. Ces fonctionnalités et outils aident à rendre des solutions sécurisées toocreate possibles sur hello plateforme Azure.

Microsoft Azure assure la confidentialité, l’intégrité et la disponibilité des données client, tout en permettant la gestion transparente des responsabilités. toohelp vous de mieux comprendre collection hello des contrôles de sécurité réseau implémenté dans Microsoft Azure à partir du point de vue du client hello, cet article, « Sécurité de réseau Azure », est écrit tooprovide une vision détaillée de la sécurité du réseau hello contrôles disponibles avec Microsoft Azure.

Cet article est destiné à tooinform vous hello large éventail de réseau sur les contrôles que vous pouvez configurer la sécurité de hello de tooenhance de déployer des solutions hello dans Azure. Si vous souhaitez dans le Microsoft l’infrastructure de réseau de hello toosecure de Bonjour plateforme Azure lui-même, consultez la section de sécurité Azure hello Bonjour [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Plateforme Azure

Azure est une plateforme de services de cloud public qui prend en charge un large éventail de systèmes d’exploitation, de langages de programmation, d’infrastructures, d’outils, de bases de données et d’appareils.  Elle permet d’exécuter des conteneurs Linux avec l’intégration de Docker, de créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js, de créer des serveurs principaux pour des appareils iOS, Android et Windows. Services de cloud computing Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous générez, ou migrez des ressources informatiques à un fournisseur de services de cloud public, vous recourez tooprotect des capacités de cette organisation vos applications et données avec hello contrôles hello et les services qu’ils sécurisent toomanage hello de votre nuage ressources.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base digne de confiance sur lesquelles les entreprises capable de répondre aux impératifs de sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de sécurité toomeet hello des déploiements de votre organisation.

## <a name="abstract"></a>Résumé

Les services de cloud public Microsoft offrent une grande évolutivité des services et de l’infrastructure, des fonctionnalités adaptées aux grandes entreprises et de nombreuses possibilités en matière de connectivité hybride. Vous pouvez choisir tooaccess ces services via hello Internet ou avec Azure ExpressRoute, qui assure la connectivité de réseau privé. plateforme de Microsoft Azure Hello vous permet de tooseamlessly étendre votre infrastructure en nuage de hello et générer des architectures multicouches. Par ailleurs, des tiers peuvent activer des fonctionnalités améliorées en offrant des services de sécurité et des appliances virtuelles.

Par leur conception, les services réseau d’Azure maximisent la flexibilité, la disponibilité, la résilience, la sécurité et l’intégrité. Ce livre blanc fournit des détails sur les fonctions de mise en réseau hello d’Azure et plus d’informations sur la façon dont les clients peuvent utiliser toohelp de fonctionnalités de sécurité natif de Azure protègent leurs informations.

Hello destiné public de ce livre blanc inclure :

- responsables techniques, administrateurs réseau et développeurs à la recherche de solutions de sécurité prises en charge et disponibles dans Azure ;

-   Petites et moyennes entreprises ou les cadres de processus d’entreprise qui veulent tooget une vue d’ensemble hello des technologies de mise en réseau Azure et les services qui sont pertinents dans les discussions de sécurité réseau Bonjour cloud public Azure.

## <a name="azure-networking-big-picture"></a>Vision globale de la mise en réseau Azure
Microsoft Azure inclut un toosupport infrastructure de mise en réseau robuste votre application et les exigences de connectivité de service. La connectivité réseau est possible entre les ressources situées dans Azure, entre locaux et Azure hébergé tooand de hello Internet et des ressources et Azure.

![Vision globale de la mise en réseau Azure](media/azure-network-security/azure-network-security-fig-1.png)

Hello [infrastructure réseau Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) Active toosecurely vous connecter des ressources Azure tooeach autres avec des réseaux virtuels (réseaux virtuels). Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique d’abonnement de tooyour réseau dédié hello cloud Azure. Vous pouvez connecter des réseaux virtuels tooyour sur des réseaux locaux.

Prend en charge Azure dédié de réseau local de liaison WAN connectivité tooyour et un réseau virtuel Azure avec [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). lien de Hello entre Azure et votre site utilise une connexion dédiée ne passe pas par hello Internet public. Si votre application Windows Azure est en cours d’exécution dans plusieurs centres de données, vous pouvez utiliser [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute demandes d’utilisateurs intelligemment sur les instances de l’application hello. Vous pouvez également acheminer tooservices trafic ne pas en cours d’exécution dans Azure s’ils sont accessibles à partir de hello Internet.

## <a name="enterprise-view-of-azure-networking-components"></a>Composants de mise en réseau Azure destinées aux grandes entreprises
Azure propose de nombreux composants de mise en réseau qui sont pertinentes toonetwork discussion sur la sécurité. Nous décrivons ces composants réseau et se concentrer sur la sécurité de hello émet toothem connexe.

> [!Note]
> Tous les aspects du réseau Azure sont décrits : nous aborderons uniquement ceux pris en compte toobe essentiel dans la planification et conception d’une infrastructure réseau sécurisée autour de vos services et les applications que vous déployez dans Azure.

Dans ce document, hello de couverture après mise en réseau des fonctionnalités d’entreprise Azure :

-   Connectivité réseau de base

-   Connectivité hybride

-   Contrôles de sécurité

-   Validation réseau

### <a name="basic-network-connectivity"></a>Connectivité réseau de base

Hello [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) permet de service vous toosecurely connecter des ressources Azure tooeach autres avec des réseaux virtuels (VNet). Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique de hello réseau Azure infrastructure dédiée tooyour abonnement. Vous pouvez également connecter des réseaux virtuels tooeach autres et réseaux à l’aide de VPN de site à site local et dédié tooyour [des liaisons WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Connectivité réseau de base](media/azure-network-security/azure-network-security-fig-2.png)

Question de hello est hello présentation d’utiliser des serveurs de toohost de machines virtuelles dans Azure, comment ces machines virtuelles connectent tooa réseau. Hello réponse est que les ordinateurs virtuels connectent tooan [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Réseaux virtuels Azure sont semblables à des réseaux de hello virtuel vous utiliser localement avec vos propres solutions de plateforme de virtualisation, telles que Microsoft Hyper-V ou VMware.

#### <a name="intra-vnet-connectivity"></a>Connectivité entre réseaux virtuels

Vous pouvez vous connecter à des réseaux virtuels tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooeither entre eux via des réseaux virtuels. Vous pouvez utiliser ou pour les deux hello suivant tooeach réseaux virtuels tooconnect du options autres :

- **Homologation :** permet aux ressources connecté toodifferent réseaux virtuels Azure dans hello même toocommunicate emplacement Azure entre eux. Hello la bande passante et latence pour le réseau virtuel est de hello hello identique comme si les ressources hello ont été connecté toohello même réseau virtuel. toolearn en savoir plus sur l’homologation, lire [d’homologation de réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Homologation](media/azure-network-security/azure-network-security-fig-3.png)

- **Connexion de réseau virtuel à réseau virtuel :** permet aux ressources connecté toodifferent réseau virtuel Azure dans hello identiques ou différents emplacements Azure. Contrairement à l’homologation, la bande passante est limitée entre les réseaux virtuels car le trafic doit passer par une passerelle VPN Azure.

![Connexion entre réseaux virtuels](media/azure-network-security/azure-network-security-fig-4.png)


toolearn plus d’informations sur la connexion de réseaux virtuels avec une connexion au réseau, lire hello [configurer un article de la connexion au réseau](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Fonctionnalités de Réseau virtuel Azure :

Comme vous pouvez le voir, un réseau virtuel Azure fournit des machines virtuelles tooconnect toohello réseau afin qu’ils peuvent se connecter tooother des ressources de réseau de façon sécurisée. Toutefois, la connectivité de base est début de hello uniquement. Hello les fonctionnalités suivantes de hello service de réseau virtuel Azure exposent des caractéristiques de sécurité de hello réseau virtuel Azure :

-   Isolation

-   Connectivité Internet

-   Connectivité des ressources Azure

-   Connectivité des réseaux virtuels

-   Connectivité locale

-   Filtrage du trafic

-   Routage

**Isolation**

Les réseaux virtuels sont [isolés](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) les uns des autres. Vous pouvez créer des réseaux virtuels distincts pour le développement, test et de production qu’utilisation hello même [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) blocs d’adresses. À l’inverse, vous pouvez créer plusieurs réseaux virtuels qui utilisent différents blocs d’adresses CIDR et connecter les réseaux entre eux. Vous pouvez segmenter un réseau virtuel en plusieurs sous-réseaux.

Azure fournit la résolution de noms interne pour les machines virtuelles et [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/) instances de rôle connecté tooa réseau virtuel. Vous pouvez éventuellement configurer un réseau virtuel toouse vos propres serveurs DNS, au lieu d’utiliser la résolution de noms interne Azure.

Vous pouvez implémenter plusieurs réseaux virtuels au sein de chaque [abonnement](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure et de chaque [région](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure. Chaque réseau virtuel est isolé des autres réseaux virtuels. Pour chaque réseau virtuel, vous pouvez :

-   Spécifier un espace d’adressage IP privé personnalisé à l’aide d’adresses (RFC 1918) publiques et privées. Azure attribue une adresse IP privée à toohello connecté de ressources réseau virtuel à partir de l’espace d’adressage hello, vous assignez.

-   Segment hello réseau virtuel dans un ou plusieurs sous-réseaux et allouer une partie du sous-réseau tooeach d’espace d’adresses réseau virtuel de hello.

-   Utiliser la résolution de noms fournie par Azure ou spécifier que votre propre serveur DNS pour une utilisation par les ressources connectées tooa réseau virtuel. toolearn plus sur la résolution de noms dans les réseaux virtuels, lire hello [la résolution de noms pour les ordinateurs virtuels et Services de cloud computing](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Connectivité Internet**

Tous les [Azure Machines virtuelles (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) et instances de rôle Services de cloud computing tooa connecté réseau virtuel ont accèdent toohello Internet, par défaut. Vous pouvez également activer des ressources toospecific accès entrant, en fonction des besoins. (VM) et les instances de rôle Services de cloud computing tooa connecté réseau virtuel ont accèdent toohello Internet, par défaut. Vous pouvez également activer des ressources toospecific accès entrant, en fonction des besoins.

Toutes les ressources de tooa connecté réseau virtuel ont connectivité sortante toohello Internet par défaut. Hello adresse IP privée de ressource de hello est l’adresse IP publique de (SNAT) tooa de traduction d’adresses de réseau source par hello infrastructure Azure. Vous pouvez modifier la connexion par défaut de hello en implémentant un routage personnalisé et un filtrage du trafic. toolearn plus en détail la connectivité Internet sortante, lire hello [présentation des connexions sortantes dans Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate entrant tooAzure ressources hello Internet ou toocommunicate toohello sortant Internet sans SNAT, une ressource doit être affectée à une adresse IP publique. toolearn plus d’informations sur les adresses IP publiques, lire hello [des adresses IP publiques](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Connectivité des ressources Azure**

[Ressources Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) telles que les Services de cloud computing et machines virtuelles peuvent être connecté toohello même réseau virtuel. ressources de Hello peuvent se connecter tooeach autres privé adresses IP, même si elles sont dans des sous-réseaux différents. Azure fournit par défaut le routage entre sous-réseaux, les réseaux virtuels et sur des réseaux locaux, afin que vous n’avez tooconfigure et gérer les itinéraires.

Vous pouvez connecter plusieurs ressources Azure tooa réseau virtuel, telles que les Machines virtuelles (VM), les Services Cloud, les environnements de Service d’application et les machines virtuelles identiques. Machines virtuelles connectent sous-réseau tooa au sein d’un réseau virtuel via une interface réseau (NIC). toolearn plus d’informations sur les cartes réseau, lire hello [interfaces réseau](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Connectivité des réseaux virtuels**

[Réseaux virtuels](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) peut être connecté tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooany avec n’importe quelle ressource sur n’importe quel autre réseau virtuel.

Vous pouvez vous connecter à des réseaux virtuels tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooeither entre eux via des réseaux virtuels. Vous pouvez utiliser ou pour les deux hello suivant tooeach réseaux virtuels tooconnect du options autres :

- **Homologation :** permet aux ressources connecté toodifferent réseaux virtuels Azure dans hello même toocommunicate emplacement Azure entre eux. Hello la bande passante et latence pour hello des réseaux virtuels est hello identique si les ressources hello ont été connecté toohello même VNet.toolearn en savoir plus sur l’homologation, lire hello [d’homologation de réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Connexion de réseau virtuel à réseau virtuel :** permet aux ressources connecté toodifferent réseau virtuel Azure dans hello identiques ou différents emplacements Azure. Contrairement à l’homologation, la bande passante est limitée entre les réseaux virtuels car le trafic doit passer par une passerelle VPN Azure. toolearn plus d’informations sur la connexion de réseaux virtuels avec une connexion au réseau. toolearn plus, en lecture hello [configurer une connexion réseau à](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Connectivité locale**

Réseaux virtuels peuvent être connectés trop[local](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) réseaux via un réseau privé entre votre réseau et Azure, ou via une connexion VPN de site à site sur Internet de hello.

Vous pouvez vous connecter votre tooa de réseau local virtuel à l’aide de n’importe quelle combinaison de hello options suivantes :

- **Réseau privé virtuel (VPN) Point-to-site :** établie entre un seul réseau d’ordinateurs connectés tooyour et hello réseau virtuel. Ce type de connexion est idéale si vous débutez avec Azure, ou pour les développeurs, car il requiert peu ou aucune modification tooyour réseau. connexion de Hello utilise communication via tooprovide chiffré le protocole SSTP hello sur hello Internet entre hello PC et hello réseau virtuel. latence Hello pour un réseau de point-to-site VPN est imprévisible étant donné que le trafic de hello traverse hello Internet.

- **VPN de site à site :** connexion établie entre votre appareil VPN et une passerelle VPN Azure. Ce type de connexion permet de n’importe quelle ressource locale que vous autorisez tooaccess un réseau virtuel. connexion de Hello est un réseau VPN IPsec/IKE qui fournit une communication chiffrée sur hello Internet entre votre appareil local et une passerelle VPN Azure de hello. latence Hello pour une connexion site à site est imprévisible étant donné que le trafic de hello traverse hello Internet.

- **Azure ExpressRoute :** connexion établie entre votre réseau et Azure via un partenaire ExpressRoute. Cette connexion est privée. Le trafic ne parcourt pas hello Internet. latence Hello pour une connexion ExpressRoute est prévisible, étant donné que le trafic ne traversent hello Internet. toolearn plus d’informations sur tous les hello précédente options de connexion, lisez hello [diagrammes de topologie de connexion](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtrage du trafic**

Le [trafic réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) entrant et sortant des machines virtuelles et des instances de rôle Services cloud peut être filtré par adresse IP source et port, adresse IP de destination et port, et protocole.

Vous pouvez filtrer le trafic réseau entre les sous-réseaux à l’aide d’une ou les deux hello options suivantes :

- **Groupes de sécurité (NSG) réseau :** chaque groupe de sécurité réseau peut contenir plusieurs règles de sécurité entrante et sortante qui vous permettent de trafic toofilter par protocole, port et adresse IP source et de destination. Vous pouvez appliquer une tooeach de groupe de sécurité réseau NIC dans une machine virtuelle. Vous pouvez également appliquer un sous-réseau de toohello NSG une carte réseau, ou autres ressources Azure, est connecté à. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Appliances de réseau virtuel :** une appliance de réseau virtuel est une machine virtuelle exécutant un logiciel qui remplit une fonction réseau, telle qu’un pare-feu. Afficher la liste des NVAs disponibles Bonjour Azure Marketplace. Il existe également des appliances de réseau virtuel qui fournissent une optimisation du réseau étendu et d’autres fonctions de trafic réseau. Les appliances de réseau virtuel sont généralement utilisées avec des itinéraires définis par l’utilisateur ou des itinéraires BGP. Vous pouvez également utiliser un trafic de toofilter NVA entre des réseaux virtuels.

**Routage**

Vous pouvez éventuellement remplacer le routage par défaut d’Azure en configurant vos propres itinéraires ou en utilisant des itinéraires BGP via une passerelle réseau.

Azure crée des tables d’itinéraires qui permettent de sous-réseau connecté tooany de ressources dans n’importe quel toocommunicate de réseau virtuel avec d’autres, par défaut. Vous pouvez implémenter une ou deux hello suivant options toooverride hello Azure crée les itinéraires par défaut :

- **Itinéraires définis par l’utilisateur :** vous pouvez créer des tables d’itinéraires personnalisés avec les itinéraires qui contrôlent où le trafic est routé toofor chaque sous-réseau. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [itinéraires définis par l’utilisateur](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Itinéraires BGP :** si vous vous connectez à votre réseau local de tooyour de réseau virtuel à l’aide d’une connexion de passerelle VPN à Azure ou ExpressRoute, vous pouvez les propager tooyour des itinéraires BGP des réseaux virtuels.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Une connectivité internet hybride : connecter le réseau local de tooan
Vous pouvez vous connecter votre tooa de réseau local virtuel à l’aide de n’importe quelle combinaison de hello options suivantes :

-   Connectivité Internet

-   VPN de point à site (VPN P2S)

-   VPN de site à site (VPN S2S)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Connectivité Internet

Comme son nom l’indique, la connectivité Internet rend vos charges de travail accessible à partir d’Internet, de hello en vous demandant d’exposer tooworkloads différents points de terminaison publics qui appartiennent à un réseau virtuel de hello. Ces charges de travail peuvent être exposées à l’aide de [équilibrage de charge connecté à Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) ou simplement affecter une adresse IP publique adresse toohello machine virtuelle. De cette manière, il devient possible de n’est pas défini sur hello Internet toobe en mesure de tooreach cet ordinateur virtuel, un pare-feu d’hôte, [réseau (NSG) les groupes de sécurité](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), et [les itinéraires définis par l’utilisateur](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) qui permettent toohappen.

Dans ce scénario, vous pourriez exposer une application nécessitant toobe, toohello public Internet et tooit tooconnect en mesure d’à partir de n’importe où, ou à des emplacements spécifiques en fonction de la configuration de hello de vos charges de travail.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>VPN de point à site ou VPN de site à site
Ces deux figurent dans hello même catégorie. Les deux doivent votre toohave de réseau virtuel une passerelle VPN et vous pouvez vous connecter à l’aide du Client VPN pour votre station de travail dans le cadre de hello de tooit [configurationPointàSite](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) ou vous pouvez configurer votre site [le périphérique VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) tooterminate en mesure de toobe un VPN de site à site. De cette manière, les appareils locaux peuvent se connecter tooresources dans hello réseau virtuel.

Une configuration de Point-to-Site (P2S) vous permet de créer une connexion sécurisée à partir d’un réseau virtuel du tooa d’ordinateur client individuel. Le P2S est une connexion VPN sur SSTP (Secure Socket Tunneling Protocol).

![VPN de point à site](media/azure-network-security/azure-network-security-fig-5.png)

Connexions de point à Site sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple à partir d’accueil ou un centre de conférence, ou lorsque vous avez seulement quelques clients qui ont besoin de réseau virtuel de tooconnect tooa.

Les connexions de ce type ne nécessitent pas de périphérique VPN ou d’adresse IP publique. Vous établissez la connexion VPN de hello à partir de l’ordinateur client de hello. Par conséquent, P2S n'est pas recommandé de façon tooconnect tooAzure au cas où vous avez besoin d’une connexion permanente à partir de nombreux appareils locaux et les ordinateurs tooyour réseau Azure.

![VPN de site à site](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Pour plus d’informations sur les connexions de Point-to-Site, consultez hello [Point-to-Site FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2).

Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe. Cet connexion a lieu plus hello Internet et vous permet de trop « tunnel » les informations à l’intérieur d’une liaison cryptée entre votre réseau et Azure. La technologie de VPN de site à site, aussi sécurisée qu’aguerrie, est déployée par des entreprises de toutes tailles depuis des décennies. Le chiffrement du tunnel est effectué par le biais du [mode de tunneling IPsec](https://technet.microsoft.com/library/cc786385.aspx).

VPN de site à site est une technologie établie, fiable et approuvée, le trafic au sein du tunnel de hello parcourt hello Internet. En outre, la bande passante est environ 200 Mbits/s maximum tooa relativement limitée.

Si, dans le cadre de vos connexions entre locaux, il vous faut un niveau de sécurité hors normes ou des performances exceptionnelles, nous vous recommandons d’utiliser la connectivité entre locaux offerte par Azure ExpressRoute. ExpressRoute représente une liaison réseau étendu dédiée entre le site local et un fournisseur d’hébergement Exchange. Comme il s’agit d’une connexion de télécommunications, vos données ne se déplacent sur hello Internet et sont donc toohello pas exposé à des risques potentiels inhérents aux communications Internet.

> [!Note]
> Pour plus d’informations sur les passerelles VPN, consultez [À propos de la passerelle VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Liaison réseau étendu dédiée
Microsoft Azure ExpressRoute vous permet d’étendre vos réseaux locaux dans hello Azure via une connexion privée dédiée facilitée par un fournisseur de connectivité.

Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ainsi, toooffer de connexions ExpressRoute plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello.

![ Liaison réseau étendu dédiée](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Pour plus d’informations sur la façon de tooconnect votre tooMicrosoft réseau à l’aide d’ExpressRoute, consultez [des modèles de connectivité ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) et [présentation technique d’ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Comme avec les options de VPN de site à site hello, ExpressRoute vous permet également tooresources tooconnect qui ne sont pas nécessairement qu’un seul réseau virtuel. En fait, en fonction de la référence (SKU) de hello, vous pouvez connecter des réseaux virtuels too10. Si vous avez hello [complémentaire](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), connexions tooup too100 des réseaux virtuels sont possibles, en fonction de la bande passante. toolearn plus d’informations sur ce que ces types de connexions regarder aimez, lire [diagrammes de topologie de connexion](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Contrôles de sécurité
Avec un réseau virtuel Azure, vous disposez d’un réseau logique sécurisé qui est isolé des autres réseaux virtuels et qui prend en charge la plupart des contrôles de sécurité que vous utilisez sur vos réseaux locaux. Les clients créent leur propre structure à l’aide de : sous-réseaux, ils utilisent leur propre plage d’adresses IP privées, configurer des tables d’itinéraires, groupes de sécurité réseau de contrôle d’accès des listes, les passerelles et les équipements virtuels toorun leurs charges de travail dans le cloud de hello.

Hello Voici les contrôles de sécurité que vous pouvez utiliser sur vos réseaux virtuels Azure :

-   Contrôles d’accès réseau

-   Itinéraires définis par l’utilisateur

-   Appliance de sécurité réseau

-   Application Gateway

-   Pare-feu d’applications web Azure

-   Contrôle de disponibilité réseau

#### <a name="network-access-controls"></a>Contrôles d’accès réseau
Bien que hello réseau virtuel Azure (VNet) est la pierre angulaire de hello du modèle de mise en réseau Azure et offre un isolement et protection, hello [groupes de sécurité réseau (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) sont hello principale de l’outil vous utilisez tooenforce et contrôle du trafic réseau règles au niveau du réseau hello.

![ Contrôles d’accès réseau](media/azure-network-security/azure-network-security-fig-8.png)


Vous pouvez contrôler l’accès en autoriser ou refuser la communication entre les charges de travail hello dans un réseau virtuel, à partir des systèmes sur des réseaux du client via la connectivité intersite, ou diriger la communication Internet.

Dans le diagramme de hello, à la fois des réseaux virtuels et des groupes de sécurité réseau se trouvent dans une couche spécifique dans la pile de sécurité globale Azure hello, où les groupes de sécurité réseau et les dispositifs réseau virtuel UDR peuvent être utilisé toocreate sécurité limites tooprotect hello déploiements d’applications dans le réseau de hello protégé.

Groupes de sécurité réseau utilisent un trafic de tooevaluate 5-tuple (et sont utilisés dans les règles que vous configurez hello pour hello NSG) :

-   [Adresse IP source et de destination](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Port source et de destination](https://technet.microsoft.com/library/dd197515)

-   Protocole : [TCP (Transmission Control Protocol](https://technet.microsoft.com/library/cc940037.aspx) ou [UDP (User Datagram Protocol)](https://technet.microsoft.com/library/cc940034.aspx)

Cela signifie que vous pouvez contrôler l’accès entre une seule machine virtuelle et un groupe de machines virtuelles, ou un seul tooanother de machine virtuelle unique machine virtuelle, ou entre des sous-réseaux entiers. Encore une fois, gardez à l’esprit qu’il s’agit d’un filtrage de paquets avec état simple et non d’une inspection de paquets complète. Un groupe de sécurité réseau n’assure aucune validation de protocole et n’offre pas de fonctionnalités IDS ou IPS au niveau du réseau.

Un groupe de sécurité réseau intègre certaines règles vous devez connaître. Ces composants sont les suivants :

-   **Autoriser tout le trafic au sein d’un réseau virtuel spécifique :** toutes les machines virtuelles sur hello même réseau virtuel Azure peuvent communiquer entre eux.

-   **Autoriser tooinbound d’équilibrage de charge Azure :** cette règle autorise le trafic de n’importe quelle adresse de destination de tooany adresse source pour l’équilibrage de charge Azure hello.

-   **Refuser tout trafic entrant :** cette règle bloque tout le trafic comme source hello Internet que vous avez explicitement autorisés.

-   **Autoriser tout le trafic toohello sortant Internet :** cette règle permet de machines virtuelles tooinitiate toohello de connexions Internet. Si vous ne souhaitez pas que ces connexions établies, vous avez besoin de toocreate un tooblock règle ces connexions ou appliquer le tunneling forcé.

#### <a name="system-routes-and-user-defined-routes"></a>Itinéraires système et itinéraires définis par l’utilisateur

Lorsque vous ajoutez des machines virtuelles (VM) tooa réseau virtuel (VNet) dans Azure, vous remarquerez que les machines virtuelles de hello sont en mesure de toocommunicate entre eux sur le réseau de hello, automatiquement. Vous n’avez pas besoin de toospecify une passerelle, bien hello machines virtuelles sont dans des sous-réseaux différents.

Hello vaut également pour la communication entre toohello de machines virtuelles hello Internet public et réseau de local tooyour même lorsqu’une connexion hybride à partir d’Azure tooyour propre centre de données est présente.

![Itinéraires système](media/azure-network-security/azure-network-security-fig-9.png)

Ce flux de communication est possible, car Azure utilise une série de toodefine d’itinéraires système le flux de trafic IP. Les itinéraires système contrôlent le flux de hello de communication Bonjour les scénarios suivants :

-   Depuis hello même sous-réseau.

-   À partir d’un sous-réseau tooanother au sein d’un réseau virtuel.

-   À partir de machines virtuelles toohello Internet.

-   À partir d’un réseau virtuel tooanother réseau virtuel via une passerelle VPN.

-   À partir d’un réseau virtuel via le réseau virtuel d’homologation de tooanother réseau virtuel ([Service chaînage](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   Un réseau virtuel tooyour sur un réseau local via une passerelle VPN.

Nombre d’entreprises disposent stricte de sécurité et les stratégies d’exigences de conformité qui nécessitent l’inspection sur site de tous les tooenforce de paquets réseau spécifique. Azure fournit un mécanisme appelé [le tunneling forcé](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) qui achemine le trafic d’hello tooon d’ordinateurs virtuels locaux en créant un itinéraire personnalisé ou en [protocole BGP (Border Gateway)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) publications via ExpressRoute ou VPN.

Le tunneling forcé dans Azure est configuré par le biais d’itinéraires définis par l’utilisateur de réseau virtuel. Redirection du trafic tooan local de site est exprimé comme passerelle VPN Azure toohello itinéraire par défaut.

Hello section suivante répertorie les limite de hello actuelle de la table de routage hello et les itinéraires pour un réseau virtuel Azure :

-   Chaque sous-réseau du réseau virtuel dispose d’une table de routage système intégrée. table de routage système Hello a hello trois groupes d’itinéraires suivants :

 -  **Les itinéraires de réseau virtuel locales :** directement toohello machines virtuelles de destination Bonjour même réseau virtuel

 - **Itinéraires locaux :** passerelle VPN Azure de toohello

 -  **L’itinéraire par défaut :** directement toohello Internet. Les paquets destinés aux toohello des adresses IP privées non couvertes par les itinéraires hello deux précédents sont supprimés.

-   Avec la version hello d’itinéraires définis par l’utilisateur, vous pouvez créer un tooadd de table de routage un itinéraire par défaut et associez ensuite hello routage table tooyour réseau virtuel sous-réseau tooenable forcé tunneling sur ces sous-réseaux.

-   Vous devez tooset un « site par défaut » entre le réseau virtuel de hello intersite sites locaux toohello connecté.

-   Le tunneling forcé doit être associé à un réseau virtuel équipé d'une passerelle VPN à routage dynamique (pas de passerelle statique).

- ExpressRoute le tunneling forcé n’est pas configuré via ce mécanisme, mais au lieu de cela, est activé par annonce un itinéraire par défaut via hello BGP ExpressRoute sessions d’homologation.

> [!Note]
> Pour plus d’informations, consultez hello [Documentation d’ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) pour plus d’informations.

#### <a name="network-security-appliances"></a>Appliances de sécurité réseau
Alors que les groupes de sécurité réseau et les itinéraires définis par l’utilisateur peuvent fournir une certaine mesure de sécurité réseau à hello couches de transport et de réseau de hello [modèle OSI](https://en.wikipedia.org/wiki/OSI_model), il doit y toobe des situations où vous voulez ou devez tooenable sécurité à des niveaux supérieurs de la pile réseau hello. Le cas échéant, nous vous recommandons de déployer les appliances de sécurité de réseau virtuel fournies par les partenaires d’Azure.

![Appliances de sécurité réseau](./media/azure-network-security/azure-network-security-fig-10.png)

Les appliances de sécurité réseau Azure améliorent la sécurité de réseau virtuel et les fonctions de réseau, et elles sont disponibles à partir de nombreux fournisseurs via hello [Azure Marketplace](https://azuremarketplace.microsoft.com). Ces appliances de sécurité virtuel peuvent être déployé tooprovide :

-   Pare-feu à haute disponibilité

-   Prévention des intrusions

-   Détection des intrusions

-   Pare-feu d’applications web (WAF)

-   Optimisation de réseau étendu

-   Routage

-   Équilibrage de la charge

-   VPN

-   Gestion de certificats

-   Active Directory

-   Authentification multifacteur

#### <a name="application-gateway"></a>Application Gateway

[Microsoft Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) est une appliance virtuelle dédiée qui propose un contrôleur de remise d’applications (ADC) en tant que service.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-11.png)

Passerelle d’application vous permet de disponibilité et performances de batterie de serveurs web toooptimize en raison du déchargement du processeur intensif SSL arrêt toohello passerelle d’application (déchargement SSL). Celle-ci offre aussi d’autres fonctionnalités de routage de couche 7, à savoir :

-   Distribution alternée du trafic entrant

-   Affinité de session basée sur les cookies

-   Routage basé sur le chemin de l’URL

-   Capacité toohost plusieurs sites Web derrière une passerelle d’Application unique


A [pare-feu d’applications web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) est également fourni dans le cadre de la passerelle d’application hello. Il assure une protection tooweb les applications courantes des vulnérabilités de web et des exploits. La passerelle Application Gateway peut être configurée en tant que passerelle Internet, passerelle exclusivement interne ou une combinaison des deux.

Le pare-feu WAF Application Gateway peut être exécuté en mode détection ou prévention. Un cas d’usage courant est de toorun administrateurs dans la détection en mode tooobserve le trafic pour les modèles malveillants. Une fois que les attaques potentielles sont détectées, activer le mode tooprevention bloque le trafic entrant suspect.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-12.png)

En outre, WAF de passerelle d’Application vous permet de surveiller les applications web contre les attaques à l’aide d’un journal WAF en temps réel qui sont intégrés à [moniteur Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) et [Azure Security Center](https://azure.microsoft.com/services/security-center/) tootrack WAF alertes et analyser facilement les tendances.

journal de mise en forme de JSON Hello est envoyé directement toohello du compte de stockage. Vous bénéficiez d’un contrôle total sur ces journaux et pouvez appliquer vos propres stratégies de rétention.

Vous pouvez aussi ingérer ces journaux dans votre propre système analytique via l’[intégration des journaux Azure](https://aka.ms/AzLog). WAF journaux sont également intégrés aux [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) afin de pouvoir utiliser analytique des journaux OMS tooexecute sophistiqué requêtes affinées.

#### <a name="azure-web-application-firewall-waf"></a>Pare-feu d’applications web (WAF) Azure

Les applications Web sont plus en plus des cibles des attaques malveillantes d’exploiter les vulnérabilités connues courantes, telles que l’injection SQL, les attaques de script entre sites et autres attaques qui s’affichent dans hello [10 premiers d’OWASP avoir](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Empêcher ces attaques dans l’application hello requiert une maintenance rigoureuse, mise à jour corrective et la surveillance de plusieurs couches de la topologie de l’application hello.

 ![Pare-feu d’applications web (WAF) Azure](./media/azure-network-security/azure-network-security-fig-13.png)

Un [pare-feu d’applications web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) centralisé permet de se prémunir contre les attaques web et de simplifier la gestion de la sécurité sans avoir à modifier l’application.

Une solution WAF peut réagir également de menace pour la sécurité tooa plus rapide par la mise à jour corrective une vulnérabilité connue à un emplacement central par rapport à la sécurisation de chacune des applications web individuelles. Les passerelles d’application existant peuvent être converti tooa web application pare-feu est activé application passerelle facilement.

#### <a name="network-availability-controls"></a>Contrôles de disponibilité réseau

Il existe différentes options toodistribute le trafic à l’aide de Microsoft Azure. Ces options fonctionnent différemment, car elles disposent d’un ensemble de fonctionnalités différent et prennent en charge différents scénarios. Elles peuvent être utilisées de manière isolée ou en les combinant.

Suivantes sont hello des contrôles de disponibilité de réseau :

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Azure Load Balancer**

Offre une haute disponibilité et les performances réseau tooyour applications. Il s’agit d’un équilibreur de charge Layer-4 (TCP, UDP) qui distribue le trafic entrant parmi des instances saines de services définis dans un jeu à charge équilibrée.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer peut être configuré pour :

-   La charge des machines de solde entrants Internet trafic toovirtual. Cette configuration est appelée [équilibrage de charge avec accès par Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   équilibrer le trafic entre des machines virtuelles dans un réseau virtuel, entre des machines virtuelles dans les services cloud ou entre des ordinateurs locaux et des machines virtuelles dans un réseau virtuel entre différents locaux. Cette configuration est appelée [équilibrage de charge interne](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Transférer le trafic externe tooa ordinateur virtuel spécifique.

Toutes les ressources de cloud de hello peut-être un toobe d’adresse IP publique accessible à partir de hello Internet. infrastructure en nuage Hello dans Azure utilise des adresses IP non routable pour ses ressources. Azure utilise la traduction d’adresses réseau (NAT) avec publique toohello de toocommunicate d’adresses IP Internet.

 **Application Gateway**

 Passerelle d’application fonctionne au niveau de la couche d’application hello (couche 7 dans la pile de référence hello OSI réseau). Elle agit comme un service de proxy inverse, termine hello client connexion et points de terminaison tooback-fin des demandes de transfert.

 **Traffic Manager**

Microsoft Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic utilisateur pour les points de terminaison de service dans différents centres de données. Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud. Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.

Traffic Manager utilise hello système DNS (Domain Name) toodirect client demande du point de terminaison plus approprié toohello selon un [méthode de routage du trafic](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) et l’intégrité de hello de points de terminaison hello. Traffic Manager fournit une gamme de routage du trafic méthodes toosuit différents besoins des applications, l’intégrité du point de terminaison [analyse](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)et un basculement automatique. Traffic Manager est résilient toofailure, y compris échec hello d’un ensemble de la région Azure.

Azure Traffic Manager vous permet de distribution de hello toocontrol du trafic entre les points de terminaison de votre application. Un point de terminaison est tout service côté Internet hébergé à l’intérieur ou à l’extérieur d’Azure.

Traffic Manager offre deux principaux avantages :

-   Distribution du trafic en fonction de tooone de plusieurs [des méthodes de routage de trafic](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Surveillance continue de l’intégrité des points de terminaison](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) et basculement automatique en cas d’échec des points de terminaison.

Lorsqu’un client essaie tooconnect tooa service, il doit tout d’abord résoudre le nom DNS de hello d’adresse IP de hello service tooan. Hello puis se connecte le service hello tooaccess toothat IP adresse. Traffic Manager utilise DNS toodirect clients toospecific des points de terminaison en fonction des règles hello de méthode de routage du trafic hello. Les clients connectent toohello sélectionné le point de terminaison directement. Traffic Manager n’est pas un proxy ou une passerelle. Traffic Manager ne voit pas de trafic hello entre le client de hello et le service de hello.

### <a name="azure-network-validation"></a>Validation réseau Azure

Validation du réseau Azure est tooensure qui hello réseau Azure fonctionne comme il est configuré et de validation peut être effectuée à l’aide hello services et fonctionnalités disponibles toomonitor hello réseau. Aide de l’Observateur réseau de Azure, vous pouvez accéder à une multitude de journalisation et des fonctionnalités de diagnostic qui vous accorder à insights toounderstand vos performances réseau et le contrôle d’intégrité. Ces fonctionnalités sont accessibles via le portail, PowerShell, l’interface CLI, l’API Rest et le Kit de développement logiciel (SDK).

Sécurité opérationnelle Azure fait référence toohello services, des contrôles et toousers disponibles de fonctionnalités pour protéger leurs données, les applications et les autres composants dans Microsoft Azure. Sécurité opérationnelle Azure repose sur une infrastructure qui intègre les connaissances hello acquises via une différentes fonctionnalités qui sont tooMicrosoft unique, y compris hello Microsoft du cycle de vie SDL (Security Development), hello Centre de réponse de sécurité Microsoft programme et une connaissance approfondie du paysage des menaces de sécurité cyber hello.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Azure Resource Manager

Hello personnes et processus qui s’appliquent à Microsoft Azure sont peut-être hello plus importante fonctionnalité de sécurité de plateforme de hello. Cette section décrit les fonctionnalités de l’infrastructure globale des centres de données Microsoft qui contribuent à améliorer et à assurer la sécurité, la continuité des activités et la confidentialité.

infrastructure Hello pour votre application est généralement constitué de nombreux composants – peut-être un ordinateur virtuel, compte de stockage et réseau virtuel, ou une application web, base de données, serveur de base de données et des services tiers. Vous ne voyez pas ces composants comme des entités distinctes, mais plutôt comme des parties associées et interdépendantes d’une seule et même entité. Vous souhaitez toodeploy, gérez et surveillez en tant que groupe. Le Gestionnaire de ressources Azure vous permet de toowork des ressources de hello dans votre solution en tant que groupe.

Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources hello pour votre solution dans une opération unique et coordonnée. Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production). Gestionnaire de ressources fournit la sécurité, l’audit et le balisage des fonctionnalités toohelp gérer vos ressources après le déploiement.

**avantages de Hello d’à l’aide du Gestionnaire de ressources**

Resource Manager offre plusieurs avantages :

-   Vous pouvez déployer, gérer et surveiller toutes les ressources hello pour votre solution en tant qu’un groupe, au lieu de gérer ces ressources individuellement.

-   Vous pouvez à plusieurs reprises déployer votre solution tout au long du cycle de vie de développement hello et avez confiance que vos ressources sont déployées dans un état cohérent.

-   Vous pouvez gérer votre infrastructure à l’aide de modèles déclaratifs plutôt que de scripts.

-   Vous pouvez définir des dépendances de hello entre les ressources, afin qu’ils sont déployés dans l’ordre correct de hello.

-   Vous pouvez appliquer l’accès contrôle tooall services dans votre groupe de ressources, car le contrôle d’accès en fonction du rôle (RBAC) est en mode natif intégré à la plate-forme de gestion hello.

-   Vous pouvez appliquer des balises tooresources toologically organiser toutes les ressources hello dans votre abonnement.

-   Vous pouvez clarifier la facturation de votre organisation en affichant les coûts d’un groupe de ressources partageant une balise.

> [!Note]
> Le Gestionnaire de ressources fournit un nouveau toodeploy de façon et gérer vos solutions. Si vous avez utilisé hello classiques de déploiement et souhaitez toolearn sur les modifications de hello, consultez [déploiement du Gestionnaire de ressources de présentation et déploiement classique](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Journalisation et surveillance réseau Azure

Azure propose de nombreux outils toomonitor, empêcher, détecter et répondre toonetwork les événements de sécurité. Hello plus puissants outils de tooyou disponibles dans cette zone sont les suivantes :

-   Network Watcher

-   Surveillance au niveau des ressources réseau

-   Log Analytics

### <a name="network-watcher"></a>Network Watcher

[Observateur de réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -surveillance basée sur un scénario est fourni avec les fonctions hello dans l’Observateur réseau. Ce service inclut la capture de paquets, le tronçon saut suivant, la vérification des flux IP, l’affichage de groupe de sécurité, les journaux de flux de groupe de sécurité réseau. Surveillance au niveau du scénario présente une fin tooend des ressources réseau dans l’analyse de ressource contraste tooindividual réseau.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

Observateur réseau est un service régional qui permet de vous toomonitor et diagnostiquer des conditions à un niveau de scénario réseau, vers et depuis Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.

Observateur réseau a actuellement hello suivant de fonctionnalités :

#### <a name="topology"></a>Topologie

La fonctionnalité [Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) retourne un graphique des ressources réseau présentes dans un réseau virtuel. graphique de Hello représente l’interconnexion hello entre la connectivité réseau de hello ressources toorepresent hello fin tooend. Dans le portail hello, topologie retourne des objets de ressource hello sur conformément à base de réseau virtuel. relations de Hello sont représentées par des lignes entre les ressources hello en dehors de la région de hello Observateur réseau, même si dans la ressource de hello groupe s’afficheront pas. ressources Hello retournées dans la vue du portail hello sont un sous-ensemble de composants réseau hello qui sont représentés graphiquement. toosee hello liste complète des ressources réseau, vous pouvez utiliser [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) ou [reste](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Comme les ressources sont retournées connexion hello entre elles sont modélisés sous deux relations.

- **Imbrication** : un réseau virtuel contient un sous-ensemble, qui contient lui-même une carte réseau.

- **Associé** : une carte réseau est associée à une machine virtuelle.

#### <a name="variable-packet-capture"></a>Capture de paquets variable

Observateur de réseau [capture des paquets variable](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) vous permet de toocreate paquet capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel. Capture des paquets permet les anomalies de réseau toodiagnose réactive et proactivity. Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.

La capture de paquets est une extension de machine virtuelle qui est démarrée à distance par le biais de Network Watcher. Cette fonctionnalité facilite la charge hello de l’exécution d’une capture de paquets manuellement sur l’ordinateur virtuel hello souhaité, ce qui permet de gagner du temps. Capture de paquets peut être déclenchée via le portail de hello, PowerShell, CLI ou API REST. Les alertes de machine virtuelle constituent un exemple de mode de déclenchement de la capture de paquets.

#### <a name="ip-flow-verify"></a>Vérification du flux IP

[Vérifiez que le flux IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) vérifie si un paquet est autorisé ou refusé tooor à partir d’un ordinateur virtuel en fonction des informations de 5-tuple. Ces informations se composent de la direction, du protocole, de l’adresse IP locale, de l’adresse IP distante, du port local et du port distant. Si les paquets hello sont refusée par un groupe de sécurité, nom hello de règle hello refusé les paquets hello est retournée. Alors que toutes les adresses IP source ou de destination peut être choisie, cette fonctionnalité permet aux administrateurs de diagnostiquer rapidement les problèmes de connectivité à partir d’ou toohello internet et à partir d’ou l’environnement local de toohello.

La vérification du flux IP cible une interface réseau d’une machine virtuelle. Flux de trafic est ensuite vérifié selon tooor de paramètres hello configuré à partir de cette interface réseau. Cette fonctionnalité est utile pour confirmer si une règle dans un groupe de sécurité réseau bloque entrée ou sortie tooor le trafic à partir d’un ordinateur virtuel.

#### <a name="next-hop"></a>Tronçon suivant

Détermine hello [tronçon suivant](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) pour les paquets routés Bonjour Azure Fabric de réseau, l’activation vous toodiagnose tout mal configuré itinéraires définis par l’utilisateur. Le trafic à partir d’une machine virtuelle est envoyé à destination tooa selon les itinéraires effectifs hello associés à une carte réseau. Tronçon suivant obtient les type de tronçon suivant hello et l’adresse IP d’un paquet à partir d’un ordinateur virtuel spécifique et la carte réseau. Cela permet de toodetermine si hello paquet est dirigée toohello destination ou est dipositif de trafic hello est noir.

Tronçon suivant retourne également la table d’itinéraires hello associée saut suivant de hello. Lorsque vous interrogez un tronçon suivant si l’itinéraire de hello est défini comme un itinéraire défini par l’utilisateur, cet itinéraire est retourné. Sinon, le tronçon suivant renvoie « Itinéraire du système ».

#### <a name="security-group-view"></a>Vue du groupe de sécurité

Obtient les règles de sécurité efficace et appliquées hello qui sont appliquées sur une machine virtuelle. Les groupes de sécurité réseau sont associés à un niveau de sous-réseau ou à un niveau de carte réseau. Lorsqu’ils sont associés à un niveau de sous-réseau, elle s’applique des instances de machine virtuelle tooall hello dans un sous-réseau de hello. Réseau [affichage du groupe de sécurité](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) retourne toutes les règles qui sont associés à un niveau de carte réseau et le sous-réseau pour un ordinateur virtuel qui fournit un aperçu de la configuration de hello et les groupes de sécurité réseau hello configuré. En outre, les règles de sécurité efficace hello sont retournées pour chacune des cartes réseau de hello dans une machine virtuelle. L’affichage du groupe de sécurité réseau vous permet de déterminer les vulnérabilités réseau d’une machine virtuelle, telles que les ports ouverts. Vous pouvez également valider si votre groupe de sécurité réseau fonctionne comme prévu selon un [comparaison entre hello configuré et hello des règles de sécurité efficace](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Journal des flux de groupe de sécurité réseau

 Flux des journaux pour les groupes de sécurité réseau permettent de tootraffic connexes toocapture journaux qui sont autorisés ou refusés par des règles de sécurité hello dans le groupe de hello. flux de Hello est défini par une 5-tuple d’informations : l’adresse IP Source, adresse IP de Destination, Port Source, le Port de Destination et protocole.

[Journaux du groupe de sécurité réseau de flux](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Résolution des problèmes de passerelle de réseau virtuel et de connexion

Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure. Il permet notamment de résoudre les problèmes liés aux ressources. La [résolution des problèmes de ressources](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) peut être appelée par PowerShell, l’interface CLI ou l’API REST. Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.

Cette section vous guide tout au long de hello différentes tâches de gestion qui sont actuellement disponibles pour le dépannage de la ressource.

-   [Résoudre les problèmes d’une passerelle de réseau virtuel](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Résoudre les problèmes d’une connexion](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Limites d’abonnement réseau

[Limites de l’abonnement du réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) vous fournissent des détails d’utilisation hello de chacune des ressources du réseau hello dans un abonnement dans une région de nombre maximal de hello des ressources disponibles.

#### <a name="configuring-diagnostics-log"></a>Configuration du journal de diagnostic

Network Watcher permet d’afficher les [journaux de diagnostic](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview). Cet affichage contient toutes les ressources réseau qui prennent en charge la journalisation des diagnostics. À partir de celui-ci, vous pouvez activer et désactiver les ressources réseau facilement et rapidement.

### <a name="network-resource-level-monitoring"></a>Surveillance au niveau des ressources réseau

Hello suivant les fonctionnalités est disponible pour l’analyse au niveau des ressources :

#### <a name="audit-log"></a>Journal d’audit

Opérations effectuées dans le cadre de la configuration de hello des réseaux sont enregistrées. Ces journaux d’audit est essentiel tooestablish conformités différents. Ces journaux peuvent être consultées dans hello portail Azure ou récupérées à l’aide des outils de Microsoft, telles que Power BI ou des outils tiers. Journaux d’audit sont disponibles via le portail de hello, PowerShell, CLI et les API Rest.

> [!Note]
> Pour plus d’informations sur les journaux d’audit, consultez [Opérations d’audit avec Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Les journaux d’audit sont disponibles pour les opérations effectuées sur toutes les ressources réseau.


#### <a name="metrics"></a>Métriques

Les métriques sont des indicateurs et des compteurs de performances collectés sur une période donnée. Les mesures sont disponibles pour Application Gateway. Métriques peuvent être des alertes tootrigger utilisé selon le seuil. Passerelle d’Application Azure par défaut surveille l’intégrité de hello de toutes les ressources dans son pool principal et supprime automatiquement n’importe quelle ressource considéré comme non intègre de pool de hello. Passerelle d’application continue des instances non intègre de toomonitor hello et ajoute les sauvegarder pool principal intègre de toohello une fois qu’ils deviennent disponibles et des sondes toohealth de répondre. Passerelle d’application envoie les sondes d’intégrité hello hello même port est défini dans les paramètres HTTP hello back-end. Cette configuration garantit que sonde hello teste hello même port que les clients utilisent tooconnect toohello principal.

> [!Note]
> Consultez [Application Diagnostics de passerelle](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview comment les métriques peuvent être utilisés toocreate alertes.

#### <a name="diagnostic-logs"></a>Journaux de diagnostic

Événements périodiques et spontanées sont créées par les ressources réseau et enregistrées dans les comptes de stockage, envoyés tooan concentrateur d’événements ou Analytique de journal. Ces journaux fournissent des analyses d’intégrité de hello d’une ressource. Ces journaux peuvent être affichés dans des outils tels que Power BI et Log Analytics. toolearn comment tooview journaux de diagnostic, visitez [Analytique de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Les journaux de diagnostic sont disponibles pour [l’équilibrage de charge](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [les groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), les itinéraires, et [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher permet d’afficher les journaux de diagnostic. Cet affichage contient toutes les ressources réseau qui prennent en charge la journalisation des diagnostics. À partir de celui-ci, vous pouvez activer et désactiver les ressources réseau facilement et rapidement.

### <a name="log-analytics"></a>Log Analytics

[Ouvrez une session Analytique](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) est un service de [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) qui surveille votre toomaintain environnements locaux et cloud leur disponibilité et les performances. Il collecte les données générées par les ressources dans vos environnements locaux et cloud et à partir d’autres analyses de tooprovide outils analyse à plusieurs sources.

Analytique de journal offre hello suivant des solutions pour l’analyse de vos réseaux :

-   Analyseur de performances réseau (NPM)

-   Azure Application Gateway Analytics

-   Azure Network Security Group Analytics

#### <a name="network-performance-monitor-npm"></a>Network Performance Monitor (NPM)
Hello [analyse des performances réseau](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) solution de gestion est un solution qui surveille l’intégrité de hello, la disponibilité et l’accessibilité des réseaux d’analyse de réseau.

Il existe une connectivité toomonitor utilisé entre :

-   le cloud public et local ;

-   les centres de données et les emplacements de l’utilisateur (filiales) ;

-   les sous-réseaux hébergeant différents niveaux d’une application multiniveau.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Azure Application Gateway Analytics dans Log Analytics

Hello suivant les journaux est pris en charge pour les passerelles d’Application :

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Hello suit les mesures est prises en charge pour les passerelles d’Application :

-   Débit sur 5 minutes

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Azure Network Security Group Analytics dans Log Analytics

Hello journaux suivants sont pris en charge pour [groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent :** contient des entrées pour le groupe de sécurité réseau, les règles sont tooVMs appliqués et les rôles d’instance en fonction de l’adresse MAC. état Hello pour ces règles est collecté toutes les 60 secondes.

- **NetworkSecurityGroupRuleCounter :** contient des entrées pour le nombre de fois où chaque groupe de sécurité réseau de règles est appliqué toodeny ou autoriser le trafic.

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur la sécurité, lisez nos rubriques détaillées sur la sécurité :

-   [Analyse de journaux pour les groupes de sécurité réseau (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Mise en réseau des innovations que toute interruption de lecteur hello cloud](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC : hello commutateur logiciel optimisant hello nuage Global de Microsoft de mise en réseau](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Comment Microsoft bâtit son puissant réseau mondial](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Le pari de l’innovation réseau](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
