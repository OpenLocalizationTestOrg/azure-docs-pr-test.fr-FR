---
title: "sécurité de gestion à distance aaaEnhance dans Azure | Documents Microsoft"
description: "Cet article décrit les étapes permettant d’améliorer la sécurité de l’administration à distance lors de l’administration des environnements Microsoft Azure, notamment les services cloud, les machines virtuelles et les applications personnalisées."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Gestion de la sécurité dans Azure
Les abonnés Azure peuvent gérer leurs environnements cloud à partir de différents périphériques, comme les stations de travail de gestion, les ordinateurs de développement ou encore les périphériques d’utilisateurs finaux privilégiés, qui disposent d’autorisations spécifiques. Dans certains cas, les fonctions d’administration sont effectuées via le web basée sur les consoles telles que hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). Dans d’autres cas, il peut être tooAzure des connexions directes à partir des systèmes locaux réseaux privés virtuels (VPN), les Services Terminal Server, les protocoles d’application client ou (par programmation) hello API de gestion de Service Azure (SMAPI). Par ailleurs, les points de terminaison de client peuvent être joints au domaine ou isolés et non gérés, comme les tablettes ou les smartphones.

Bien que plusieurs fonctionnalités d’accès et l’administration fournissent un riche ensemble d’options, variabilité peut ajouter un déploiement de cloud tooa risque. Il peut être difficile toomanage, suivre et auditer les actions d’administration. Variabilité peut-être également introduire des menaces de sécurité via l’accès non réglementées tooclient points de terminaison qui sont utilisés pour la gestion des services de cloud computing. Les stations de travail personnelles ou communes destinées au développement et à la gestion de l’infrastructure introduisent des menaces imprévisibles, notamment avec la navigation Web (par exemple, lors d’attaques de point d’eau) ou la messagerie électronique (par exemple, ingénierie sociale et hameçonnage).

![][1]

Hello potentiel pour les attaques augmente dans ce type d’environnement, car il s’agit des stratégies de sécurité tooconstruct difficile et mécanismes tooappropriately gérer interfaces d’accès aux tooAzure (par exemple, SMAPI) à partir de points de terminaison largement variés.

### <a name="remote-management-threats"></a>Menaces liées à la gestion à distance
Attaquants tentent souvent l’accès privilégié de toogain par compromettre les informations d’identification de compte (par exemple, par le biais de force un mot de passe, hameçonnage et regrouper les informations d’identification), ou en INDUISANT les utilisateurs à exécuter du code nuisible (par exemple, de sites Web nuisibles lecteur par télécharge ou dangereux de pièces jointes). Dans un environnement cloud géré à distance, compte violations peuvent entraîner des tooan des risques accrus tooanywhere échéance, accès à tout moment.

Même avec un contrôle étroit sur des comptes d’administrateur principal, comptes d’utilisateur de niveau inférieur peuvent être faiblesses tooexploit utilisés dans la stratégie de sécurité d’un autre. Manque de formation de sécurité appropriés peut également provoquer toobreaches via leur divulgation accidentelle ou l’exposition des informations de compte.

Lorsqu’une station de travail utilisateur sert aux tâches d’administration, elle peut être compromise à de nombreux niveaux, Si un utilisateur est exploration hello web, à l’aide des outils 3e et open source ou ouverture d’un fichier de document dangereux qui contient un cheval de Troie.

En règle générale, plus les attaques ciblées qui entraîne des violations de données peut être tracé toobrowser exploits, plug-ins (par exemple, Flash, PDF, Java) et « spear phishing » (courrier électronique) sur les ordinateurs de bureau. Ces machines peut-être au niveau administratif ou tooaccess des autorisations au niveau du service live serveurs ou périphériques pour les opérations lorsqu’il est utilisé pour le développement ou la gestion d’autres ressources réseau.

### <a name="operational-security-fundamentals"></a>Principes de base pour la sécurité opérationnelle
Pour la gestion et les opérations plus sécurisé, vous pouvez réduire la surface d’attaque d’un client en réduisant le nombre de hello de points d’entrée possibles. Cette opération peut être réalisée grâce aux principes de sécurité de séparation des tâches et de répartition des environnements.

Isoler les fonctions sensibles à partir d’un autre toodecrease hello probabilité qu’une erreur au niveau d’un conduit tooa violation dans une autre. Exemples :

