---
title: aaaIsolation Bonjour Cloud Public Azure | Documents Microsoft
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
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Isolation Bonjour Cloud Public Azure
##  <a name="introduction"></a>Introduction
### <a name="overview"></a>Vue d'ensemble
les clients Azure tooassist actuels et futurs comprendre et utiliser hello différentes fonctionnalités liées à la sécurité disponibles dans et environnantes hello plateforme Azure, Microsoft a développé une série de livres blancs, les vues d’ensemble de la sécurité, les meilleures pratiques, et Listes de contrôle.
les rubriques de Hello en termes de largeur et la profondeur de plage et sont régulièrement mises à jour. Ce document fait partie de cette série tel qu’indiqué dans la section abstraite hello qui suit.

### <a name="azure-platform"></a>Plateforme Azure
Azure est une plateforme de service de cloud ouverte et flexible qui prend en charge hello plus vaste choix de systèmes d’exploitation, langages de programmation, infrastructures, outils, bases de données et les appareils. Vous pouvez par exemple afficher :
- exécuter des conteneurs Linux avec l’intégration Docker ;
- créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js ; et
- créer des serveurs principaux pour les appareils iOS, Android et Windows.

Microsoft Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous générez, ou migrez des ressources informatiques à un fournisseur de services de cloud public, vous recourez tooprotect des capacités de cette organisation vos applications et données avec hello contrôles hello et les services qu’ils sécurisent toomanage hello de votre nuage ressources.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base fiable sur laquelle entreprises peuvent répondre aux besoins de leur sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de hello toomeet sécurité de vos déploiements. Ce document vous aide à répondre à ces exigences.

### <a name="abstract"></a>Résumé

Microsoft Azure vous permet de toorun applications et des machines virtuelles (VM) sur une infrastructure physique partagée. Une des applications de toorunning hello premiers motivations économiques dans un environnement de cloud est le coût de hello toodistribute hello capacité de ressources partagées entre plusieurs clients. Cette pratique de mutualisation améliore l’efficacité en multiplexant des ressources entre différents clients à faible coût. Malheureusement, il présente également le risque de hello du partage de serveurs physiques et les autres toorun de ressources d’infrastructure de vos machines virtuelles qui peuvent appartenir tooan arbitraire et potentiellement malveillant utilisateur et les applications sensibles.

Cet article décrit comment Microsoft Azure fournit une isolation contre les utilisateurs malveillants et non intentionnelle et sert un guide d’architecture des solutions de cloud computing en offrant différents tooarchitects de choix d’isolation. Ce livre blanc se concentre sur la technologie hello de plateforme Azure et les contrôles de sécurité du côté client et ne tente pas de tooaddress SLA, tarification des modèles et des considérations relatives à la pratique DevOps.

## <a name="tenant-level-isolation"></a>Isolation au niveau du client
Une des hello principaux avantages du cloud computing est le concept d’une infrastructure commune partagée entre nombreux clients simultanément, début tooeconomies de mise à l’échelle. Ce concept est appelé mutualisation. Microsoft travaille en permanence tooensure qu’architecture mutualisée de hello de Cloud de Microsoft Azure prend en charge les normes de sécurité, la confidentialité, confidentialité, intégrité et disponibilité.

En hello contexte du cloud, un client peut être défini comme un client ou d’une organisation qui possède et gère une instance spécifique de ce service cloud. Avec la plateforme d’identité hello fourni par Microsoft Azure, un client est simplement une instance dédiée d’Azure Active Directory (Azure AD) qui reçoit et possède quand elle s’inscrit à un service cloud Microsoft de votre organisation.

Chaque annuaire Azure AD est distinct et indépendant des autres annuaires Azure AD. Comme un immeuble de bureaux d’entreprise est un tooonly spécifique de ressource sécurisée de votre organisation, un annuaire Azure AD est également conçu toobe une ressource sécurisée pour une utilisation par votre entreprise. Hello architecture, Azure AD isole les informations de données et l’identité du client de brassage. Autrement dit, les utilisateurs et les administrateurs d’un annuaire Azure AD ne peuvent pas accéder aux données d’un autre annuaire par accident ou malveillance.

### <a name="azure-tenancy"></a>Location Azure
Architecture mutualisée Azure (abonnement Azure) fait référence tooa « client/facturation » relation et unique [client](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) dans [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). L’isolation au niveau du client dans Microsoft Azure est obtenue à l’aide d’Azure Active Directory et des [contrôles basés sur les rôles](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) qu’il propose. Chaque abonnement Azure est associé à un répertoire Azure Active Directory (AD).

