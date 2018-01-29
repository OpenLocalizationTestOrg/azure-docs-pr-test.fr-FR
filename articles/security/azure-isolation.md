---
title: Isolation dans le cloud public Azure | Microsoft Docs
description: "Découvrez les services informatiques cloud qui incluent une large sélection d’instances de calcul et de services pouvant être mis à l’échelle automatiquement pour répondre aux besoins de votre application ou de votre entreprise."
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
ms.date: 11/21/2017
ms.author: TomSh
ms.openlocfilehash: a153d70e077ad63a042e76d0c4ae40e3cc067a2a
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/22/2017
---
# <a name="isolation-in-the-azure-public-cloud"></a>Isolation dans le cloud public Azure
##  <a name="introduction"></a>Introduction
### <a name="overview"></a>Vue d'ensemble
Pour aider les clients actuel et futurs d’Azure à comprendre et à utiliser les différentes fonctionnalités liées à la sécurité disponibles dans la plateforme Azure et autour de celle-ci, Microsoft a développé une série de livres blancs, de présentations de sécurité, de meilleures pratiques et de listes de vérification.
Les rubriques sont aussi précises que variées et sont mises à jour régulièrement. Ce document fait partie de cette série, comme décrit dans la section Résumé ci-après.

### <a name="azure-platform"></a>Plateforme Azure
Azure est une plateforme de services cloud ouverte et flexible, qui prend en charge un large éventail de systèmes d’exploitation, de langages de programmation, d’infrastructures, d’outils, de bases de données et d’appareils. Vous pouvez par exemple afficher :
- exécuter des conteneurs Linux avec l’intégration Docker ;
- créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js ; et
- créer des serveurs principaux pour les appareils iOS, Android et Windows.

Microsoft Azure prend en charge les technologies auxquelles des millions de développeurs et de professionnels de l’informatique font déjà confiance.

Lorsque vous générez ou faites migrer des ressources informatiques vers un fournisseur de services cloud public, vous comptez sur les capacités de cette organisation à protéger vos applications et données avec les services et les contrôles qu’elle vous fournit pour gérer la sécurité de vos ressources cloud.

L’infrastructure d’Azure est conçue de l’installation vers les applications pour héberger des millions de clients simultanément, et constitue une base fiable permettant de répondre aux besoins des entreprises en matière de sécurité. En outre, Azure vous offre un large éventail d’options de sécurité configurables, ainsi que la possibilité de contrôler ces options pour vous permettre de personnaliser la sécurité et de répondre ainsi aux exigences uniques de vos déploiements. Ce document vous aide à répondre à ces exigences.

### <a name="abstract"></a>Résumé

Microsoft Azure vous permet d’exécuter des applications et des machines virtuelles sur une infrastructure physique partagée. L’une des principales motivations économiques pour exécuter des applications dans un environnement cloud est la possibilité de répartir le coût des ressources partagées entre plusieurs clients. Cette pratique de mutualisation améliore l’efficacité en multiplexant des ressources entre différents clients à faible coût. Malheureusement, elle présente également le risque de partager des serveurs physiques et d’autres ressources d’infrastructure pour exécuter vos machines virtuelles et applications sensibles appartenant peut-être à un utilisateur arbitraire et potentiellement malveillant.

Cet article explique comment Microsoft Azure fournit une isolation contre les utilisateurs malveillants et non malveillants, et sert de guide pour concevoir des solutions cloud en proposant aux architectes différentes options d’isolation. Ce livre blanc se concentre sur la technologie de plateforme Azure et les contrôles de sécurité orientés client, et n’essaie pas de répondre aux considérations relatives aux SLA, aux modèles de tarification et aux pratiques DevOps.

## <a name="tenant-level-isolation"></a>Isolation au niveau du client
L’un des principaux avantages du cloud est le concept d’une infrastructure commune partagée entre plusieurs clients simultanément, ce qui conduit à des économies d’échelle. Ce concept est appelé mutualisation. Microsoft travaille en permanence pour veiller à ce que l’architecture mutualisée de Microsoft Cloud Azure prenne en charge les normes de disponibilité, d’intégrité, de confidentialité et de sécurité.

Dans le contexte du cloud, un client peut être défini comme un client ou une organisation qui possède et gère une instance spécifique de ce service cloud. Avec la plateforme d’identité fournie par Microsoft Azure, un client consiste simplement en une instance dédiée d’Azure Active Directory (Azure AD) que votre organisation reçoit et possède quand elle s’inscrit à un service cloud Microsoft.

