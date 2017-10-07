---
title: "aaaMicrosoft centre de données virtuel de Azure | Documents Microsoft"
description: "Découvrez comment toobuild votre virtuelles du centre de données dans Azure"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Centre de données virtuel Microsoft Azure
**Microsoft Azure** : accélérez votre migration, faites des économies et intégrez des applications et des données locales

## <a name="overview"></a>Vue d'ensemble
Migration tooAzure des applications sur site, même sans modification importante (une approche appelée « de courbes d’élévation et MAJ »), offre aux organisations hello une infrastructure sécurisée et rentable. Toutefois, toomake hello plus de souplesse de hello possible pour le cloud computing, les entreprises doivent évoluer leur avantage de tootake des architectures de capacités de Azure. Microsoft Azure offre des services et une infrastructure hyperscale, des capacités et une fiabilité de qualité professionnelle, ainsi que de nombreuses options de connectivité hybride. Les clients peuvent choisir tooaccess ces cloud services via hello Internet ou avec Azure ExpressRoute, qui fournit une connectivité de réseau privé. plateforme de Microsoft Azure Hello permet clients tooseamlessly étendre leur infrastructure en nuage de hello et générer des architectures multicouches. En outre, les partenaires Microsoft fournissent des fonctionnalités améliorées en offrant des services de sécurité et des équipements virtuels qui sont optimisés toorun dans Azure.

Cet article fournit une vue d’ensemble des modèles et les conceptions qui peuvent être utilisé toosolve hello préoccupations architecturales de mise à l’échelle, de performances et de sécurité en matière de déplacement en masse toohello cloud sont confrontés à de nombreux clients. Vue d’ensemble de comment toofit différents rôles informatiques d’organisation dans la gestion de hello et gouvernance de système de hello est également indiqué, à optimiser les coûts et en matière de toosecurity d’accentuation.

## <a name="what-is-a-virtual-data-center"></a>Qu’est-ce qu’un centre de données virtuel ?
Bonjour solutions de cloud computing premiers jours, ont été conçus toohost unique relativement isolé, applications, dans le spectre de public hello. Cette approche a donné de bons résultats pendant quelques années. Toutefois, solutions est devenu évident que les avantages de hello du cloud et plusieurs charges de travail à grande échelle ont été hébergés sur le cloud de hello, sécurité, fiabilité, les performances, d’adressage et coût préoccupations des déploiements dans un ou plusieurs régions est devenu essentielles tout au long de hello cycle de vie du service de cloud hello.

Hello cloud déploiement diagramme suivant présente quelques exemples de failles de sécurité (zone rouge) et d’espace pour les équipements de l’optimisation réseau virtuel entre les charges de travail (jaune).

[![0]][0]

Hello centre de données virtuel (vDC) est née de cette nécessité de mise à l’échelle de charges de travail toosupport enterprise et hello doivent toodeal problèmes hello a introduit la prise en charge des applications à grande échelle dans un cloud public hello.

Un vDC n’est pas simplement hello des charges de travail dans le cloud de hello, mais également hello réseau, sécurité, gestion et l’infrastructure (par exemple, DNS et Services Active Directory). Il fournit généralement également un tooan arrière connexion privée locale centre de données ou de réseau. Les charges de travail plus déplacement tooAzure, il est important toothink sur hello prise en charge d’infrastructure et les objets placés dans ces charges de travail. Envisager soigneusement structuration des ressources peut éviter la prolifération de hello de centaines de « îlots de charge de travail » qui doivent être gérés séparément avec flux de données indépendant, les modèles de sécurité et les problèmes de conformité.

Un centre de données virtuel constitue essentiellement une série d’entités distinctes mais associées qui présentent une infrastructure, des fonctionnalités et des capacités sous-jacentes communes. En consultant vos charges de travail comme un vDC intégré, vous pouvez bénéficier de réduction des coûts d’échéance tooeconomies d’échelle, une sécurité optimisée via le composant de données et flux de centralisation, ainsi que des opérations plus faciles, la gestion et des audits de conformité.

> [!NOTE]
> Il est important soit de toounderstand qui hello vDC **pas** un produit Azure discrète, mais la combinaison hello diverses fonctionnalités et capacités trop répondent à vos besoins exacts. vDC est un moyen de vous réfléchissez à vos charges de travail et les toomaximize d’utilisation d’Azure, vos ressources et les capacités dans le cloud de hello. Hello virtuel contrôleur de domaine est par conséquent une approche modulaire sur la façon de toobuild les services informatiques Bonjour Azure, en respectant les rôles d’organisation et des responsabilités.

Hello vDC peut aider les entreprises les charges de travail et les applications dans Azure pourquoi les scénarios suivants :

-   Hébergement de plusieurs charges de travail associées
-   Migration des charges de travail à partir d’un tooAzure d’environnement sur site
-   Implémentation d’exigences de gestion partagée ou centralisée de la sécurité et des accès dans l’ensemble des charges de travail
-   Combinaison appropriée de DevOps et d’un service informatique centralisé pour une grande entreprise

