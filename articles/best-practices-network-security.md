---
title: "meilleures pratiques de la sécurité de réseau aaaAzure | Documents Microsoft"
description: "Découvrez que certaines des principales fonctionnalités hello disponibles dans Azure toohelp créent des environnements de réseau sécurisés"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Services de cloud computing et sécurité réseau Microsoft
Les services cloud Microsoft offrent une grande évolutivité des services et de l’infrastructure, des capacités de niveau d'entreprise et de nombreuses options de connectivité hybride. Clients peuvent choisir tooaccess ces services via hello Internet ou avec Azure ExpressRoute, qui assure la connectivité de réseau privé. plateforme de Microsoft Azure Hello permet clients tooseamlessly étendre leur infrastructure en nuage de hello et générer des architectures multicouches. Par ailleurs, des tiers peuvent activer des fonctionnalités améliorées en offrant des services de sécurité et des appliances virtuelles. Ce livre blanc fournit une vue d’ensemble des problèmes de sécurité et d’architecture dont les clients doivent tenir compte lorsqu’ils utilisent des services de cloud computing Microsoft auxquels ils accèdent avec ExpressRoute. Il décrit également la création de services plus sécurisés dans les réseaux virtuels Azure.

## <a name="fast-start"></a>Démarrage rapide
Hello suivant le graphique de la logique peut diriger vous tooa exemple spécifique de hello de nombreuses techniques de sécurité disponibles avec hello plateforme Azure. Pour référence rapide, recherchez exemple hello mieux adapté à votre cas. Pour obtenir des explications développées, poursuivez la lecture sur papier hello.
[![0]][0]