Chaque annuaire Azure AD est distinct et indépendant des autres annuaires Azure AD. De la même manière qu’un immeuble de bureaux d’entreprise est un élément d’actif sûr propre à votre organisation, un annuaire Azure AD est également conçu pour être un élément d’actif sûr pour les seuls besoins de votre organisation. Par son architecture, Azure AD isole les données et les informations d’identité des clients, ce qui évite tout risque de brassage. Autrement dit, les utilisateurs et les administrateurs d’un annuaire Azure AD ne peuvent pas accéder aux données d’un autre annuaire par accident ou malveillance.

### <a name="azure-tenancy"></a>Location Azure
La location Azure (abonnement Azure) fait référence à une relation « client/facturation » et à un [client](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) unique dans [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). L’isolation au niveau du client dans Microsoft Azure est obtenue à l’aide d’Azure Active Directory et des [contrôles basés sur les rôles](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) qu’il propose. Chaque abonnement Azure est associé à un répertoire Azure Active Directory (AD).

Les utilisateurs, groupes et applications de ce répertoire peuvent gérer les ressources de l’abonnement Azure. Vous pouvez affecter ces droits d’accès à l’aide du portail Azure, des outils en ligne de commande Azure ou des API de gestion Azure. Un client Azure AD est logiquement isolé à l’aide de limites de sécurité afin qu’aucun client ne puisse accéder aux autres clients, ni leur nuire intentionnellement ou accidentellement. Azure AD s’exécute sur les serveurs de « systèmes nus » isolés sur un segment réseau séparé, où le filtrage de paquets au niveau de l’hôte et le pare-feu Windows bloquent le trafic et les connexions indésirables.

- L’accès aux données dans Azure AD requiert l’authentification des utilisateurs via un service d’émission de jeton de sécurité (STS). Les informations sur l’existence de l’utilisateur, l’état activé et le rôle sont utilisées par le système d’autorisation pour déterminer si l’accès demandé au client cible est autorisé pour cet utilisateur dans cette session.

![Location Azure](./media/azure-isolation/azure-isolation-fig1.png)


- Les clients sont des conteneurs discrets n’ayant aucune relation entre eux.

- Il n’existe aucun accès entre les clients, sauf si l’administrateur d’un client lui en accorde un via la fédération ou l’approvisionnement des comptes d’utilisateur d’autres clients.

- L’accès physique aux serveurs qui composent le service Azure AD et l’accès direct aux systèmes de serveur principal AD sont limités.

- Les utilisateurs d’Azure AD n’ont pas accès aux emplacements ou aux ressources physiques, et il leur est donc impossible de contourner les vérifications de stratégie RBAC logique stipulées ci-après.

Pour les diagnostics et les besoins de maintenance, un modèle opérationnel qui fait appel à un système d’élévation des privilèges immédiat est nécessaire et utilisé. Azure AD Privileged Identity Management (PIM) introduit le concept d’administrateur éligible. Les [administrateurs](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) éligibles doivent être des utilisateurs qui nécessitent un accès privilégié de temps à autres, mais pas tous les jours. Ce rôle reste inactif jusqu’à ce l’utilisateur ait besoin d’un tel accès ; dans ce cas, il complète un processus d’activation et devient administrateur actif pour une durée prédéterminée.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory héberge chaque client dans son propre conteneur protégé, avec des stratégies et des autorisations vers et dans le conteneur uniquement détenues et gérées par le client.

Le concept de conteneurs client est profondément ancré dans le service de répertoire à toutes les couches, des portails jusqu’au stockage permanent.

Même lorsque les métadonnées de plusieurs clients Azure Active Directory sont stockées sur le même disque physique, il n’existe aucune relation entre les conteneurs autres que celles définies par le service de répertoire, qui est régi par l’administrateur du client.