* Tâches d’administration ne doivent pas être combinés avec les activités qui peuvent provoquer des tooa compromis (par exemple, les programmes malveillants par courrier électronique de l’administrateur qui puis infecte un serveur d’infrastructure).
* Une station de travail utilisée pour les opérations de sensibilité élevée ne doit pas être hello même système utilisé par exemple pour hello navigation Internet à haut risque.

Réduire la surface d’attaque du système hello en supprimant des logiciels inutiles. Exemple :

* Standard d’administration, prise en charge ou station de travail de développement ne devrait pas nécessiter l’installation d’un client de messagerie ou d’autres applications de productivité si l’objectif principal de l’appareil hello est toomanage les services de cloud computing.

Les systèmes clients qui ont tooinfrastructure d’accès administrateur composants doivent être soumis toohello plus strict stratégie tooreduce des risques de sécurité. Exemples :

* Stratégies de sécurité peuvent inclure des paramètres de stratégie de groupe qui refusent l’accès Internet ouvert à partir de dispositif de hello et utilisation d’une configuration de pare-feu restrictifs.
* Utilisez des réseaux privés virtuels (VPN) de sécurité du protocole Internet (IPsec) si un accès direct est requis.
* Configurez des domaines Active Directory de gestion et de développement distincts.
* Isolez et filtrez du trafic réseau de la station de travail de gestion.
* Utilisez des logiciels anti-programme malveillant.
* Implémenter des risques de hello tooreduce l’authentification multifacteur des informations d’identification volées.

La consolidation des ressources d’accès et la suppression des points de terminaison non gérés simplifient également les tâches de gestion.

### <a name="providing-security-for-azure-remote-management"></a>Mesures de sécurité pour la gestion à distance Azure
Azure offre une sécurité des administrateurs de tooaid mécanismes qui gèrent les services cloud Azure et les machines virtuelles. Ces mécanismes sont les suivants :

* Authentification et [contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-configure.md).
* Surveillance, journalisation et audit.
* Certificats et communications chiffrées.
* Portail de gestion Web.
* Filtrage des paquets réseau.

Avec la configuration de sécurité côté client et le déploiement de centre de données d’une passerelle de gestion, il représente des données toorestrict et analyse administrateur accès toocloud applications possibles.

> [!NOTE]
> Certaines recommandations contenues dans cet article peuvent entraîner une augmentation des taux d’utilisation des données, des réseaux ou des ressources de calcul, débouchant sur des coûts de licence ou d’abonnement supplémentaires.
>
>

## <a name="hardened-workstation-for-management"></a>Station de travail renforcée pour la gestion
objectif Hello de renforcement d’une station de travail est tooeliminate tous les, mais les fonctions les plus critiques hello requis pour qu’il toooperate, rendre la surface d’attaque potentielle hello aussi petite que possible. Renforcement de la sécurité système inclut en réduisant le nombre hello de services et applications, limiter l’exécution de l’application, restriction tooonly d’accès réseau est donc nécessaire, installés et en conservant toujours une système hello toodate. En outre, une station de travail renforcée pour la gestion permet de faire la distinction entre les outils et les activités d’administration d’une part, et les autres tâches incombant à l’utilisateur final d’autre part.

Dans un environnement d’entreprise local, vous pouvez limiter la surface d’attaque hello de votre infrastructure physique via des réseaux de gestion dédiée, les salles de serveurs qui ont accès à la carte et les stations de travail qui s’exécutent sur les zones protégées du réseau de hello. Dans le cloud ou hybride modèle informatique, être soucieux sur les services de gestion sécurisée peut être plus complexe en raison d’un manque de hello de ressources de tooIT d’accès physique. L’implémentation de solutions de protection nécessite une configuration logicielle soignée, des processus axés sur la sécurité et des stratégies exhaustives.

À l’aide d’un encombrement logiciel réduite de privilèges dans une station de travail verrouillée pour la gestion de cloud et pour le développement d’applications, peut réduire les risques hello des incidents de sécurité en adoptant des environnements de développement et la gestion à distance hello. Une configuration de sécurité renforcée de station de travail peut empêcher le compromis hello de comptes qui sont des ressources de cloud critique toomanage utilisé par la fermeture de divers moyens courants utilisés par les programmes malveillants et les attaques. En particulier, vous pouvez utiliser [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) et toocontrol de la technologie Hyper-V et isoler le comportement du système client et d’atténuer les menaces, y compris le courrier électronique ou la navigation sur Internet.