[Exemple 1 : Créer un réseau de périmètre (également appelé DMZ, zone démilitarisée ou DMZ ou sous-réseau filtré) toohelp protéger les applications avec des groupes de sécurité réseau (NSG).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Exemple 2 : Créer un périmètre réseau toohelp protéger les applications avec un pare-feu et des groupes de sécurité réseau.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Exemple 3 : Créer un périmètre réseau toohelp protéger les réseaux à un pare-feu, un itinéraire défini par l’utilisateur (UDR) et un groupe de sécurité réseau.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Exemple 4 : Ajouter une connexion hybride avec un réseau privé virtuel (VPN) d’appliance virtuelle de site à site.](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Exemple 5 : Ajouter une connexion hybride avec une passerelle VPN Azure de site à site.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Exemple 6 : Ajouter une connexion hybride avec ExpressRoute.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Exemples d’ajout de connexions entre les réseaux virtuels, la haute disponibilité et le chaînage des propriétés du service seront ajoutés toothis document sur hello prochains mois.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Conformité et protection des infrastructures Microsoft
les organisations toohelp conforme aux nationales, régionales, et les exigences spécifiques régissant la collecte de hello et utilisation des données des individus, Microsoft offre plus de 40 attestations et certifications. Hello plus complète jeu de n’importe quel fournisseur de service cloud.

Pour plus d’informations, consultez les informations de compatibilité hello sur hello [Microsoft Trust Center][TrustCenter].

Microsoft propose une approche complète tooprotect infrastructure nécessaire toorun une évolutivité globale services cloud. Infrastructure de cloud de Microsoft inclut le matériel, les logiciels, les réseaux et d’administration et le personnel chargé des opérations, en outre toohello physique centres de données.

![2]

Cette approche fournit une Fondation plus sécurisée pour les clients toodeploy leurs services Bonjour cloud de Microsoft. étape suivante de Hello pour les clients toodesign et créer un tooprotect d’architecture de sécurité de ces services.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Architectures de sécurité traditionnelles et réseaux de périmètre
Bien que Microsoft investissements massifs protéger l’infrastructure de cloud hello, les clients doivent également protéger leurs services de cloud computing et les groupes de ressources. Une approche multicouche de toosecurity fournit profitent hello. Une zone de sécurité de type réseau de périmètre protège les ressources réseau internes d’un réseau non approuvé. Un réseau de périmètre fait référence toohello bords ou des parties du réseau de hello qui se situent entre hello Internet et de l’entreprise hello protégé infrastructure informatique.

Dans les réseaux d’entreprise classique, l’infrastructure de base hello est fortement enrichi au périmètre hello, avec plusieurs couches de dispositifs de sécurité. limite de Hello de chaque couche se compose des appareils et des points de mise en œuvre de stratégie. Chaque couche peut inclure une combinaison de hello suivant de périphériques de sécurité réseau : pare-feu, protection contre les attaques de déni de Service (DoS), la détection d’Intrusion ou des systèmes de Protection (intrusion) et périphériques VPN. Application de la stratégie peut prendre l’écran hello de stratégies de pare-feu, de listes de contrôle d’accès (ACL) ou de routage spécifique. Hello première ligne de défense dans réseau hello, accepter directement de trafic entrant en provenance d’Internet, de hello est une combinaison de ces mécanismes tooblock attaques et du trafic dangereux tout en permettant aux demandes légitimes davantage dans un réseau de hello. Ce trafic achemine directement tooresources hello réseau de périmètre. Cette ressource peut ensuite « communiquer » avec tooresources plus en réseau hello, en transit limite suivant de hello pour la validation du premier. couche la plus éloignée Hello est appelé réseau de périmètre hello, car cette partie du réseau de hello est exposé toohello Internet, généralement avec une certaine forme de protection sur les deux côtés. Hello figure suivante montre un exemple d’un réseau de périmètre de sous-réseau unique dans un réseau d’entreprise, avec deux limites de sécurité.

![3]

Il existe de nombreuses architectures utilisés tooimplement un réseau de périmètre. Ces architectures peuvent avec divers mécanismes chaque trafic tooblock de limite de plage à partir d’un réseau de périmètre de plusieurs sous-réseaux de charge simple équilibrage tooa et protéger les couches les plus profondes hello hello réseau d’entreprise. Comment le réseau de périmètre hello est créée dépend de hello des besoins spécifiques de l’organisation de hello et sa tolérance au risque global.

Les clients déplacent leurs clouds toopublic de charges de travail, il est critique toosupport des fonctionnalités similaires pour l’architecture de réseau de périmètre dans Azure toomeet conformité en matière de sécurité. Ce document fournit aux clients des instructions pour créer un environnement réseau sécurisé dans Azure. Il se concentre sur le réseau de périmètre hello, mais il inclut également des informations complètes sur de nombreux aspects de sécurité réseau. Hello suivant questions informe cette discussion :

* Comment créer un réseau de périmètre dans Azure ?
* Quelles sont de réseau de périmètre hello fonctionnalités Azure disponibles toobuild hello ?
* Comment les charges de travail principales peuvent-elles être protégées ?
* Comment les charges de travail toohello de communication contrôlée Internet dans Azure ?
* Comment hello sur des réseaux locaux peuvent être protégés à partir des déploiements dans Azure ?
* Dans quels cas les fonctionnalités de sécurité Azure natives doivent-elles être utilisées par rapport aux appliances ou services tiers ?

Hello suivant schéma montre les différentes couches de sécurité Qu'azure fournit toocustomers. Ces couches sont natif Bonjour plateforme Azure lui-même et fonctions définies par le client :

![4]

Entrant à partir de hello Internet, DDoS Azure vous aide à protéger contre les attaques à grande échelle sur Azure. couche de suivante Hello est définie par le client des adresses IP publiques (points de terminaison), qui sont utilisé toodetermine le trafic peut passer par le réseau virtuel de hello cloud service toohello. L’isolement du réseau virtuel Azure natif garantit l’isolement complet de tous les autres réseaux et la circulation du trafic uniquement au moyen des méthodes et des chemins d’accès configurés par l’utilisateur. Ces chemins d’accès et les méthodes sont la couche suivante hello, où les groupes de sécurité réseau et les dispositifs réseau virtuel UDR peuvent être utilisé toocreate sécurité limites tooprotect hello déploiements d’applications dans le réseau de hello protégé.

Hello suivant présente une vue d’ensemble des réseaux virtuels Azure. Ces réseaux virtuels sont créés par les clients et leurs charges de travail déployées y sont connectées. Les réseaux virtuels sont base hello de toutes les fonctionnalités de sécurité réseau hello requis tooestablish un périmètre réseau tooprotect des déploiements clients dans Azure.

## <a name="overview-of-azure-virtual-networks"></a>Vue d’ensemble des réseaux virtuels Azure
Avant que le trafic Internet pour pouvoir obtenir toohello réseaux virtuels Azure, il existe deux couches de sécurité, toohello inhérents à la plateforme Azure :

1.    **Protection DDoS**: protection DDoS est une couche de hello Azure réseau physique qui protège hello plateforme Azure lui-même contre les attaques par Internet à grande échelle. Ces attaques utiliser plusieurs nœuds de « robots » dans un toooverwhelm de la tentative d’un service Internet. Azure comprend un maillage de protection DDoS robuste sur toutes les connexions entrantes, sortantes et inter-régions Azure. Cette couche de protection DDoS possède pas d’attributs configurables par l’utilisateur et n’est pas accessible toohello client. couche de protection DDoS Hello protège Azure en tant que plateforme contre les attaques à grande échelle, il analyse également le trafic sortant et le trafic de région cross-Azure. À l’aide des équipements virtuels du réseau sur le réseau virtuel de hello, des couches supplémentaires de résilience peuvent être configurés par le client hello contre une attaque de l’échelle plus petite qui ne déclencher protection au niveau de plate-forme hello. Un exemple de DDoS en action ; Si un ordinateur à adresse IP d’internet a été attaqué par une attaque DDoS à grande échelle, Azure détecte des sources d’attaques de hello hello et lire à vitesse variable hello incriminée trafic avant d’atteindre sa destination prévue. Dans presque tous les cas, hello attaqué du point de terminaison n’est pas affecté par une attaque de hello. Aucun trafic n’est affecté tooother de points de terminaison, seul point de terminaison hello attaqué hello très rare qu’un point de terminaison est affecté. Les autres clients et services ne sont donc pas impactés par cette attaque. Il est critique toonote qu’Azure DDoS recherche uniquement les attaques à grande échelle. Il est possible que votre service spécifique peut être submergé avant le dépassement des seuils de niveau de protection de plateforme hello. Par exemple, un site web sur un serveur A0 IIS unique pourrait être mis en mode hors connexion par une attaque DDoS avant que la protection contre les DDoS au niveau de la plateforme Azure ne l'identifie comme une menace.

2.  **Les adresses IP publiques**: adresse IP publique (activés via les points de terminaison de service, les adresses IP publiques, passerelle d’Application et autres fonctionnalités Azure qui présentent une ressource de tooyour internet routé publique IP adresse toohello) des adresses permettent aux services cloud ou les groupes de ressources toohave les adresses IP Internet publiques et les ports exposés. point de terminaison de Hello utilise l’adresse interne du toohello trafic tooroute traduction d’adresses réseau (NAT) et le port sur hello réseau virtuel Azure. Ce chemin d’accès est hello pour principal moyen toopass trafic externe au réseau virtuel de hello. adresses IP publiques de Hello sont configurable toodetermine le trafic qui est passé dans, et où et comment il est traduit sur le réseau virtuel de toohello.

Une fois que le trafic atteint le réseau virtuel de hello, il existe de nombreuses fonctionnalités qui entrent en jeu. Réseaux virtuels Azure sont hello fondation pour les clients tooattach leurs charges de travail et où la sécurité de base au niveau du réseau s’applique. Il est un réseau privé (une superposition du réseau virtuel) dans Azure pour les clients avec hello suivant les fonctionnalités et caractéristiques :

* **Isolation du trafic**: un réseau virtuel est la limite de d’isolation du trafic hello sur hello plateforme Azure. Machines virtuelles (VM) dans un réseau virtuel ne peut pas communiquer directement tooVMs dans un réseau virtuel différent, même si les deux réseaux virtuels est créés par hello même client. Cet isolement est une propriété critique qui garantit que les machines virtuelles et les communications du client restent privées dans un réseau virtuel.

>[!NOTE]
>Isolation du trafic fait référence uniquement tootraffic *entrant* toohello des réseaux virtuels. Par le trafic sortant de valeur par défaut à partir de toohello de réseau virtuel hello internet est autorisée, mais peut être évitée si vous le souhaitez en groupes de sécurité réseau.
>
>

* **Topologie de plusieurs niveaux**: les réseaux virtuels permettent aux clients topologie à plusieurs niveaux de toodefine en allouant des sous-réseaux et désigner des espaces d’adressage distincts pour différents éléments ou à « couche » de leurs charges de travail. Ces regroupements logiques topologies activer la stratégie d’accès différents toodefine clients basée sur les types de charges de travail hello et également contrôlent le flux de trafic entre les couches de hello.
* **Connexions entre différents locaux**: les clients peuvent établir des connexions entre locaux entre un réseau virtuel et plusieurs sites locaux ou d’autres réseaux virtuels dans Azure. tooconstruct une connexion, les clients peuvent utiliser d’homologation de réseau virtuel, les passerelles VPN Azure, les équipements virtuels réseau tiers ou ExpressRoute. Azure prend en charge les VPN de site à site (S2S) à l’aide des protocoles IPsec/IKE standards et de la connectivité privée ExpressRoute.
* **Groupe de sécurité réseau** permet aux clients toocreate règles (ACL) au niveau de hello souhaité de granularité : interfaces, des ordinateurs virtuels individuels ou des sous-réseaux virtuels du réseau. Les clients peuvent contrôler l’accès en autoriser ou refuser la communication entre les charges de travail hello dans un réseau virtuel, à partir des systèmes sur des réseaux du client via la connectivité intersite, ou diriger la communication Internet.
* **UDR** et **le transfert IP** permettent aux clients de chemins de communication hello toodefine entre différents niveaux au sein d’un réseau virtuel. Les clients peuvent déployer un pare-feu, les services IDS/IPS et d’autres appliances virtuelles et acheminer le trafic réseau à travers ces appliances de sécurité pour l’application de stratégies de limites de sécurité, l’audit et l’inspection.
* **Réseau virtuel** Bonjour Azure Marketplace : appliances de sécurité telles que les pare-feu, les équilibreurs de charge et les ID/adresses IP sont disponibles dans Azure Marketplace de hello et hello Galerie d’images de machine virtuelle. Les clients peuvent déployer ces appareils dans leurs réseaux virtuels et en particulier, à leur environnement de réseau sécurisé sécurité limites (y compris les sous-réseaux de réseau de périmètre hello) toocomplete un à plusieurs niveaux.

Avec ces fonctionnalités et les fonctions, un exemple de la façon dont une architecture de réseau de périmètre peut être construite dans Azure est hello suivant schéma :

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Caractéristiques et conditions requises d’un réseau de périmètre
réseau de périmètre Hello est la partie frontale hello de réseau hello, interagissant directement de communication de hello Internet. les paquets Hello entrants doivent traverser des appliances de sécurité hello, tels que les pare-feu hello, ID et adresses IP, avant d’atteindre les serveurs principaux de hello. Paquets Internet liées à partir de charges de travail hello peuvent également circuler via les appliances de sécurité hello dans le réseau de périmètre hello pour l’application des stratégies, d’inspection et de l’audit à des fins, avant de quitter le réseau de hello. En outre, réseau de périmètre hello peut héberger des passerelles VPN intersite entre les réseaux virtuels client et sur des réseaux locaux.

### <a name="perimeter-network-characteristics"></a>Caractéristiques d’un réseau de périmètre
Faisant référence à la figure précédente hello, hello les caractéristiques d’un réseau de périmètre bon sont les suivantes :

* Accès sur Internet :
  * sous-réseau de réseau de périmètre Hello lui-même est connecté à Internet, communique directement avec hello Internet.
  * Les adresses IP publiques, des adresses IP virtuelles et/ou des points de terminaison de service passer les périphériques et réseau frontal du toohello du trafic Internet.
  * Le trafic entrant à partir de hello Qu'internet transmet des dispositifs de sécurité avant les autres ressources sur le réseau frontal de hello.
  * Si la sécurité de trafic sortant est activée, le trafic passe par le biais des dispositifs de sécurité, comme étape finale de hello, avant de le transmettre toohello Internet.
* Réseau protégé :
  * Il n’existe aucun chemin d’accès direct à partir de l’infrastructure de base toohello hello Internet.
  * Infrastructure de base de canaux toohello doit traverser les dispositifs de sécurité telles que les groupes de sécurité réseau, les pare-feu ou les périphériques VPN.
  * Autres périphériques pas doivent établir une passerelle Internet et hello infrastructure de base.
  * Dispositifs de sécurité sur les deux hello exposés à Internet et de réseau protégé de hello faisant face à des limites du réseau de périmètre hello (par exemple, les icônes de pare-feu de hello deux sont affichées dans la figure précédente hello) peut être un équipement virtuel unique avec des règles différenciés ou interfaces pour chaque limite. Par exemple, un appareil physique, séparé logiquement, gestion de la charge pour les limites du réseau de périmètre hello hello.
* Autres pratiques courantes et contraintes :
  * Les charges de travail ne doivent pas stocker d’informations professionnelles stratégiques.
  * Déploiements et les configurations de réseau tooperimeter accès et les mises à jour sont des administrateurs de tooonly limitée autorisé.

### <a name="perimeter-network-requirements"></a>Conditions requises pour le réseau de périmètre
tooenable ces caractéristiques, suivez les instructions sur la configuration requise de réseau virtuel tooimplement un réseau de périmètre réussie :

* **Architecture de sous-réseaux :** spécifiez hello virtuel réseau telles que dédié un sous-réseau complet en tant que réseau de périmètre hello, séparé des autres sous-réseaux Bonjour même réseau virtuel. Cette séparation garantit le trafic de hello entre le réseau de périmètre hello et d’autres flux de niveaux de sous-réseau interne ou privé via un pare-feu ou un équipement virtuel d’intrusion.  Itinéraires définis par l’utilisateur limite hello sous-réseaux sont requis tooforward cette appliance virtuelle toohello de trafic.
* **Groupe de sécurité réseau :** sous-réseau de réseau de périmètre hello lui-même doit être ouvert tooallow la communication avec hello Internet, mais qui ne signifie pas que les clients doivent être en ignorant des groupes de sécurité réseau. Suivez courantes sécurité pratiques toominimize hello réseau surfaces exposées toohello Internet. Verrouiller des plages d’adresse distante hello autorisées des déploiements tooaccess hello ou protocoles d’application spécifique hello et les ports qui sont ouverts. Il peut arriver, cependant, qu'un verrouillage complet ne soit pas possible. Par exemple, si les clients ont un site Web externe dans Azure, réseau de périmètre hello doit autoriser les demandes web entrantes hello à partir de toute adresse IP publique, mais doit ouvrir uniquement les ports d’application web hello : TCP sur le port 80 et/ou TCP sur le port 443.
* **Table de routage :** sous-réseau de réseau de périmètre hello lui-même doit être en mesure de toocommunicate toohello Internet directement, mais ne doit pas permettre tooand communication directe à partir de réseaux de fin ou locale précédent hello sans passer par un pare-feu ou Dispositif de sécurité.
* **Configuration des appliances de sécurité :** tooroute et inspecter des paquets entre le réseau de périmètre hello et rest hello des réseaux de hello protégé, hello appliances de sécurité telles que les pare-feu, ID, et les appareils d’adresses IP multirésident. Ils peuvent avoir des cartes réseau distinctes pour le réseau de périmètre hello et sous-réseaux de back-end hello. cartes d’interface réseau dans le réseau de périmètre hello Hello communiquent directement tooand de hello Internet, avec hello NSG correspondante et périmètre de hello table de routage du réseau. NIC Hello connexion sous-réseaux de back-end toohello ont plus restreinte des tables de routage de sous-réseau principal hello et des groupes de sécurité réseau.
* **Fonctionnalités des appliances de sécurité :** appliances de sécurité hello déployés dans le réseau de périmètre hello généralement effectuer hello suivant de fonctionnalités :
  * Pare-feu : Application des règles de pare-feu ou des stratégies de contrôle d’accès pour les demandes entrantes hello.
  * Détection et la prévention des menaces : détecter et atténuer les attaques malveillantes de hello Internet.
  * Audit et journalisation : gestion de journaux d’audit et d’analyse détaillés.
  * Proxy inversé : hello entrants de redirection des demandes toohello correspondant sur les serveurs principaux. Cette redirection implique le mappage et traduction des adresses de destination hello sur les appareils frontal hello, en général, pare-feu, toohello les adresses de serveur principal.
  * Proxy avant : fournissant NAT et l’audit pour la communication initialisée à partir de toohello de réseau virtuel hello Internet.
  * Routeur : Transfert entre sous-réseaux le trafic entrant et à l’intérieur du réseau virtuel de hello.
  * Périphérique VPN : qui agit comme hello entre différents locaux pour les passerelles VPN intersite connectivité VPN entre le client sur des réseaux locaux et des réseaux virtuels Azure.
  * Serveur VPN : acceptation de clients VPN connectant tooAzure des réseaux virtuels.

> [!TIP]
> Conserver hello suivant deux groupes distincts : les personnes hello autorisé tooaccess hello périmètre réseau sécurité engrenage et hello personnes autorisées en tant qu’administrateurs de développement, de déploiement ou d’opérations de l’application. Conserver une distinction entre ces groupes permet une répartition des tâches et empêche qu’une seule personne contourne les contrôles de sécurité des applications et de sécurité réseau.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Toobe aux questions posée lors de la génération des limites du réseau
Dans cette section, sauf mention, le terme hello « réseaux » fait référence tooprivate Azure réseaux virtuels créés par un administrateur de l’abonnement. terme de Hello ne fait pas référence toohello les réseaux physiques sous-jacents dans Azure.

En outre, Azure les réseaux virtuels sont souvent utilisés tooextend traditionnel sur des réseaux locaux. Il est possible de tooincorporate site à site ou hybride ExpressRoute mise en réseau des solutions avec des architectures de réseau de périmètre. Ce lien hybride est un aspect important de la création de limites de sécurité réseau.

Hello trois questions suivantes sont critiques tooanswer lorsque vous créez un réseau avec un réseau de périmètre et plusieurs limites de sécurité.

#### <a name="1-how-many-boundaries-are-needed"></a>1) Combien de limites sont nécessaires ?
premier point de décision Hello est toodecide le nombre de limites de sécurité sont nécessaires dans un scénario donné :

* Une limite : un réseau de périmètre frontal hello, entre le réseau virtuel de hello et hello Internet.
* Deux frontières : un sur hello côté Internet du réseau de périmètre hello et l’autre entre le sous-réseau de réseau de périmètre hello et sous-réseaux principal hello hello réseaux virtuels Azure.
* Trois limites : un côté hello Internet du réseau de périmètre hello entre le réseau de périmètre hello et sous-réseaux de back-end et entre des sous-réseaux hello principal et le réseau local de hello.
* N limites : nombre variable. Selon les exigences de sécurité, il n’existe aucun toohello limiter le nombre de limites de sécurité qui peuvent être appliqués dans un réseau donné.

Hello nombre et le type des limites nécessaires varient selon risque tolérance de panne et hello scénario spécifique une société en cours d’implémentation. Cette décision est souvent prise conjointement par plusieurs groupes au sein d’une entreprise, parmi lesquels figurent souvent une équipe spécialiste des risques et de la conformité, une équipe chargée du réseau et de la plateforme et une équipe de développement des applications. Personnes possédant des connaissances de sécurité, les données hello impliquées et les technologies hello utilisés doit être un prononcer cette possibilités de sécurité appropriés de décision tooensure hello pour chaque implémentation.

> [!TIP]
> Utilisez hello plus petit nombre de limites qui répondent aux exigences de sécurité hello dans une situation donnée. Avec les limites de plus, opérations et la résolution des problèmes peuvent être plus difficile, ainsi hello gestion surcharge liées à la gestion hello plusieurs stratégies de limite dans le temps. Toutefois, des limites insuffisantes augmentent les risques. Solde de hello de recherche est critique.
>
>

![6]

Hello figure précédente montre une vue d’ensemble d’un réseau de limite de sécurité de trois. limites de Hello sont entre hello périmètre réseau et hello Internet, hello Azure frontaux et principaux des sous-réseaux privés et hello sous-réseau principal Azure et hello local d’entreprise.

#### <a name="2-where-are-hello-boundaries-located"></a>(2) dans lequel sont trouvent les limites de hello ?
Une fois que le nombre hello de limites est décidé, où tooimplement les est hello point de décision suivant. Il existe généralement trois possibilités :

* À l'aide d'un service Internet intermédiaire (par exemple, un pare-feu d'applications web cloud, non abordé dans ce document)
* À l'aide des fonctionnalités natives et/ou des appliances de réseau virtuel dans Azure
* À l’aide de périphériques physiques sur le réseau local de hello

Sur les réseaux Azure purement, options de hello sont des fonctionnalités natives de Azure (par exemple, les équilibreurs de charge Azure) ou les dispositifs de réseau virtuel à partir de hello riche écosystème de partenaires de Azure (par exemple, les pare-feu de Point de vérification).

Si une limite est nécessaire entre Azure et un réseau local, les dispositifs de sécurité hello peuvent résider sur chaque côté de la connexion de hello (ou les deux côtés). Par conséquent, une décision sur le matériel de sécurité tooplace hello emplacement.

Dans la figure précédente hello, hello Internet-à-réseau des limites de hello avant-back-end entièrement contenus dans Azure et doivent être des fonctionnalités natives de Azure ou équipements virtuels du réseau. Dispositifs de sécurité sur hello limite entre Azure (principal ou sous-réseau) et réseau d’entreprise de hello peut être soit sur hello côté Azure côté local de hello ou même une combinaison d’appareils sur les deux côtés. Il peut y avoir des avantages importants et option tooeither inconvénients à prendre en compte au sérieux.

Par exemple, à l’aide du matériel de sécurité physique existant sur hello local côté réseau a parti hello qu’aucune nouvelle ENGRENAGE n’est nécessaire. Une reconfiguration suffit. Hello, toutefois, inconvénient que tout le trafic doit revenir à partir de toobe de réseau local toohello Azure vu par engrenage de sécurité hello. Ainsi le trafic Azure vers Azure peut entraîner une latence importante et affectent l’expérience utilisateur et les performances d’application, si elle a été forcé précédent toohello local du réseau pour l’application de stratégie de sécurité.

#### <a name="3-how-are-hello-boundaries-implemented"></a>(3) l’implémentation des limites de hello ?
Chaque limite de sécurité auront probablement placer les exigences de capacité différente (par exemple, les ID et les règles de pare-feu sur hello côté Internet du réseau de périmètre hello, mais uniquement les ACL entre le réseau de périmètre hello et sous-réseau principal). Choisir le périphérique (ou combien d’appareils) dépend de toouse hello scénario et sécurité requises. Bonjour suivant la section, les exemples 1, 2 et 3 décrivent certaines options qui peuvent être utilisées. Vérification des fonctionnalités de réseau natif Azure hello et appareils hello disponibles dans Azure à partir de l’écosystème de partenaires hello montre toosolve disponibles du large éventail d’options hello pratiquement n’importe quel scénario.

Un autre point de décision d’implémentation de la clé est comment tooconnect hello sur le site réseau avec Azure. Utiliser hello passerelle virtuelle Azure ou un matériel de réseau virtuel ? Ces options sont décrites en détail dans hello après section (exemples 4, 5 et 6).

En outre, le trafic entre les réseaux virtuels dans Azure peut être nécessaire. Ces scénarios seront ajoutées dans hello futures.

Une fois que vous connaissez les réponses hello toohello précédent questions, hello [Fast Start](#fast-start) section peut vous aider à identifier les exemples les plus appropriées pour un scénario donné.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Exemples : Création de limites de sécurité avec les réseaux virtuels Azure
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Exemple 1, Build un toohelp de réseau de périmètre protéger les applications avec des groupes de sécurité réseau
[Sauvegarder le début de tooFast](#fast-start) | [détaillé des instructions pour cet exemple de génération][Example1]

[![7]][7]

#### <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, il existe un abonnement qui contient hello suivant des ressources :

- un seul groupe de ressources.
- un réseau virtuel avec deux sous-réseaux « FrontEnd » et « BackEnd »,
- Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux
- un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
- deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »),
- Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),
- Une adresse IP publique associée au serveur web d’application hello

Pour les scripts et un modèle Azure Resource Manager, consultez hello [des instructions de génération détaillées][Example1].

#### <a name="nsg-description"></a>Description du groupe de sécurité réseau
Dans cet exemple, un groupe NSG est créé, puis chargé avec six règles.

> [!TIP]
> En règle générale, vous devez créer vos règles « Autoriser » spécifiques en premier lieu, suivie de hello plus générique « Refuser » règles. Hello priorité détermine les règles sont évaluées en premier. Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées. Les règles de groupe de sécurité réseau peuvent être appliquées dans soit hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).
>
>

De façon déclarative, hello suivant les règles est généré pour le trafic entrant :

1. Le trafic DNS interne (port 53) est autorisé.
2. Le trafic RDP (port 3389) à partir d’Internet de hello tooany ordinateur virtuel est autorisé.
3. Le trafic HTTP (port 80) à partir du serveur de tooweb hello Internet (IIS01) est autorisé.
4. Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.
5. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.
6. Tout trafic (tous les ports) à partir du sous-réseau principal de hello sous-réseau frontal toohello est refusé.

Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent. Mais, étant donné que la règle 3 a une priorité plus élevée, elle est la seule à s’appliquer et la règle 5 n’entre pas en jeu. Par conséquent, demande HTTP de hello serait autorisée serveur web de toohello. Si ce trafic même a essayé de serveur de hello DNS01 tooreach, règle 5 (refuser) serait hello tooapply premier et le trafic de hello serait pas toopass toohello server. Règle 6 (refuser) blocs hello sous-réseau frontal de communiquer avec le sous-réseau principal de toohello (à l’exception du trafic autorisé dans les règles 1 et 4). Cet ensemble de règles protège le réseau de serveur principal hello au cas où un intrus compromet l’application hello web frontal hello. les intrus Hello sont peu réseau « protégé » accès toohello principal (uniquement tooresources exposée sur le serveur de AppVM01 hello).

Il existe une règle de trafic sortant par défaut qui autorise le trafic sortant toohello Internet. Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant. toolock vers le bas le trafic dans les deux directions, routage défini par l’utilisateur est requis (voir l’exemple 3).

#### <a name="conclusion"></a>Conclusion
Cet exemple est un moyen relativement simple et rapide d’isoler le sous-réseau principal hello le trafic entrant. Pour plus d’informations, consultez hello [des instructions de génération détaillées][Example1]. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre réseau avec des scripts PowerShell classiques.
* Comment toobuild ce périmètre réseau avec un modèle Azure Resource Manager.
* Des descriptions détaillées de chaque commande NSG.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic est autorisé ou refusé dans chaque couche.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Exemple 2 Build un toohelp de réseau de périmètre protéger des applications avec un pare-feu et des groupes de sécurité réseau
[Sauvegarder le début de tooFast](#fast-start) | [détaillé des instructions pour cet exemple de génération][Example2]

[![8]][8]

#### <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, il existe un abonnement qui contient hello suivant des ressources :

* un seul groupe de ressources.
* un réseau virtuel avec deux sous-réseaux « FrontEnd » et « BackEnd »,
* Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux
* Une appliance virtuelle de réseau, un pare-feu, dans ce cas connecté sous-réseau frontal de toohello
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »),
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),