Les utilisateurs, des groupes et des applications à partir de ce répertoire peuvent gérer des ressources Bonjour abonnement Azure. Vous pouvez affecter ces droits d’accès à l’aide des API de gestion Azure hello portail Azure et les outils de ligne de commande Azure. Un client Azure AD est logiquement isolé à l’aide de limites de sécurité afin qu’aucun client ne puisse accéder aux autres clients, ni leur nuire intentionnellement ou accidentellement. Azure AD s’exécute sur les serveurs de « systèmes nus » isolés sur un segment réseau séparé, où le filtrage de paquets au niveau de l’hôte et le pare-feu Windows bloquent le trafic et les connexions indésirables.

- Toodata d’accès dans Azure AD nécessite l’authentification des utilisateurs via un [service de jeton de sécurité (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Pour plus d’informations sur l’existence de l’utilisateur hello, état activé et rôle sont utilisés par toodetermine de système d’autorisation hello si hello accès demandé toohello cible client n’est autorisé pour cet utilisateur dans cette session.

![Location Azure](./media/azure-isolation/azure-isolation-fig1.png)


- Les clients sont des conteneurs discrets n’ayant aucune relation entre eux.

- Il n’existe aucun accès entre les clients, sauf si l’administrateur d’un client lui en accorde un via la fédération ou l’approvisionnement des comptes d’utilisateur d’autres clients.

- Tooservers accès physiques qui composent le service de hello Azure AD et les systèmes principaux tooAzure annonce un accès direct, est limitée.

- Azure AD les utilisateurs n’ont aucun accès à des ressources toophysical ou des emplacements, et par conséquent, il n’est pas possible pour les toobypass hello RBAC stratégie vérifications logiques indiquées suivant.

Pour les diagnostics et les besoins de maintenance, un modèle opérationnel qui fait appel à un système d’élévation des privilèges immédiat est nécessaire et utilisé. Azure AD Privileged Identity Management (PIM) introduit le concept de hello d’administrateur éligible. Les [administrateurs](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) éligibles doivent être des utilisateurs qui nécessitent un accès privilégié de temps à autres, mais pas tous les jours. rôle de Hello est inactif jusqu'à ce que l’utilisateur de hello requiert un accès, puis de terminer un processus d’activation et qu’il devienne un administrateur actif d’une période prédéterminée.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory héberge chaque client dans son propre conteneur protégé, avec les stratégies et aux autorisations tooand conteneur hello uniquement détenues et gérées par le client hello.

concept Hello de conteneurs de locataire est profondément ancrés dans les esprits dans le service d’annuaire hello à toutes les couches, de portails tous hello stockage toopersistent de façon.

Même lorsque les métadonnées à partir de plusieurs clients Azure Active Directory sont stockée sur hello même physique du disque, il n’existe aucune relation entre les conteneurs hello autre que celui défini par le service d’annuaire hello, qui à son tour est dictée par l’administrateur de client hello.

### <a name="azure-role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle Azure (RBAC)
[Azure contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) vous aide à vous tooshare différents composants disponibles dans un abonnement Azure en fournissant la gestion de l’accès affinée pour Azure. RBAC Azure vous permet de droits toosegregate au sein de votre organisation et accorder l’accès selon ce que les utilisateurs doivent tooperform leur travail. Plutôt que de donner à tous des autorisations illimitées au sein de l’abonnement ou des ressources Azure, vous pouvez autoriser uniquement certaines actions.

RBAC Azure a trois rôles de base qui s’appliquent à des types de ressources tooall :

- **Propriétaire** dispose des ressources de tooall un accès complet, y compris hello toodelegate droit accès tooothers.

- **Collaborateur** peut créer et gérer tous les types de ressources Azure, mais ne peut pas accorder l’accès tooothers.

- **Lecteur** peut consulter les ressources Azure existantes.

![Contrôle d’accès en fonction du rôle Azure](./media/azure-isolation/azure-isolation-fig3.png)

autres rôles RBAC hello dans Azure Hello autoriser la gestion de ressources Azure spécifiques. Par exemple, hello collaborateur d’un ordinateur virtuel permet hello utilisateur toocreate et gérer des ordinateurs virtuels. Il ne pas leur donne accès toohello réseau virtuel Azure ou sous-réseau hello hello machine virtuelle se connecte à.

[Les rôles intégrés RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) liste rôles hello disponibles dans Azure. Il spécifie les opérations hello et étendue que chaque rôle prédéfini accorde toousers. Si vous envisagez d’utiliser toodefine vos propres rôles pour encore plus de contrôle, consultez Comment toobuild [rôles personnalisés dans Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Certaines autres fonctionnalités pour Azure Active Directory incluent :
- Azure AD permet aux applications de tooSaaS de l’authentification unique, quel que soit l’endroit où elles sont hébergées. Certaines applications sont fédérées avec Azure AD, d’autres utilisent le mot de passe de l’authentification unique. Les applications fédérées peuvent également prendre en charge l’approvisionnement d’utilisateurs et la [mise au coffre des mots de passe](https://www.techopedia.com/definition/31415/password-vault).

- Toodata d’accès dans [Azure Storage](https://azure.microsoft.com/services/storage/) est contrôlé via l’authentification. Chaque compte de stockage possède une clé primaire ([clé de compte de stockage](https://docs.microsoft.com/azure/storage/storage-create-storage-account), ou SAK) et une clé secrète secondaire (signature d’accès partagé hello ou SAS).

- Azure AD fournit l’identité en tant que service par le biais de la fédération en utilisant les [services de fédération Active Directory (AD FS)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), la synchronisation et la réplication avec les annuaires locaux.

- [L’authentification multifacteur Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) est le service d’authentification multifacteur hello qui requiert des connexions utilisateurs tooverify à l’aide d’une application mobile, un appel téléphonique ou un message texte. Il peut être utilisé avec Azure AD toohelp sécurisée des ressources locales avec le serveur de l’authentification multifacteur Azure hello, ainsi qu’avec des applications personnalisées et les répertoires à l’aide du Kit de développement logiciel de hello.

- [Les Services de domaine Active Directory Azure](https://azure.microsoft.com/services/active-directory-ds/) vous permet de joindre un domaine Active Directory de tooan machines virtuelles sans déployer des contrôleurs de domaine. Vous pouvez signer dans des machines virtuelles toothese avec vos informations d’identification Active Directory d’entreprise et administrer les ordinateurs virtuels appartenant à un domaine à l’aide des lignes de base de sécurité de stratégie de groupe tooenforce sur toutes vos machines virtuelles Azure.

- [Azure B2C Active Directory](https://azure.microsoft.com/services/active-directory-b2c/) fournit un service de gestion d’identité globale hautement disponible pour les applications consommateur qui s’adapte toohundreds de millions d’identités. Le service peut être intégré sur l’ensemble des plateformes web et mobiles. Vos consommateurs peuvent se connecter tooall vos applications par le biais des expériences personnalisables à l’aide de leurs comptes sociaux existants ou en créant des informations d’identification.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Isolation des administrateurs Microsoft et suppression des données
Microsoft prend les mesures fort tooprotect vos données à partir de tout accès non autorisé ou l’utilisation par des personnes non autorisées. Ces processus opérationnels et les contrôles sont soutenues par hello [des termes du contrat de Services en ligne](http://aka.ms/Online-Services-Terms), qui offrent des engagements contractuels qui régissent l’accès aux données de tooyour.

-   Les ingénieurs de Microsoft n’ont pas de données de tooyour d’accès par défaut dans le cloud de hello. Cet accès leur est accordé, sous la supervision de la direction, uniquement lorsque cela est nécessaire. Ce dernier est attentivement contrôlé et consigné, et révoqué dès qu’il n’est plus nécessaire.

-   Microsoft peut appel à d’autres services tooprovide limitée de sociétés de sa part. Sous-traitants peuvent accéder aux données uniquement toodeliver hello technique pour lequel, nous les avons embauché tooprovide, et il est interdit de les utiliser à d’autres fins. En outre, ils sont toomaintain lié contractuellement hello confidentialité des informations de nos clients.

Services professionnels avec certifications auditées telles que la norme ISO/IEC 27001 sont régulièrement vérifiés par Microsoft et accredited audit entreprises, d’exécuter l’exemple audits tooattest cet accès, uniquement à des fins de besoins légitimes. Vous pouvez accéder à vos données client à tout moment et pour quelque raison que ce soit.

Si vous supprimez toutes les données, Microsoft Azure supprime les données hello, y compris les copies mises en cache ou de sauvegarde. Pour les services dans l’étendue, cette suppression se produit dans les 90 jours après la fin de hello de période de rétention hello. (Les services dans l’étendue sont définis dans la section des termes du contrat de traitement des données hello de notre [des termes du contrat de Services en ligne](http://aka.ms/Online-Services-Terms).)

Si un lecteur de disque utilisé pour le stockage rencontre une défaillance matérielle, il est en toute sécurité [effacées ou détruit](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) avant Microsoft retourne fabricant toohello pour un remplacement ou de réparation. Hello données hello lecteur sont remplacées tooensure qui hello de données ne peut pas être récupérée par quelque moyen que.

## <a name="compute-isolation"></a>Isolation du calcul
Microsoft Azure fournit plusieurs services en nuage informatiques qui incluent une large sélection des instances de calcul & services peuvent évoluer haut et bas automatiquement toomeet hello aux besoins de votre application ou votre entreprise. Ces service et l’instance de calcul offrent une isolation au niveau des données sur plusieurs niveaux toosecure sans sacrifier la souplesse hello dans la configuration aux demandes des utilisateurs.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Isolation de systèmes d’exploitation racine et Hyper-V entre des machines virtuelles racine et des machines virtuelles invitées
La plateforme de calcul Azure repose sur la virtualisation des machines, ce qui signifie que tout le code client s’exécute dans une machine virtuelle Hyper-V. Sur chaque nœud Azure (ou point de terminaison réseau), il existe un hyperviseur qui s’exécute directement sur le matériel de hello et divise un nœud dans un nombre variable d’ordinateurs virtuels invités (ordinateurs virtuels).


![Isolation de systèmes d’exploitation racine et Hyper-V entre des machines virtuelles racine et des machines virtuelles invitées](./media/azure-isolation/azure-isolation-fig4.jpg)


Chaque nœud a également une VM racine spécial, qui s’exécute hello du système d’exploitation hôte. Une limite critique est isolation hello de racine hello machine virtuelle à partir de l’invité hello machines virtuelles et invité hello machines virtuelles à partir d’une autre, géré par hello hyperviseur et le système d’exploitation de la racine hello. appariement d’hyperviseur/à la racine du système d’exploitation Hello tire parti des dizaines d’années de Microsoft de l’expérience de sécurité de système d’exploitation et l’apprentissage plus récente à partir Hyper-V de Microsoft, tooprovide une isolation stricte des machines virtuelles invitées.

Hello plateforme Azure utilise un environnement virtualisé. Les instances utilisateur fonctionnent comme des machines virtuelles autonomes qui n’ont pas de serveur d’accès tooa hôte physique, et l’isolation est appliquée à l’aide des niveaux de privilège de (en anneau-0/en anneau-3) de processeur physique.

Anneau 0 est hello plus privilégié et 3 hello moins. système d’exploitation invité de Hello exécute 1 moindre privilège en anneau et les applications exécutées hello moins privilégié en anneau 3. Cette virtualisation des ressources physiques conduit tooa distinction claire entre le système d’exploitation invité et l’hyperviseur, ce qui entraîne une séparation de sécurité supplémentaire entre hello deux.

Hello hyperviseur Azure agit comme un micro-noyau et passe toutes les demandes d’accès matériel à partir de l’invité virtual machines toohello hôte pour le traitement à l’aide d’une interface de mémoire partagée appelée VMBus. Cela empêche les utilisateurs d’obtenir un système de toohello l’accès en lecture/écriture/exécution brut et réduit le risque de hello du partage des ressources système.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Algorithme de placement de machine virtuelle avancé et protection contre les attaques par canal auxiliaire
Une attaque de cross-VM implique deux étapes : placer une machine virtuelle sous contrôle de code adversaire sur le même hôte qu’un des victime de hello machines virtuelles de hello et puis violer hello isolation Limite tooeither dérober des données sensibles victime ou affecte ses performances pour cupidité ou d’altération. Microsoft Azure peut vous protéger contre ces deux étapes via un algorithme de sélection de placement de machine virtuelle avancé et une protection contre toutes les attaques par canal auxiliaire connues, y compris les machines virtuelles de voisin bruyant.

### <a name="hello-azure-fabric-controller"></a>Hello contrôleur de structure Azure
Hello contrôleur de structure Azure est chargé d’allouer des ressources d’infrastructure tootenant les charges de travail, et qu’elle gère une communication unidirectionnelle à partir d’ordinateurs toovirtual hello. algorithme de placement de machine virtuelle Hello du contrôleur de structure Azure hello est toopredict très sophistiqué et pratiquement impossible en tant que le niveau de l’hôte physique.

![Hello contrôleur de structure Azure](./media/azure-isolation/azure-isolation-fig5.png)

Hello hyperviseur Azure applique la mémoire et séparation du processus entre les machines virtuelles et achemine en toute sécurité aux clients tooguest du système d’exploitation de trafic réseau. Cela élimine la possibilité d’une attaque par canal auxiliaire au niveau de la machine virtuelle.

Dans Azure, ordinateur virtuel de la racine hello est spécial : il s’exécute un système d’exploitation renforcé appelé hello racine du système d’exploitation qui héberge un agent de l’ensemble fibre optique (FA). FAs sont utilisés dans activer toomanage invité agents (GA) au sein de l’invité de systèmes d’exploitation sur des machines virtuelles de client. Ils gèrent également les nœuds de stockage.

collection d’hyperviseur Azure, Hello racine du système d’exploitation/FA, et client machines virtuelles/gaz comprend un nœud de calcul. Les agents de structure sont gérés par un contrôleur de structure qui se trouve en dehors des nœuds de calcul et de stockage (les clusters de calcul et de stockage sont gérés par des contrôleurs de structure distincts). Si un client met à jour le fichier de configuration de l’application pendant son exécution, hello FC communique avec hello FA, lequel contacte ensuite gaz, qui informe l’application hello hello modification de configuration. Dans le cas de hello d’une défaillance matérielle, hello FC matériel disponible et automatiquement redémarrer Bonjour machine virtuelle.

![Contrôleur de structure Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

Communication d’un agent tooan de contrôleur de structure est unidirectionnelle. l’agent de Hello implémente un service protégée par SSL qui ne répond qu’à partir du contrôleur de hello toorequests. Il ne peut pas lancer le contrôleur toohello de connexions ou d’autres nœuds internes privilégiés. Hello FC traite toutes les réponses comme s’ils étaient non approuvés.


![Contrôleur de structure](./media/azure-isolation/azure-isolation-fig7.png)

Isolation s’étend de hello VM racine à partir d’ordinateurs virtuels invités et hello machines virtuelles invitées à partir d’un autre. Les nœuds de calcul sont également isolés des nœuds de stockage pour une protection renforcée.


Hello hyperviseur et le système d’exploitation hôte de hello fournissent des paquets réseau - filtres toohelp vous assurer que les ordinateurs virtuels non approuvés ne peut pas générer un trafic falsifié recevoir le trafic n'adressé pas toothem, points de terminaison de diriger le trafic tooprotected infrastructure ou envoi/réception trafic de diffusion inapproprié.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Autres règles configurées par l’Agent du contrôleur Fabric tooIsolate machine virtuelle
Par défaut, tout le trafic est bloqué quand un ordinateur virtuel est créé, et l’agent du contrôleur hello fabric configure ensuite hello paquet filtre tooadd règles et les exceptions tooallow autorisé le trafic.

Il existe deux catégories de règles qui sont programmées :

-   **Règles de configuration des machines ou d’infrastructure** : par défaut, toutes les communications sont bloquées. Il est des exceptions tooallow un toosend de machine virtuelle et de recevoir du trafic DHCP et DNS. Machines virtuelles peuvent également envoyer le trafic toohello « public » internet et envoyer le trafic tooother ordinateurs virtuels au sein hello même réseau virtuel Azure et hello du serveur d’activation du système d’exploitation. liste des ordinateurs virtuels Hello des destinations sortantes autorisées n’inclut pas les sous-réseaux de routeur Azure, de gestion Azure et d’autres propriétés de Microsoft.

-   **Fichier de configuration de rôle :** définit hello entrants listes de contrôle d’accès (ACL) basées sur le modèle de service du client hello.

### <a name="vlan-isolation"></a>Isolation du VLAN
Chaque cluster comporte trois VLAN :

![Isolation du VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   réseau local virtuel principal – Hello interconnexions les nœuds clients non approuvés

-   Hello FC VLAN – contient approuvé FCs et prise en charge de systèmes

-   Hello périphérique VLAN : contient le réseau approuvé et autres périphériques d’infrastructure

La communication est autorisée à partir de toohello de réseau local virtuel FC hello réseau local virtuel principal, mais ne peut pas être lancé à partir de toohello de réseau local virtuel principal hello FC VLAN. Communication hello principal VLAN toohello du périphérique réseau local virtuel est également bloquée. Cela garantit que, même si un nœud qui exécute le code du client est compromis, il ne peut pas attaques nœuds sur hello FC ou périphérique VLAN.

## <a name="storage-isolation"></a>Isolation du stockage
### <a name="logical-isolation-between-compute-and-storage"></a>Isolation logique entre le calcul et le stockage
Dans le cadre de sa conception fondamentale, Microsoft Azure sépare le calcul basé sur les machines virtuelles du stockage. Cette séparation permet de calcul et stockage tooscale indépendamment, rendant isolation et plus facile tooprovide une architecture mutualisée.

Par conséquent, les exécutions de stockage Azure sur un ordinateur distinct avec aucune tooAzure de connectivité réseau de calcul à l’exception logiquement. [Cela](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) signifie que lorsqu’un disque virtuel est créé, l’espace disque n’est pas alloué pour sa capacité totale. Au lieu de cela, une table est créée qui mappe les adresses sur tooareas de disque virtuel hello sur le disque physique de hello et que la table est vide. **Hello la première fois qu'un client écrit des données sur le disque virtuel hello, sur le disque physique de hello est alloué, et un tooit de pointeur est placé dans la table de hello.**
### <a name="isolation-using-storage-access-control"></a>Isolation à l’aide du contrôle d’accès de stockage
Le **contrôle d’accès dans le stockage Azure** dispose d’un modèle de contrôle d’accès simple. Chaque abonnement Azure peut créer un ou plusieurs comptes de stockage. Chaque compte de stockage a une clé secrète unique d’accès utilisé toocontrol tooall des données dans ce compte de stockage.

![Isolation à l’aide du contrôle d’accès de stockage](./media/azure-isolation/azure-isolation-fig9.png)

**Accéder aux données de stockage tooAzure (y compris les Tables)** peut être contrôlé via un [SAS (Shared Access Signature)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) jeton, qui accorde l’accès d’une étendue. SAS Hello est créé via un modèle de requête (URL), signé avec hello [SAK (clé de compte de stockage)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Qui [signé URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) peut être donné tooanother processus (qui est, déléguée), qui peut ensuite remplir hello les détails de la requête de hello et demander de hello hello du service de stockage. Une SAP vous permet de toogrant accès tooclients sans révéler la clé de secret principal du compte de stockage hello.

Hello SAP signifie que nous pouvons accorder à qu'un client des autorisations limitées, tooobjects dans notre compte de stockage pour une période de temps et avec un jeu d’autorisations spécifié. Nous pouvons accorder ces autorisations limitées sans avoir tooshare vos clés d’accès de compte.

### <a name="ip-level-storage-isolation"></a>Isolation du stockage au niveau de l’adresse IP
Vous pouvez activer des pare-feu et définir une plage d’adresses IP pour vos clients approuvés. Avec une plage d’adresses IP, seuls les clients qui ont une adresse IP au sein de la plage de hello défini peuvent se connecter trop[Azure Storage](https://docs.microsoft.com/azure/storage/storage-security-guide).

Données de stockage IP peuvent être protégées contre les utilisateurs via un mécanisme de mise en réseau qui est utilisé tooallocate un tunnel dédié ou dédié de stockage de tooIP de trafic.

### <a name="encryption"></a>Chiffrement
Azure propose les types de données tooprotect de chiffrement suivants :
-   Chiffrement en transit

-   Chiffrement au repos

#### <a name="encryption-in-transit"></a>Chiffrement en transit
Le chiffrement en transit est un mécanisme de protection des données transmises sur des réseaux. Le stockage Azure vous permet de sécuriser les données à l’aide des éléments suivants :

-   Le [chiffrement au niveau du transport](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit) (HTTPS, par exemple) lorsque vous transférez des données vers ou à partir d’Azure Storage.

-   Le [chiffrement câblé](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), par exemple le chiffrement SMB 3.0 pour les partages de fichiers Azure.

-   [Le chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), les données de salutation tooencrypt avant leur transfert dans les données de stockage et toodecrypt salutation après leur transfert hors stockage.

#### <a name="encryption-at-rest"></a>Chiffrement au repos
Pour de nombreuses organisations, le [chiffrement des données au repos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) est une étape obligatoire du processus de gestion de la confidentialité, de la conformité et de la souveraineté des données. Trois fonctionnalités Azure fournissent un chiffrement des données « au repos ».

-   [Chiffrement du Service Storage](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) vous permet de toorequest que service de stockage hello chiffrer automatiquement des données lors de l’écriture de tooAzure stockage.

-   [Le chiffrement côté client](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) fournit également la fonctionnalité hello du chiffrement au repos.

-   [Le chiffrement des disques Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) vous permet des disques tooencrypt hello du système d’exploitation et des disques de données utilisées par une machine virtuelle IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) pour les machines virtuelles vous permet de répondre aux exigences de conformité et de sécurité des organisations en chiffrant vos disques de machine virtuelle (y compris les disques d’amorçage et disques de données) avec des clés et stratégies que vous pouvez contrôler dans [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Hello des solutions de chiffrement de disque pour Windows est basée sur [le chiffrement de lecteur BitLocker Microsoft](https://technet.microsoft.com/library/cc732774.aspx), et hello solution Linux est basée sur [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

solution de Hello prend en charge hello les scénarios suivants pour les machines virtuelles IaaS lorsqu’ils sont activés dans Microsoft Azure :
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

solution de Hello ne prend pas en charge hello suivant la technologie de mise en production hello, fonctionnalités et scénarios :

-   Machines virtuelles IaaS de niveau de base

-   Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux

-   Machines virtuelles IaaS qui sont créés à l’aide de la méthode de création VM hello classique

-   Intégration à votre service de gestion de clés local

-   Azure Files (système de partage de fichiers), NFS (Network File System), volumes dynamiques et machines virtuelles Windows configurées avec des systèmes RAID logiciels

## <a name="sql-azure-database-isolation"></a>Isolation de base de données SQL Azure
Base de données SQL est un service de base de données relationnelle dans le cloud de Microsoft hello en fonction de moteur de Microsoft SQL Server de pointe hello et capable de gérer des charges de travail critiques. SQL Database offre une isolation prévisible des données au niveau du compte, en fonction de la géographie/région et du réseau avec quasiment aucun besoin d’administration.

### <a name="sql-azure-application-model"></a>Modèle d’application SQL Azure

La base de données [Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) est un service de bases de données relationnelles sur le cloud, basé sur les technologies SQL Server. Elle propose un service de bases de données mutualisé, évolutif et hautement disponible, hébergé par Microsoft dans le cloud.

À partir d’une perspective d’application SQL Azure fournit hello suivant hiérarchie : à chaque niveau est la relation contenant-contenu de type un-à-plusieurs de niveaux inférieurs.

![Modèle d’application SQL Azure](./media/azure-isolation/azure-isolation-fig10.png)

abonnement et compte de hello sont Microsoft Azure plateforme concepts tooassociate facturation et gestion.

Les bases de données et serveurs logiques sont des concepts propres à SQL Azure et sont gérés à l’aide de SQL Azure, fournis par les interfaces OData et TSQL ou via le portail SQL Azure intégré au portail Azure.

Les serveurs SQL Azure ne sont pas des instances de machines virtuelles ou physiques. Ce sont en fait des collections de bases de données, de stratégies de sécurité et de gestion, qui sont stockées une base de données « master logique ».

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Les bases de données master logiques comprennent :

-   Connexions SQL utilisé tooconnect toohello server

-   Règles de pare-feu

Les informations relatives à l’utilisation et la facturation pour les bases de données SQL Azure hello même serveur logique ne sont pas garanties toobe sur hello même instance physique dans le cluster de SQL Azure, à la place les applications doivent fournir nom de base de données cible hello lors de la connexion.

Du point de vue du client, un serveur logique est créé dans une région géographique graphique lors de la création du serveur de hello hello se produit dans un des clusters hello dans la région de hello.

### <a name="isolation-through-network-topology"></a>Isolation au travers de la topologie du réseau

Lorsqu’un serveur logique est créé et son nom DNS est inscrit, hello DNS pointe toohello donc appelée adresse « Passerelle VIP » dans le centre de données spécifique hello emplacement de serveur de hello.

Derrière hello adresse IP virtuelle (adresse IP virtuelle), nous avons une collection de services de la passerelle sans état. En règle générale, les passerelles interviennent si une coordination est nécessaire entre plusieurs sources de données (base de données master, base de données utilisateur, etc.). Services de la passerelle implémentent suivant de hello :
-   **Proxy de connexion TDS.** Cela inclut la recherche de base de données utilisateur dans un cluster de serveur principal hello, l’implémentation de séquence de connexion hello et hello TDS paquets toohello principal et transfert.

-   **Gestion de base de données.** Cela inclut l’implémentation d’une collection d’opérations de base de données de flux de travail toodo CREATE/ALTER/DROP. opérations de base de données Hello peuvent être appelées par espionner les paquets TDS ou explicite APIs OData.

-   Opérations utilisateur/de connexion CREATE/ALTER/DROP

-   Opérations de gestion de serveur logique via des API OData

![Isolation au travers de la topologie du réseau](./media/azure-isolation/azure-isolation-fig12.png)

couche Hello derrière les passerelles hello est appelée « principal ». Il s’agit où toutes les données hello est stocké de manière hautement disponible. Chaque élément de données est toobelong ladite tooa « partition » ou « basculement », chacun d’eux ayant au moins trois réplicas. Les réplicas sont stockés et répliqués par le moteur SQL Server et gérés par un tooas système communément de basculement « infrastructure ».

En règle générale, hello au système principal ne communique pas les systèmes sortants tooother pour des raisons de sécurité. Il s’agit de systèmes toohello réservé dans la couche frontale (passerelle) de hello. les ordinateurs de niveau de passerelle Hello ont des privilèges sur la surface d’attaque hello principal machines toominimize hello limités comme mécanisme de défense en profondeur.

### <a name="isolation-by-machine-function-and-access"></a>Isolation par accès et fonction de machines
SQL Azure se compose de services s’exécutant sur différentes fonctions de machines. SQL Azure est divisé en « principal » de la base de données Cloud environnements et de « frontale » (/ gestion de la passerelle), avec un principe général hello qui uniquement le trafic dans back-end et pas les. environnement de front-end Hello peut communiquer toohello en dehors du monde d’autres services et en général, dispose uniquement d’autorisations limitées dans terminale hello (suffisamment toocall hello points d’entrée il tooinvoke des besoins).

## <a name="networking-isolation"></a>Isolation du réseau
Le déploiement Azure comporte plusieurs couches d’isolation réseau. Hello diagramme suivant montre différentes couches d’un isolement réseau Qu'azure fournit toocustomers. Ces couches sont natif Bonjour plateforme Azure lui-même et fonctions définies par le client. Trafic entrant à partir d’Internet de hello, DDoS de Azure fournit une isolation contre les attaques à grande échelle sur Azure. couche de suivante Hello d’isolation est définie par le client des adresses IP publiques (points de terminaison), qui sont utilisé toodetermine le trafic peut passer par le réseau virtuel de hello cloud service toohello. L’isolement du réseau virtuel Azure natif garantit l’isolement complet de tous les autres réseaux et la circulation du trafic uniquement au moyen des méthodes et des chemins d’accès configurés par l’utilisateur. Ces chemins d’accès et les méthodes sont la couche suivante hello, où les dispositifs réseau virtuel, UDR et groupes de sécurité réseau peuvent être utilisé toocreate d’isolation des limites tooprotect hello déploiements d’applications dans le réseau de hello protégé.

![Isolation du réseau](./media/azure-isolation/azure-isolation-fig13.png)

**Isolation du trafic :** A [réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) hello le trafic d’isolation limite sur hello plateforme Azure. Machines virtuelles (VM) dans un réseau virtuel ne peut pas communiquer directement tooVMs dans un réseau virtuel différent, même si les deux réseaux virtuels est créés par hello même client. Cet isolement est une propriété critique qui garantit que les machines virtuelles et les communications du client restent privées dans un réseau virtuel.

Le [sous-réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) offre une couche d’isolation supplémentaire dans le réseau virtuel en fonction de la plage d’adresses IP. Les adresses IP dans le réseau virtuel de hello, vous pouvez diviser un réseau virtuel dans plusieurs sous-réseaux pour la sécurité et d’organisation. Machines virtuelles et PaaS rôle instances déployées toosubnets (identiques ou différents) d’un réseau virtuel peuvent communiquer entre eux sans aucune configuration supplémentaire. Vous pouvez également configurer [le groupe de sécurité réseau (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow ou refuser l’instance de machine virtuelle de tooa le trafic réseau en fonction des règles configurées dans la liste de contrôle d’accès (ACL) du groupe de sécurité réseau. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau.

## <a name="next-steps"></a>Étapes suivantes

- [Options d’isolation du réseau pour les machines dans les réseaux virtuels Windows Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Cela inclut le scénario de serveurs frontaux et principaux classique hello où les ordinateurs dans un sous-réseau ou un réseau principal peuvent autoriser uniquement certains clients ou autres ordinateurs tooconnect tooa point de terminaison particulier selon une liste blanche d’adresses IP.

- [Isolation du calcul](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure fournit un divers services de calcul basé sur le cloud qui incluent une large sélection des instances de calcul et de services qui peuvent mettre à l’échelle haut et bas automatiquement toomeet hello aux besoins de votre application ou votre entreprise.

- [Isolation du stockage](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure sépare le calcul basé sur les machines virtuelles du client du stockage. Cette séparation permet de calcul et stockage tooscale indépendamment, rendant isolation et plus facile tooprovide une architecture mutualisée. Par conséquent, les exécutions de stockage Azure sur un ordinateur distinct avec aucune tooAzure de connectivité réseau de calcul à l’exception logiquement. Toutes les demandes s’exécutent sur HTTP ou HTTPS en fonction du choix du client.