Sur une station de travail renforcée, hello administratrice un compte d’utilisateur standard (ce qui bloque l’exécution de niveau administrateur) et les applications associées sont contrôlées par une liste verte. éléments de base de Hello d’une station de travail renforcée sont les suivantes :

* Analyse et mise à jour corrective actives. Déployer des logiciels anti-programme malveillant, effectuer des analyses régulières vulnérabilité et mettre à jour toutes les stations de travail à l’aide de la mise à jour de sécurité plus récente hello en temps voulu.
* Fonctionnalités limitées. Désinstallez toutes les applications qui ne sont pas nécessaires et désactivez les services inutiles (démarrage).
* Renforcement du réseau. Utilisez le pare-feu Windows règles tooallow uniquement des adresses IP valides, les ports et les URL associées tooAzure management. Vérifiez que cette station de travail toohello des connexions à distance entrantes sont également bloqués.
* Restriction d’exécution. Autoriser uniquement un ensemble de fichiers exécutables prédéfinis qui sont nécessaires pour la gestion toorun (appelée tooas « de refus par défaut »). Par défaut, les utilisateurs doivent être autorisation refusées toorun un programme, sauf si elle est explicitement définie dans hello de liste verte.
* Séparation des privilèges. Gestion des utilisateurs de station de travail n’a pas doivent avoir des privilèges d’administration sur l’ordinateur local de hello lui-même. De cette manière, ils ne peuvent pas modifier configuration hello du système ou des fichiers de système de hello, intentionnellement ou non.