Pour les scripts et un modèle Azure Resource Manager, consultez hello [des instructions de génération détaillées][Example2].

#### <a name="nsg-description"></a>Description du groupe de sécurité réseau
Dans cet exemple, un groupe NSG est créé, puis chargé avec six règles.

> [!TIP]
> En règle générale, vous devez créer vos règles « Autoriser » spécifiques en premier lieu, suivie de hello plus générique « Refuser » règles. Hello priorité détermine les règles sont évaluées en premier. Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées. Les règles de groupe de sécurité réseau peuvent être appliquées dans soit hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).
>
>

De façon déclarative, hello suivant les règles est généré pour le trafic entrant :

1. Le trafic DNS interne (port 53) est autorisé.
2. Le trafic RDP (port 3389) à partir d’Internet de hello tooany ordinateur virtuel est autorisé.
3. N’importe quel trafic (tous les ports) toohello réseau virtuel appliance Internet (pare-feu) est autorisée.
4. Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.
5. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.
6. Tout trafic (tous les ports) à partir du sous-réseau principal de hello sous-réseau frontal toohello est refusé.

Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante de pare-feu toohello hello, règles 3 (autoriser) et 5 (refuser) s’appliquent. Mais, étant donné que la règle 3 a une priorité plus élevée, elle est la seule à s’appliquer et la règle 5 n’entre pas en jeu. Par conséquent, la demande de hello HTTP serait autorisée toohello pare-feu. Si ce même trafic essayait serveur hello IIS01 de tooreach, même s’il est sur le sous-réseau frontal de hello, la règle 5 (refuser) s’appliquent, et le trafic de hello serait pas toopass toohello server. Règle 6 (refuser) blocs hello sous-réseau frontal de communiquer avec le sous-réseau principal de toohello (à l’exception du trafic autorisé dans les règles 1 et 4). Cet ensemble de règles protège le réseau de serveur principal hello au cas où un intrus compromet l’application hello web frontal hello. les intrus Hello sont peu réseau « protégé » accès toohello principal (uniquement tooresources exposée sur le serveur de AppVM01 hello).

