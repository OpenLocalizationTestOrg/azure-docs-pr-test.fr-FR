---
title: "Meilleures pratiques de sécurité réseau d’aaaAzure | Documents Microsoft"
description: "Cet article détaille les meilleures pratiques en matière de sécurité réseau, sur la base de capacités Azure intégrées."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Meilleures pratiques en matière de sécurité réseau - Azure
Microsoft Azure permet aux appareils de tooother en réseau de machines virtuelles et les appareils tooconnect en les plaçant sur des réseaux virtuels Azure. Un réseau virtuel Azure est une construction de réseau virtuel qui vous permet de tooconnect virtual interface cartes tooa réseau virtuel tooallow basée sur IP communications réseau entre les périphériques réseau activé. Machines virtuelles connecté tooan réseau virtuel Azure sont en mesure de tooconnect toodevices sur hello même réseau virtuel Azure, les différents réseaux virtuels Azure sur hello Internet, ou encore sur vos réseaux locaux.

Dans cet article, nous aborderons différentes meilleures pratiques en matière de sécurité réseau sur Azure. Ces meilleures pratiques sont dérivés de notre expérience avec mise en réseau Azure et les expériences hello de clients comme vous-même.

Pour chaque meilleure pratique, nous allons détailler les éléments suivants :

* Les meilleures pratiques de hello est
* Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
* Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
* Meilleure pratique de toohello alternatives possibles
* Comment vous pouvez apprendre tooenable hello il est recommandé

Cet article de meilleures pratiques de la sécurité de réseau Azure repose sur un avis consensus et les capacités de la plateforme Azure et les ensembles de fonctionnalités, telles qu’elles existent au moment de hello que cet article a été écrit. Avis et les technologies changent au fil du temps et de cet article sera mis à jour sur un tooreflect régulièrement ces modifications.

Les meilleures pratiques en matière de sécurité réseau sur Azure qui sont abordées dans le cadre de cet article sont les suivantes :

* Segmentation logique des sous-réseaux
* Contrôle du comportement de routage
* Activation du tunneling forcé
* Utilisation d’appliances de réseau virtuel
* Déploiement de zones DMZ pour la segmentation de sécurité
* Éviter l’exposition toohello Internet avec les liaisons WAN dédiées
* Optimisation de la durée active et des performances
* Utilisation de l’équilibrage de charge global
* Désactiver l’accès RDP tooAzure Machines virtuelles
* Activation d’Azure Security Center
* Extension de votre centre de données dans Azure

