---
title: "aaaNetwork concepts de sécurité et de la configuration requise dans Azure | Documents Microsoft"
description: " Cet article facilite vous toounderstand ce que Microsoft Azure a toooffer dans la zone hello de sécurité réseau. Nous de fournir des explications de base pour les concepts de sécurité réseau et la configuration requise et informations sur Azure sont toooffer dans chacun de ces domaines. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Présentation de la sécurité réseau Azure
Microsoft Azure inclut un toosupport infrastructure de mise en réseau robuste votre application et les exigences de connectivité de service. La connectivité réseau est possible entre les ressources situées dans Azure, entre locaux et Azure hébergé tooand de hello Internet et des ressources et Azure.

Hello cet article vise toomake il plus facile pour vous toounderstand ce que Microsoft Azure a toooffer dans la zone hello de sécurité réseau. Il décrit les notions de base sur les exigences et les concepts de la sécurité réseau. Nous fournissons également vous plus d’informations sur Azure a toooffer dans chacun de ces domaines ainsi que les liens toohelp vous bénéficiez d’une meilleure compréhension des zones intéressantes.

Cet article de présentation de la sécurité réseau Azure se concentre sur hello suivant de zones :

* Mise en réseau Azure
* Contrôle d’accès réseau
* Accès à distance sécurisé et connectivité intersite
* Disponibilité
* Résolution de noms
* Architecture DMZ
* Surveillance et détection des menaces


## <a name="azure-networking"></a>Mise en réseau Azure
Les machines virtuelles nécessitent une connectivité réseau. toosupport cette exigence, Azure nécessite toobe d’ordinateurs virtuels connecté tooan réseau virtuel Azure. Un réseau virtuel Azure est une construction logique reposant sur l’infrastructure du réseau Azure physique hello. Chaque réseau virtuel logique Azure est isolé des autres réseaux virtuels Azure. Cela permet de s’assurer que le trafic réseau dans vos déploiements n’est pas accessible tooother les clients de Microsoft Azure.

En savoir plus :