Il existe une règle de trafic sortant par défaut qui autorise le trafic sortant toohello Internet. Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant. toolock vers le bas le trafic dans les deux directions, routage défini par l’utilisateur est requis (voir l’exemple 3).

#### <a name="firewall-rule-description"></a>Description de la règle de pare-feu
Sur le pare-feu hello, règles de transfert doivent être créé. Règle de cet exemple uniquement le trafic Internet-limite des itinéraires toohello pare-feu et les puis serveur toohello web, qu’un seul transfert traduction d’adresses réseau (NAT) est nécessaire.

règle de transfert de Hello accepte n’importe quelle adresse source entrant qui rencontre pare-feu hello lors de la tentative tooreach HTTP (port 80 ou 443 pour HTTPS). Il a envoyé en dehors de l’interface locale du pare-feu hello et rediriger le serveur web toohello hello adresse IP de 10.0.1.5.

#### <a name="conclusion"></a>Conclusion
Cet exemple est une méthode relativement simple de protection de votre application avec un pare-feu et isoler le sous-réseau principal hello le trafic entrant. Pour plus d’informations, consultez hello [des instructions de génération détaillées][Example2]. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre réseau avec des scripts PowerShell classiques.
* Comment toobuild cet exemple avec un modèle Azure Resource Manager.
* Descriptions détaillées de chaque commande NSG et règle de pare-feu.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic est autorisé ou refusé dans chaque couche.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Exemple 3 Build un toohelp de réseau de périmètre protéger les réseaux avec un pare-feu et UDR et un groupe de sécurité réseau
[Sauvegarder le début de tooFast](#fast-start) | [détaillé des instructions pour cet exemple de génération][Example3]

[![9]][9]

#### <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, il existe un abonnement qui contient hello suivant des ressources :

* un seul groupe de ressources.
* Un réseau virtuel avec trois sous-réseaux : « SecNet », « FrontEnd » et « BackEnd »
* Un réseau virtuel, un pare-feu, dans ce cas connecté toohello SecNet sous-réseau
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »),
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),