Vous pouvez appliquer tout cela à l’aide de [les objets de stratégie de groupe](https://www.microsoft.com/download/details.aspx?id=2612) (GPO) dans les Services de domaine Active Directory (AD DS) et les appliquer à vos comptes de gestion de gestion (local) domaine tooall.

### <a name="managing-services-applications-and-data"></a>Gestion des services, des applications et des données
Configuration des services cloud Azure est effectuée via hello portail Azure ou SMAPI, via l’interface de ligne de commande Windows PowerShell hello ou une application personnalisée qui tire parti de ces interfaces RESTful. Azure Active Directory (Azure AD), Azure Storage, les sites Web Azure et Azure Virtual Network font partie des services qui utilisent ces mécanismes.

Les applications déployées – l’ordinateur virtuel fournissent leurs propres outils clients et les interfaces en fonction des besoins, par exemple hello Microsoft Management Console (MMC), une console de gestion d’entreprise (par exemple, Microsoft System Center ou Windows Intune) ou la gestion d’un autre application : Microsoft SQL Server Management Studio, par exemple. Ces outils se trouvent généralement dans un environnement d’entreprise ou sur un réseau client. Ils peuvent dépendre de protocoles réseau spécifiques, comme le protocole RDP (Remote Desktop Protocol), qui nécessitent des connexions directes avec état. Certains peuvent avoir des interfaces web compatible qui ne doivent pas être ouvertement publiés ou accessibles via Internet de hello.

Vous pouvez restreindre l’accès tooinfrastructure et la plateforme de gestion des services dans Azure à l’aide de [l’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication.md), [certificats de gestion X.509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)et les règles de pare-feu. Hello portail Azure et SMAPI requièrent la sécurité TLS (Transport Layer). Toutefois, les services et applications que vous déployez dans Azure vous obliger les mesures de protection tootake qui sont appropriées en fonction de votre application. Ces opérations sont souvent plus faciles avec une station de travail renforcée normalisée.

### <a name="management-gateway"></a>Passerelle de gestion
toocentralize administration tous les accès et simplifier la surveillance et la journalisation, vous pouvez déployer une dédiée [passerelle Bureau à distance](https://technet.microsoft.com/library/dd560672) server (passerelle Bureau à distance) dans votre site réseau, connecté tooyour environnement Azure.

Une passerelle des services Bureau à distance désigne un service de proxy RDP basé sur une stratégie et qui met en application des exigences de sécurité. L’implémentation d’une passerelle des services Bureau à distance avec la protection d’accès réseau (NAP) Windows Server garantit que seuls les clients répondant aux critères d’intégrité de la sécurité établis par les objets de stratégie de groupe des services de domaine Active Directory (AD DS) peuvent se connecter. Par ailleurs :

* Configurer un [certificat de gestion Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) sur hello passerelle Bureau à distance afin qu’il soit hello uniquement autorisée de l’hôte tooaccess hello portail Azure.
* Jointure toohello de passerelle Bureau à distance hello même [domaine de gestion](http://technet.microsoft.com/library/bb727085.aspx) comme hello stations de travail administrateur. Cela est nécessaire lorsque vous utilisez un VPN IPsec de site à site ou ExpressRoute au sein d’un domaine qui entretient une tooAzure d’approbation à sens unique Active Directory, ou si vous vous fédérez des informations d’identification entre vos locaux instance des services AD DS et Azure AD.
* Configurer un [stratégie d’autorisation de connexion client](http://technet.microsoft.com/library/cc753324.aspx) toolet hello passerelle Bureau à distance Vérifiez que nom de l’ordinateur client hello est valid (joint au domaine) et tooaccess autorisées hello portail Azure.
* Utilisez IPsec pour [VPN Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther protéger le trafic de gestion contre le vol d’écoute clandestine et jetons, ou envisager d’un lien Internet isolé via [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* Activez l’authentification multifacteur (grâce à [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) ou l’authentification par carte à puce pour les administrateurs qui se connectent au moyen de la passerelle des services Bureau à distance.
* Configurer la source de [restrictions par adresse IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) ou [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) dans nombre de hello toominimize Azure de points de terminaison de gestion autorisés.

## <a name="security-guidelines"></a>Conseils de sécurité
En général, aidant les stations de travail toosecure administrateur pour une utilisation avec le cloud de hello est similaire toohello pratiques utilisées pour toute station de travail locale : réduite, par exemple, la build et des autorisations restrictives. Certains aspects uniques de gestion du cloud sont plus analogue tooremote ou la gestion hors bande. Celles-ci incluent hello utilisation et l’audit des informations d’identification, un accès à distance sécurisé et la détection des menaces et de réponse.

### <a name="authentication"></a>Authentification
Vous pouvez utiliser des adresses IP sources d’ouverture de session Azure restrictions tooconstrain pour accéder aux outils d’administration et les demandes d’accès de l’audit. toohelp Azure identifier gestion les clients (stations de travail et/ou les applications), vous pouvez configurer SMAPI (via développées par les clients des outils tels que des applets de commande Windows PowerShell) et toobe de certificats côté client Gestion hello toorequire portail Azure en outre tooSSL les certificats installés. Il est vivement recommandé d’exiger l’application de l’authentification multifacteur pour tous les accès administrateur.

Certaines applications ou certains services déployés dans Azure peuvent avoir leurs propres mécanismes d’authentification pour l’accès utilisateur ou administrateur, tandis que d’autres tirent pleinement avantage d’Azure AD. Selon si vous vous fédérez les informations d’identification via les Services de fédération Active Directory (AD FS), à l’aide de la synchronisation d’annuaire ou de la gestion des comptes d’utilisateur uniquement dans hello de cloud computing, à l’aide de [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (qui fait partie de Azure AD Premium) vous permet de gérer les cycles de vie des identités entre les ressources de hello.

### <a name="connectivity"></a>Connectivité
Plusieurs mécanismes est tooyour de connexions clientes sécurisées toohelp disponible des réseaux virtuels Azure. Deux de ces mécanismes, [VPN de site à site](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) et [point-to-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), activer l’utilisation de hello du secteur IPsec standard (S2S) ou hello [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) pour le chiffrement et le tunneling. Lorsque Azure se connecte gestion toopublic gérer des services Azure tels que hello portail Azure, Azure nécessite Hypertext Transfer protocole HTTPS (Secure).

Une station de travail renforcée autonome qui ne se connecte pas via une passerelle Bureau à distance tooAzure utilisez hello basé sur SSTP point-to-site VPN toocreate hello connexion initiale toohello réseau virtuel Azure et puis établir tooindividual de connexion RDP virtuel machines à partir de tunnel VPN de hello.

### <a name="management-auditing-vs-policy-enforcement"></a>Audit de gestion et application de stratégies
Il existe deux approches pour aider le processus de gestion toosecure : mise en œuvre de l’audit et la stratégie. Ces deux approches offrent un contrôle complet, mais il n’est pas toujours possible de les utiliser. En outre, chaque approche présente les différents niveaux de risque, le coût et effort associées à la gestion de la sécurité, notamment en matière de niveau de toohello de confiance de personnes et les architectures de système.

Surveillance, la journalisation et audit fournissent une base pour le suivi et la présentation des activités d’administration, mais il peut être pas toujours possible tooaudit toutes les actions de terminer le détail due toohello de données générées. L’audit de l’efficacité des stratégies de gestion hello hello n’est cependant recommandé.

L’application de stratégies incluant des contrôles d’accès stricts permet d’instaurer des mécanismes de programmation afin de régir les actions d’administration, et elle garantit l’utilisation de toutes les mesures de protection disponibles. Journalisation fournit la preuve de l’application, dans l’enregistrement de tooa d’addition qui a fait quoi, où et quand. Journalisation également vous permet de tooaudit et crosscheck plus d’informations sur la façon dont les administrateurs respectent les stratégies, et fournit une preuve d’activités

## <a name="client-configuration"></a>Configuration de client
Nous recommandons trois configurations principales pour une station de travail renforcée. atouts majeurs de Hello entre eux sont coût, facilité d’utilisation et l’accessibilité, tout en conservant un profil de sécurité similaire sur toutes les options. Hello tableau suivant fournit une analyse courte de tooeach avantages et les risques de hello. (Notez que « PC d’entreprise » fait référence à tooa PC configuration de bureau standard qui est déployée pour tous les utilisateurs de domaine, quel que soit les rôles).

| Configuration | Avantages | Inconvénients |
| --- | --- | --- |
| Station de travail renforcée autonome |Station de travail étroitement contrôlée |Coût plus élevé pour les stations de travail dédiées |
| - | Réduction des risques d’exploitation de l’application |Efforts de gestion accrus |
| - | Séparation nette des responsabilités | - |
| PC d’entreprise servant de machine virtuelle |Réduction des coûts matériels | - |
| - | Séparation des rôles et des applications | - |
| Toogo Windows avec le chiffrement de lecteur BitLocker |Compatibilité avec la plupart des ordinateurs |Suivi des ressources |
| - | Rentabilité et portabilité | - |
| - | Environnement de gestion isolé |- |

Il est important que hello renforcée station de travail est hôte de hello et pas hello invité, sans rien entre hello hôte matériel de hello et de système d’exploitation. Suivant hello « principe source propre » (également appelé « origine sécurisée ») signifie que cet hôte hello doit être hello plus renforcé. Sinon, hello renforcée station de travail (invité) est tooattacks sujet sur système hello sur lequel il est hébergé.

Vous pouvez isoler davantage de fonctions d’administration par le biais des images de système dédié pour chaque station de travail renforcée qui ont uniquement des outils hello et des autorisations nécessitent pour la gestion des sélectionnez Azure cloud des applications, avec local AD DS objets GPO pour hello tâches nécessaires.

Pour les environnements informatiques sans infrastructure locale (par exemple, aucun accès tooa local de domaine Active Directory de l’instance de stratégie de groupe, car tous les serveurs sont dans le cloud de hello), un service comme [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) peut simplifier de déploiement et de gestion configurations de station de travail.

### <a name="stand-alone-hardened-workstation-for-management"></a>Station de travail renforcée autonome pour la gestion
Avec une station de travail renforcée autonome, les administrateurs disposent d’un ordinateur de bureau ou d’un ordinateur portable pour les tâches d’administration, et d’un autre ordinateur de bureau ou ordinateur portable pour les tâches restantes. Un toomanaging de station de travail dédiée vos services Azure ne nécessite pas d’autres applications installées. En outre, l’utilisation de stations de travail compatibles avec le [Module de plateforme sécurisée](https://technet.microsoft.com/library/cc766159) (TPM) ou une technologie de chiffrement matériel similaire permet d’authentifier les appareils et empêche certaines attaques. Module de plateforme sécurisée permettre prennent également en charge la protection complète de volume du lecteur de système de hello à l’aide de [le chiffrement de lecteur BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

Dans le scénario de station de travail autonome renforcé hello (voir ci-dessous), instance locale de hello du pare-feu Windows (ou un pare-feu non Microsoft client) est configuré tooblock connexions, telles que RDP entrantes. administrateur de Hello peut ouvrir une session toohello renforcée station de travail et de démarrer une session RDP qui se connecte tooAzure après l’établissement d’un VPN de se connecter à un réseau virtuel Azure, mais ne peut pas ouvrir une session tooa d’entreprise PC et utilisez RDP tooconnect toohello renforcés de station de travail lui-même.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>PC d’entreprise servant de machine virtuelle
Dans les cas où une station de travail renforcée autonome distincte est coût prohibitif ou pas pratique, hello renforcée station de travail peut héberger une machine virtuelle tooperform des tâches non administratives.

![][3]

tooavoid plusieurs risques de sécurité qui peuvent survenir à partir d’à l’aide d’une station de travail pour la gestion des systèmes et d’autres tâches quotidiennes, vous pouvez déployer un toohello d’ordinateur virtuel Hyper-V Windows renforcé station de travail. Cet ordinateur virtuel peut être utilisé comme hello PC d’entreprise. environnement de PC d’entreprise Hello peut rester isolée hello hôte, ce qui réduit la surface d’attaque et supprime des activités quotidiennes de l’utilisateur hello (par exemple, courrier électronique) à partir de la coexistence avec des tâches d’administration sensibles.

machine virtuelle PC d’entreprise de Hello s’exécute dans un espace protégé et fournit des applications utilisateur. hôte de Hello reste une « nouvelle source » et applique les stratégies de réseau strict dans le système d’exploitation de racine hello (par exemple, blocage RDP de l’accès à partir de l’ordinateur virtuel de hello).

### <a name="windows-toogo"></a>Windows tooGo
Toorequiring autre un autre une station de travail renforcée autonome est toouse un [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) lecteur, une fonctionnalité qui prend en charge une fonctionnalité de démarrage USB côté client. Windows tooGo permet aux utilisateurs tooboot un PC compatible tooan isolé image du système en cours d’exécution à partir d’un lecteur flash USB chiffré. Il fournit des contrôles supplémentaires pour les points de terminaison de l’administration à distance, car l’image de hello pouvant être entièrement géré par un groupe informatique d’entreprise, avec les stratégies de sécurité strictes, une build du système d’exploitation minimale, et prend en charge du module de plateforme sécurisée.

Dans la figure hello ci-dessous, image portable de hello est un système de joint au domaine tooAzure uniquement de tooconnect préconfigurés, requiert l’authentification multifacteur, et bloque tout le trafic de gestion non. Si un utilisateur des démarrages hello même image d’entreprise standard toohello de PC et essaie de l’accès à la passerelle Bureau à distance pour les outils de gestion Azure, la session de hello est bloquée. Windows tooGo devient hello racine-système d’exploitation et des couches supplémentaires sont requis (hôte de système d’exploitation, hyperviseur, machine virtuelle) qui peut être encore plus vulnérables aux attaques de toooutside.

![][4]

Il est important toonote que les disques mémoire flash USB sont perdues plus facilement à un PC de bureau moyenne. Utilisation de BitLocker tooencrypt hello volume complet, avec un mot de passe fort rend moins probable qu’un attaquant peut utiliser image du lecteur hello à des fins nuisibles. En outre, en cas de perte de hello disque mémoire flash USB, révocation et [émettre un nouveau certificat de gestion](https://technet.microsoft.com/library/hh831574.aspx) avec un mot de passe rapide réinitialisation peut réduire les risques. Journaux d’audit d’administration résident dans Azure, pas sur le client hello, ce qui réduit encore la perte potentielle de données.

## <a name="best-practices"></a>Meilleures pratiques
Envisagez de hello suivant les recommandations supplémentaires lorsque vous gérez des applications et des données dans Azure.

### <a name="dos-and-donts"></a>Choses à faire et à ne pas faire
Ne supposez pas qu’une station de travail a été verrouillée qu’autres exigences de sécurité courantes n’est pas nécessitent toobe remplie. risque potentiel de Hello est plus élevé en raison des niveaux d’accès avec élévation de privilèges qui possèdent généralement des comptes d’administrateur. Exemples de risques et leur sécurité autre sont présentés dans le tableau hello ci-dessous.

| À ne pas faire | À faire |
| --- | --- |
| N’envoyez pas d’informations d’identification administrateur ou d’autres informations sensibles (par exemple, certificats SSL ou certificats de gestion) par courrier électronique. |Préservez la confidentialité des données en fournissant oralement les noms et les mots de passe de compte (sans les stocker dans la messagerie vocale), installez les certificats client/serveur à distance (par le biais d’une session chiffrée), effectuez des téléchargements à partir d’un partage réseau protégé ou procédez à une distribution manuelle au moyen de supports amovibles. |
| - | Gérez de manière proactive les cycles de vie de votre certificat de gestion. |
| Ne stockez pas de mots de passe non chiffrés ou non hachés dans le système de stockage de l’application (feuilles de calcul, sites SharePoint, partages de fichiers, etc.). |Établir des principes de sécurité de gestion et de système de sécurisation renforcée des stratégies et les appliquer l’environnement de développement tooyour. |
| - | Utilisez [améliorée atténuation expérience Toolkit 5.5](https://technet.microsoft.com/security/jj653751) épinglage de certificat règles des sites SSL/TLS tooAzure tooensure accès approprié. |
| Ne partagez pas de comptes ni de mots de passe entre plusieurs administrateurs, et ne réutilisez pas les mots de passe sur plusieurs comptes d’utilisateur ou services, notamment pour les médias sociaux ou d’autres activités non administratives. |Créer un toomanage de compte Microsoft dédié à votre abonnement Azure, un compte qui n’est pas utilisé pour les adresses e-mail personnelles. |
| N’envoyez pas de fichiers de configuration par courrier électronique. |Les profils et les fichiers de configuration doivent être installés à partir d’une source approuvée (par exemple, lecteur flash USB chiffré), et non à partir d’un mécanisme qui peut être facilement compromis, comme le courrier électronique. |
| N’utilisez pas de mots de passe d’ouverture de session trop simples ou trop faibles. |Appliquez des stratégies de mot de passe fort, des cycles d’expiration (modification à la première utilisation), des délais d’expiration de la console et l’automatisation des verrouillages de compte. Utilisez un système de gestion de mot de passe client compatible avec l’authentification multifacteur pour l’accès par mot de passe. |
| N’exposent pas toohello de ports de gestion Internet. |Verrouiller les ports Azure et l’accès à la gestion toorestrict des adresses IP. Pour plus d’informations, consultez hello [de sécurité réseau Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) livre blanc. |
| - | Utilisez des pare-feu, des réseaux privés virtuels et une protection d’accès réseau pour toutes les connexions de gestion. |

## <a name="azure-operations"></a>Opérations Azure
Dans le cadre du fonctionnement de la technologie Azure, les ingénieurs d’exploitation et le support technique qui peuvent accéder aux systèmes de production Azure utilisent [des stations de travail PC renforcées avec des machines virtuelles](#stand-alone-hardened-workstation-for-management) configurées pour autoriser un accès au réseau d’entreprise interne et aux applications (courrier électronique, intranet, etc.). Tous les ordinateurs de station de travail de gestion disposent de TPM, lecteur de démarrage hôte hello est chiffré avec BitLocker et ils sont joints tooa spécial unité d’organisation (UO) dans principal de domaine d’entreprise de Microsoft.

Le renforcement du système est mis en application au travers de la stratégie de groupe, avec la centralisation des mises à jour logicielles. Pour l’audit et l’analyse, les journaux des événements (par exemple, la sécurité et AppLocker) sont collectées à partir de stations de travail de gestion et enregistrés tooa point central.

En outre, dédiés jump-boîtes sur le réseau de Microsoft qui nécessitent l’authentification à deux facteurs sont réseau de production de tooAzure tooconnect utilisé.

## <a name="azure-security-checklist"></a>Liste de contrôle de sécurité Azure
En réduisant le nombre de hello de tâches que les administrateurs peuvent effectuer sur une station de travail renforcée permet de réduire la surface d’attaque hello dans votre environnement de gestion et de développement. Hello utilisation suivant technologies toohelp protéger votre station de travail renforcée :

* Renforcement d’Internet Explorer. navigateur Internet Explorer Hello (ou n’importe quel navigateur web, dans notre exemple) est un point d’entrée de clé pour le code nuisible d’échéance tooits des interactions très bien avec les serveurs externes. Passez en revue vos stratégies de clients et optez pour un mode protégé, la désactivation des modules complémentaires, la désactivation des téléchargements de fichiers et le filtrage [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Assurez-vous que les avertissements de sécurité s’affichent correctement. Utilisez les zones Internet et créez une liste de sites de confiance pour lesquels vous avez configuré un renforcement raisonnable. Bloquez tous les autres sites et le code intégré du navigateur, comme les contrôles ActiveX et Java.
* Utilisateur standard. En cours d’exécution comme un utilisateur standard offre un certain nombre d’avantages, hello majeurs qui est que le vol d’informations d’identification de l’administrateur via les programmes malveillants devient plus difficile. En outre, un compte d’utilisateur standard ne dispose pas des privilèges élevés sur le système d’exploitation de racine hello et plusieurs API et les options de configuration est verrouillés par défaut.
* AppLocker. Vous pouvez utiliser [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello programmes et les scripts que les utilisateurs peuvent exécuter. Vous pouvez utiliser AppLocker en mode d’audit ou d’application. Par défaut, AppLocker a une règle d’autorisation qui permet aux utilisateurs qui ont un toorun jeton admin tout le code sur le client de hello. Cette règle existe tooprevent des administrateurs de verrouiller eux-mêmes, et elle s’applique uniquement les jetons tooelevated. Consultez également l’intégrité du code dans le cadre de la [sécurité de base](http://technet.microsoft.com/library/dd348705.aspx) Windows Server.
* Signature de code. La signature de code pour tous les scripts et les outils utilisés par les administrateurs offre un moyen simple de déployer des stratégies de verrouillage d’application. Hachages n’évoluent pas avec le code de toohello de modifications rapides et les chemins d’accès ne fournissent pas un niveau élevé de sécurité. Vous devez combiner des règles AppLocker avec un PowerShell [stratégie d’exécution](http://technet.microsoft.com/library/ee176961.aspx) qui seulement permet au code signé spécifique et des scripts toobe [exécutée](http://technet.microsoft.com/library/hh849812.aspx).
* Stratégie de groupe. Créer une stratégie d’administration globale qui est appliqué tooany domaine station de travail qui est utilisée pour la gestion (et de bloquer l’accès à partir de tous les autres) et toouser comptes authentifiés sur ces stations de travail.
* Approvisionnement plus sécurisé. Protéger votre image de la station de travail renforcés de ligne de base toohelp protéger contre la falsification. Utiliser des mesures de sécurité telles que le chiffrement et les images de toostore d’isolation, les ordinateurs virtuels et les scripts et restreindre l’accès (peut-être utiliser une auditée-dans/extraction process).
* Mise à jour corrective. Maintenir une cohérence build (ou avoir des images distinctes pour le développement, les opérations et les autres tâches d’administration), analyse de modifications et les logiciels malveillants régulièrement, conserver l’accumulation hello toodate et activer uniquement les ordinateurs lorsqu’ils sont nécessaires.
* Chiffrement. Assurez-vous que les stations de travail administration ont un toomore de module de plateforme sécurisée active de manière sécurisée [système de fichiers EFS](https://technet.microsoft.com/library/cc700811.aspx) (Encrypting File System) et de BitLocker. Si vous utilisez Windows tooGo, utilisez uniquement des clés USB chiffrés avec BitLocker.
* Gouvernance. Utilisez toocontrol de stratégie de groupe AD DS Windows de tous les administrateurs hello interfaces, telles que le partage de fichiers. Incluez les stations de travail de gestion dans l’audit, la surveillance et la journalisation. Effectuez le suivi des accès et de l’utilisation au niveau administrateur et développeur.

## <a name="summary"></a>Résumé
Une station de travail renforcée pour l’administration de vos services cloud Azure, de vos machines virtuelles et de vos applications peut vous aider à lutter contre de nombreux risques et des menaces découlant de la gestion à distance de l’infrastructure informatique critique. Azure et Windows fournissent les mécanismes que vous pouvez employer toohelp protéger et contrôlent le comportement de communications, l’authentification et client.

## <a name="next-steps"></a>Étapes suivantes
Hello ressources suivantes sont disponible tooprovide plus d’informations sur Azure et les services de Microsoft, dans les éléments de toospecific plus référencés dans ce document :

* [Sécurisation de l’accès privilégié](https://technet.microsoft.com/library/mt631194.aspx) – obtenir des détails techniques hello pour concevoir et créer une station de travail d’administration sécurisée pour la gestion de Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) - en savoir plus sur les fonctionnalités de plateforme Windows Azure hello de protéger l’infrastructure Azure et hello les charges de travail qui s’exécutent sur Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) --où des failles de sécurité de Microsoft, y compris les problèmes avec Azure, peuvent être signalées ou par courrier électronique trop[secure@microsoft.com](mailto:secure@microsoft.com)
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) – suivre toodate sur hello plus récente en mode de sécurité Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