* [Présentation du réseau virtuel.](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Contrôle d’accès réseau
Contrôle d’accès réseau est act hello de limitation de tooand de connectivité à partir de périphériques spécifiques ou des sous-réseaux au sein d’un réseau virtuel Azure. objectif de Hello de contrôle d’accès réseau est le tooyour toolimit accéder aux machines virtuelles et les utilisateurs tooapproved des services et périphériques. Contrôles d’accès sont basés sur Autoriser ou refuser le décisions pour tooand des connexions à partir de votre ordinateur virtuel ou d’un service.

Azure prend en charge plusieurs types de contrôle d’accès réseau tels que :

* Contrôle de la couche réseau
* Contrôle du routage et tunneling forcé
* Appliances de sécurité de réseau virtuel

### <a name="network-layer-control"></a>Contrôle de la couche réseau
Tout déploiement sécurisé requiert certaines mesures de contrôle d’accès réseau. objectif de Hello de contrôle d’accès réseau est toorestrict machine virtuelle toohello nécessaire systèmes et communication que les autres tentatives de communication sont bloqués.

Si vous avez besoin de contrôle d’accès au réseau de base (basé sur l’adresse IP et hello TCP ou protocoles UDP), vous pouvez utiliser des groupes de sécurité réseau. Un groupe de sécurité réseau (NSG) est une base pare-feu de filtrage des paquets avec état et elle active l’accès toocontrol vous selon un [5-tuple](https://www.techopedia.com/definition/28190/5-tuple). Les groupes de sécurité réseau n’effectuent pas d’inspection de la couche d’application ni de contrôles d’accès authentifiés.

En savoir plus :

* [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Contrôle du routage et tunneling forcé
Hello capacité toocontrol comportement de routage sur vos réseaux virtuels Azure est une fonctionnalité de contrôle de sécurité et d’accès réseau critiques. Si le routage est configuré correctement, applications et services hébergés sur votre machine virtuelle peuvent se connecter les appareils toounauthorized, y compris les systèmes appartenant et exploité par des personnes malveillantes potentielles.

Mise en réseau Azure prend en charge le comportement de routage hello capacité toocustomize hello pour le trafic réseau sur vos réseaux virtuels Azure. Cela vous permet de tooalter hello par défaut routage entrées de la table dans votre réseau virtuel Azure. Le contrôle du comportement de routage vous permet de vous assurer que tout le trafic en provenance d’un appareil ou d’un groupe d’appareils donné entre ou quitte votre réseau virtuel par un point spécifique.

Par exemple, vous pouvez disposer d’une appliance de sécurité de réseau virtuel sur votre réseau virtuel Azure. Vous souhaitez toomake assurer que tous les tooand le trafic à partir de votre réseau virtuel Azure traverse ce dispositif de sécurité virtuel. Pour cela, vous pouvez configurer les [itinéraires définis par l’utilisateur](../virtual-network/virtual-networks-udr-overview.md) dans Azure.

[Le tunneling forcé](https://www.petri.com/azure-forced-tunneling) est un mécanisme que vous pouvez utiliser tooensure vos services ne sont pas autorisées tooinitiate un toodevices de connexion sur Internet de hello. Notez que cela est différent d’accepter les connexions entrantes et en répondant toothem. Serveurs web frontaux doivent toorequests toorespond à des hôtes Internet, et donc le trafic provenant d’Internet est autorisé entrant toothese web des serveurs hello sont autorisés à toorespond.

Ce que vous ne souhaitez tooallow est un tooinitiate de serveur web frontal une requête sortante. Ces demandes peuvent représenter un risque de sécurité, car ces connexions peut être utilisé toodownload contre les programmes malveillants. Même si vous ne voulez que ces frontal tooinitiate serveurs sortant demande toohello Internet, vous pouvez tooforce les toogo via votre site web proxy afin que vous pouvez tirer parti de l’URL, le filtrage et la journalisation.

Au lieu de cela, vous souhaiteriez toouse forcé tunneling tooprevent cela. Lorsque vous activez le tunneling forcé, toutes les connexions toohello Internet sont forcés via votre passerelle locale. Vous pouvez configurer le tunneling forcé en utilisant les itinéraires définis par l’utilisateur.

En savoir plus :

* [Présentation des itinéraires définis par l’utilisateur et du transfert IP](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Appliances de sécurité de réseau virtuel
Tandis que les groupes de sécurité réseau, itinéraires définis d’utilisateur et le tunneling forcé vous fournissent un niveau de sécurité au niveau des couches de transport et de réseau hello Hello [modèle OSI](https://en.wikipedia.org/wiki/OSI_model), il peut arriver lorsque vous souhaitez que la sécurité tooenable à des niveaux supérieurs réseau de hello.

Vos besoins en matière de sécurité peuvent inclure :

* Authentification et autorisation avant d’autoriser l’accès tooyour application
* La détection et la gestion des intrusions
* Une inspection de la couche d’application pour les protocoles de niveau supérieur
* Un filtrage des URL
* Un logiciel anti-programme malveillant et antivirus au niveau du réseau
* Une protection anti-robot
* Un contrôle d’accès aux applications
* Protection DDoS supplémentaire (au-dessus hello de la protection fournie DDoS hello tissu Azure lui-même)

Ces fonctionnalités avancées de sécurité réseau peuvent être mises en œuvre via une solution de partenaire Azure. Vous pouvez trouver des solutions de sécurité de réseau partenaire Azure plus récente de hello en visitant hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) et en recherchant « sécurité » et « sécurité réseau. »

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Accès à distance sécurisé et connectivité intersite
Le programme d’installation, la configuration et gestion de vos ressources Azure doit toobe effectuée à distance. En outre, vous souhaiterez peut-être toodeploy [informatiques hybrides](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) solutions qui ont des composants locaux et Bonjour cloud public Azure. Ces scénarios nécessitent un accès à distance sécurisé.

Mise en réseau Azure prend en charge hello sécuriser l’accès à distance les scénarios suivants :

* Connecter des stations de travail individuelles tooan réseau virtuel Azure
* Connecter votre tooan de réseau local sur le réseau virtuel Azure avec un réseau privé virtuel
* Connecter votre tooan de réseau local sur le réseau virtuel Azure avec une liaison WAN dédiée
* Connecter des réseaux virtuels Azure tooeach autres

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Connecter des stations de travail individuelles tooan réseau virtuel Azure
Il peut arriver lorsque vous souhaitez tooenable des opérations ou les développeurs personnel toomanage machines virtuelles et services dans Azure. Par exemple, vous devez accéder à ordinateur virtuel de tooa sur un réseau virtuel Azure et votre stratégie de sécurité n’autorise pas l’accès à distance RDP ou SSH tooindividual virtual machines. Dans ce cas, vous pouvez utiliser une connexion VPN de point à site.

Hello connexion VPN utilise hello point-to-site [VPN SSTP](https://technet.microsoft.com/library/cc731352.aspx) protocole tooenable tooset vous une connexion privée et sécurisée entre les utilisateurs de hello et hello réseau virtuel Azure. Une fois la connexion VPN de hello établie, hello sera en mesure de tooRDP ou SSH sur hello VPN lier à un ordinateur virtuel sur hello du réseau virtuel Azure (en supposant que hello utilisateur peut s’authentifier et est autorisé).

En savoir plus :

* [Configurer un tooa de connexion de Point à Site du réseau virtuel à l’aide de PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>Connecter votre réseau local tooan réseau virtuel Azure avec un réseau privé virtuel
Vous souhaiterez tooconnect votre réseau d’entreprise, ou des parties de celui-ci, tooan réseau virtuel Azure. Il s’agit d’un scénario d’informatique hybride courant dans lequel les entreprises [étendent leur centre de données local dans Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). Dans de nombreux cas, les entreprises hébergent une partie du service dans Azure et l’autre partie dans leur centre de données local, notamment lorsque la solution comprend des serveurs web frontaux dans Azure et des bases de données principales locales. Ces types de connexions « intersite » offrent une gestion plus sécurisée des ressources hébergées dans Azure et prennent en charge des scénarios tels que l’extension des contrôleurs de domaine Active Directory dans Azure.

Une façon tooaccomplish il s’agit de toouse un [VPN de site à site](https://www.techopedia.com/definition/30747/site-to-site-vpn). Hello différence entre un réseau VPN de site à site et un réseau de point-to-site VPN est qu’un VPN de point-to-site connecte à un tooan de périphérique réseau virtuel Azure, lors d’un VPN de site à site connecte à un réseau virtuel Azure de tooan tout le réseau (par exemple, votre réseau local) . Tooan de VPN de site à site réseau virtuel Azure utilisent le protocole VPN du mode tunnel de la IPsec hautement sécurisé hello.

En savoir plus :

* [Créer un gestionnaire de ressources de VNet avec une connexion VPN de site à site à l’aide de hello portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Planification et conception de la passerelle VPN](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Connecter votre réseau virtuel Azure de tooan réseau local avec une liaison WAN dédiée
Les connexions VPN de point à site et de site à site offrent une véritable connectivité intersite. Toutefois, certaines organisations Examinons les hello toohave suivant présente deux inconvénients :

* Connexions VPN de déplacement des données sur Internet de hello : cela expose ces connexions toopotential problèmes de sécurité lors du déplacement des données via un réseau public. En outre, il est impossible de garantir la fiabilité et la disponibilité des connexions Internet.
* TooAzure des connexions VPN réseaux virtuels peut-être être considérées comme bande passante limitée pour certaines applications et les besoins, en tant qu’ils max out à environ 200 Mbits/s.

Les organisations doivent hello plus haut niveau de sécurité et la disponibilité pour les connexions entre différents locaux généralement utiliser les liaisons WAN dédiées tooconnect tooremote sites. Azure fournit que Hello de capacité toouse une liaison WAN dédiée, que vous pouvez utiliser tooconnect votre tooan de réseau local sur le réseau virtuel Azure. Pour cela, vous devez utiliser Azure ExpressRoute.

En savoir plus :

* [Présentation technique d’ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Connecter des réseaux virtuels Azure tooEach autres
Il est possible que vous toouse plusieurs réseaux virtuels Azure pour vos déploiements. Plusieurs raisons peuvent vous encourager à le faire, Une des raisons de hello peut-être toosimplify gestion ; une autre peut être pour des raisons de sécurité. Quelle que soit la motivation hello ou raisonnement pour placer les ressources sur différents réseaux virtuels Azure, il peut arriver lorsque vous souhaitez que les ressources sur chacun des tooconnect de réseaux hello avec l’autre.

L’une des options serait de services sur un seul tooservices tooconnect de réseau virtuel Azure sur un autre réseau virtuel Azure par « de bouclage dans » via hello Internet. connexion de Hello serait démarrer sur un réseau virtuel Azure, parcourez hello Internet, puis revenir toohello destination réseau virtuel Azure. Cette option expose hello connexion toohello sécurité problèmes inhérents tooany communication basée sur Internet.

Une meilleure option peut être toocreate virtuel Azure réseau sur Azure virtuel réseau VPN de site à site. Ce réseau virtuel de Azure Virtual Network pour Azure VPN de site à site utilise hello même [le mode de tunnel IPsec](https://technet.microsoft.com/library/cc786385.aspx) protocole comme indiquée ci-dessus pour la connexion hello intersite site-à-site VPN.

avantage Hello de virtuel Azure réseau sur Azure virtuel réseau VPN de site à site est que hello VPN est établie via hello infrastructure réseau Azure au lieu de la connexion sur Internet de hello. Ainsi, que vous avez une couche supplémentaire de sécurité comparé toosite-to-site VPN qui se connectent via Internet de hello.

En savoir plus :

* [Configurer une connexion de réseau virtuel à réseau virtuel à l’aide d’Azure Resource Manager et de PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Availability
La disponibilité est au cœur de tout programme de sécurité. Si vos systèmes et les utilisateurs ne peuvent pas accéder à ce qu’ils doivent tooaccess sur hello réseau, hello service peut être considéré comme compromis. Azure présente les technologies de réseau que hello prise en charge après les mécanismes haute disponibilité :

* Équilibrage de charge basé sur HTTP
* Équilibrage de charge au niveau du réseau
* Équilibrage de charge global

Équilibrage de charge est un tooequally mécanisme conçu répartir les connexions entre plusieurs appareils. objectifs Hello d’équilibrage de charge sont :

* Augmenter la disponibilité – lorsque vous chargez équilibrer les connexions entre plusieurs appareils, une ou plusieurs des appareils de hello peuvent devenir indisponible et services hello en cours d’exécution sur hello restant en ligne de périphériques peuvent continuer de contenu de hello tooserve à partir du service de hello
* Augmenter les performances : lorsque vous chargez équilibrer les connexions entre plusieurs appareils, un seul appareil n’a pas processeur de hello tootake atteint. Au lieu de cela, les demandes de traitement et mémoire hello pour héberger un contenu de hello est répartie sur plusieurs appareils.

### <a name="http-based-load-balancing"></a>Équilibrage de charge basé sur HTTP
Organisations que les services web exécution souhaitent souvent toohave un équilibrage de charge basé sur HTTP devant ces toohelp de services web de garantir des niveaux de performances et haute disponibilité adéquats. En revanche les équilibreurs de charge de tootraditional basée sur le réseau, hello décisions équilibrage de charge apportées par les programmes d’équilibrage de charge basé sur HTTP sont basées sur les caractéristiques du protocole hello HTTP, pas sur les protocoles de couches de transport et de réseau hello.

tooprovide vous HTTP d’équilibrage de charge pour les services web, Azure fournit hello de passerelle d’Application Azure. prend en charge de la passerelle d’Application Azure Hello :

* Basée sur HTTP équilibrage de charge – décisions équilibrage de charge sont effectuées en fonction de protocole de toohello spécial caractéristique HTTP
* Affinité de session basée sur le cookie – cette fonctionnalité permet de s’assurer que les connexions établies tooone des serveurs hello derrière cet équilibrage de charge reste intact entre serveur et client de hello. La stabilité des transactions est ainsi garantie.
* Déchargement SSL – lorsqu’une connexion cliente est établie avec équilibrage de charge hello, que la session entre le client de hello et équilibrage de charge hello est chiffrée à l’aide de hello HTTPS (SSL /) protocole. Toutefois, les performances de tooincrease de commande, vous disposez d’hello option toohave hello connexion entre l’équilibrage de charge hello et serveur web de hello derrière hello charge équilibrage utiliser hello HTTP (non chiffré) le protocole. Il s’agit de tooas référencé « déchargement SSL », car les serveurs web de hello derrière un équilibreur de charge hello ne rencontrez pas de surcharge du processeur hello impliqué dans le chiffrement et doivent donc être tooservice en mesure de requêtes plus rapidement.
* URL de routage en fonction du contenu – cette fonctionnalité rend possible pour les décisions de toomake d’équilibrage de charge hello sur où les connexions tooforward basée sur URL cible de hello. Cela offre une plus grande flexibilité que les solutions qui répartissent la charge en fonction des adresses IP.

En savoir plus :

* [Vue d’ensemble d’Application Gateway](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Équilibrage de charge au niveau du réseau
En revanche tooHTTP d’équilibrage de charge, équilibrage de charge au niveau réseau permet de charger l’équilibrage des décisions basées sur IP adresse et port (TCP ou UDP) les numéros.
Vous pouvez bénéficier des avantages de hello réseau au niveau d’équilibrage de charge dans Azure à l’aide de hello équilibrage de charge Azure. Certaines caractéristiques clés de hello équilibrage de charge Azure sont les suivantes :

* Équilibrage de charge au niveau du réseau basé sur les adresses IP et les numéros de port
* Prise en charge de l’ensemble des protocoles de couche d’application
* Équilibre la charge de machines virtuelles de tooAzure et instances de rôle des services de cloud computing
* Peut être utilisé à la fois pour les applications et les machines virtuelles accessibles sur Internet (équilibrage de charge externe) et non accessibles sur Internet (équilibrage de charge interne)
* Point de terminaison de surveillance, qui est utilisé toodetermine si un des services hello derrière un équilibreur de charge hello soient plus disponible

En savoir plus :

* [Équilibrage de charge accessible sur Internet entre plusieurs services ou machines virtuelles](../load-balancer/load-balancer-internet-overview.md)
* [Présentation de l’équilibrage de charge interne](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Équilibrage de charge global
Certaines organisations souhaiteront hello plus haut niveau de disponibilité possibles. Une façon tooreach que globalement les applications toohost dans cet objectif n’est distribué centres de données. Lorsqu’une application est hébergée dans les centres de données situés dans l’ensemble de Bonjour, il est possible pour un toobecome de l’ensemble de la région géopolitiques non disponible et encore application hello et en cours d’exécution.

En outre les avantages de la disponibilité toohello que vous obtenez en hébergeant des applications dans des centres de données distribués internationalement, vous pouvez également obtenir des gains de performance. Ces avantages de performances peuvent être obtenues à l’aide d’un mécanisme qui dirige les requêtes pour hello service toohello centre de données est la plus proche de l’appareil toohello qui demande hello.

Avec l’équilibrage de charge global, vous améliorez donc aussi bien la disponibilité que les performances. Dans Azure, vous pouvez bénéficier des avantages de hello global d’équilibrage de charge à l’aide de Azure Traffic Manager.

En savoir plus :

* [Qu’est-ce que Traffic Manager ?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Résolution de noms
La résolution de noms est une fonctionnalité essentielle pour tous les services que vous hébergez dans Azure. Du point de vue de la sécurité, une compromission de la fonction de résolution de noms hello peut entraîner des demandes de redirection tooan attaquant à partir du site de l’attaquant tooan de vos sites. Une résolution de noms sécurisée est donc requise pour tous vos services hébergés dans le cloud.

Il existe deux types de résolution de noms que vous avez besoin de tooaddress :

* Résolution de noms interne : la résolution de noms interne est utilisée par les services hébergés sur vos réseaux virtuels Azure, sur vos réseaux locaux ou sur les deux. Les noms utilisés pour la résolution de nom interne ne sont pas accessibles via hello Internet. Pour une sécurité optimale, il est important que votre schéma de résolution de nom interne n’est pas accessible tooexternal utilisateurs.
* Résolution de noms externe : la résolution de noms externe est utilisée par les personnes et les appareils qui se trouvent en dehors de vos réseaux virtuels Azure et de vos réseaux locaux. Il s’agit de noms hello qui sont visible toohello Internet et services de nuage utilisé toodirect connexion tooyour.

Pour la résolution de noms interne, vous avez deux options :

* Un serveur DNS associé au réseau virtuel Azure : lorsque vous créez un réseau virtuel Azure, un serveur DNS est automatiquement créé. Ce serveur DNS peut résoudre les noms de hello hello les ordinateurs situés sur ce réseau virtuel Azure. Ce serveur DNS n’est pas configurable et est géré par le Gestionnaire de l’infrastructure Azure hello, ce qui rend une solution de résolution de nom sécurisée.
* Mettre votre propre serveur DNS : vous pouvez hello consistant à placer un serveur DNS de votre choix sur votre réseau virtuel Azure. Ce serveur DNS peut être qu'un répertoire Active Directory intégré au serveur DNS ou une solution de serveur DNS fournie par le partenaire d’Azure, vous pouvez obtenir à partir de hello Azure Marketplace.

En savoir plus :

* [Présentation du réseau virtuel.](../virtual-network/virtual-networks-overview.md)
* [Gestion des serveurs DNS utilisés par un réseau virtuel](../virtual-network/virtual-network-manage-network.md#dns-servers)

Pour la résolution DNS externe, vous avez également deux options :

* Héberger votre propre serveur DNS externe sur site
* Héberger votre propre serveur DNS externe via un fournisseur de services

Les grandes organisations préfèrent généralement héberger leurs serveurs DNS sur site. Pour cela, ils peuvent, car ils ont hello de mise en réseau expertise présence toodo donc.

Dans la plupart des cas, il s’agit d’une meilleure toohost la résolution de noms DNS des services avec un fournisseur de services. Ces fournisseurs de services ont hello connaissance des réseaux et présence tooensure très haute disponibilité pour vos services de résolution de noms. Disponibilité est essentielle pour les services DNS, car si la résolution de noms de services échouent, personne ne sera être en mesure de tooreach faisant face à des services Internet.

Azure offre une haute disponibilité et performant une solution DNS externe sous forme de hello d’Azure DNS. Cette solution de résolution de nom externe tire parti de l’infrastructure de DNS Azure hello dans le monde entier. Il vous permet de toohost votre domaine dans Azure à l’aide hello les mêmes informations d’identification, les API, outils et facturation en tant que vos autres services Azure. Dans le cadre d’Azure, il hérite également des contrôles de sécurité renforcée hello intégrées à la plateforme de hello.

En savoir plus :

* [Vue d'ensemble d’Azure DNS](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>Architecture DMZ
De nombreuses entreprises utilisent DMZ toosegment leur toocreate réseaux une zone de mémoire tampon entre hello Internet et leurs services. partie du réseau de périmètre Hello du réseau de hello est considérée comme une zone de sécurité faible et aucune des ressources de valeur élevée ne sont placés dans ce segment de réseau. Vous verrez généralement des périphériques de sécurité réseau qui ont une interface réseau sur le segment de réseau de périmètre de hello et une autre interface tooa connecté réseau qui a des machines virtuelles et services qui acceptent les connexions entrantes à partir de hello Internet.

Il existe plusieurs variantes de conception de réseau de périmètre et hello décision toodeploy un réseau de périmètre, puis sur le type de réseau de périmètre toouse si vous décidez de toouse, est basé sur vos exigences de sécurité réseau.

En savoir plus :

* [Services cloud et sécurité réseau Microsoft](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Surveillance et détection des menaces

Azure fournit des fonctionnalités toohelp vous dans cette zone clée anticipée détection, analyse et hello capacité toocollect et examiner le trafic réseau.

### <a name="azure-network-watcher"></a>Azure Network Watcher
Observateur de réseau Azure comprend un grand nombre de fonctionnalités qui vous aider à résoudre, ainsi que de fournir un tout nouvel ensemble d’outils tooassist identification hello de problèmes de sécurité.

[Affichage du groupe de sécurité ](/network-watcher/network-watcher-security-group-view-overview.md) aide à la conformité de l’audit et la sécurité des ordinateurs virtuels et peut être utilisé tooperform programmation audits comparant les stratégies de lignes de base hello définies par les règles de tooeffective de votre organisation pour chacun de vos machines virtuelles. Cela peut vous aider à identifier les différences de configuration.

[Capture des paquets](/network-watcher/network-watcher-packet-capture-overview.md) vous permet de toocapture tooand de trafic réseau de la machine virtuelle de hello. Outre les aider à en vous donnant les statistiques réseau toocollect et hello résolution des problèmes d’application capture des paquets de problèmes peut être précieuse dans enquête hello des intrusions. Vous pouvez également utiliser cette fonctionnalité avec les fonctions Azure toostart réseau capture dans la réponse toospecific Azure alertes.

Pour plus d’informations sur l’Observateur réseau de Azure et comment toostart certaines fonctionnalités de hello de test dans vos laboratoires Examinons hello [Observateur réseau Azure la présentation des moniteurs](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Observateur de réseau Azure est toujours en version préliminaire publique afin qu’il ne peut pas avoir hello même niveau de disponibilité et la fiabilité en tant que services sont en général version en disponibilité. Certaines fonctionnalités ne sont peut-être pas prises en charge, disposent peut-être de capacités limitées et ne sont peut-être pas disponibles dans tous les emplacements Azure. Pour les notifications actualisées hello sur la disponibilité et l’état de ce service, vérifiez hello [page mises à jour Azure](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure Security Center
Centre de sécurité vous aide à empêcher, détecter et répondre toothreats et fournit le qu'augmentation de la visibilité et contrôler, sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste ensemble de solutions de sécurité.

Azure Security Center vous permet d’optimiser et de surveiller la sécurité réseau grâce aux opérations suivantes :

* Mise à disposition de recommandations relatives à la sécurité réseau
* Analyse de l’état de hello de votre configuration de sécurité réseau
* Génération d’alertes vous toonetwork basé menaces à la fois aux niveaux de réseau et de point de terminaison hello

En savoir plus :

* [Introduction tooAzure centre de sécurité](../security-center/security-center-intro.md)


### <a name="logging"></a>Journalisation
La journalisation au niveau du réseau est un élément clé de tout scénario de sécurité réseau. Dans Azure, vous pouvez consigner les informations obtenues pour enregistrer des informations sur le niveau des groupes de sécurité réseau tooget réseau. La journalisation des groupes de sécurité réseau vous permet de consigner les données des journaux suivants :

* [Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) – ces journaux sont tooview utilisé toutes les opérations envoyées tooyour Azure abonnements. Ces journaux sont activés par défaut et peuvent être utilisés dans hello portail Azure. Ils étaient auparavant nommés « Journaux d’audit » ou « Journaux des opérations ».
* Journaux des événements : ces journaux permettent de savoir quelles règles de groupe de sécurité réseau (NSG) ont été appliquées.
* Les journaux de compteur – ces journaux indiquer combien de fois chaque règle de groupe de sécurité réseau a été appliqué toodeny ou autorisent le trafic.

Vous pouvez également utiliser [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), une visualisation des données puissant outil, tooview et analyser ces journaux.

En savoir plus :

* [Analyse de journaux pour les groupes de sécurité réseau (NSG)](../virtual-network/virtual-network-nsg-manage-log.md)