Pour les scripts et un modèle Azure Resource Manager, consultez hello [des instructions de génération détaillées][Example3].

#### <a name="udr-description"></a>Description du routage défini par l’utilisateur
Par défaut, hello suivant les itinéraires du système est définie en tant que :

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hello VNETLocal est toujours un ou plusieurs préfixes d’adresse définie qui composent le réseau virtuel de hello pour ce réseau spécifique (autrement dit, il change de réseau toovirtual de réseau virtuel, selon la façon dont chaque réseau virtuel spécifique est définie). les itinéraires système restantes Hello sont statiques et par défaut indiquée dans le tableau de hello.

Dans cet exemple, deux tables de routage sont créés, un pour les sous-réseaux frontaux et principaux hello. Chaque table est chargée avec des itinéraires statiques appropriés pour hello donné de sous-réseau. Dans cet exemple, chaque table possède trois itinéraires qui dirige tout le trafic (0.0.0.0/0) via le pare-feu hello (tronçon suivant = l’adresse IP virtuelle de matériel) :

1. Le trafic de sous-réseau local avec aucun saut suivant défini tooallow sous-réseau local toobypass hello pare-feu.
2. Le trafic réseau virtuel avec un tronçon suivant défini en tant que pare-feu. Ce saut suivant remplace la règle par défaut hello qui permet de tooroute le trafic de réseau virtuel local directement.
3. Tous les autres le trafic (0/0) avec un tronçon suivant défini en tant que les pare-feu hello.