## <a name="logically-segment-subnets"></a>Segmentation logique des sous-réseaux
[Réseaux virtuels Azure](https://azure.microsoft.com/documentation/services/virtual-network/) sont similaires LAN tooa sur votre réseau local. Hello idée derrière un réseau virtuel Azure est que vous créez un seul réseau IP privé adresse basée sur l’espace sur lequel vous pouvez placer tous les votre [des Machines virtuelles Azure](https://azure.microsoft.com/services/virtual-machines/). Hello privés espaces d’adressage IP disponibles sont Bonjour classe A (10.0.0.0/8), classe B (172.16.0.0/12) et la classe C (192.168.0.0/16) plages.

Toowhat similaire vous localement, vous devez l’espace d’adressage plus grande toosegment hello en sous-réseaux. Vous pouvez utiliser [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) en fonction de vos sous-réseaux principes toocreate au sous-réseau.

Routage entre des sous-réseaux se produit automatiquement et vous n’avez pas besoin toomanually configurer des tables de routage. Toutefois, le paramètre par défaut de hello est qu’il n’y a aucun contrôle d’accès réseau entre les sous-réseaux hello que vous créez sur hello réseau virtuel Azure. Dans les contrôles d’accès réseau ordre toocreate entre sous-réseaux, vous devez tooput quelque chose entre des sous-réseaux hello.

Une des opérations de hello vous pouvez utiliser tooaccomplish cette tâche est un [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) (NSG). Groupes de sécurité réseau sont simple une inspection des paquets les périphériques qui utilisent hello 5-tuple (hello source IP, port source, adresse IP de destination, le port de destination et protocole de couche 4) approchent toocreate ou refus des règles pour le trafic réseau. Vous pouvez autoriser ou refuser le trafic tooand à partir d’une adresse IP unique, tooand à partir de plusieurs adresses IP ou le même tooand de sous-réseaux entiers.

À l’aide de groupes de sécurité réseau pour le contrôle d’accès réseau entre les sous-réseaux vous permet de tooput les ressources qui appartiennent toohello même zone de sécurité ou de rôle dans leurs propres sous-réseaux. Prenons l’exemple d’une application simple à 3 couches : une couche web, une couche de logique d’application et une couche de base de données. Vous placez les machines virtuelles qui appartiennent tooeach de ces niveaux dans leurs propres sous-réseaux. Puis vous utilisez le trafic toocontrol de groupes de sécurité réseau entre les sous-réseaux de hello :

* Machines virtuelles du niveau Web peut déclencher uniquement des ordinateurs de connexions toohello application logique et peut accepter uniquement les connexions à partir de hello Internet
* Ordinateurs virtuels logique d’application peut seulement initier des connexions avec le niveau de la base de données et peut accepter uniquement les connexions à partir de la couche de hello web
* Impossible d’initier la connexion avec quoi que ce soit en dehors de leur propre sous-réseau de machines virtuelles de niveau base de données et peut accepter uniquement les connexions à partir de la couche de logique d’application hello

toolearn plus sur les groupes de sécurité réseau et comment vous pouvez les utiliser toologically segment vos réseaux virtuels Azure, lisez l’article de hello [qu’est un groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Contrôle du comportement de routage
Lorsque vous placez un ordinateur virtuel sur un réseau virtuel Azure, vous remarquerez que l’ordinateur virtuel hello peuvent se connecter tooany autre machine virtuelle sur hello même réseau virtuel Azure, même si hello autres ordinateurs virtuels se trouvent sur des sous-réseaux différents. Hello pourquoi cela est possible parce qu’il existe une collection d’itinéraires système qui sont activées par défaut qui autorisent ce type de communication. Ces itinéraires par défaut autoriser les ordinateurs virtuels sur hello même réseau virtuel Azure tooinitiate entre eux et avec hello Internet (pour les communications sortantes toohello Internet uniquement).

Tandis que les itinéraires système hello par défaut sont utiles dans de nombreux scénarios de déploiement, il existe lorsque vous souhaitez la configuration de routage toocustomize hello pour vos déploiements. Ces personnalisations vous permettra de tooconfigure hello suivant saut adresse tooreach des destinations spécifiques.

Nous vous recommandons de configurer des itinéraires définis par l’utilisateur lorsque vous déployez une appliance de sécurité de réseau virtuel (nous en parlerons dans le cadre d’une meilleure pratique à venir).

> [!NOTE]
> Itinéraires définis d’utilisateur ne sont pas nécessaires et les itinéraires de système par défaut hello fonctionne dans la plupart des cas.
>
>

Plus d’informations sur les itinéraires définis d’utilisateur et la manière dont tooconfigure par la lecture de l’article de hello [que sont les itinéraires définis d’utilisateur et le transfert IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Activation du tunneling forcé
toobetter comprendre le tunneling forcé, il est utile toounderstand quelles » le tunneling fractionné » est.
exemple Hello le plus courant de tunneling fractionné apparaît avec les connexions VPN. Imaginez que vous établissez une connexion VPN à partir de votre réseau d’entreprise tooyour hôtel salle. Cette connexion vous permet de tooconnect tooresources sur votre réseau d’entreprise et toutes les communications tooresources, sur votre réseau d’entreprise passent par le tunnel VPN de hello.

Que se passe-t-il lorsque vous souhaitez tooresources tooconnect sur hello Internet ? Lorsque le tunneling fractionné est activé, ces connexions accédez directement toohello Internet et non par le biais de hello VPN tunnel. Des experts en sécurité envisager cette toobe un risque potentiel et par conséquent est recommandé que le tunneling fractionné désactivé et toutes les connexions, ceux destinés à hello Internet et ceux destinés à des ressources d’entreprise, via un tunnel VPN de hello. Hello l’avantage est que toohello connexions Internet sont ensuite forcé par le biais des dispositifs de sécurité de réseau d’entreprise hello qui ne serait pas le cas de hello si le client VPN de hello connecté toohello Internet en dehors de tunnel VPN de hello.

Maintenant nous allons mettre cela sauvegarder les machines toovirtual sur un réseau virtuel Azure. les itinéraires par défaut Hello pour un réseau virtuel Azure autorise des machines virtuelles tooinitiate toohello de trafic Internet. Cela trop peut représenter un risque de sécurité, que ces connexions sortantes peuvent augmenter la surface d’attaque hello d’un ordinateur virtuel et être exploitées par des personnes malveillantes.
Pour cette raison, nous vous recommandons d’activer le tunneling forcé sur vos machines virtuelles lorsque la connectivité entre locaux est établie entre votre réseau virtuel Azure et votre réseau local. Nous parlerons un peu plus tard de la connectivité entre locaux.

Si vous n’avez pas d’une connexion entre locaux, assurez-vous que vous tirer parti des groupes de sécurité réseau (décrit précédemment) ou Azure réseau virtuel sécurité matériels (décrit ci-après) tooprevent les connexions sortantes toohello Internet à partir de votre virtuel Azure Machines.

toolearn en savoir plus sur le tunneling forcé et comment tooenable, lisez l’article de hello [configurer Tunneling forcé à l’aide de PowerShell et le Gestionnaire de ressources Azure](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Utilisation d’appliances de réseau virtuel
Alors que les groupes de sécurité réseau et l’utilisateur définie par le routage peuvent fournir une certaine mesure de sécurité réseau à hello couches de transport et de réseau de hello [modèle OSI](https://en.wikipedia.org/wiki/OSI_model), il doit y toobe des situations où vous allez voulez ou devez tooenable sécurité à des niveaux élevés de pile de hello. Le cas échéant, nous vous recommandons de déployer les appliances de sécurité de réseau virtuel fournies par les partenaires d’Azure.

Ces appliances peuvent offrir des niveaux de sécurité nettement plus élevés que ceux des contrôles appliqués au niveau du réseau. Voici quelques-unes des fonctionnalités de sécurité réseau hello fournies par les appliances de sécurité de réseau virtuel :

* Installation de pare-feu
* Détection et prévention des intrusions
* Gestion des vulnérabilités
* Contrôle des applications
* Détection des anomalies basée sur le réseau
* Filtrage web
* Antivirus
* Protection contre les botnets

S’il vous faut un niveau plus élevé de sécurité réseau que celui qu’offrent les contrôles d’accès au niveau du réseau, nous vous invitons à envisager le déploiement d’appliances de sécurité du réseau virtuel Azure.

toolearn sur les appliances de sécurité réseau virtuel Azure sont disponibles et leurs fonctionnalités, visitez le site hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) et recherchez « sécurité » et « sécurité réseau ».

## <a name="deploy-dmzs-for-security-zoning"></a>Déploiement de zones DMZ pour la segmentation de sécurité
Un réseau de périmètre « réseau de périmètre » est physique ou segment de réseau logique qui est conçu tooprovide une couche supplémentaire de sécurité entre vos actifs et les hello Internet. Hello hello DMZ vise tooplace spécialisée périphériques de contrôle d’accès réseau sur le bord hello du réseau de hello DMZ afin que seul le trafic souhaité est autorisé au-delà de périphérique de sécurité réseau hello et à votre réseau virtuel Azure.

DMZ est utiles, car vous pouvez vous concentrer votre gestion contrôle d’accès réseau, analyse, de journalisation et de rapports sur les appareils hello en périphérie hello de votre réseau virtuel Azure. Ici, vous devez généralement activer la prévention des DDoS, les systèmes de détection et de prévention des intrusions (IDS/IPS), les règles et stratégies de pare-feu, le filtrage web, les fonctions anti-programme malveillant du réseau, etc. périphériques de sécurité réseau Hello se trouvent entre hello Internet et votre réseau virtuel Azure et ont une interface sur les deux réseaux.

Bien que cela soit hello conception de base un réseau de périmètre, il existe de nombreuses conceptions de réseau de périmètre différents, tels que DOS à DOS, triple hébergement, multirésident et d’autres.

Nous vous recommandons pour tous les déploiements de haute sécurité que vous envisagez de déployer un niveau de hello tooenhance réseau de périmètre de sécurité réseau pour vos ressources Azure.

toolearn plus d’informations sur les réseaux DMZ et comment toodeploy dans Azure, lisez l’article de hello [sécurité du réseau et Services Cloud Microsoft](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Éviter l’exposition toohello Internet avec les liaisons WAN dédiées
De nombreuses organisations ont choisi d’itinéraire d’informatique hybride hello. Dans un environnement hybride, certaines des informations de hello société sont dans Azure, tandis que d’autres restent sur site. Dans de nombreux cas, certains composants d’un service seront exécutés dans Azure, tandis que d’autres le seront localement.

Hybrides hello scénario informatique, il est généralement un certain type de connectivité entre différents locaux. Cela intersite connectivité autorise hello entreprise tooconnect leur tooAzure de réseaux locaux des réseaux virtuels. Deux solutions de connectivité entre locaux sont disponibles :

* VPN de site à site
* ExpressRoute

[Un VPN de site à site](../vpn-gateway/vpn-gateway-site-to-site-create.md) assure une connexion privée virtuelle entre le réseau local et un réseau virtuel Azure. Cet connexion a lieu plus hello Internet et vous permet de trop « tunnel » les informations à l’intérieur d’une liaison cryptée entre votre réseau et Azure. La technologie de VPN de site à site, aussi sécurisée qu’aguerrie, est déployée par des entreprises de toutes tailles depuis des décennies. Le chiffrement du tunnel est effectué par le biais du [mode de tunneling IPsec](https://technet.microsoft.com/library/cc786385.aspx).

VPN de site à site est une technologie établie, fiable et approuvée, le trafic au sein du tunnel de hello parcourt hello Internet. En outre, la bande passante est limitée relativement tooa maximum sur 200 Mbits/s.

Si, dans le cadre de vos connexions entre locaux, il vous faut un niveau de sécurité hors normes ou des performances exceptionnelles, nous vous recommandons d’utiliser la connectivité entre locaux offerte par Azure ExpressRoute. ExpressRoute représente une liaison réseau étendu dédiée entre le site local et un fournisseur d’hébergement Exchange. Comme il s’agit d’une connexion de télécommunications, vos données ne se déplacent sur hello Internet et sont donc toohello pas exposé à des risques potentiels inhérents aux communications Internet.

toolearn plus d’informations sur le fonctionnement d’Azure ExpressRoute et comment toodeploy, veuillez lire l’article de hello [présentation technique d’ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Optimisation de la durée active et des performances
Confidentialité, intégrité et disponibilité (CID) composent triples hello plus influent du aujourd'hui modèle de sécurité. La confidentialité est sur le chiffrement et la confidentialité, intégrité consiste à s’assurer que les données ne sont pas modifiées par des personnes non autorisées et disponibilité consiste à s’assurer que les personnes autorisées sont en mesure de tooaccess hello informations auxquelles ils peuvent tooaccess. Un manquement dans l’un ou l’autre de ces domaines peut constituer une faille de sécurité potentielle.

La notion de disponibilité peut être rapprochée de la durée active et des performances. Si un service est défaillant, les informations sont inaccessibles. Si les performances sont médiocres donc en tant que données de hello toomake inutilisables, nous pouvons envisagez hello données toobe inaccessible. Par conséquent, à partir du point de vue de la sécurité, nous devons toodo quelque nous pouvons toomake que nos services ont des performances et une disponibilité optimale.
Une méthode courante et efficace utilisé tooenhance disponibilité et performances toouse l’équilibrage de charge. L’équilibrage de charge est une méthode de répartition du trafic réseau entre les serveurs qui font partie d’un service. Par exemple, si vous avez des serveurs web frontaux dans le cadre de votre service, vous pouvez utiliser l’équilibrage de charge du trafic hello toodistribute sur vos serveurs web frontaux plusieurs.

Cette distribution du trafic augmente la disponibilité, car si un des serveurs web de hello devient indisponible, équilibrage de charge hello cesse d’envoyer le trafic toothat serveur et rediriger le trafic toohello serveurs qui sont toujours en ligne. L’équilibrage de charge permet également de performances, comme hello processeur, réseau et la mémoire système de traitement pour le traitement des demandes est distribuée à tous les serveurs d’équilibrage de charge hello.

Nous vous recommandons de tirer parti aussi souvent que possible de l’équilibrage de charge, selon les besoins de vos services. Nous traitons pertinence Bonjour les sections suivantes.
Au niveau du réseau virtuel Azure de hello, Azure fournit que des trois principales options d’équilibrage de charge :

* Équilibrage de charge basé sur HTTP
* Équilibrage de charge externe
* Équilibrage de charge interne

## <a name="http-based-load-balancing"></a>Équilibrage de charge basé sur HTTP
Équilibrage de charge basé sur HTTP base décisions concernant les connexions au serveur toosend à l’aide des caractéristiques du protocole de hello HTTP. Azure propose un équilibrage de charge HTTP qui passe par nom hello de passerelle d’Application.

Nous vous recommandons de tirer parti d’Azure Application Gateway dans les cas suivants :

* Les applications qui nécessitent des demandes à partir de hello même tooreach de session client/utilisateur hello même d’ordinateur virtuel principal. Exemples : applications de panier d’achat et serveurs de messagerie.
* Applications qui toofree des batteries de serveurs web à partir de la terminaison SSL surcharge en tirant parti de la passerelle d’Application [déchargement SSL](https://f5.com/glossary/ssl-offloading) fonctionnalité.
* Les applications, tel qu’un réseau de diffusion de contenu, qui requièrent plusieurs demandes HTTP sur hello même toobe de connexion TCP longue routés ou charger toodifferent à charge équilibrée sur les serveurs principaux.

toolearn en savoir plus sur le fonctionnement de la passerelle d’Application Azure et comment vous pouvez l’utiliser dans vos déploiements, lisez l’article de hello [vue d’ensemble de la passerelle Application](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Équilibrage de charge externe
L’équilibrage de charge externe intervient lorsque les connexions entrantes de hello Internet sont à charge équilibrée entre vos serveurs situés dans un réseau virtuel Azure. équilibrage de charge externe Azure Hello peut vous fournir cette fonctionnalité et nous vous recommandons d’utiliser lorsque vous ne nécessitent pas les sessions rémanentes hello ou de déchargement SSL.

En revanche tooHTTP d’équilibrage de charge, hello équilibreur de charge externe utilise les informations au niveau des couches de transport et de réseau hello hello OSI réseau modèle toomake décisions sur les serveur tooload solde de connexion à.

Nous vous recommandons d’utiliser l’équilibrage de charge externe chaque fois que vous avez [applications sans état](http://whatis.techtarget.com/definition/stateless-app) accepter les demandes entrantes à partir de hello Internet.

toolearn en savoir plus sur le fonctionnement de hello équilibrage de charge externe Azure et comment vous pouvez le déployer, lisez l’article de hello [prise en main la création d’un équilibrage de charge faisant face à Internet dans le Gestionnaire de ressources à l’aide de PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Équilibrage de charge interne
L’équilibrage de charge interne est similaire tooexternal équilibrage de charge et utilise hello même mécanisme tooload solde connexions toohello serveurs derrière eux. Hello seule différence est qu’équilibrage de charge hello dans ce cas accepte les connexions à partir d’ordinateurs virtuels qui ne sont pas hello Internet. Dans la plupart des cas, les connexions de hello qui sont acceptées pour l’équilibrage de charge sont initiées par les périphériques sur un réseau virtuel Azure.

Nous vous recommandons d’utiliser pour les scénarios qui tire parti de cette fonctionnalité, par exemple lorsque vous devez tooload solde connexions tooSQL serveurs ou serveurs web interne d’équilibrage de charge interne.

toolearn en savoir plus sur le fonctionnement de l’équilibrage de charge interne Azure et comment vous pouvez le déployer, lisez l’article de hello [prise en main la création d’un équilibreur de charge interne à l’aide de PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Utilisation de l’équilibrage de charge global
Cloud public informatique rend possible toodeploy globalement des applications distribuées qui comportent des composants situés dans des centres de données du monde hello. Cela est possible sur Microsoft Azure en raison de la présence de centre de données globales du tooAzure. En revanche les technologies d’équilibrage toohello mentionné précédemment, l’équilibrage de charge global rend possible toomake services disponibles même lorsque des centres de données entier peut devenir indisponible.

[Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/) propose ce type d’équilibrage de charge dans Azure. Traffic Manager fait est solde de tooload possible services tooyour de connexions basés sur l’emplacement de hello d’utilisateur de hello.

Par exemple, si l’utilisateur de hello effectue un service demande tooyour hello Europe, connexion de hello est services tooyour dirigée situés dans un centre de données de l’Union européenne. Cette partie de Traffic Manager vous aide à tooimprove performance d’équilibrage de charge globale, car la connexion toohello le plus proche du centre de données est plus rapide que la connexion toodatacenters sont loin.

Côté hello disponibilité, l’équilibrage de charge global permet de s’assurer que votre service est disponible même si un centre de données entier devient indisponible.

Par exemple, si un centre de données Azure devient indisponible en raison des raisons de tooenvironmental ou échéance toooutages (telles que les pannes de réseau), les connexions tooyour service serait reroutés toohello le plus proche du centre de données en ligne. Cet équilibrage de charge global s’effectue sur la base de stratégies DNS, que vous pouvez créer dans Traffic Manager.

Nous vous recommandons d’utiliser Traffic Manager pour une solution de cloud que vous développez qui possède une portée largement distribuée dans plusieurs régions et nécessite un hello plus haut niveau de disponibilité possible.

toolearn plus sur Azure Traffic Manager et comment toodeploy, lisez l’article de hello [Nouveautés Traffic Manager](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Désactiver l’accès RDP/SSH tooAzure Machines virtuelles
Il est possible de tooreach des Machines virtuelles Azure à l’aide de hello [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) et hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) les protocoles (SSH). Ces protocoles rendent possible toomanage ordinateurs virtuels à partir d’emplacements distants et sont standard dans le calcul du centre de données.

problème de sécurité potentiel Hello avec à l’aide de ces protocoles sur hello Internet est que des personnes malveillantes peuvent utiliser différentes [en force brute](https://en.wikipedia.org/wiki/Brute-force_attack) techniques toogain accès tooAzure Machines virtuelles. Une fois que des personnes malveillantes hello accèdent, vous pouvez utiliser votre machine virtuelle comme un point de lancement pour compromettre d’autres ordinateurs sur votre réseau virtuel Azure ou même attaquer des périphériques réseau en dehors d’Azure.

Pour cette raison, nous vous conseillons de désactiver direct RDP et SSH accès tooyour des Machines virtuelles Azure à partir de hello Internet. Après que direct RDP et SSH accèdent à partir de hello Qu'internet est désactivée, vous disposez d’autres options que vous pouvez utiliser ces machines virtuelles tooaccess pour la gestion à distance :

* VPN de point à site
* VPN de site à site
* ExpressRoute

L’expression [VPN de point à site](../vpn-gateway/vpn-gateway-point-to-site-create.md) est synonyme de connexion du client/serveur VPN pour un accès à distance. Point-to-site offre un tooan de tooconnect mono-utilisateur réseau virtuel Azure sur hello Internet. Une fois la connexion de point-to-site hello est établie, hello sera en mesure de toouse RDP ou SSH tooconnect tooany ordinateurs virtuels situés sur le réseau virtuel Azure de hello hello utilisateur connectés toovia point-to-site VPN. Cela suppose que l’utilisateur hello est autorisé tooreach ces ordinateurs virtuels.

Point-to-site VPN est plus sûre que les connexions RDP ou SSH directes, car les utilisateurs hello a tooauthenticate à deux reprises avant que de connexion tooa virtual machine. Tout d’abord, hello utilisateur besoins tooauthenticate (et autorisé) connexion de tooestablish hello point-to-site VPN ; en second lieu, hello utilisateur besoins tooauthenticate (et autorisé) tooestablish hello RDP ou SSH session.

A [VPN de site à site](../vpn-gateway/vpn-gateway-site-to-site-create.md) se connecte un réseau de tooanother réseau entier sur hello Internet. Vous pouvez utiliser un tooconnect VPN de site à votre tooan de réseau local sur le réseau virtuel Azure. Si vous déployez un VPN de site à site, les utilisateurs de votre réseau local seront machines toovirtual tooconnect en mesure de votre réseau virtuel Azure à l’aide de hello RDP ou SSH protocole hello connexion VPN site à site et ne nécessite pas tooallow direct RDP ou SSH accéder via hello Internet.

Vous pouvez également utiliser un toohello similaire de liaison WAN dédiée tooprovide fonctionnalités VPN de site à site. Hello principales différences sont les 1. liaison WAN dédié Hello ne traversent hello Internet et 2. Les liaisons WAN dédiées sont généralement plus stables et performantes. Azure fournit une solution de liaison WAN dédiée sous forme de hello de [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Activation d’Azure Security Center
Azure Security Center vous aide à empêcher, détecter et répondre toothreats et fournit le qu'augmentation de la visibilité et contrôler, sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Azure Security Center vous permet d’optimiser et de surveiller la sécurité réseau grâce aux opérations suivantes :

* Mise à disposition de recommandations relatives à la sécurité réseau
* Analyse de l’état de hello de votre configuration de sécurité réseau
* Génération d’alertes vous toonetwork basé menaces à la fois aux niveaux de réseau et de point de terminaison hello

Nous vous recommandons vivement d’activer Azure Security Center pour tous vos déploiements Azure.

toolearn plus d’informations sur le centre de sécurité Azure et comment tooenable pour vos déploiements, lisez l’article de hello [Introduction tooAzure centre de sécurité](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Extension sécurisée de votre centre de données dans Azure
L’informatique d’entreprise nombreuses organisations cherchent tooexpand cloud hello au lieu de la croissance de leurs centres de données locale. Cette expansion représente une extension de l’infrastructure informatique en nuage public de hello. En tirant parti de coexistence des options de connectivité qu’il est possible de tootreat vos réseaux virtuels Azure en tant qu’un autre sous-réseau dans votre environnement local l’infrastructure du réseau.

Toutefois, il y a beaucoup de planification et conception nécessitant toobe traités premier. Cela est particulièrement important dans la zone hello de sécurité réseau. Une de hello meilleures méthodes toounderstand comment vous approcher de ce type de conception est toosee un exemple.

Microsoft a créé hello [diagramme d’Architecture de référence de centre de données Extension](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) et prenant en charge la garantie toohelp comprendre cette extension de centre de données un aspect. Cela fournit une implémentation de référence d’exemple que vous pouvez utiliser tooplan et concevoir un nuage de toohello extension sécurisée enterprise centre de données. Nous vous recommandons de consulter cette tooget document une idée de hello principaux composants d’une solution sécurisée.

toolearn en savoir plus sur la façon dont toosecurely étendre votre centre de données dans Azure, veuillez consulter la vidéo de hello [tooMicrosoft d’étendre votre centre de données Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