Hello avantages hello de clé toounlock de vDC, est une topologie centralisée (hub et spoke) avec un mélange de fonctionnalités Azure : [réseau virtuel Azure][VNet], [NSG] [ NSG], [Réseau virtuel d’homologation][VNetPeering], [itinéraires définis par l’utilisateur (UDR)][UDR]et l’identité Azure avec [ Contrôle d’accès de Base de rôle (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>Qui doit utiliser un centre de données virtuel ?
Tout client Azure qui doit toomove plus de deux charges de travail dans Azure peut tirer parti de réfléchir à l’aide des ressources communes. Selon l’ordre de grandeur hello, des applications même peuvent bénéficier de l’utilisation de modèles de hello et composants utilisés toobuild un vDC.

Si votre organisation possède une centralisé, réseau, de la sécurité et/ou de l’équipe/service de conformité, un vDC peut aider à appliquer les points de la stratégie, la répartition des droits et garantir l’uniformité de hello sous-jacent de composants communs en donnant autant les équipes d’application liberté et contrôle est approprié pour vos besoins.

Les organisations qui cherchent à tooDevOps peuvent utiliser les concepts de vDC hello tooprovide autorisé poches de ressources Azure et vérifiez qu’ils ont un contrôle total au sein de ce groupe (abonnement ou ressource dans un abonnement commun), mais le réseau de hello et limites de sécurité restent conformes comme défini par une stratégie centralisée dans un concentrateur réseau virtuel et le groupe de ressources.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Considérations en matière d’implémentation d’un centre de données virtuel
Lorsque vous concevez un vDC, il existe plusieurs problèmes pivot tooconsider :

-   Services d’identité et d’annuaire
-   Infrastructure de sécurité
-   Cloud toohello de connectivité
-   Connexion au sein du cloud de hello

##### <a name="identity-and-directory-service"></a>*Services d’identité et d’annuaire*
Services d’annuaire et identité sont un aspect clé de données de tous les postes de charge, à la fois localement et dans le cloud de hello. L’identité est aspects tooall connexes d’accès et autorisation tooservices dans hello vDC. toohelp vous assurer que seuls les utilisateurs autorisés et processus accéder à votre compte Azure et ressources, Azure utilise plusieurs types d’informations d’identification pour l’authentification. Notamment les mots de passe (tooaccess hello compte Azure), les clés de chiffrement, les signatures numériques et les certificats. [*Azure Multi-Factor Authentication* (MFA)][MFA] est une couche de sécurité supplémentaire pour l’accès aux services Azure. Azure MFA fournit une authentification forte avec un éventail d’options de vérification simple, un appel téléphonique, message texte ou notification d’application mobile et permettent aux clients de méthode de hello toochoose qu’ils préfèrent.

Les grandes entreprises doit toodefine un processus de gestion d’identité qui décrit la gestion hello des identités individuelles, leur authentification, d’autorisation, rôles et des privilèges dans ou entre hello vDC. objectifs Hello de ce processus doivent être tooincrease sécurité et la productivité tout en diminuant le coût, l’arrêt et les tâches manuelles répétitives.

Les entreprises/organisations peuvent nécessiter une combinaison de services complexe pour différents cœurs de métier, et les employés assument fréquemment plusieurs rôles lorsqu’ils sont impliqués dans divers projets. Un vDC nécessite une bonne coopération entre différentes équipes, chacun avec des définitions de rôle spécifique, les systèmes tooget en cours d’exécution avec une bonne gouvernance. matrice Hello des responsabilités, des accès et des droits peut être extrêmement complexe. La gestion des identités dans le vDC est implémentée par le biais d’[*Azure Active Directory* (AAD)][AAD] et du contrôle d’accès en fonction du rôle (RBAC).

Un service d’annuaire est une infrastructure d’informations partagée pour la localisation, la gestion, l’administration et l’organisation des éléments et ressources réseau utilisés quotidiennement. Ces ressources peuvent inclure des volumes, des dossiers, des fichiers, des imprimantes, des utilisateurs, des groupes, des appareils et d’autres objets. Chaque ressource hello réseau est considéré comme un objet par le serveur d’annuaire hello. Les informations concernant une ressource sont stockées sous la forme d’une collection d’attributs associée à cette ressource ou à cet objet.

Tous les services métiers en ligne Microsoft reposent sur Azure Active Directory (AAD) pour la connexion et les autres besoins en matière d’identification. Azure Active Directory est une solution cloud complète et hautement disponible de gestion des identités et des accès qui associe des services d'annuaire principaux, une gouvernance avancée des identités et la gestion de l'accès aux applications. AAD peut être intégré à Active Directory en local tooenable unique authentification pour tous les basée sur le cloud et hébergé localement les applications (sur site). attributs d’utilisateur Hello d’Active Directory locale peuvent être automatiquement synchronisée tooAAD.

Un administrateur global est tooassign requis pas toutes les autorisations dans un vDC. À la place chaque département spécifique (ou un groupe d’utilisateurs ou services dans le Service d’annuaire de hello) peut avoir toomanage requis des autorisations de hello leurs propres ressources au sein d’un vDC. La structuration des autorisations doit être équilibrée. En effet, un nombre d’autorisations excessif risque de compromettre les performances, tandis que des autorisations insuffisantes ou trop flexibles sont susceptibles d’accroître les risques pour la sécurité. Azure contrôle d’accès en fonction du rôle (RBAC) vous aide à tooaddress ce problème, en offrant la gestion de l’accès affinée pour les ressources d’informations.

##### <a name="security-infrastructure"></a>*Infrastructure de sécurité*
Infrastructure de sécurité, dans le contexte de hello d’un vDC, est principalement la segmentation de trafic en hello du segment de réseau virtuel spécifique, et vDC flux des toocontrol entrante et tout au long de hello vDC toohello connexes. Azure repose sur une architecture mutualisée qui empêche le trafic non autorisé et accidentel entre les déploiements, par le biais de l’isolement du réseau virtuel (VNet), d’ACL, d’équilibreurs de charge et de filtres IP, ainsi que de stratégies de flux de trafic. La traduction d’adresses réseau (NAT) sépare le trafic réseau interne du trafic externe.

Hello tissu Azure alloue des ressources d’infrastructure tootenant les charges de travail et gère les communications tooand à partir de machines virtuelles (VM). Hello hyperviseur Azure met en œuvre la mémoire et le processus de séparation entre les machines virtuelles et en toute sécurité aux clients d’itinéraires réseau trafic tooguest du système d’exploitation.

##### <a name="connectivity-toohello-cloud"></a>*Cloud toohello de connectivité*
Hello vDC requiert une connectivité avec des réseaux externes toooffer services toocustomers, partenaires et/ou aux utilisateurs internes. Cela signifie généralement connectivité toohello Internet, mais aussi tooon local réseaux et centres de données.

Clients peuvent créer leur toocontrol de stratégies de sécurité qu’et comment les services spécifiques vDC hébergé sont accessibles à partir de hello Internet à l’aide des équipements virtuels de réseau (avec le filtrage et le trafic de contrôle) et les stratégies de routage personnalisées et (filtrage) réseau Le routage défini par l’utilisateur et groupes de sécurité réseau).

Les entreprises doivent souvent tooconnect VDC tooon locaux des centres de données ou d’autres ressources. Hello connectivité entre les réseaux locaux et Azure est donc un aspect essentiel lors de la conception d’une architecture efficace. D’entreprises disposent d’une interconnexion entre vDC locaux et sur deux toocreate de différentes façons dans Azure : transit sur hello Internet et/ou par des connexions directes privées.

Un [ **VPN de Site à Site Azure** ] [ VPN] est un service d’interconnexion sur hello Internet entre les réseaux locaux et vDC hello, établi via sécurisé chiffré connexions (tunnels IPsec/IKE). Connexion de Site à Site Azure est toocreate flexible, rapide et ne nécessite pas de marchés supplémentaires, comme toutes les connexions qui se connectent via internet de hello.

[**ExpressRoute** ] [ ExR] est un service de connectivité Azure qui vous permet de créer des connexions privées entre hello et vDC sur des réseaux locaux. Les connexions ExpressRoute n’entrez pas plus hello Internet public et offrent une sécurité accrue, de fiabilité et plus élevé accélère (Gbits/s de too10), ainsi que la latence cohérente. ExpressRoute est très utile pour VDC, en tant que ExpressRoute clients peuvent obtenir les avantages de hello de règles de conformité associées des connexions privées.

Le déploiement de connexions ExpressRoute implique la souscription d’un engagement auprès d’un fournisseur de services ExpressRoute. Pour les clients qui doivent toostart rapidement, il est souvent utilisé tooinitially connectivité tooestablish VPN de Site à Site entre les ressources locales et vDC hello et migrer tooExpressRoute connexion.

##### <a name="connectivity-within-hello-cloud"></a>*Connexion au sein du cloud de hello*
[Réseaux virtuels] [ VNet] et [réseau virtuel d’homologation] [ VNetPeering] est hello base mise en réseau des services de connectivité à l’intérieur d’un vDC. Un réseau virtuel garantit une frontière naturelle d’isolation pour les ressources de vDC et réseau virtuel d’homologation permet intérieur entre différents réseaux virtuels au sein de hello même région Azure. Contrôler le trafic à l’intérieur d’un réseau virtuel et entre les réseaux virtuels doivent toomatch règles d’un ensemble de sécurité spécifié via les listes de contrôle d’accès ([groupe de sécurité réseau][NSG]), [équipements virtuels du réseau ] [ NVA]et les tables de routage personnalisées ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Vue d’ensemble d’un centre de données virtuel

### <a name="topology"></a>Topologie
Hub et spoke modèle étendu hello centre de données virtuel au sein d’une seule région Azure

[![1]][1]

concentrateur de Hello est zone centrale de hello qui contrôle et inspecte le trafic d’entrée et/ou de sortie entre les différentes zones : Internet, sur site, et hello spokes. topologie hub and spoke de Hello donne hello informatique une stratégies de sécurité efficace tooenforce dans un emplacement central, tout en réduisant le risque de hello pour une configuration incorrecte et des risques.

concentrateur de Hello contient les composants service communs hello consommées par les rayons hello. Voici quelques exemples classiques de services centraux communs :

-   infrastructure d’Active Directory Windows Hello (liés à service AD FS avec hello) requis pour l’authentification utilisateur des tiers l’accès à des réseaux non approuvés avant la mise en route accès toohello les charges de travail dans hello spoke
-   Un service tooresolve attribution de noms DNS pour les charges de travail hello dans hello spokes, tooaccess ressources locales et sur Internet de hello
-   Une infrastructure à clé publique, tooimplement l’authentification unique sur les charges de travail
-   Contrôle de flux (TCP/UDP) entre les spokes hello et Internet
-   Contrôle de flux entre les spoke hello et locales
-   Le cas échéant, contrôle de flux entre deux rayons

Hello vDC réduit le coût global à l’aide d’infrastructure de concentrateur partagé hello entre plusieurs spokes.

rôle de Hello de chaque membre spoke peut être toohost différents types de charges de travail. Hello spokes peuvent également fournir une approche modulaire pour les déploiements repeatable (par exemple, développement et test, les tests d’acceptation utilisateur, pré-production et production) de hello mêmes charges de travail. Hello spokes peuvent également être utilisé toosegregate et permettre à différents groupes au sein de votre organisation (par exemple, les groupes de DevOps). À l’intérieur d’un spoke, il est possible toodeploy une charge de travail de base ou complexes charges de travail à plusieurs niveaux avec le trafic de contrôle entre les couches de hello.

##### <a name="subscription-limits-and-multiple-hubs"></a>Limites d’abonnement et concentrateurs multiples
Dans Azure, chaque composant, tout type hello, est déployé dans un abonnement Azure. isolation Hello des composants Azure dans différents abonnements Azure peut satisfaire les exigences hello de différents départements, telles que la définition des différents niveaux de l’accès et l’autorisation.

Un seul vDC peut évoluer nombre toolarge de rayons, bien que, comme avec tous les systèmes informatiques, il existe des limites de plateformes. déploiement de concentrateur Hello est lié tooa abonnement Azure spécifique, qui présente les restrictions et les limites (par exemple, un nombre maximal de réseau virtuel homologations - voir [abonnement Azure et limites de service, quotas et contraintes] [ Limits] pour plus d’informations). Dans les cas où les limites peuvent être un problème, l’architecture de hello peut évoluer davantage en étendant le modèle de hello d’un cluster de tooa hub-spokes unique de hub et Spoke. Plusieurs concentrateurs situés dans une ou plusieurs régions Azure peuvent être interconnectés à l’aide d’un réseau privé virtuel ExpressRoute ou de site à site.

[![2]][2]

augmente les efforts de gestion et de coût hello du système de hello Hello introduction de plusieurs concentrateurs et serait uniquement justifiée par l’évolutivité (exemples : limites du système ou redondance) et la réplication régionale (exemples : récupération de performances ou d’urgence par l’utilisateur). Dans les scénarios qui requièrent plusieurs concentrateurs, tous les concentrateurs hello efforcez-vous hello toooffer même ensemble de services pour facilité.

##### <a name="interconnection-between-spokes"></a>Interconnexion entre les rayons
À l’intérieur d’un seul spoke, il est possible tooimplement complexe plusieurs niveaux les charges de travail. Les configurations à plusieurs niveaux peuvent être implémentées à l’aide de sous-réseaux (un pour chaque couche) Bonjour même réseau virtuel et filtrage hello flux à l’aide de groupes de sécurité réseau.

Sur hello autre part, un architecte peut vouloir des toodeploy une charge de travail à plusieurs niveaux entre plusieurs réseaux virtuels. À l’aide du réseau virtuel d’homologation, spokes peuvent se connecter spokes tooother Bonjour même concentrateur ou concentrateurs différents. Un exemple typique de ce scénario est le cas de hello où le traitement des serveurs d’applications sont dans un spoke (VNet), tandis que la base de données hello est déployé dans un autre spoke (VNet). Dans ce cas, il est facile toointerconnect spokes hello avec le réseau virtuel d’homologation et éviter ainsi transitant par le concentrateur de hello. Un examen minutieux de l’architecture et la sécurité doit être effectuée tooensure en ignorant les hub hello ne contourner l’audit de points qui peuvent uniquement exister dans le hub de hello ou de sécurité importantes.

[![3]][3]

Spokes peuvent également être spoke tooa interconnectés qui agit comme un concentrateur. Cette approche crée une hiérarchie à deux niveaux : concentrateur de hello hello spoke de niveau supérieur de hello (niveau 0) deviennent des rayons inférieurs (niveau 1) de la hiérarchie de hello. spokes Hello de vDC doivent tooforward hello trafic toohello concentrateur central tooreach out toohello local ou réseau internet. Une architecture à deux niveaux de concentrateur introduit routage complexe qui supprime les avantages hello d’une relation simple hub/spoke.

Bien que Azure autorise des topologies complexes, un des principes de base hello du concept de vDC hello est la répétabilité et la simplicité. travail de gestion toominimize, hello simple hub/spoke convient hello vDC référence architecture recommandée.

### <a name="components"></a>Composants
Un centre de données virtuel comporte quatre types de composants de base : **infrastructure**, **réseaux de périmètre**, **charges de travail** et **surveillance**.

Chaque type de composant intègre plusieurs ressources et fonctionnalités Azure. Votre vDC est constitué des instances de plusieurs types de composants et de nombreuses variantes de hello même type de composant. Par exemple, vous pouvez disposer de nombreuses instances de charge de travail distinctes, séparées de façon logique, qui représentent différentes applications. Vous utilisez ces différents types de composants et instances tooultimately générer hello vDC.

[![4]][4]

Hello précédente architecture de haut niveau d’un vDC affiche différents types de composants utilisés dans différentes zones d’une topologie hub-rayons de hello. diagramme de Hello illustre les composants d’infrastructure dans les différentes parties de l’architecture de hello.

Une bonne pratique (pour un centre de données local ou un vDC) consiste à baser les droits d’accès et les privilèges sur un groupe. La manipulation de groupes, plutôt que d’utilisateurs individuels, garantit une gestion cohérente des stratégies d’accès entre les équipes et contribue à minimiser les erreurs de configuration. L’assignation et supprime les utilisateurs tooand vous aide à des groupes appropriés maintien à jour des privilèges hello d’un utilisateur spécifique.

Chaque groupe de rôle doit avoir un préfixe unique sur leurs noms rend facile tooidentify le groupe auquel est associé avec les charges de travail. Par exemple, une charge de travail hébergeant un service d’authentification peut être associée à des groupes appelés *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps et AuthServiceInfraOps*. De même pour centralisée rôles ou des rôles non liés de service spécifique de tooa, peut être précédés de « Corp », *CorpNetOps* par exemple.

De nombreuses organisations utilisent une variation de hello suivant groupes tooprovide une répartition principale des rôles :

-   Hello *groupe informatique centralisé (Corp)* hello la propriété droits toocontrol infrastructure (par exemple, la mise en réseau et sécurité) des composants et par conséquent a besoin du rôle de hello toohave de collaborateurs sur les abonnement hello (et disposer du contrôle concentrateur de Hello) et les droits de contributeur dans hello spokes du réseau. Une grande organisation répartit généralement ces responsabilités de gestion entre plusieurs équipes, telles qu’un groupe Opérations de réseau (CorpNetOps), exclusivement axé sur la mise en réseau, et un groupe Opérations de sécurité (CorpSecOps), chargé de la stratégie de pare-feu et de sécurité. Dans ce cas, deux groupes différents doivent toobe créé pour l’attribution de ces rôles personnalisés.
-   Hello *dev & groupe de test (AppDevOps)* a hello responsabilité toodeploy les charges de travail (applications ou Services). Ce groupe prend hello de contributeur de la Machine virtuelle pour les déploiements IaaS et/ou de l’un ou rôles de collaborateur plus PaaS (consultez [rôles intégrés pour du contrôle d’accès][Roles]). Si vous le souhaitez hello dev & équipe des tests peut-être visibilité toohave sur des stratégies de sécurité (NSG) et stratégies de routage (UDR) à l’intérieur du concentrateur de hello ou un spoke spécifique. Par conséquent, des rôles de toohello d’ajout de collaborateur pour les charges de travail, ce groupe doit également rôle hello de lecteur du réseau.
-   Hello *group de fonctionnement et maintenance (CorpInfraOps ou AppInfraOps)* ont hello la responsabilité de la gestion des charges de travail de production. Ce groupe doit toobe un contributeur de l’abonnement sur les charges de travail dans un abonnement de production. Certaines organisations peuvent également évaluer s’ils ont besoin d’un groupe d’équipe prise en charge escalade de verrous supplémentaires avec le rôle de hello de collaborateur d’abonnement en production et dans l’abonnement de concentrateur central hello, dans l’ordre toofix éventuels problèmes de configuration en production de hello environnement.

Un vDC est structuré de sorte que les groupes créés pour la gestion de concentrateur de hello les groupes informatique central hello ont des groupes correspondants au niveau de la charge de travail hello. En outre, toomanaging hub ressources uniquement hello centrales groupes informatiques serait toocontrol en mesure de l’accès externe et les autorisations de niveau supérieur sur les abonnement hello. Toutefois, les groupes de charges de travail serait toocontrol en mesure de ressources et les autorisations de leur réseau virtuel indépendamment sur le service informatique Central.

Hello vDC besoins toobe partitionnées toosecurely hôte plusieurs projets sur chaque ligne d’entreprise (LOB). Tous les projets nécessitent plusieurs environnements isolés (développement, test d’acceptation utilisateur (UAT), production). Les abonnements Azure distincts pour chacun de ces environnements assurent un isolement naturel.

[![5]][5]

Hello diagramme précédent montre relation hello entre les projets d’une organisation, les utilisateurs, les groupes et les environnements hello où hello Azure les composants sont déployés.

Dans le contexte informatique, un environnement (ou niveau) désigne généralement un système dans lequel plusieurs applications sont déployées et exécutées. Les grandes entreprises utilisent un environnement de développement (dans lequel les modifications sont initialement effectuées et testées) et un environnement de production (destiné aux utilisateurs finaux). Ces environnements sont séparés, souvent plusieurs intermédiaires entre les environnements de déploiement de tooallow en plusieurs phases (déploiement), le test et la restauration en cas de problèmes. Architectures de déploiement varient considérablement, mais généralement les processus de base hello de développement (DEV) et à la production (PROD) est toujours suivi.

Une architecture communément employée pour ces types d’environnements multiniveau est constituée d’environnements DevOps (développement et test), UAT (intermédiaire) et de production. Les organisations peuvent exploiter unique ou plusieurs Azure AD aux locataires toodefine accès et les droits des environnements toothese. Hello diagramme précédent illustre un cas où deux différents locataires Azure AD sont utilisés : un pour DevOps UAT et hello autre exclusivement pour la production.

Hello la présence d’AD Azure différents locataires applique une séparation hello entre les environnements. Hello du même groupe d’utilisateurs (par exemple, informatique Central) tooauthenticate à l’aide d’un autre tooaccess d’URI un autre client Active Directory doit modifier les rôles de hello ou autorisations de hello soit DevOps ou les environnements de production d’un projet. présence de Hello utilisateur différents environnements d’authentification tooaccess différents réduit les éventuelles interruptions et autres problèmes dus à des erreurs humaines.

#### <a name="component-type-infrastructure"></a>Type de composant : infrastructure
Ce type de composant où réside la plupart des hello infrastructure de prise en charge. Il s’agit également du composant auquel vos équipes informatique, sécurité et/ou conformité centralisées consacrent la majorité de leur temps.

[![6]][6]

Composants d’infrastructure fournissent une interconnexion entre hello différents composants d’un vDC et sont présents dans le concentrateur de hello et hello spokes. Hello responsable de la gestion et maintenance des composants d’infrastructure hello est généralement assignée toohello centre informatique et/ou de l’équipe de sécurité.

Une des tâches principales hello hello équipe d’infrastructure informatique est la cohérence de hello tooguarantee des schémas d’adresse IP dans toute entreprise de hello. Hello privé IP adresse espace affecté toohello vDC doit toobe cohérente et ne chevauchent pas avec les adresses IP privées affectés sur votre réseau local.

Bien que NAT sur hello local routeurs de bord ou dans Azure environnements pour éviter les conflits d’adresses IP, il ajoute des composants d’infrastructure complications tooyour. Simplicité de gestion est un des objectifs clés de hello de vDC, à l’aide de problèmes d’IP NAT toohandle n’est pas une solution recommandée.

Composants d’infrastructure contient hello suivant de fonctionnalités :

-   [**Services d’identité et d’annuaire**][AAD]. Type de ressource tooevery accès dans Azure est contrôlé par une identité stockée dans un service d’annuaire. Hello directory service stocke non seulement hello la liste des utilisateurs, mais également hello tooresources de droits d’accès dans un abonnement Azure spécifique. Ces services peuvent exister uniquement dans le cloud, ou être synchronisés avec l’identité locale stockée dans Active Directory.
-   [**Réseau virtuel**][VPN]. Réseaux virtuels sont un des principaux composants d’un vDC et activer toocreate une limite d’isolation du trafic sur hello plateforme Azure. Un réseau virtuel est constitué d’un ou de plusieurs segments de réseau virtuel, chacun étant doté d’un préfixe de réseau IP (sous-réseau) spécifique. Hello réseau virtuel définit une zone de périmètre interne où les machines virtuelles IaaS et PaaS services peuvent établir des communications privées. Machines virtuelles (et les services PaaS) dans un réseau virtuel ne peut pas communiquer directement tooVMs (et les services PaaS) dans un autre réseau virtuel, même si les deux réseaux virtuels est créés par hello même client, sous hello même abonnement. Cet isolement est une propriété critique qui garantit que les machines virtuelles et les communications du client restent privées dans un réseau virtuel.
-   [**Itinéraire défini par l’utilisateur**][UDR]. Le trafic dans un réseau virtuel est acheminé par défaut en fonction de la table de routage système hello. Un itinéraire de l’utilisateur définissent est une table de routage personnalisée que les administrateurs réseau peuvent associer tooone ou sous-réseaux toooverwrite hello un comportement plus de la table de routage système hello et définir un chemin d’accès de communication au sein d’un réseau virtuel. présence de Hello de UDRs garantit que le trafic sortant à partir de hello spoke passage des machines virtuelles personnalisées spécifiques et/ou des équipements virtuels du réseau et les équilibreurs de charge présents dans le concentrateur de hello et dans les rayons hello.
-   [**Groupe de sécurité réseau (NSG)**][NSG]. Un groupe de sécurité réseau est une liste de règles de sécurité qui font office de filtrage du trafic sur les sources IP, la destination IP, les protocoles, les ports de source IP et les ports de destination IP. Hello NSG peut être appliqué tooa sous-réseau, une carte de réseau virtuel associée à une machine virtuelle Azure, ou les deux. groupes de sécurité réseau Hello sont essentiel tooimplement un contrôle de flux approprié dans le concentrateur de hello et hello spokes. niveau de Hello de sécurité offerte par hello NSG est une fonction des ports ouverts et dans quel but. Les clients doivent appliquer des filtres supplémentaires par machine virtuelle avec un pare-feu d’hôte telles que IPtables ou hello du pare-feu Windows.
-   **DNS (Domain Name System)**. résolution de noms Hello des ressources Bonjour réseaux virtuels d’un vDC est fournie via DNS. étendue de Hello de résolution de noms de la valeur par défaut de hello DNS est limité toohello réseau virtuel. En règle générale, un service DNS personnalisé doit toobe déployé dans le hub de hello dans le cadre des services courants, mais consommateurs de hello principal des services DNS se trouvent dans les spoke hello. Si nécessaire, aux clients de créer une structure hiérarchique de DNS avec la délégation de rayons de toohello de zones DNS.
-   [**Abonnement][SubMgmt] et [Gestion des groupes de ressources][RGMgmt]**. Un abonnement définit un toocreate frontière naturelle plusieurs groupes de ressources dans Azure. Les ressources d’un abonnement sont regroupées dans des conteneurs logiques nommés groupes de ressources. Hello, groupe de ressources représente un groupe logique tooorganize hello des ressources d’un vDC.
-   [**Contrôle d’accès en fonction du rôle (RBAC)**][RBAC]. Via RBAC, il est possible toomap le rôle organisationnel, ainsi que de droits tooaccess Azure des ressources spécifiques, ce qui permet de vous toorestrict utilisateurs tooonly un sous-ensemble spécifique d’actions. Avec RBAC, vous pouvez accorder l’accès en assignant hello rôle approprié toousers, des groupes et des applications au sein de l’étendue de pertinentes hello. Hello portée d’une attribution de rôle peut être un abonnement Azure, un groupe de ressources ou une seule ressource. Le mécanisme RBAC autorise l’héritage des autorisations. Un rôle attribué à une portée parent accorde également l’accès toohello les enfants qu’il contient. À l’aide de RBAC, vous pouvez séparer les droits et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail. Par exemple, un employé d’utiliser RBAC toolet gérer les ordinateurs virtuels dans un abonnement, pendant que l’autre peut gérer les bases de données SQL dans hello même abonnement.
-   [**Homologation de réseaux virtuels**][VNetPeering]. Hello fonctionnalité fondamental utilisée toocreate hello infrastructure d’un vDC est homologation de réseau virtuel, un mécanisme qui connecte deux réseaux virtuels (réseaux virtuels) Bonjour même région via réseau hello hello Azure du centre de données.

#### <a name="component-type-perimeter-networks"></a>Type de composant : réseaux de périmètre
[Réseau de périmètre] [ DMZ] composants (également appelé réseau DMZ) vous permettent de connectivité de réseau tooprovide avec votre local ou les réseaux de centre de données physique, ainsi que n’importe quel tooand de connectivité de hello Internet. Il s’agit également des composants auxquels vos équipes réseau et sécurité consacrent généralement la majorité de leur temps.

Flux de paquets entrants par le biais des appliances de sécurité hello dans le hub hello, tels que les pare-feu hello, ID et adresses IP, avant d’atteindre les serveurs principaux hello hello spokes. Internet liés aux paquets à partir de charges de travail hello doit également circulent à travers les appliances de sécurité hello dans le réseau de périmètre hello pour l’application des stratégies, d’inspection et de l’audit à des fins, avant de quitter le réseau de hello.

Composants réseau de périmètre fournissent hello suivant de fonctionnalités :

-   [Réseaux virtuels][VNet], [itinéraires définis par l’utilisateur][UDR], [groupes de sécurité réseau][NSG]
-   [Appliance virtuelle réseau][NVA]
-   [Équilibreur de charge][ALB]
-   [Application Gateway][AppGW] / [Pare-feu d’applications web (WAF)][WAF]
-   [Adresses IP publiques][PIP]

En règle générale, les hello centrale informatiques et les équipes de sécurité ont la responsabilité de définition de la demande et les opérations hello des réseaux de périmètre.

[![7]][7]

mise en œuvre hello affiche Hello diagramme précédent de deux périmètre avec toohello d’accès internet et un local réseau, les deux résident dans le hub de hello. Dans une méthode unique, toointernet de réseau de périmètre hello capable d’évoluer toosupport un grand nombre d’objets LOB, à l’aide de plusieurs batteries de serveurs de pare-feu d’applications Web (WAFs) et/ou le pare-feu.

[**Réseaux virtuels** ] [ VNet] concentrateur de hello repose généralement sur un réseau virtuel avec plusieurs sous-réseaux toohost hello autre type de services de filtrage et en inspectant tooor le trafic à partir de hello internet via NVAs, WAFs, et les passerelles d’Application Windows Azure.

[**Itinéraires définis par l’utilisateur**][UDR] Ces itinéraires permettent aux clients de déployer des pare-feu, des systèmes de détection et de prévention d’intrusion et d’autres appliances virtuelles, et de router le trafic réseau à travers ces appliances de sécurité à des fins d’application de stratégies de limites de sécurité, d’audit et d’inspection. UDRs peuvent être créés dans les deux hello tooguarantee rayons de l’hub et hello qui transits le trafic via hello des machines virtuelles personnalisées spécifiques, les dispositifs réseau virtuel et les équilibreurs de charge utilisés par hello vDC. tooguarantee que le trafic généré à partir d’ordinateurs virtuels qui se trouvent dans hello spoke transit toohello correct équipements virtuels, un UDR doit toobe défini dans des sous-réseaux de spoke de hello hello en définissant l’adresse IP frontale de hello d’équilibreur de charge interne hello en tant que tronçon suivant hello. équilibreur de charge interne Hello distribue des équipements virtuels hello le trafic interne toohello (pool de serveur principal d’un équilibreur de charge).

[![8]][8]

[**Réseau virtuel** ] [ NVA] dans le hub de hello, hello réseau de périmètre avec toohello accès internet est normalement gérée grâce à une batterie de serveurs de pare-feu et/ou des pare-feu d’applications Web (WAFs).

Différents départements utilisent généralement de nombreuses applications web, de ces applications ont tendance à toosuffer à partir de différents des vulnérabilités et des exploits potentiels. Pare-feu d’Applications Web sont un type spécial de produit toodetect les attaques contre les applications web (HTTP/HTTPS) de manière plus approfondie qu’un pare-feu générique. Comparaison avec la technologie de pare-feu tradition, WAFs ont un ensemble de fonctionnalités spécifiques tooprotect web interne serveurs contre les menaces.

Une batterie de serveurs de pare-feu est un groupe de pare-feu travaillent en tandem sous hello même administration commune, avec un ensemble de sécurité règles tooprotect hello des charges de travail hébergée dans les rayons hello et contrôle l’accès tooon des réseaux locaux. Une batterie de serveurs de pare-feu a moins spécialisé logiciels comparée avec une WAF, mais dispose d’une application large étendue toofilter et examiner n’importe quel type de trafic en entrée et de sortie. Batteries de serveurs de pare-feu sont normalement implémentées dans Azure via des équipements virtuels réseau (NVAs), qui sont disponibles dans hello Azure marketplace.

Il est recommandé de jeu toouse celui de NVAs pour le trafic provenant de hello Internet, et un autre pour le trafic d’origine sur site. Utiliser qu’un ensemble de NVAs pour deux d’est un risque de sécurité, car elle ne fournit aucun périmètre de sécurité entre deux jeux de hello du trafic réseau. À l’aide de NVAs distincts hello et la complexité de la vérification des règles de sécurité, indique clairement les règles correspondent toowhich les demande réseau entrantes.

La plupart des grandes entreprises gèrent plusieurs domaines. DNS Azure peut être toohost utilisé hello les enregistrements DNS pour un domaine particulier. Exemple : hello adresse IP virtuelle (VIP) du programme d’équilibrage de charge externe Azure hello (ou hello WAFs) peut être inscrits dans l’enregistrement A de hello d’un enregistrement DNS de Azure.

[**Azure Load Balancer**][ALB] L’équilibreur de charge Azure offre un service haute disponibilité de couche 4 (TCP, UDP), qui peut distribuer le trafic entrant entre des instances de service définies dans un jeu d’équilibrage de la charge. Le trafic envoyé toohello équilibrage de charge à partir de points de terminaison frontales (points de terminaison IP publics ou des points de terminaison IP privés) peut être redistribué avec ou sans adresse traduction tooa ensemble de pool d’adresses IP principale (exemples en cours ; Les dispositifs réseau virtuel ou des machines virtuelles).

L’équilibrage de charge Azure peut détecter intégrité hello hello différentes instances de serveur ainsi et lorsque une sonde échoue toorespond hello charge équilibrage s’arrête envoi d’instance non intègre de trafic toohello. Dans un vDC, nous avons présence hello d’un équilibreur de charge externe dans le concentrateur hello (par exemple, solde hello trafic tooNVAs) et dans les rayons de hello (tooperform des tâches telles que l’équilibrage du trafic entre les différentes machines virtuelles d’une application multicouche).

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway est une appliance virtuelle dédiée qui intègre Application Delivery Controller (ADC) sous la forme d’un service, offrant ainsi diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application. Il vous permet de productivité de batterie de serveurs web toooptimize en déchargeant la passerelle d’application UC intensif SSL arrêt toohello. Il fournit également des autres fonctionnalités de routage de couche 7, y compris la distribution Round robin de trafic entrant d’affinité de session basée sur un cookie, le routage basé sur le chemin d’accès URL et hello capacité toohost plusieurs sites Web derrière une passerelle d’Application unique. Un pare-feu d’applications web (WAF) est également fourni dans le cadre de la passerelle d’application hello WAF référence (SKU). Cette référence (SKU) offre une protection tooweb les applications courantes des vulnérabilités de web et des exploits. La passerelle Application Gateway peut être configurée en tant que passerelle internet, passerelle interne uniquement ou une combinaison des deux. 

[**Adresses IP publiques** ] [ PIP] activation de fonctionnalités de certains Azure vous tooassociate service points de terminaison tooa adresse IP publique qui permet de tooyour ressource toobe accessible à partir de hello internet. Ce point de terminaison utilise l’adresse interne de traduction d’adresses réseau (NAT) tooroute trafic toohello et le port sur hello réseau virtuel Azure. Ce chemin d’accès est hello pour principal moyen toopass trafic externe au réseau virtuel de hello. adresses IP publiques de Hello peuvent être configuré toodetermine le trafic qui est passé dans, et où et comment il est traduit sur le réseau virtuel de toohello.

#### <a name="component-type-monitoring"></a>Type de composant : surveillance
Composants de contrôle fournissent la visibilité et la génération d’alertes de tous les hello des autres types de composants. Toutes les équipes doivent avoir toomonitoring d’accès pour les composants de hello et services, ils ont accès. Si vous avez un équipes de support technique ou d’opérations aide centralisé, ils ont besoin des données de toohello access toohave intégrée fournies par ces composants.

Azure offre différents types de journalisation et de surveillance du comportement de hello tootrack services Azure hébergés de ressources. Gouvernance et contrôle des charges de travail dans Azure est en fonction non seulement de collecte de données de journal, mais également des actions de tootrigger de capacité de hello basées sur les événements signalés spécifiques.

Il existe deux principaux types de journaux dans Azure :

-   [**Journaux d’activité** ] [ ActLog] (appelée également en tant que « Journal opérationnel ») donnent une idée des opérations hello qui ont été effectuées sur les ressources hello abonnement Azure. Ces journaux signalent les événements de panneau hello pour vos abonnements. Chaque ressource Azure génère des journaux d’audit.

-   [**Les journaux de Diagnostic Azure** ] [ DiagLog] sont des fichiers journaux générés par une ressource qui fournissent des données riches et fréquentes relatives au fonctionnement de hello de cette ressource. le contenu de ces journaux Hello varie selon le type de ressource.

[![9]][9]

Dans un vDC, il s’agit de journaux de groupes de sécurité réseau hello tootrack extrêmement important, en particulier, ces informations :

-   [**Journaux des événements**][NSGLog]: fournit des informations sur les règles du groupe de sécurité réseau sont tooVMs appliqués et les rôles d’instance en fonction de l’adresse MAC.
-   [**Journaux de compteur**][NSGLog]: effectue le suivi du nombre de fois où chaque groupe de sécurité réseau, la règle a été exécutée toodeny ou autoriser le trafic.

Tous les journaux peuvent être stockés dans des comptes de stockage Azure à des fins d’audit, d’analyse statique ou de sauvegarde. Lorsque les journaux de hello sont stockés dans un compte de stockage Azure, les clients peuvent utiliser différents types d’infrastructures tooretrieve, préparer, analyser et visualiser cet état de hello de tooreport de données et l’intégrité des ressources de cloud.

Les grandes entreprises doivent déjà avoir acquis une infrastructure standard pour l’analyse des systèmes locaux et peut étendre que framework toointegrate journaux générés par les déploiements de cloud. Pour les organisations qui souhaitent tookeep tous hello journalisation dans le cloud de hello, [Microsoft Operations Management Suite (OMS)] [ OMS] est un bon choix. La solution OMS étant implémentée sous la forme d’un service informatique, elle peut être opérationnelle rapidement, avec un investissement minimal dans des services d’infrastructure. OMS peut également s’intégrer avec des composants de System Center tels que System Center Operations Manager tooextend vos investissements de gestion existants dans le cloud de hello.

Analytique des journaux OMS est un composant de hello OMS framework toohelp collecter, de corrélation, recherche et agir sur les données de performances et de journal générés par cloud d’infrastructure, les applications, les systèmes d’exploitation de composants. Il permet aux clients des informations opérationnelles en temps réel grâce à une recherche intégrée et des tableaux de bord personnalisés tooanalyze tous les enregistrements de hello dans toutes les charges de travail dans un vDC.

#### <a name="component-type-workloads"></a>Type de composant : charges de travail
Les composants de type charge de travail désignent l’emplacement où résident vos applications et services proprement dits. Il s’agit également du composant auquel vos équipes de développement d’applications consacrent la majorité de leur temps.

possibilités de charge de travail de Hello sont réellement illimitées. Hello Voici quelques-uns des types de charges de travail possible hello :

**Applications métiers internes**

Les applications Line-of-business sont opération en cours d’ordinateur applications toohello critiques de l’entreprise. Les applications métiers présentent certaines caractéristiques en commun :

-   **Interactives**. Les applications métiers sont interactives par nature : elles reçoivent des données et renvoient des résultats ou rapports.
-   **Pilotées par les données**. Applications métier sont des données de bases de données toohello accès fréquent ou autre support de stockage.
-   **Intégrées**. LOB applications offre l’intégration avec d’autres systèmes au sein ou en dehors de l’organisation de hello.

**Les clients confrontés à des sites web (exposés à Internet ou interne)** la plupart des applications qui interagissent avec hello Internet sont des sites web. Azure offre hello capacité toorun un site web un VM IaaS ou à partir d’un [Azure Web Apps] [ WebApps] site (PaaS). Azure Web Apps prend en charge l’intégration avec les réseaux virtuels permettent de déployer hello hello Web Apps dans un vDC parlé hello. Avec hello intégration de réseau virtuel, vous n’avez pas besoin tooexpose un point de terminaison Internet pour vos applications, mais pourrez utiliser hello ressources internet non routable adresse privée à partir de votre réseau virtuel privé à la place.

**Données/Analytique Big** lorsque tooscale les très gros volume de tooa a besoin de données, bases de données ne peuvent pas adapter correctement. Technologie de Hadoop offre un système toorun distribué des requêtes en parallèle sur un grand nombre de nœuds. Les clients ont hello option toorun les charges de données dans des machines virtuelles IaaS ou PaaS ([HDInsight][HDI]). HDInsight prend en charge le déploiement dans un réseau virtuel basée sur l’emplacement, cluster tooa déployé dans un rayon de hello vDC.

**Événements et messagerie**
[Azure Event Hubs][EventHubs] est un service d’ingestion de télémétrie hyperscale qui collecte, transforme et stocke des millions d’événements. Comme une plate-forme de diffusion en continu distribuée, il offre une latence faible et rétention de temps configurable, ce qui vous tooingest de gros volumes de données de télémétrie dans Azure et lire ces données à partir de plusieurs applications. Le service Event Hubs prend en charge le traitement de pipelines en temps réel et par lots sur le même flux.

Il est possible d’implémenter un service de messagerie cloud haute fiabilité entre les applications et les services par le biais du service [Azure Service Bus][ServiceBus] qui offre une messagerie répartie asynchrone entre un client et un serveur, ainsi qu’une messagerie structurée du type premier entré, premier sorti (FIFO) et des fonctionnalités de publication/abonnement.

[![10]][10]

### <a name="multiple-vdc"></a>vDC multiples
Jusqu'à présent, cet article se sont concentrées sur un seul vDC, qui décrivent les composants de base hello et architecture qui contribuent vDC résilient de tooa. Fonctionnalités Azure telles que les groupes à haute disponibilité Azure charge équilibrage, NVAs, identiques, ainsi que d’autres mécanismes contribuent tooa système qui vous permettent de niveaux de contrat SLA solides toobuild dans vos services de production.

Toutefois, un seul vDC est hébergé dans une région et est vulnérable toomajor panne qui peut-être affecter cette région entière. Clients désireux tooachieve SLA élevés besoin de services de hello de tooprotect par le biais des déploiements de hello même projet VDC deux (ou plus), placés dans des régions différentes.

Dans questions tooSLA de plus, il existe plusieurs scénarios courants où déployer plusieurs VDC sens :

-   Présence régionale/mondiale
-   Récupération d’urgence
-   Trafic de toodivert mécanisme entre le contrôleur de domaine

#### <a name="regionalglobal-presence"></a>Présence régionale/mondiale
Les centres de données Azure sont présents dans de nombreuses régions du monde. Lorsque vous sélectionnez plusieurs centres de données Azure, les clients doivent tooconsider de deux facteurs connexes : distances géographiques et la latence. Les clients doivent tooevaluate hello géographique sépare hello VDC distance hello entre hello vDC et les utilisateurs finaux hello toooffer hello meilleure expérience utilisateur.

Hello région Azure où se trouvent VDC besoin également tooconform avec des obligations réglementaires établies par une juridiction juridique sous lequel s’exécute votre organisation.

#### <a name="disaster-recovery"></a>Récupération d’urgence
implémentation de Hello d’un plan de récupération d’urgence est type toohello étroitement liés de charge de travail concerné et état de la charge de travail hello capacité toosynchronize hello entre VDC différents. Dans l’idéal, la plupart des clients souhaitez toosynchronize les données d’application entre les déploiements en cours d’exécution dans deux mécanisme de tooimplement un basculement rapide VDC différents. La plupart des applications sont toolatency sensibles, et qui peut entraîner des potentiels de délai d’attente et de retard dans la synchronisation des données.

La synchronisation ou l’analyse des pulsations des applications dans différents VDC nécessitent une communication entre ces derniers. Deux vDC situés dans des régions distinctes peuvent être connectés par le biais de différentes méthodes :

-   Homologation privée ExpressRoute lorsque les concentrateurs de vDC hello sont connecté toohello même circuit ExpressRoute
-   plusieurs circuits ExpressRoute connecté via le segment principal de votre entreprise et votre maillage vDC toohello connecté des circuits ExpressRoute
-   Connexions de réseau privé virtuel de site à site entre les concentrateurs de vos vDC dans chaque région Azure

Hello connexion ExpressRoute est généralement mécanisme hello préférée en raison de la bande passante et de latence cohérente lors du transit via hello backbone de Microsoft.

Aucun toovalidate recette magic une application est distribuée entre les deux (ou plus) VDC différents situés dans des régions différentes. Les clients doivent exécuter réseau qualification tests tooverify hello latence et la bande passante de connexions de hello et la cible si la réplication synchrone ou asynchrone des données est appropriée et quelles hello optimal temps de récupération (RTO) peut être utilisé pour votre charges de travail.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Trafic de toodivert mécanisme entre le contrôleur de domaine
Une technique performante toodivert hello le trafic entrant dans un contrôleur de domaine tooanother est basé sur DNS. [Azure Traffic Manager] [ TM] utilise hello système DNS (Domain Name) mécanisme toodirect hello par l’utilisateur le trafic toohello plus approprié point de terminaison public dans un vDC spécifique. À travers des sondes, Traffic Manager vérifie périodiquement l’intégrité du service hello de points de terminaison publics dans VDC différents et, en cas de défaillance de ces points de terminaison, il achemine automatiquement vDC secondaire de toohello.

Traffic Manager fonctionne sur les points de terminaison publics Azure et peut être utilisé, par exemple, tooAzure de trafic toocontrol/détournent les machines virtuelles et les applications Web dans hello approprié vDC. Traffic Manager est résilient même en face de hello d’un échec de l’ensemble de la région Azure et peuvent contrôler la distribution de hello du trafic utilisateur pour les points de terminaison de service dans différentes VDC selon plusieurs critères (par exemple, une défaillance d’un service dans un vDC spécifique, ou en sélectionnant vDC Hello avec une latence réseau la plus basse hello pour les clients hello).

### <a name="conclusion"></a>Conclusion
Centre de données virtuel de Hello est une approche toodata centre la migration cloud hello qui utilise une combinaison de fonctionnalités et capacités toocreate une architecture évolutive dans Azure qui optimise l’utilisation de ressources de cloud, en réduisant les coûts et à la simplification du système gouvernance. concept de vDC Hello est basée sur une topologie hub-spokes, fournissant les services partagés courantes dans le hub de hello et autoriser des applications/charges de travail spécifiques dans les rayons hello. Un vDC correspond à la structure de hello des rôles d’entreprise, où plusieurs services (service informatique Central, DevOps, opération et la maintenance) fonctionnent ensemble, chacun avec une liste spécifique des rôles et des droits. Un vDC répond aux exigences de hello pour une migration « De courbes d’élévation et MAJ », mais il fournit également de nombreux avantages toonative les déploiements de cloud.

## <a name="references"></a>Références
Hello suivant les fonctionnalités abordé dans ce document. Cliquez sur toolearn de liens hello plus.

| | | |
|-|-|-|
|Fonctionnalités réseau|Équilibrage de la charge.|Connectivité|
|[Réseaux virtuels Azure][VNet]</br>[Groupes de sécurité réseau][NSG]</br>[Journaux de groupe de sécurité réseau][NSGLog]</br>[Itinéraire défini par l’utilisateur][UDR]</br>[Appliances virtuelles réseau][NVA]</br>[Adresses IP publiques][PIP]|[Azure Load Balancer (L3) ][ALB]</br>[Application Gateway (L7) ][AppGW]</br>[Pare-feu d’applications web][WAF]</br>[Azure Traffic Manager][TM] |[Homologation de réseaux virtuels][VNetPeering]</br>[Réseau privé virtuel][VPN]</br>[ExpressRoute][ExR]
|Identité</br>|Analyse</br>|Meilleures pratiques</br>|
|[Azure Active Directory][AAD]</br>[Multi-Factor Authentication][MFA]</br>[Contrôle d’accès en fonction du rôle][RBAC]</br>[Rôles Azure Active Directory par défaut][Roles] |[Journaux d’activité][ActLog]</br>[Journaux de diagnostic][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Meilleures pratiques en matières de réseaux de périmètre][DMZ]</br>[Gestion des abonnements][SubMgmt]</br>[Gestion des groupes de ressources][RGMgmt]</br>[Limites d’abonnement Azure][Limits] |
|Autres services Azure|
|[Azure Web Apps][WebApps]</br>[HDInsights (Hadoop) ][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>Étapes suivantes
 - Explorer [réseau virtuel d’homologation][VNetPeering], hello technologie sous-jacente pour vDC hub et spoke conceptions
 - Implémentez [AAD] [ AAD] tooget main [RBAC] [ RBAC] exploration
 - Développer un modèle de gestion d’abonnement et de ressources et RBAC modéliser toomeet hello structure, configuration requise et les stratégies de votre organisation. planification de l’activité plus importante Hello. Dans la mesure du possible, planifiez les réorganisations, les fusions, les nouvelles gammes de produits, etc.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Exemples de chevauchement de composants" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Exemple de haut niveau de vDC hub-and-spoke"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Cluster de concentrateurs et de rayons"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Rayon à rayon"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Diagramme de niveau bloc de hello vDC"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Utilisateurs, groupes, abonnements et projets"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Diagramme d’infrastructure de haut niveau"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Diagramme d’infrastructure de haut niveau"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "Homologation de réseaux virtuels et réseaux de périmètre"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Diagramme de surveillance de haut niveau"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Diagramme de charge de travail de haut niveau"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