> [!TIP]
> N’ayant ne pas d’entrée de sous-réseau local hello dans hello UDR sauts sous-réseau local communications.
>
> * Dans notre exemple, 10.0.1.0/24 pointant tooVNETLocal est critique ! Sans lui, paquet en laissant hello serveur Web (10.0.1.4) destinés aux tooanother serveur local (par exemple) 10.0.1.25 échouera car ils seront envoyés toohello NVA. Hello NVA il enverra toohello sous-réseau et sous-réseau de hello il renverra toohello NVA dans une boucle infinie.
> * risque de Hello d’une boucle de routage est généralement plus élevés sur les appareils avec plusieurs cartes réseau qui sont les sous-réseaux connectés tooseparate, ce qui est souvent d’équipements de local traditionnel.
>
>

Une fois que les tables de routage hello sont créés, ils doivent être liée tootheir sous-réseaux. Hello sous-réseau frontal table de routage, une fois créé et lié toohello sous-réseau, ressemble à ce résultat :

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR peut désormais être sous-réseau de passerelle toohello appliquée sur le hello ExpressRoute circuit est connecté.
>
> Exemples de tooenable périmètre de votre réseau avec ExpressRoute ou de mise en réseau de site à site sont présentés dans les exemples 3 et 4.
>
>

#### <a name="ip-forwarding-description"></a>Description du transfert IP
Le transfert IP est un tooUDR de fonctionnalité d’accompagnement. Le transfert IP est un paramètre sur une appliance virtuelle qui lui permet de tooreceive le trafic adressé ne sont pas spécifiquement toohello appliance et puis transférer cette destination finale tooits de trafic.

Par exemple, si AppVM01 effectue une demande adressée au serveur DNS01 toohello, UDR achemine ce pare-feu toohello. Avec le transfert IP activé, trafic hello pour la destination de DNS01 hello (10.0.2.4) est accepté par l’application hello (10.0.0.4), puis transféré tooits sa destination finale (10.0.2.4). Sans le transfert IP activée sur le pare-feu hello, le trafic ne serait pas accepté par appliance de hello même si la table d’itinéraires hello a pare-feu hello en tant que tronçon suivant de hello. toouse une appliance virtuelle, il est critique tooremember tooenable avec UDR de transfert.

#### <a name="nsg-description"></a>Description du groupe de sécurité réseau
Dans cet exemple, un groupe NSG est créé, puis chargé avec une seule règle. Ce groupe est ensuite lié uniquement toohello frontaux et principaux sous-réseaux (pas hello SecNet). Déclarative hello règle est en cours de génération :

* Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (tous les sous-réseaux) est refusé.

Bien que dans cet exemple, on utilise des NSG, son principal objectif est celui d’une couche secondaire de défense contre les erreurs de configuration manuelle. Hello vise tooblock tout le trafic entrant à partir de hello Internet tooeither hello sous-réseaux frontaux ou principaux. Flux uniquement le trafic via le pare-feu hello SecNet sous-réseau toohello (et, le cas échéant, sur des sous-réseaux toohello frontal ou principal). De plus, avec des règles UDR hello en place, tout le trafic qui faites-en hello frontaux ou principaux sous-réseaux serait dirigé out toohello pare-feu (Merci tooUDR). pare-feu de Hello verriez ce trafic comme flux asymétrique et tomberaient le trafic sortant de hello. Par conséquent il existe trois couches de sécurité protégeant des sous-réseaux hello :

* Aucune adresse IP publique sur une carte d’interface réseau FrontEnd ou BackEnd.
* Groupes de sécurité réseau qui empêche le trafic à partir de hello Internet.
* Hello suppression asymétrique le trafic de pare-feu.

Un point intéressant concernant hello NSG dans cet exemple est qu’il contient uniquement une seule règle, ce qui est toodeny Internet trafic toohello réseau virtuel entier, y compris le sous-réseau de sécurité hello. Toutefois, étant donné que hello que NSG n’est lié toohello frontaux et principaux sous-réseaux, règle de hello n’est pas traité sur le trafic entrant sous-réseau de sécurité toohello. Par conséquent, le trafic acheminé sous-réseau de sécurité toohello.

#### <a name="firewall-rules"></a>Règles de pare-feu
Sur le pare-feu hello, règles de transfert doivent être créé. Étant donné que les pare-feu hello sont de blocage ou transfert tout entrant, sortant et le trafic réseau intra-virtuel, de règles de pare-feu sont nécessaires. En outre, tout le trafic entrant atteint adresse IP publique de hello Service de sécurité (sur des ports différents), toobe traitée par le pare-feu hello. La meilleure pratique consiste toodiagram des flux logiques hello avant de configurer les sous-réseaux hello et règles de pare-feu, tooavoid reprendre ultérieurement. Bonjour figure suivante est une vue logique de règles de pare-feu hello pour cet exemple :

![10]

> [!NOTE]
> En fonction de hello Qu'appliance virtuelle de réseau utilisé, les ports de gestion hello varient. Dans cet exemple, il est fait référence à un pare-feu Barracuda NextGen Firewall utilisant les ports 22, 801 et 807. Consultez hello appliance fournisseur documentation toofind hello exacte ports utilisés pour la gestion de périphérique hello utilisé.
>
>

#### <a name="firewall-rules-description"></a>Description des règles de pare-feu
Bonjour précédant diagramme logique, sous-réseau de sécurité hello n’est pas affiché, car le pare-feu de hello est la seule ressource de hello sur ce sous-réseau. diagramme de Hello affiche les règles de pare-feu hello et comment ils logiquement autoriser ou refuser des flux de trafic, pas hello routé chemin d’accès réel. En outre, des ports externes hello sélectionnés pour hello le trafic RDP sont des ports sont plus élevées (8014 – 8026) et ont été tooloosely sélectionné s’alignent hello a deux octets de l’adresse IP locale de hello pour faciliter la lisibilité (par exemple, l’adresse du serveur local 10.0.1.4 est associé avec le port externe 8014). Cependant, tous les ports supérieurs non conflictuels peuvent être utilisés.

Pour cet exemple, nous avons besoin de sept types de règles :