### <a name="azure-role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle Azure (RBAC)
Le [contrôle d’accès en fonction du rôle Azure (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) vous permet de partager des composants disponibles dans un abonnement Azure en fournissant une gestion des accès affinée pour Azure. Azure RBAC vous permet de séparer les tâches au sein de votre organisation et d’accorder les accès en fonction de ce dont les utilisateurs ont besoin pour travailler. Plutôt que de donner à tous des autorisations illimitées au sein de l’abonnement ou des ressources Azure, vous pouvez autoriser uniquement certaines actions.

Le contrôle d’accès en fonction du rôle Azure comporte trois rôles de base qui s’appliquent à tous les types de ressources :

- **Propriétaire** dispose d’un accès total à toutes les ressources, ainsi que le droit de déléguer l’accès à d’autres personnes.

- **Contributeur** peut créer et gérer tous les types de ressources Azure, mais ne peut pas accorder l’accès à d’autres personnes.

- **Lecteur** peut consulter les ressources Azure existantes.

![Contrôle d’accès en fonction du rôle Azure](./media/azure-isolation/azure-isolation-fig3.png)

Les autres rôles RBAC dans Azure permettent de gérer des ressources Azure spécifiques. Par exemple, le rôle de contributeur de machine virtuelle permet à l’utilisateur de créer et gérer des machines virtuelles. Il ne lui donne pas accès au réseau virtuel Azure, ni au sous-réseau auquel la machine virtuelle se connecte.

Les [rôles RBAC intégrés](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) répertorient les rôles disponibles dans Azure. Elle indique les opérations et l’étendue que chaque rôle intégré accorde aux utilisateurs. Si vous avez besoin de définir vos propres rôles pour un meilleur contrôle, découvrez comment créer [des rôles personnalisés dans RBAC Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Certaines autres fonctionnalités pour Azure Active Directory incluent :
- Azure AD permet l’authentification unique sur les applications SaaS, quel que soit l’endroit où elles sont hébergées. Certaines applications sont fédérées avec Azure AD, d’autres utilisent le mot de passe de l’authentification unique. Les applications fédérées peuvent également prendre en charge l’approvisionnement d’utilisateurs et la [mise au coffre des mots de passe](https://www.techopedia.com/definition/31415/password-vault).

- L’accès aux données dans [Azure Storage](https://azure.microsoft.com/services/storage/) est contrôlé via l’authentification. Chaque compte de stockage possède une clé primaire ([clé de compte de stockage](https://docs.microsoft.com/azure/storage/storage-create-storage-account) ou SAK) et une clé secrète secondaire (signature d’accès partagé ou SAP).

- Azure AD fournit l’identité en tant que service par le biais de la fédération en utilisant les [services de fédération Active Directory (AD FS)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), la synchronisation et la réplication avec les annuaires locaux.

- [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) est le service d’authentification multifacteur qui demande aux utilisateurs de vérifier les connexions à l’aide d’une application mobile, d’un appel téléphonique ou d’un message texte. Ce service est utilisable avec Azure AD afin de sécuriser les ressources locales avec le serveur Azure Multi-Factor Authentication, ainsi qu’avec des applications et annuaires personnalisés à l’aide du Kit de développement logiciel (SDK).

- [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) vous permet de joindre des machines virtuelles Azure à un domaine Active Directory sans déployer de contrôleurs de domaine. Vous pouvez vous connecter à ces machines virtuelles avec vos informations d’identification Active Directory d’entreprise, et administrer les machines virtuelles jointes au domaine en utilisant une stratégie de groupe pour appliquer des lignes de base de sécurité sur toutes vos machines virtuelles Azure.

- Pour les applications accessibles aux consommateurs, [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) fournit un service de gestion des identités global et hautement disponible, qui s’adapte à des centaines de millions d’identités. Le service peut être intégré sur l’ensemble des plateformes web et mobiles. Vos consommateurs peuvent se connecter à toutes vos applications par le biais d’expériences personnalisables en utilisant leurs comptes de réseaux sociaux existants ou en créant des informations d’identification.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Isolation des administrateurs Microsoft et suppression des données
Microsoft prend des mesures de sécurité importantes pour protéger vos données de tout accès indésirable ou de toute utilisation par des personnes non autorisées. Ces contrôles et processus opérationnels sont soutenus par les [conditions de Microsoft Online Services](http://aka.ms/Online-Services-Terms), qui proposent des engagements contractuels régissant l’accès à vos données.

-   Les ingénieurs de Microsoft ne bénéficient pas d’un accès par défaut à vos données dans le cloud. Cet accès leur est accordé, sous la supervision de la direction, uniquement lorsque cela est nécessaire. Ce dernier est attentivement contrôlé et consigné, et révoqué dès qu’il n’est plus nécessaire.

-   Microsoft peut faire appel à d’autres sociétés pour fournir des services limités en son nom. Les sous-traitants peuvent uniquement accéder aux données des clients pour fournir les services pour lesquels nous leur avons fait appel, et il leur est interdit de les utiliser à d’autres fins. En outre, ils s’engagent contractuellement à maintenir la confidentialité des données de nos clients.

Les services professionnels avec des certifications vérifiées telles que ISO/IEC 27001 sont régulièrement contrôlés par Microsoft et des entreprises d’audit agréées, qui effectuent des vérifications par échantillonnage pour attester que cet accès est réalisé uniquement à des fins professionnelles légitimes. Vous pouvez accéder à vos données client à tout moment et pour quelque raison que ce soit.

Si vous supprimez des données, Microsoft Azure supprime les données, y compris les copies mises en cache ou de sauvegarde. Pour les services dans l’étendue, cette suppression aura lieu dans les 90 jours suivant la fin de la période de rétention. (Les services dans l’étendue sont définis dans la section Data Processing Terms (Conditions relatives au traitement des données) de nos [conditions Microsoft Online Services](http://aka.ms/Online-Services-Terms).)

Si un lecteur de disque utilisé pour le stockage rencontre une défaillance matérielle, il est [effacé ou détruit](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) de façon sûre avant que Microsoft ne le renvoie au fabricant pour effectuer un remplacement ou une réparation. Les données sur le lecteur sont remplacées pour vous assurer qu’elles ne puissent pas être récupérées par quelque moyen que ce soit.

## <a name="compute-isolation"></a>Isolation du calcul
Microsoft Azure propose divers services informatiques cloud qui incluent une large sélection d’instances de calcul et de services pouvant être mis à l’échelle automatiquement pour répondre aux besoins de votre application ou de votre entreprise. Ces services et instances de calcul offrent une isolation à plusieurs niveaux pour sécuriser les données sans compromettre la flexibilité de la configuration exigée par les clients.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Isolation de systèmes d’exploitation racine et Hyper-V entre des machines virtuelles racine et des machines virtuelles invitées
La plateforme de calcul Azure repose sur la virtualisation des machines, ce qui signifie que tout le code client s’exécute dans une machine virtuelle Hyper-V. Sur chaque nœud Azure (ou point de terminaison réseau), il existe un hyperviseur qui s’exécute directement sur le matériel et divise un nœud en un nombre variable de machines virtuelles invitées.


![Isolation de systèmes d’exploitation racine et Hyper-V entre des machines virtuelles racine et des machines virtuelles invitées](./media/azure-isolation/azure-isolation-fig4.jpg)


Chaque nœud a également une machine virtuelle racine spéciale qui exécute le système d’exploitation hôte. Une limite critique correspond à l’isolation de la machine virtuelle racine des machines virtuelles invitées et entre les machines virtuelles invitées, gérée par l’hyperviseur et le système d’exploitation racine. La paire hyperviseur/système d’exploitation racine tire parti des dizaines d’années d’expérience de Microsoft en matière de sécurité des systèmes d’exploitation et des enseignements plus récents sur Hyper-V de Microsoft pour fournir une isolation renforcée des machines virtuelles invitées.

La plateforme Azure utilise un environnement virtualisé. Les instances utilisateur fonctionnent comme des machines virtuelles autonomes qui n’ont pas accès à un serveur hôte physique, et cette isolation est appliquée à l’aide des niveaux de privilège (Anneau 0/Anneau 3) de processeur physique.

L’anneau 0 est le plus privilégié, et l’anneau 3 le moins privilégié. Le système d’exploitation invité s’exécute dans un anneau 1 moins privilégié, tandis que les applications s’exécutent dans l’anneau 3, le moins privilégié. Cette virtualisation des ressources physiques entraîne une séparation claire entre le système d’exploitation invité et l’hyperviseur, ce qui donne lieu à une séparation de sécurité supplémentaire entre les deux.

L’hyperviseur d’Azure agit comme un micronoyau et transfère toutes les demandes d’accès matériel des machines virtuelles invitées vers l’hôte à des fins de traitement au moyen d’une interface de mémoire partagée appelée VMBus. Cela empêche les utilisateurs d’obtenir un accès brut en lecture/écriture/exécution au système, et réduit le risque de partage des ressources système.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Algorithme de placement de machine virtuelle avancé et protection contre les attaques par canal auxiliaire
Une attaque entre les machines virtuelles implique deux étapes : placer une machine virtuelle contrôlée par l’adversaire sur le même hôte que l’une des machines virtuelles victimes et violer la limite d’isolation pour dérober des informations sensibles à la victime ou affecter ses performances par cupidité ou vandalisme. Microsoft Azure peut vous protéger contre ces deux étapes via un algorithme de sélection de placement de machine virtuelle avancé et une protection contre toutes les attaques par canal auxiliaire connues, y compris les machines virtuelles de voisin bruyant.

### <a name="the-azure-fabric-controller"></a>Contrôleur de structure Azure
Le contrôleur de structure Azure est chargé d’allouer des ressources d’infrastructure aux charges de travail des clients, et gère les communications unidirectionnelles de l’hôte vers les machines virtuelles. L’algorithme de placement de machine virtuelle du contrôleur de structure Azure est très sophistiqué et presque impossible à prédire au niveau de l’hôte physique.

![Contrôleur de structure Azure](./media/azure-isolation/azure-isolation-fig5.png)

L’hyperviseur Azure applique la séparation de mémoire et de processus entre les machines virtuelles, et achemine en toute sécurité le trafic réseau vers les clients du système d’exploitation invité. Cela élimine la possibilité d’une attaque par canal auxiliaire au niveau de la machine virtuelle.

Dans Azure, la machine virtuelle racine est spéciale : elle exécute un système d’exploitation renforcé appelé système d’exploitation racine qui héberge un agent de structure. Les agents de structure servent à gérer les agents invités au sein des systèmes d’exploitation invités sur les machines virtuelles de client. Ils gèrent également les nœuds de stockage.

La collection d’hyperviseur Azure, d’agent de structure/de système d’exploitation racine et d’agent invité/de machines virtuelles de client comprend un nœud de calcul. Les agents de structure sont gérés par un contrôleur de structure qui se trouve en dehors des nœuds de calcul et de stockage (les clusters de calcul et de stockage sont gérés par des contrôleurs de structure distincts). Si un client met à jour le fichier de configuration de l’application pendant son exécution, le contrôleur de structure communique avec l’agent de structure, lequel contacte ensuite les agents invités qui notifient l’application de la modification apportée à la configuration. En cas de défaillance matérielle, le contrôleur de structure recherchera automatiquement le matériel disponible et redémarrera la machine virtuelle dessus.

![Contrôleur de structure Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

La communication entre un contrôleur de structure et un agent est unidirectionnelle. L’agent implémente un service protégé par SSL qui répond uniquement aux demandes du contrôleur. Il ne peut pas initier de connexions vers le contrôleur ou d’autres nœuds internes avec des privilèges. Le contrôleur de structure traite toutes les réponses comme si elles n’étaient pas approuvées.


![Contrôleur de structure](./media/azure-isolation/azure-isolation-fig7.png)

L’isolation s’étend de la machine virtuelle racine aux machines virtuelles invitées et entre les machines virtuelles invitées. Les nœuds de calcul sont également isolés des nœuds de stockage pour une protection renforcée.


L’hyperviseur et le système d’exploitation hôte fournissent des filtres de paquets réseau afin de garantir que les machines virtuelles non approuvées ne puissent pas générer de trafic falsifié ou recevoir du trafic qui ne leur est pas destiné, diriger le trafic vers les points de terminaison de l’infrastructure protégés, ou envoyer/recevoir le trafic de diffusion inapproprié.


### <a name="additional-rules-configured-by-fabric-controller-agent-to-isolate-vm"></a>Règles supplémentaires configurées par l’agent du contrôleur de structure pour isoler la machine virtuelle
Par défaut, tout le trafic est bloqué lorsqu’une machine virtuelle est créée. Ensuite, l’agent du contrôleur de structure configure le filtre de paquets pour ajouter des règles et exceptions pour laisser passer le trafic autorisé.

Il existe deux catégories de règles qui sont programmées :

-   **Règles de configuration des machines ou d’infrastructure** : par défaut, toutes les communications sont bloquées. Il existe des exceptions qui permettent d’autoriser une machine virtuelle à envoyer et recevoir le trafic DHCP et DNS. Les machines virtuelles peuvent également envoyer le trafic vers l’Internet « public » et vers d’autres machines virtuelles dans le même réseau virtuel Azure et le serveur d’activation du système d’exploitation. La liste de destinations sortantes autorisées des machines virtuelles n’inclut pas les sous-réseaux de routeur Azure, la gestion Azure, ni d’autres propriétés Microsoft.

-   **Fichier de configuration de rôle** : celui-ci définit les listes de contrôle d’accès entrant en fonction du modèle de service du client.

### <a name="vlan-isolation"></a>Isolation du VLAN
Chaque cluster comporte trois VLAN :

![Isolation du VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   Le VLAN principal, qui interconnecte les nœuds des clients non approuvés.

-   Le VLAN du contrôleur de structure, qui contient les systèmes de support et les contrôleurs de structure approuvés.

-   Le VLAN de l’appareil, qui contient les autres appareils de l’infrastructure et le réseau approuvés.

La communication du VLAN du contrôleur de structure vers le VLAN principal est autorisée, mais ne peut pas être initiée à partir du VLAN principal vers le VLAN du contrôleur de structure. La communication est également bloquée du VLAN principal vers le VLAN de l’appareil. Cela permet de s’assurer que même si un nœud qui exécute le code du client est compromis, il ne peut pas attaquer les nœuds sur les VLAN du contrôleur de structure ou de l’appareil.

## <a name="storage-isolation"></a>Isolation du stockage
### <a name="logical-isolation-between-compute-and-storage"></a>Isolation logique entre le calcul et le stockage
Dans le cadre de sa conception fondamentale, Microsoft Azure sépare le calcul basé sur les machines virtuelles du stockage. Cette séparation permet de mettre à l’échelle le calcul et le stockage de façon indépendante et ainsi de faciliter l’isolation et la mutualisation.

Par conséquent, le stockage Azure s’exécute sur un matériel distinct sans connectivité réseau au calcul Azure, sauf sous forme logique. [Cela](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) signifie que lorsqu’un disque virtuel est créé, l’espace disque n’est pas alloué pour sa capacité totale. Au lieu de cela, une table est créée et mappe les adresses sur le disque virtuel aux zones du disque physique et cette table est initialement vide. **La première fois qu’un client écrit des données sur le disque virtuel, l’espace sur le disque physique est alloué, et un pointeur vers celui-ci est placé dans la table.**
### <a name="isolation-using-storage-access-control"></a>Isolation à l’aide du contrôle d’accès de stockage
Le **contrôle d’accès dans le stockage Azure** dispose d’un modèle de contrôle d’accès simple. Chaque abonnement Azure peut créer un ou plusieurs comptes de stockage. Chaque compte de stockage a une clé secrète unique qui est utilisée pour contrôler l’accès à toutes les données dans ce compte de stockage.

![Isolation à l’aide du contrôle d’accès de stockage](./media/azure-isolation/azure-isolation-fig9.png)

**L’accès aux données de stockage Azure (y compris aux tables)** peut être contrôlé via un jeton [SAP (signature d’accès partagé)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1), qui accorde un accès étendu. La SAP est créée via un modèle de requête (URL), signé avec la [SAK (clé de compte de stockage)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Cette [URL signée](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) peut être donnée à un autre processus (c.-à-d. déléguée), qui peut ensuite renseigner les détails de la requête et l’envoyer au service de stockage. Une SAP vous permet d’accorder l’accès en fonction du temps aux clients sans révéler la clé secrète du compte de stockage.

La SAP nous permet d’accorder à un client des autorisations limitées à des objets de notre compte de stockage pendant une période donnée et avec un ensemble défini d’autorisations. Nous pouvons accorder ces autorisations limitées sans partager les clés d’accès de votre compte.

### <a name="ip-level-storage-isolation"></a>Isolation du stockage au niveau de l’adresse IP
Vous pouvez activer des pare-feu et définir une plage d’adresses IP pour vos clients approuvés. Avec une plage d’adresses IP, seuls les clients qui ont une adresse IP dans la plage définie peuvent se connecter au [stockage Azure](https://docs.microsoft.com/azure/storage/storage-security-guide).

Les données de stockage d’adresses IP peuvent être protégées des utilisateurs non autorisés via un mécanisme de mise en réseau qui est utilisé pour allouer un tunnel dédié de trafic au stockage d’adresses IP.

### <a name="encryption"></a>Chiffrement
Azure propose les types de chiffrement suivants pour protéger les données :
-   Chiffrement en transit

-   Chiffrement au repos

#### <a name="encryption-in-transit"></a>Chiffrement en transit
Le chiffrement en transit est un mécanisme de protection des données transmises sur des réseaux. Le stockage Azure vous permet de sécuriser les données à l’aide des éléments suivants :

-   Le [chiffrement au niveau du transport](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit) (HTTPS, par exemple) lorsque vous transférez des données vers ou à partir d’Azure Storage.

-   Le [chiffrement câblé](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), par exemple le chiffrement SMB 3.0 pour les partages de fichiers Azure.

-   Le [chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), pour chiffrer les données avant leur transfert vers Storage et les déchiffrer après leur transfert à partir de Storage.

#### <a name="encryption-at-rest"></a>Chiffrement au repos
Pour de nombreuses organisations, le [chiffrement des données au repos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) est une étape obligatoire du processus de gestion de la confidentialité, de la conformité et de la souveraineté des données. Trois fonctionnalités Azure fournissent un chiffrement des données « au repos ».

-   [Storage Service Encryption](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) vous permet de demander que le service de stockage chiffre automatiquement les données lors de leur écriture dans Azure Storage.

-   [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) fournit également la fonctionnalité de chiffrement au repos.

-   [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) vous permet de chiffrer les disques de données et de système d’exploitation utilisés par une machine virtuelle IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) pour les machines virtuelles vous permet de répondre aux exigences de conformité et de sécurité des organisations en chiffrant vos disques de machine virtuelle (y compris les disques d’amorçage et disques de données) avec des clés et stratégies que vous pouvez contrôler dans [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

La solution Disk Encryption pour Windows est basée sur le [chiffrement de lecteur Microsoft BitLocker](https://technet.microsoft.com/library/cc732774.aspx) et la solution Linux est basée sur le chiffrement [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

La solution prend en charge les scénarios de machines virtuelles IaaS suivants lorsqu’ils sont activés dans Microsoft Azure :
-   Prise en main d’Azure Key Vault

-   Machines virtuelles de niveau Standard : machines virtuelles IaaS des séries A, D, DS, G, GS, etc.

-   Activation du chiffrement sur les machines virtuelles IaaS Windows et Linux

-   Désactivation du chiffrement sur les systèmes d’exploitation et les lecteurs de données pour les machines virtuelles IaaS Windows

-   Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux

-   Activation du chiffrement sur les machines virtuelles IaaS exécutant le système d’exploitation client Windows

-   Activation du chiffrement sur les volumes avec chemins d’accès de montage

-   Activation du chiffrement sur les machines virtuelles Linux configurées avec entrelacement de disques (RAID) à l’aide de [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Activation du chiffrement sur les machines virtuelles Linux à l’aide de [LVM (Gestionnaire de volumes logiques)](https://msdn.microsoft.com/library/windows/desktop/bb540532) pour les disques de données

-   Activation du chiffrement sur les machines virtuelles Windows configurées à l’aide d’espaces de stockage

-   Toutes les régions publiques Azure sont prises en charge

La solution ne prend pas en charge les scénarios, fonctionnalités et technologies suivants dans la version :

-   Machines virtuelles IaaS de niveau de base

-   Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux

-   Machines virtuelles IaaS créées à l’aide de la méthode classique de création de machines virtuelles

-   Intégration à votre service de gestion de clés local

-   Azure Files (système de partage de fichiers), NFS (Network File System), volumes dynamiques et machines virtuelles Windows configurées avec des systèmes RAID logiciels

## <a name="sql-azure-database-isolation"></a>Isolation de base de données SQL Azure
SQL Database est un service de base de données relationnelle dans le cloud Microsoft, qui repose sur le moteur Microsoft SQL Server numéro un du marché, pouvant traiter des charges de travail stratégiques. SQL Database offre une isolation prévisible des données au niveau du compte, en fonction de la géographie/région et du réseau avec quasiment aucun besoin d’administration.

### <a name="sql-azure-application-model"></a>Modèle d’application SQL Azure

La base de données [Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) est un service de bases de données relationnelles sur le cloud, basé sur les technologies SQL Server. Elle propose un service de bases de données mutualisé, évolutif et hautement disponible, hébergé par Microsoft dans le cloud.

Du point de vue des applications, SQL Azure fournit la hiérarchie suivante : chaque niveau dispose d’une imbrication un-à-plusieurs pour les niveaux en dessous.

![Modèle d’application SQL Azure](./media/azure-isolation/azure-isolation-fig10.png)

Le compte et l’abonnement sont des concepts de plateforme Microsoft Azure à associer à la facturation et la gestion.

Les bases de données et serveurs logiques sont des concepts propres à SQL Azure et sont gérés à l’aide de SQL Azure, fournis par les interfaces OData et TSQL ou via le portail SQL Azure intégré au portail Azure.

Les serveurs SQL Azure ne sont pas des instances de machines virtuelles ou physiques. Ce sont en fait des collections de bases de données, de stratégies de sécurité et de gestion, qui sont stockées une base de données « master logique ».

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Les bases de données master logiques comprennent :

-   Les connexions SQL utilisées pour se connecter au serveur

-   Règles de pare-feu

Les informations relatives à l’utilisation et la facturation pour les bases de données SQL Azure du même serveur logique ne sont pas nécessairement sur la même instance physique du cluster SQL Azure. Au lieu de cela, les applications doivent fournir le nom de la base de données cible lors de la connexion.

Du point de vue du client, un serveur logique est créé dans une région géographique, tandis que la création réelle du serveur se produit dans l’un des clusters de la région.

### <a name="isolation-through-network-topology"></a>Isolation au travers de la topologie du réseau

Lorsqu’un serveur logique est créé et son nom DNS inscrit, ce dernier pointe vers « l’adresse IP virtuelle de passerelle » dans le centre de données spécifique dans lequel le serveur a été placé.

Derrière l’adresse IP virtuelle, nous avons une collection de services de passerelle sans état. En règle générale, les passerelles interviennent si une coordination est nécessaire entre plusieurs sources de données (base de données master, base de données utilisateur, etc.). Les services de passerelle implémentent les éléments suivants :
-   **Proxy de connexion TDS.** Cela inclut la localisation de la base de données utilisateur dans le cluster de serveur principal, l’implémentation de la séquence de connexion puis le transfert des paquets TDS au serveur principal et inversement.

-   **Gestion de base de données.** Cela inclut l’implémentation d’une collection de flux de travail pour effectuer des opérations de base de données CREATE/ALTER/DROP. Les opérations de base de données peuvent être appelées par des paquets TDS de détection ou des API OData explicites.

-   Opérations utilisateur/de connexion CREATE/ALTER/DROP

-   Opérations de gestion de serveur logique via des API OData

![Isolation au travers de la topologie du réseau](./media/azure-isolation/azure-isolation-fig12.png)

La couche derrière les passerelles est appelée « back-end ». C’est ici que toutes les données sont stockées dans un environnement hautement disponible. Chaque élément de données est supposé appartenir à une « partition » ou à une « unité de basculement », ayant au moins trois réplicas. Les réplicas sont stockés et répliqués par le moteur SQL Server et gérés par un système de basculement souvent appelé « structure ».

En règle générale, le système back-end ne communique pas en sortie avec d’autres systèmes pour des raisons de sécurité. Cela est réservé aux systèmes de la couche front-end (passerelle). Les machines au niveau de la passerelle ont des privilèges limités sur les machines du back-end pour réduire la surface d’attaque comme un mécanisme de défense en profondeur.

### <a name="isolation-by-machine-function-and-access"></a>Isolation par accès et fonction de machines
SQL Azure se compose de services s’exécutant sur différentes fonctions de machines. SQL Azure est divisé entre des environnement « front-end » (passerelle/gestion) et une base de données cloud « back-end », en partant du principe que le trafic entre uniquement dans le back-end, mais n’en sort pas. L’environnement front-end peut communiquer avec d’autres services du monde extérieur, et en général a uniquement des autorisations limitées dans le back-end (suffisamment pour appeler les points d’entrée qu’il doit appeler).

## <a name="networking-isolation"></a>Isolation du réseau
Le déploiement Azure comporte plusieurs couches d’isolation réseau. Le schéma suivant montre les différentes couches d’isolation réseau fournies aux clients par Azure. Ces couches sont natives à la fois sur la plateforme Azure elle-même et dans les fonctionnalités définies par le client. Issue d’Internet, la protection DDoS Azure offre une isolation contre les attaques à grande échelle menées contre Azure. Les adresses IP publiques (points de terminaison) définies par les clients constituent la couche d’isolation suivante et servent à déterminer quel trafic peut traverser le service cloud pour atteindre le réseau virtuel. L’isolement du réseau virtuel Azure natif garantit l’isolement complet de tous les autres réseaux et la circulation du trafic uniquement au moyen des méthodes et des chemins d’accès configurés par l’utilisateur. Ces chemins d’accès et méthodes constituent la couche suivante, où les groupes de sécurité réseau, le routage défini par l’utilisateur et les appliances virtuelles réseau peuvent servir à créer des limites d’isolation afin de protéger les déploiements d’applications dans le réseau protégé.

![Isolation du réseau](./media/azure-isolation/azure-isolation-fig13.png)

**Isolation du trafic** : un [réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) est la limite d’isolation du trafic sur la plateforme Azure. Les machines virtuelles dans un réseau virtuel ne peuvent pas communiquer directement avec les machines virtuelles dans un autre réseau virtuel, même si les deux réseaux virtuels sont créés par le même client. Cet isolement est une propriété critique qui garantit que les machines virtuelles et les communications du client restent privées dans un réseau virtuel.

Le [sous-réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) offre une couche d’isolation supplémentaire dans le réseau virtuel en fonction de la plage d’adresses IP. Avec la plage d’adresses IP appartenant au réseau virtuel, vous pouvez diviser un réseau virtuel en plusieurs sous-réseaux pour l’organisation et la sécurité. Les machines virtuelles et les instances de rôle PaaS déployées sur des sous-réseaux (identiques ou différents) au sein d’un réseau virtuel peuvent communiquer entre elles sans qu’il y ait besoin de configuration supplémentaire. Vous pouvez également configurer un [groupe de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) pour autoriser ou refuser le trafic réseau vers une instance de machine virtuelle en fonction des règles configurées dans la liste de contrôle d’accès du groupe de sécurité réseau. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, les règles ACL s’appliquent à toutes les instances de machine virtuelle présentes dans ce sous-réseau.

## <a name="next-steps"></a>Étapes suivantes

- [Options d’isolation du réseau pour les machines dans les réseaux virtuels Windows Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Cela inclut le scénario classique de front-end et back-end où les machines dans un réseau back-end particulier ou un sous-réseau peuvent autoriser uniquement certains clients ou d’autres ordinateurs à se connecter à un point de terminaison particulier en fonction d’une liste approuvée d’adresses IP.

- [Isolation du calcul](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure propose divers services informatiques cloud qui incluent une large sélection d’instances de calcul et de services pouvant être mis à l’échelle automatiquement pour répondre aux besoins de votre application ou de votre entreprise.

- [Isolation du stockage](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure sépare le calcul basé sur les machines virtuelles du client du stockage. Cette séparation permet de mettre à l’échelle le calcul et le stockage de façon indépendante et ainsi de faciliter l’isolation et la mutualisation. Par conséquent, le stockage Azure s’exécute sur un matériel distinct sans connectivité réseau au calcul Azure, sauf sous forme logique. Toutes les demandes s’exécutent sur HTTP ou HTTPS en fonction du choix du client.