* Règles externes (pour le trafic entrant) :
  1. Règle de pare-feu de gestion : règle de redirection de cette application permet le trafic toopass toohello les ports de gestion de l’appliance virtuelle de réseau hello.
  2. Règles RDP (pour chaque serveur Windows) : ces quatre règles (une pour chaque serveur) autorisent la gestion des hello des serveurs individuels via RDP. quatre règles RDP Hello peuvent également être réduits dans une seule règle, selon les fonctions hello de l’appliance virtuelle sur le réseau hello utilisé.
  3. Règles de trafic d’application : il y a deux de ces règles, hello tout d’abord pour le trafic web frontal de hello et hello seconde pour le trafic principal de hello (par exemple, niveau toodata web server). configuration Hello de ces règles varie selon l’architecture en réseau hello (où sont placés vos serveurs) et flux de trafic (le trafic hello direction du flux, et quels ports sont utilisés).
     * règle de première Hello permet de serveur d’applications hello application réelle du trafic tooreach hello. Tandis que hello autres règles de sécurité et de gestion, règles de trafic d’application sont ce que permettent tooaccess d’utilisateurs ou des services externes aux applications de hello. Pour cet exemple, il n’y a qu’un serveur web sur le port 80. Par conséquent, une seule application règle de pare-feu redirige le trafic entrant toohello adresse IP externe, interne adresse IP des serveurs toohello web. session de trafic Hello redirigé se traduirait via NAT toohello interne au serveur.
     * règle de seconde Hello est hello principal règle tooallow hello web tootalk toohello AppVM01 serveur (mais pas AppVM02) via n’importe quel port.
* Règles internes (pour le trafic intra-réseau virtuel)
  1. Règle de tooInternet sortantes : cette règle autorise le trafic de n’importe quel réseau toopass toohello sélectionné réseaux. Cette règle est généralement une règle par défaut déjà présent sur le pare-feu hello, mais dans un état désactivé. Pour cet exemple, cette règle doit être activée.
  2. Règle de DNS : cette règle permet uniquement DNS (port 53) le trafic toopass toohello serveurDNS. Pour cet environnement, la plupart du trafic à partir de hello frontal toohello back-end est bloqué. Cette règle autorise spécifiquement le DNS à partir de n'importe quel sous-réseau local.
  3. Règle de toosubnet de sous-réseau : cette règle est tooallow n’importe quel serveur hello sous-réseau principal tooconnect tooany serveur sur le sous-réseau frontal de hello (mais pas les hello inverse).
* Règle de prévention de défaillance (pour le trafic qui ne correspond pas hello précédente) :
  1. Refuser toutes les règles de trafic : cette règle de refus doit toujours être règle finale de hello (en termes de priorité), et par conséquent si un flux de trafic échoue toomatch des hello précédant les règles qu’il est supprimé par cette règle. Cette règle est une règle par défaut et est généralement mise en place et active. Aucune modification n’est généralement nécessaire toothis règle.

> [!TIP]
> Sur hello n’importe quel port de trafic application deuxième règle, toosimplify cet exemple, est autorisé. Dans un scénario réel, les plages de port et l’adresse de la plus spécifiques hello doivent être surface d’attaque hello tooreduce utilisés de cette règle.
>
>

Une fois que les règles précédentes hello sont créés, il est important priorité hello tooreview chacun le trafic tooensure de règle est autorisée ou refusée comme vous le souhaitez. Pour cet exemple, les règles de hello sont dans l’ordre de priorité.

#### <a name="conclusion"></a>Conclusion
Cet exemple est plus complexe, mais un moyen de protection et l’isolement réseau de hello que hello exemples précédents de terminer. (Exemple 2 protège uniquement l’application hello et exemple 1 isole simplement les sous-réseaux). Cette conception permet de surveiller le trafic dans les deux directions et protège non seulement les serveurs d’application entrants hello mais applique la stratégie de sécurité réseau pour tous les serveurs sur ce réseau. En outre, en fonction de l’application hello utilisée, le trafic complète l’audit et reconnaissance peuvent être obtenus. Pour plus d’informations, consultez hello [des instructions de génération détaillées][Example3]. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre exemple réseau avec des scripts PowerShell classiques.
* Comment toobuild cet exemple avec un modèle Azure Resource Manager.
* Des descriptions détaillées de chaque UDR, commande NSG et règle de pare-feu.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic est autorisé ou refusé dans chaque couche.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Exemple 4 : Ajouter une connexion hybride avec un réseau VPN d’appliance virtuelle de site à site
[Sauvegarder tooFast début](#fast-start) | Build obtenir des instructions détaillées disponible prochainement

[![11]][11]

#### <a name="environment-description"></a>Description de l’environnement
Tooany des types de réseau de périmètre hello décrits dans les exemples 1, 2 ou 3 peut être ajouté à un réseau hybride à l’aide d’une appliance virtuelle de réseau (NVA).

Comme indiqué dans la figure précédente hello, une connexion VPN sur hello Internet (site à site) est utilisé tooconnect un tooan de réseau local sur un réseau virtuel Azure via une NVA.

> [!NOTE]
> Si vous utilisez ExpressRoute avec option d’homologation publique Azure hello activée, un itinéraire statique doit être créé. Cet itinéraire statique doit acheminer toohello adresse IP du VPN NVA votre Internet d’entreprise et non par l’intermédiaire de hello connexion ExpressRoute. session VPN hello peut provoquer des problèmes Hello NAT requis sur hello ExpressRoute l’homologation publique Azure une option.
>
>

Une fois que hello VPN est en place, hello NVA devient concentrateur central de hello pour tous les sous-réseaux et les réseaux. règles de transfert de pare-feu Hello déterminent les flux sont autorisées, le trafic sont traduites via NAT, sont redirigés ou sont supprimées (même pour les flux de trafic entre le réseau local de hello et Azure).

Flux de trafic doivent être envisagés avec précaution, car ils peuvent être optimisées ou détérioré par ce modèle de conception, hello spécifique en fonction des cas d’usage.

À l’aide d’environnement hello créé dans l’exemple 3 et ajout d’une connexion de réseau hybride VPN de site à site, puis génère hello suivant modèle :

[![12]][12]

Hello local routeur ou tout autre périphérique réseau qui est compatible avec votre NVA pour VPN, serait client VPN de hello. Ce périphérique physique est responsable de l’initialisation et de maintenir la connexion VPN de hello avec votre NVA.

Logiquement toohello NVA, réseau de hello ressemble à quatre distinct « zones de sécurité » avec des règles de hello sur en cours de NVA hello directeur principal de hello du trafic entre ces zones :

![13]

#### <a name="conclusion"></a>Conclusion
Ajout de Hello d’un tooan de connexion de réseau de site à site VPN hybride réseau virtuel Azure peut étendre hello sur réseau local à Azure de manière sécurisée. À l’aide d’une connexion VPN, le trafic est chiffré et achemine via hello Internet. Hello NVA dans cet exemple fournit un emplacement central de tooenforce et gérer la stratégie de sécurité hello. Pour plus d’informations, consultez hello détaillée (à venir) d’instructions de génération. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre exemple réseau avec des scripts PowerShell.
* Comment toobuild cet exemple avec un modèle Azure Resource Manager.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic circule dans cette conception.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Exemple 5 : Ajouter une connexion hybride avec une passerelle VPN Azure de site à site
[Sauvegarder tooFast début](#fast-start) | Build obtenir des instructions détaillées disponible prochainement

[![14]][14]

#### <a name="environment-description"></a>Description de l’environnement
Type de réseau de périmètre tooeither décrit dans les exemples 1 ou 2 peut être ajouté à un réseau hybride à l’aide d’une passerelle VPN Azure.

Comme indiqué dans hello précédant figure, une connexion VPN sur hello Internet (site à site) est utilisé tooconnect un tooan de réseau local sur un réseau virtuel Azure via une passerelle VPN Azure.

> [!NOTE]
> Si vous utilisez ExpressRoute avec option d’homologation publique Azure hello activée, un itinéraire statique doit être créé. Cet itinéraire statique doit acheminer toohello adresse IP du VPN NVA votre Internet d’entreprise et non par l’intermédiaire de hello ExpressRoute WAN. session VPN hello peut provoquer des problèmes Hello NAT requis sur hello ExpressRoute l’homologation publique Azure une option.
>
>

Hello figure suivante illustre hello deux bords de réseau dans cet exemple. Sur les bords première hello hello NVA et des groupes de sécurité réseau contrôlent le flux de trafic pour les réseaux Azure au sein et entre Azure hello Internet. Hello deuxième arête est la passerelle VPN Azure hello, qui est un bord de réseau distinct et isolé entre locaux et Azure.

Flux de trafic doivent être envisagés avec précaution, car ils peuvent être optimisées ou détérioré par ce modèle de conception, hello spécifique en fonction des cas d’usage.

À l’aide d’environnement hello créé dans l’exemple 1 et ajout d’une connexion de réseau hybride VPN de site à site, puis génère hello suivant modèle :

[![15]][15]

#### <a name="conclusion"></a>Conclusion
Ajout de Hello d’un tooan de connexion de réseau de site à site VPN hybride réseau virtuel Azure peut étendre hello sur réseau local à Azure de manière sécurisée. À l’aide de la passerelle VPN Azure native de hello, votre trafic IPSec chiffré et achemine via hello Internet. En outre, à l’aide de la passerelle VPN Azure de hello peut fournir une option économique (aucune licence supplémentaire de coût comme avec les tiers NVAs). Cette option est plus économique dans l’exemple 1, où aucune appliance virtuelle réseau n’est utilisée. Pour plus d’informations, consultez hello détaillée (à venir) d’instructions de génération. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre exemple réseau avec des scripts PowerShell.
* Comment toobuild cet exemple avec un modèle Azure Resource Manager.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic circule dans cette conception.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Exemple 6 : Ajouter une connexion hybride avec ExpressRoute
[Sauvegarder tooFast début](#fast-start) | Build obtenir des instructions détaillées disponible prochainement

[![16]][16]

#### <a name="environment-description"></a>Description de l’environnement
Mise en réseau hybride à l’aide d’une ExpressRoute connexion d’homologation privée peut être ajouté un type de réseau de périmètre tooeither décrit dans les exemples 1 ou 2.

Comme indiqué dans hello précédant figure, l’homologation privée ExpressRoute fournit une connexion directe entre votre réseau local et le hello réseau virtuel Azure. Le trafic passe uniquement réseau de fournisseur de service hello et réseau de Microsoft Azure hello, jamais toucher hello Internet.

> [!TIP]
> Le trafic réseau d’entreprise à l’aide d’ExpressRoute conserve les désactiver hello Internet. Il prend également en charge les accords de niveau de service de votre fournisseur ExpressRoute. Hello passerelle Azure peut passer des Gbits/s too10 grâce à ExpressRoute, alors que le site à site VPN débit maximal de passerelle Azure hello est 200 Mbits/s.
>
>

Comme indiqué dans hello suivant schéma, avec cette hello option environnement a maintenant deux bords de réseau. Hello NVA et le groupe de sécurité réseau du trafic flux de contrôle pour les réseaux Azure au sein et entre Azure et hello Internet, alors que la passerelle de hello est un bord de réseau distinct et isolé entre locaux et Azure.

Flux de trafic doivent être envisagés avec précaution, car ils peuvent être optimisées ou détérioré par ce modèle de conception, hello spécifique en fonction des cas d’usage.

À l’aide d’environnement hello créé dans l’exemple 1, puis en ajoutant une connexion de réseau hybride ExpressRoute, génère hello suivant modèle :

[![17]][17]

#### <a name="conclusion"></a>Conclusion
Ajout de Hello d’une connexion de réseau privé de ExpressRoute homologation peut étendre des réseau local de hello dans Azure dans une latence sécurisée, inférieure, effectuer plus de manière. À l’aide de hello natif passerelle Azure, comme dans cet exemple, fournit également une option économique (non supplémentaire relatifs aux licences comme avec les tiers NVAs). Pour plus d’informations, consultez hello détaillée (à venir) d’instructions de génération. Vous trouverez les instructions suivantes :

* Comment toobuild ce périmètre exemple réseau avec des scripts PowerShell.
* Comment toobuild cet exemple avec un modèle Azure Resource Manager.
* Des scénarios de flux de trafic détaillés, montrant comment le trafic circule dans cette conception.

## <a name="references"></a>Références
### <a name="helpful-websites-and-documentation"></a>Sites web et documentation utiles
* Accès à Azure avec Azure Resource Manager :
* Accès à Azure avec PowerShell : [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Documentation relative à la mise en réseau virtuelle : [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Documentation relative aux groupes de sécurité réseau : [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Documentation relative au routage défini par l’utilisateur : [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Passerelles virtuelles Azure : [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* VPN de site à site : [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Documentation d’ExpressRoute (être toocheck que les sections « Getting Started » et « Comment » hello) : [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Organigramme des options de sécurité"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Fonctionnalités de sécurité Azure"
[3]: ./media/best-practices-network-security/dmzcorporate.png "Une zone DMZ dans un réseau d’entreprise"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Architecture de sécurité Azure"
[5]: ./media/best-practices-network-security/dmzazure.png "Une zone DMZ dans un réseau virtuel Azure"
[6]: ./media/best-practices-network-security/dmzhybrid.png "Réseau hybride avec trois limites de sécurité"
[7]: ./media/best-practices-network-security/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"
[8]: ./media/best-practices-network-security/example2design.png "Zone DMZ entrante avec NVA et NSG"
[9]: ./media/best-practices-network-security/example3design.png "Zone DMZ bidirectionnelle avec NVA, NSG et UDR"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "affichage logique de règles de pare-feu de hello"
[11]: ./media/best-practices-network-security/example3designoptions.png "Zone DMZ avec réseau hybride connecté à une NVA"
[12]: ./media/best-practices-network-security/example4designs2s.png "Zone DMZ avec NVA connectée à l’aide d’un VPN de site à site"
[13]: ./media/best-practices-network-security/example4networklogical.png "Réseau logique du point de vue de la NVA"
[14]: ./media/best-practices-network-security/example5designoptions.png "Zone DMZ avec réseau hybride de site à site connecté à une passerelle Azure"
[15]: ./media/best-practices-network-security/example5designs2s.png "Zone DMZ avec passerelle Azure utilisant un VPN de site à site"
[16]: ./media/best-practices-network-security/example6designoptions.png "Zone DMZ avec réseau hybride ExpressRoute connecté à une passerelle Azure"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Zone DMZ avec passerelle Azure utilisant une connexion ExpressRoute"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
