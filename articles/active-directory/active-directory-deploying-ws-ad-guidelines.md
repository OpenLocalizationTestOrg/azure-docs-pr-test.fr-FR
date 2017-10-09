---
title: "aaaGuidelines de déploiement de Windows Server Active Directory sur des Machines virtuelles Azure | Documents Microsoft"
description: Si vous savez comment les Services de domaine Active Directory de toodeploy et Active Directory Federation Services local, apprendre comment ils fonctionnent sur des machines virtuelles.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Recommandations en matière de déploiement de Windows Server Active Directory sur des machines virtuelles Windows Azure
Cet article explique les différences importantes de hello entre les Services de fédération Active Directory (AD FS) sur site ou de les déployer sur les machines virtuelles Microsoft Azure et de déploiement Windows Server Active Directory domaine Services (AD DS).

## <a name="scope-and-audience"></a>Portée et public ciblé
article de Hello est destiné aux utilisateurs familiers de déployer Active Directory local. Elle traite des différences hello entre le déploiement sur Microsoft Azure virtual machines/réseaux virtuels et les déploiements d’Active Directory locaux traditionnels d’Active Directory. Machines virtuelles et des réseaux virtuels Azure font partie d’un Infrastructure-as-a-Service (IaaS) pour tooleverage aux organisations informatiques des ressources de cloud de hello.

Pour ceux qui ne sont pas familiarisés avec le déploiement d’Active Directory, consultez hello [Guide de déploiement d’AD DS](https://technet.microsoft.com/library/cc753963) ou [planifier votre déploiement AD FS](https://technet.microsoft.com/library/dn151324.aspx) selon le cas.

Cet article suppose que hello lecteur connaît hello suivant concepts :

* Déploiement et gestion de Windows Server AD DS
* Déploiement et configuration de l’infrastructure de toosupport un domaine Active Directory DNS
* Déploiement et gestion de Windows Server AD FS
* Déploiement, configuration et gestion des applications par partie de confiance (sites et services web) qui consomment des jetons Windows Server AD FS
* Concepts générales d’une machine virtuelle, par exemple comment tooconfigure a virtual machine, virtuel des disques et des réseaux virtuels

Cet article met en évidence les exigences de hello pour un scénario de déploiement hybride dans lequel les services de Windows Server AD DS ou AD FS sont en partie déployés localement et en partie déploiement sur des machines virtuelles. Hello examine d’abord les différences critiques hello entre l’exécution de Windows Server AD DS et AD FS sur des machines virtuelles Azure et locaux et les points de décision importante qui affectent la conception et déploiement. rest Hello de papier hello explique des recommandations pour chacun des points de décision hello dans plus de détails, et comment tooapply hello les scénarios de déploiement toovarious des recommandations.

Cet article ne traite pas de configuration hello de [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), qui est un service basé sur REST qui fournit des fonctionnalités de contrôle d’accès et de gestion identité pour les applications cloud. Azure Active Directory (Azure AD) et Windows Server AD DS sont, toutefois, tooprovide ensemble de toowork conçu une solution de gestion des identités et des accès pour informatiques hybrides environnements et des applications modernes. toohelp comprendre les différences de hello et les relations entre Windows Server AD DS et Azure AD, tenez compte hello qui suit :

1. Vous pouvez exécuter Windows Server AD DS dans le cloud de hello sur des machines virtuelles lorsque vous utilisez Azure tooextend votre centre de données local dans le cloud de hello.
2. Vous pouvez utiliser Azure AD toogive vos applications d’unique authentification tooSoftware-as-a-Service (SaaS) des utilisateurs. Microsoft Office 365, par exemple, fait appel à cette technologie, et les applications exécutées sous Azure ou d’autres plateformes cloud peuvent également y recourir.
3. Vous pouvez utiliser Azure AD (son Service Access Control) toolet utilisateur se connecte en utilisant des identités à partir de Facebook, Google, Microsoft et d’autres tooapplications de fournisseurs d’identité qui sont hébergées dans le cloud de hello ou localement.

Pour plus d’informations sur ces différences, consultez l’article [Principes de base de la gestion des identités Azure](fundamentals-identity.md).

## <a name="related-resources"></a>Ressources associées
Vous pouvez télécharger et exécuter hello [Azure Virtual Machine Readiness Assessment](https://www.microsoft.com/download/details.aspx?id=40898). Hello évaluation automatiquement examiner votre environnement local et générer un rapport personnalisé basé sur hello conseils trouvent dans toohelp de cette rubrique vous migrez hello environnement tooAzure.

Nous vous recommandons également tout d’abord examiner hello, guides, vidéos et didacticiels qui couvrent hello rubriques suivantes :

* [Configurer un réseau virtuel uniquement dans hello portail Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Configurer un VPN de Site à Site dans hello portail Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Installer une nouvelle forêt Active Directory sur un réseau virtuel Azure](active-directory-new-forest-virtual-machine.md)
* [Installation d’un contrôleur de domaine Active Directory de réplication dans un réseau virtuel Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Iaas des professionnels de l’informatique Microsoft Azure : principes de base des machines virtuelles (01)](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Iaas des professionnels de l’informatique Microsoft Azure :(05) Création de réseaux virtuels pour la connectivité entre différents locaux](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Introduction
Hello conditions requises fondamentales pour le déploiement de Windows Server Active Directory sur des machines virtuelles Azure diffèrent peu de déployer en local (et virtuels, mesure toosome, machines physiques). Par exemple, Bonjour cas de Windows Server AD DS, si les contrôleurs de domaine hello (DC) que vous déployez sur les machines virtuelles sont des réplicas dans un existant sur site domaine/forêt d’entreprise, puis hello déploiement Azure est traité presque Bonjour comme peut traiter un autre site Active Directory Windows Server supplémentaire. Autrement dit, sous-réseaux doivent être définis dans un domaine Active Directory, un site créé et les sous-réseaux hello lié toothat site connecté sites tooother à l’aide de liens de sites appropriés. Il existe, toutefois, certaines différences sont courantes tooall Azure déploiements et certaines qui varient scénario de déploiement spécifique toohello correspondants. Deux différences fondamentales sont décrites ci-après :

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Machines virtuelles peut-être le réseau d’entreprise de connectivité toohello local.
Connexion des machines virtuelles tooan arrière local réseau d’entreprise nécessite un réseau virtuel Azure, qui inclut un site à site ou réseau privé virtuel (VPN) site-to-point tooseamlessly en mesure de composant de se connecter des machines virtuelles Azure et ordinateurs locaux. Ce composant VPN peut également permettre local domaine membre ordinateurs tooaccess un domaine Active Directory Windows Server dont les contrôleurs de domaine sont hébergés exclusivement sur des machines virtuelles. Il est important toonote, cependant, que si hello VPN échoue, l’authentification et autres opérations qui dépendent de Windows Server Active Directory échouera également. Alors que les utilisateurs peuvent être en mesure de toosign à l’aide de la mise en cache informations d’identification existantes, tous les pair à pair ou de tentatives d’authentification de client-serveur pour les tickets ont encore toobe émis ou sont obsolètes échoue.

Consultez [réseau virtuel](http://azure.microsoft.com/documentation/services/virtual-network/) pour une vidéo de démonstration et une liste de didacticiels pas à pas, y compris [configurer un VPN de Site à Site Bonjour Azure portal](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Vous pouvez également déployer Windows Server Active Directory sur un réseau virtuel Azure qui ne dispose pas d’accès à un réseau local. Hello dans cette rubrique, toutefois, supposent qu’un réseau virtuel Azure est utilisé, car il fournit des fonctions qui sont essentielles tooWindows Server d’adressage IP.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Les adresses IP doivent être configurées à l’aide d’Azure PowerShell.
Les adresses dynamiques sont allouées par défaut, mais utilisent à la place de tooassign d’applet de commande Set-AzureStaticVNetIP hello une adresse IP statique. Cette applet de commande définit une adresse IP statique qui persistera pendant la réparation de service et l’arrêt/le redémarrage de la machine virtuelle. Pour plus d’informations, consultez [Static internal IP address for virtual machines](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)(Adresse IP interne statique pour les machines virtuelles).

## <a name="BKMK_Glossary"></a>Termes et définitions
Hello Voici une liste non exhaustive de termes pour différentes technologies Azure qui seront référencés dans cet article.

* **Machines virtuelles**: offre IaaS de hello dans Azure qui permet aux clients toodeploy machines virtuelles exécutant presque n’importe quelle traditionnellement charge de travail de serveur sur site.
* **Réseau virtuel Azure**: hello mise en réseau de service dans Azure qui permet aux clients de créer et gérer des réseaux virtuels dans Azure et les lier en toute sécurité tootheir propre infrastructure sur site réseau à l’aide d’un réseau privé virtuel (VPN).
* **Adresse IP virtuelle**: une sur internet d’adresses IP qui est liée pas tooa spécifique ordinateur ou réseau carte d’interface. Services de cloud computing bénéficient d’une adresse IP virtuelle pour recevoir le trafic réseau qui est redirigé tooan machine virtuelle Azure. Une adresse IP virtuelle est une propriété d’un service cloud qui contient une ou plusieurs machines virtuelles Azure. Notez également qu’un réseau virtuel Azure peut contenir un ou plusieurs services cloud. Les adresses IP virtuelles fournissent des fonctions d’équilibrage de charge.
* **Adresse IP dynamique**: il s’agit hello adresse IP interne uniquement. Pour les machines virtuelles qui hébergent les rôles de serveur DNS du contrôleur de domaine/hello, il doit être configuré comme une adresse IP statique (en utilisant l’applet de commande Set-AzureStaticVNetIP de hello).
* **Réparation de service**: hello processus dans lequel Azure restaure automatiquement un tooa service état en cours d’exécution à nouveau après la détection de ce service hello a échoué. Réparation de service est un des aspects hello Azure qui prend en charge de la disponibilité et la résilience. Bien qu’improbable, résultat hello après un incident de réparation pour un contrôleur de domaine en cours d’exécution sur un ordinateur virtuel de service est similaire redémarrage non planifié de tooan, mais a des effets quelques :
  
  * carte réseau virtuelle de Hello Bonjour VM change
  * Hello adresse MAC de carte réseau virtuelle de hello change
  * Hello ID de processeur/Hello VM change
  * Hello IP configuration de carte réseau virtuelle de hello ne sera pas modifiée tant que hello machine virtuelle est attachée tooa des réseaux virtuels et hello adresse IP de la machine virtuelle est statique.
  
  Aucun de ces comportements n’affecte Windows Server Active Directory, car il n’a aucune dépendance sur l’adresse MAC de hello ou ID de processeur /, et tous les déploiements de Windows Server Active Directory sur Azure sont recommandées toobe exécuter sur un réseau virtuel Azure, comme indiqué plus haut .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Il est contrôleurs de domaine Active Directory Windows Server toovirtualize sans échec ?
Déploiement de Windows Server Active Directory contrôleurs de domaine sur des machines virtuelles est sujet toohello mêmes règles que l’exécution de contrôleurs de domaine local dans une machine virtuelle. L’exécution de contrôleurs de domaine virtualisés constitue une pratique prudente tant que vous respectez les instructions de sauvegarde et de restauration des contrôleurs de domaine. Pour plus d’informations sur les contraintes et les recommandations d’exécution des contrôleurs de domaine virtualisés, consultez la page [Exécution de contrôleurs de domaine dans Hyper-V](https://technet.microsoft.com/library/dd363553).

Les hyperviseurs fournissent ou banalisent les technologies susceptibles de poser problème pour plusieurs systèmes distribués, notamment Windows Server Active Directory. Par exemple, sur un serveur physique, vous pouvez cloner un disque ou utiliser l’état de hello arrière tooroll méthodes non prises en charge d’un serveur, y compris à l’aide de réseaux SAN et ainsi de suite, mais cela sur un serveur physique est beaucoup plus difficile que la restauration d’un instantané d’ordinateur virtuel dans un hyperviseur. Azure propose des fonctionnalités pouvant entraîner hello mêmes effets indésirables. Par exemple, vous ne devez pas copier les fichiers VHD des contrôleurs de domaine au lieu d’effectuer des sauvegardes régulières, car leur restauration peut entraîner une situation toousing instantané restauration des fonctionnalités similaires.

De telles restaurations introduisent des bulles USN qui peuvent entraîner des États de divergentes toopermanently entre les contrôleurs de domaine. Cela peut être la cause de divers problèmes, notamment :

* des objets en attente ;
* des mots de passe incohérents ;
* des valeurs d’attribut incohérentes ;
* Si le contrôleur de schéma hello est restaurée des incompatibilités de schéma

Pour plus d’informations sur la manière dont les contrôleurs de domaine peuvent être affectés, consultez [USN and USN Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback)(USN et restauration d’USN).

À partir de Windows Server 2012, [des dispositifs de protection supplémentaires sont intégrés dans tooAD DS](https://technet.microsoft.com/library/hh831734.aspx). Ces mécanismes de protection permettent de protéger les contrôleurs de domaine virtualisés contre les problèmes susmentionnés hello, tant que plateforme de l’hyperviseur sous-jacent hello prend en charge VM-GenerationID. Azure prend en charge VM-GenerationID, ce qui signifie que les contrôleurs de domaine qui exécutent Windows Server 2012 ou version ultérieure sur les machines virtuelles ont des garanties supplémentaires hello.

> [!NOTE]
> Vous devez arrêter et redémarrer une machine virtuelle qui exécute le rôle de contrôleur de domaine hello dans Azure hello système d’exploitation invité au lieu d’utiliser hello **arrêter** option Bonjour le portail Azure. Aujourd'hui, à l’aide de tooshut de portail hello une machine virtuelle entraîne hello toobe de machine virtuelle libérée. Une machine virtuelle a parti hello de ne pas entraîner de frais, mais elle réinitialise également hello VM-GenerationID, ce qui n’est pas souhaitable pour un contrôleur de domaine. Lorsque hello VM-GenerationID est réinitialisé, hello ID d’invocation de la base de données hello AD DS est également réinitialisé, hello pool RID est rejeté et SYSVOL est marqué comme ne faisant pas autorité. Pour plus d’informations, consultez [Introduction tooActive Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) et [virtualisation DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Pourquoi déployer Windows Server AD DS sur des machines virtuelles Azure ?
De nombreux scénarios de déploiement de Windows Server AD DS sont parfaitement adaptés au déploiement sur des machines virtuelles Azure. Par exemple, supposons que vous avez une société en Europe qui doit tooauthenticate des utilisateurs dans un emplacement distant en Asie. Hello entreprise n'a pas encore déployé Windows Server Active Directory contrôleurs de domaine en Asie en raison du coût de toohello toodeploy limitées et leur expertise toomanage hello serveurs après le déploiement. Les demandes d’authentification provenant d’Asie sont donc traitées par les contrôleurs de domaine déployés en Europe, mais avec des performances mitigées. Dans ce cas, vous pouvez déployer un contrôleur de domaine sur un ordinateur virtuel que vous avez spécifié doit être exécuté dans hello centre de données Azure en Asie. Attacher ce tooan de contrôleur de domaine réseau virtuel Azure qui est connecté directement toohello les emplacement distant améliorera les performances de l’authentification.

Azure convient également comme un site de récupération d’urgence substitute toootherwise urgence coûteux. Hello relativement faible coût de l’hébergement d’un petit nombre de contrôleurs de domaine et un seul réseau virtuel sur Azure représente une alternative intéressante.

Enfin, vous souhaiterez peut-être toodeploy une application réseau sur Azure, tels que SharePoint, ce qui nécessite Active Directory Windows Server mais n’a aucune dépendance sur hello de réseau local ou hello d’entreprise Active Directory Windows Server. Dans ce cas, configuration requise du serveur déploiement d’une forêt isolée sur Azure toomeet hello SharePoint est optimal. Là encore, le déploiement d’applications de réseau qui ont besoin connectivité toohello locaux du réseau et hello Active Directory d’entreprise est également pris en charge.

> [!NOTE]
> Étant donné qu’il fournit une connexion de couche 3, hello composant VPN qui assure la connectivité entre un réseau virtuel Azure et un réseau local permettre également activer des serveurs membres exécutés localement tooleverage les contrôleurs de domaine qui s’exécutent en tant que machines virtuelles sur Azure réseau virtuel. Mais si hello VPN n’est pas disponible, la communication entre les ordinateurs locaux et contrôleurs de domaine Azure ne fonctionnera pas, ce qui entraîne l’authentification et diverses autres erreurs.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Différences entre le déploiement de contrôleurs de domaine Windows Server Active Directory sur des machines virtuelles Azure et leur déploiement en local
* Pour les scénarios de déploiement Active Directory Windows Server comprenant une seule machine virtuelle, il est nécessaire toouse un réseau virtuel Azure pour la cohérence des adresses IP. Notez que ce guide suppose que les contrôleurs de domaine s’exécutent sur un réseau virtuel Azure.
* Comme pour les contrôleurs de domaine locaux, l’utilisation d’adresses IP statiques est recommandée. Une adresse IP statique peut uniquement être configurée à l’aide d’Azure PowerShell. Pour plus d’informations, consultez [Static internal IP address for VMs](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) (Adresse IP interne statique pour les machines virtuelles). Si vous avez l’analyse des systèmes ou autres solutions qui vérifient la configuration d’adresse IP statique hello système d’exploitation invité, vous pouvez affecter hello même statique IP adresse toohello propriétés des cartes réseau de machine virtuelle de hello. Mais sachez que la carte réseau hello sera ignorée si hello machine virtuelle subit une réparation de service ou d’arrêt dans le portail de hello et son adresse est désallouée. Dans ce cas, hello adresse IP statique dans Bonjour Invité devra toobe réinitialiser.
* Déploiement de machines virtuelles sur un réseau virtuel ne pas impliquent (ou nécessitent) connectivité tooan arrière local réseau ; réseau virtuel de Hello permet simplement. Vous devez créer un réseau virtuel pour établir la communication privée entre Azure et votre réseau local. Vous devez toodeploy un point de terminaison VPN sur le réseau local de hello. Hello VPN est ouvert toohello Azure sur un réseau local. Pour plus d’informations, consultez [présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md) et [configurer un VPN de Site à Site Bonjour Azure Portal](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Une option trop[créer un VPN de point-to-site](../vpn-gateway/vpn-gateway-point-to-site-create.md) est tooconnect disponible des ordinateurs Windows directement tooan réseau virtuel Azure.
> 
> 

* Que vous créiez ou non un réseau virtuel, Azure facture le trafic sortant, mais pas le trafic entrant. Les différents choix de conception de Windows Server Active Directory peuvent affecter le volume de trafic sortant généré par un déploiement. Par exemple, le déploiement d’un contrôleur de domaine en lecture seule (RODC) limite le trafic sortant, puisqu’il ne le réplique pas. Mais la décision de hello toodeploy un RODC doit toobe comparée hello besoin tooperform écrire des opérations sur hello contrôleur de domaine et hello [compatibilité](https://technet.microsoft.com/library/cc755190) que les applications et services dans le site de hello avoir avec RODC. Pour plus d’informations sur les frais liés au trafic, consultez la page [Tarification Azure](http://azure.microsoft.com/pricing/).
* Pendant que vous avez un contrôle complet sur le toouse de ressources de serveur pour les machines virtuelles locales, telles que la mémoire RAM, taille du disque et ainsi de suite, vous devez sélectionner dans une liste de tailles préconfigurées de serveur sur Azure. Pour un contrôleur de domaine, un disque de données est nécessaire dans le disque de système d’exploitation toohello ajout dans la base de données de commandes toostore hello Active Directory Windows Server.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Est-il possible de déployer Windows Server AD FS sur des machines virtuelles Azure ?
Oui, vous pouvez déployer des services ADFS Windows Server sur des machines virtuelles et hello [meilleures pratiques pour le déploiement AD FS](https://technet.microsoft.com/library/dn151324.aspx) local s’appliquent également tooAD FS déploiement sur Azure. Mais certaines des meilleures pratiques de hello telles que l’équilibrage de charge et haute disponibilité exigent des technologies au-delà proposées AD FS. Elles doivent être fournies par l’infrastructure sous-jacente de hello. Nous allons passer en revue quelques-unes de ces meilleures pratiques et voir comment les appliquer à l’aide de machines virtuelles Azure et d’un réseau virtuel Azure.

1. **Serveurs (STS) service de jeton de sécurité n’exposez jamais directement toohello Internet.**
   
    Ceci est important car hello STS émet des jetons de sécurité. Par conséquent, les serveurs STS telles que les serveurs AD FS doivent être traités avec hello même niveau de protection qu’un contrôleur de domaine. Si un service STS est compromis, des utilisateurs malveillants ont hello capacité tooissue des jetons d’accès qui contiennent potentiellement les revendications de leurs applications en choisissant l’option de toorelying et d’autres serveurs STS dans des organisations autorisées à approuver.
2. **Déployer des contrôleurs de domaine Active Directory pour tous les domaines d’utilisateurs Bonjour même réseau que les serveurs hello AD FS.**
   
    Serveurs AD FS utilisent les utilisateurs tooauthenticate de Services de domaine Active Directory. Il est recommandé de contrôleurs de domaine toodeploy hello même réseau que les serveurs de hello AD FS. Cela permet la continuité d’activité en cas de lien de hello entre hello réseau Azure et votre réseau local est rompue et permet une latence plus faible et améliorer les performances pour les connexions.
3. **Déployer plusieurs nœuds AD FS pour la haute disponibilité et l’équilibrage de charge de hello.**
   
    Dans la plupart des cas, Échec de hello d’une application qui permet à AD FS est inacceptable, car les applications hello nécessitant des jetons de sécurité sont souvent critiques. Par conséquent, et étant donné que AD FS se situe maintenant dans hello chemin critique tooaccessing applications critiques, le service de hello AD FS doit être hautement disponible via plusieurs proxys AD FS et des serveurs AD FS. distribution tooachieve d’équilibreurs de charge, les demandes sont généralement déployés devant les proxys hello AD FS et les serveurs hello AD FS.
4. **Déployer un ou plusieurs nœuds de proxy d’application web pour accéder à Internet.**
   
    Lorsque les utilisateurs ont besoin d’applications tooaccess protégées par le service de hello AD FS, disponible à partir de toobe de besoins du service FS hello AD hello internet. Pour cela, vous devez déployer le service de Proxy d’Application Web hello. Il est fortement recommandé de toodeploy plus que d’un seul nœud à des fins hello de haute disponibilité et l’équilibrage de charge.
5. **Restreindre l’accès à partir des ressources réseau de hello Proxy d’Application Web nœuds toointernal.**
   
    tooallow des utilisateurs externes tooaccess AD FS à partir de hello internet, vous devez les nœuds de Proxy d’Application Web toodeploy (ou Proxy AD FS dans les versions antérieures de Windows Server). Hello proxy d’Application Web nœuds sont directement exposés toohello Internet. Ils ne sont pas requis toobe appartenant au domaine et ils seulement doivent accéder aux toohello AD FS serveurs via les ports TCP 443 et 80. Il est fortement recommandé que tooall communication autres ordinateurs (en particulier les contrôleurs de domaine) est bloquée.
   
    Pour cela, vous devez généralement agir en local au moyen d’une zone démilitarisée (DMZ). Les pare-feu utilisent un mode d’autorisation du trafic de toorestrict opération hello DMZ toohello sur un réseau local (autrement dit, seul le trafic à partir de hello les adresses IP spécifiées et over spécifié des ports est autorisé, et tout autre trafic est bloqué).

Hello diagramme suivant montre une traditionnelle locale déploiement AD FS.

![Diagramme d’un déploiement local de services de fédération Active Directory traditionnels](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Toutefois, étant donné que Azure ne fournit pas de capacités de pare-feu natif et complet, autres options doivent toobe utilisé toorestrict trafic. Hello tableau suivant présente chaque option et de ses avantages et inconvénients.

| Option | Avantage | Inconvénient |
| --- | --- | --- |
| [Listes de contrôle d’accès (ACL) du réseau Azure](../virtual-network/virtual-networks-acl.md) |Configuration initiale moins coûteuse et plus simple. |Configuration ACL réseau supplémentaire requise si de nouvelles machines virtuelles sont ajoutés toohello déploiement |
| [Appliance Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) |Mode d’autorisation par liste d’approbation ; aucune configuration ACL réseau requise. |Augmentation des coûts et configuration initiale plus coûteuse. |

Dans ce cas, Hello étapes toodeploy AD FS sont les suivantes :

1. Créer un réseau virtuel avec une connectivité intersite, à l’aide d’un réseau privé virtuel (VPN) ou [d’ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Déployer des contrôleurs de domaine sur le réseau virtuel de hello. Cette étape est facultative mais recommandée.
3. Déployer des serveurs d’AD FS joints au domaine sur le réseau virtuel de hello.
4. Créer un [jeu d’équilibrage de charge interne](http://azure.microsoft.com/blog/internal-load-balancing/) qui comprend des serveurs hello AD FS et utilise une nouvelle adresse IP privée dans le réseau virtuel de hello (une adresse IP dynamique).
   
   1. Mettre à jour DNS toocreate hello FQDN toopoint toohello (dynamique) adresse IP privée du jeu d’équilibrage de charge interne hello.
5. Créer un service cloud (ou un réseau virtuel distinct) hello pour les nœuds de Proxy d’Application Web.
6. Déployer des nœuds de Proxy d’Application Web hello dans le service de cloud computing hello ou de réseau virtuel
   
   1. Créez un jeu d’équilibrage de charge externe qui inclut des nœuds de Proxy d’Application Web hello.
   2. Mettre à jour hello externes DNS (FQDN) de nom toopoint toohello cloud service adresse IP publique (adresse IP virtuelle hello).
   3. Configurer AD FS proxys toouse hello nom de domaine complet correspondant du jeu d’équilibrage de charge interne toohello pour les serveurs hello AD FS.
   4. Mettre à jour les sites web basés sur des revendications toouse hello FQDN externe pour leur fournisseur de revendications.
7. Restreindre l’accès entre l’ordinateur tooany de Proxy d’Application Web dans le réseau virtuel de hello AD FS.

le trafic toorestrict, le jeu d’équilibrage de charge hello pour l’équilibrage de charge interne Azure hello doit toobe configurée pour que le trafic tooTCP les ports 80 et 443, et tous les autres le trafic toohello dynamique adresse IP interne du jeu d’équilibrage hello est supprimé.

![Diagramme des ACL réseau ADFS avec autorisation TCP 443 + 80.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Serveurs de trafic toohello AD FS sont autorisés uniquement par hello les sources suivantes :

* équilibrage de charge interne Azure Hello.
* adresse IP de Hello d’un administrateur sur le réseau local de hello.

> [!WARNING]
> conception de Hello doit empêcher les nœuds de Proxy d’Application Web d’atteindre les autres machines virtuelles hello réseau virtuel Azure ou tous les emplacements de réseau local de hello. Qui peut être fait en configurant des règles de pare-feu dans l’appliance locale de hello pour les connexions Express Route ou un périphérique VPN de hello pour les connexions VPN de site à site.
> 
> 

Une option de toothis inconvénient est hello besoin tooconfigure hello ACL réseau pour plusieurs appareils, y compris l’équilibreur de charge interne, les serveurs de hello AD FS et les autres serveurs ajoutés toohello des réseaux virtuels. Si n’importe quel appareil est ajouté toohello déploiement sans configurer tooit de trafic réseau ACL toorestrict, tout déploiement de hello peut être menacé. Si les adresses IP de hello de nœuds de Proxy d’Application Web hello est susceptible de changer, les ACL du réseau hello doit être réinitialisé (ce qui signifie que les proxys hello doit être configuré toouse [dynamique des adresses IP statiques](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![ADFS sur Azure avec ACL réseau.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Une autre option consiste à toouse hello [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) toocontrol d’application le trafic entre les serveurs proxy AD FS et les serveurs de hello AD FS. Cette option est conforme aux meilleures pratiques de sécurité et de haute disponibilité et nécessite moins d’administration après l’installation initiale de hello, car l’appliance Barracuda NG Firewall de hello fournit un mode d’autorisation de l’administration du pare-feu, et il peut être installé directement sur un réseau virtuel Azure. Cela élimine les ACL réseau tooconfigure besoin de hello chaque fois qu’un nouveau serveur est ajouté toohello déploiement. Néanmoins, cette option ajoute un certain degré de complexité au déploiement initial et entraîne des coûts supplémentaires.

Dans ce cas, deux réseaux virtuels sont déployés au lieu d’un seul. Nous les appellerons le réseau virtuel 1 et le réseau virtuel 2. VNet1 contient les proxys hello et VNet2 hello STS et le réseau d’entreprise de hello réseau connexion toohello précédent. VNet1 est donc physiquement (bien que virtuellement) isolé VNet2 et, à son tour, hello réseau d’entreprise. VNet1 puis tooVNet2 connecté utilise une technologie de tunneling spéciale appelée Architecture en réseau indépendant (TINA) comme Transport. Bonjour tunnel TINA est attaché tooeach des réseaux virtuels de hello à l’aide d’un pare-feu Barracuda NG — un Barracuda sur chacun des réseaux virtuels de hello.  Pour la haute disponibilité, il est recommandé de déployer deux Barracudas sur chaque réseau virtuel ; un actif, hello autre passif. Ils offrent extrêmement des capacités de pare-feu qui nous permettent d’opération de hello toomimic d’un réseau de périmètre local traditionnel dans Azure.

![ADFS sur Azure avec pare-feu.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Pour plus d’informations, consultez [ADFS : étendre un toohello d’application frontale locale prenant en charge de revendications Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Un déploiement autre tooAD FS si hello vise Office 365 l’authentification unique
Il existe un autre purement et simplement toodeploying autre AD FS si votre objectif est seulement tooenable connectez-vous à Office 365. Dans ce cas, vous pouvez simplement déployer DirSync avec mot de passe synchronisation locale et obtenir hello même résultat final avec la complexité de déploiement minime, car cette approche ne nécessite pas ADFS ni Azure.

Hello tableau suivant compare le processus de connexion hello fonctionnement avec et sans déploiement d’AD FS.

| Authentification unique Office 365 avec AD FS et DirSync | Connexion à Office 365 identique avec DirSync + synchronisation de mots de passe |
| --- | --- |
| 1. hello utilisateur ouvre une session sur le réseau d’entreprise de tooa et est authentifié tooWindows Server Active Directory. |1. hello utilisateur ouvre une session sur le réseau d’entreprise de tooa et est authentifié tooWindows Server Active Directory. |
| 2. utilisateur de hello tente tooaccess Office 365 (je @contoso.com). |2. utilisateur de hello tente tooaccess Office 365 (je @contoso.com). |
| 3. Office 365 redirige hello utilisateur tooAzure AD. |3. Office 365 redirige hello utilisateur tooAzure AD. |
| 4. Étant donné que Azure AD ne peut pas authentifier l’utilisateur de hello et comprend qu’il existe une relation d’approbation avec ADFS local, il redirige hello utilisateur tooAD FS. |4. Azure AD ne peut pas accepter les tickets Kerberos directement et par conséquent, cet utilisateur hello Entrez les informations d’identification n’existe aucune relation d’approbation. |
| 5. hello l’utilisateur envoie un Kerberos ticket toohello AD FS STS. |5. utilisateur de hello entre hello même localement un mot de passe, et Azure Active Directory les valide sur le nom d’utilisateur hello et un mot de passe qui ont été synchronisé par DirSync. |
| 6. AD FS transforme hello toohello de ticket Kerberos requis jeton format/revendications et redirige l’utilisateur de hello tooAzure AD. |6. Azure AD redirige hello utilisateur tooOffice 365. |
| 7. utilisateur de hello authentifie tooAzure AD (une autre transformation se produit). |7. hello utilisateur peut se connecter tooOffice 365 et OWA à l’aide du jeton d’Azure AD hello. |
| 8. Azure AD redirige hello utilisateur tooOffice 365. | |
| 9. hello utilisateur est en mode silencieux connecté sur tooOffice 365. | |

Bonjour Office 365 avec synchronisation d’annuaire avec le scénario de synchronisation de mot de passe (sans ADFS), l’authentification unique est remplacée par « même authentification » où « même » indique que les utilisateurs doivent confirmer leurs informations d’identification locales même lorsqu’ils accèdent à Office 365. Notez que ces données peuvent être mémorisées par toohelp de navigateur de l’utilisateur hello réduire les invites suivantes.

### <a name="additional-food-for-thought"></a>Autres éléments de réflexion
* Si vous déployez un proxy AD FS sur une machine virtuelle Azure, les serveurs de connectivité toohello AD FS est nécessaire. S’ils sont locaux, il est recommandé de tirer parti de connectivité VPN de site à site de hello fournie par hello réseau virtuel tooallow hello Proxy d’Application Web nœuds toocommunicate avec leurs serveurs AD FS.
* Si vous déployez un serveur AD FS sur Azure virtual machine, connectivité tooWindows contrôleurs de domaine du serveur Active Directory, les magasins d’attributs, et que les bases de données de Configuration n’est nécessaires et peut également nécessiter une ExpressRoute ou une connexion VPN site à site entre un réseau hello Azure virtuel hello et réseau local.
* Des frais s’appliquent le trafic de tooall à partir de machines virtuelles Azure (trafic sortant). Si le coût est un facteur déterminant hello, il est conseillé de toodeploy nœuds de Proxy d’Application Web hello sur Azure, en laissant hello AD FS serveurs locaux. Si les serveurs hello AD FS sont déployés sur des machines virtuelles ainsi, des frais supplémentaires seront exposés tooauthenticate local utilisateurs. Le trafic sortant génère un coût, quelle que soit ou non il parcourt hello ExpressRoute ou hello connexion VPN de site à site.
* Si vous décidez natif équilibrage du serveur d’Azure toouse les fonctionnalités de haute disponibilité des serveurs AD FS, notez que l’équilibrage de charge fournit les sondes sont toodetermine utilisé hello la santé de machines virtuelles hello service de cloud computing hello. Dans les cas de hello des machines virtuelles Azure (comme les rôles tooweb ou de travail exécutées), une sonde personnalisée est nécessaire, car l’agent hello qui répond sondes par défaut de toohello n’est pas présent sur les machines virtuelles. Par souci de simplicité, vous pouvez utiliser une sonde TCP personnalisée — Ceci exige uniquement qu’une connexion TCP (un segment TCP SYN envoyé et a répondu toowith un segment TCP SYN ACK) contrôle d’intégrité de la machine virtuelle toodetermine établie avec succès. Vous pouvez configurer hello sonde personnalisée toouse tout toowhich de port TCP que vos ordinateurs virtuels sont à l’écoute.

> [!NOTE]
> Ordinateurs qui ont besoin de hello tooexpose que même ensemble de ports directement toohello Internet (par exemple le port 80 et 443) ne peuvent pas partager hello même service cloud. Il est, par conséquent, recommandé que vous créez un service cloud dédié pour vos serveurs ADFS Windows Server dans tooavoid commande potentiel se chevauche entre les exigences du port pour une application et Windows Server AD FS.
> 
> 

## <a name="deployment-scenarios"></a>Scénarios de déploiement
Hello après section souligne courants de déploiement scénarios toodraw attention tooimportant les considérations qui doivent être prises en compte. Chaque scénario comporte des détails sur les liens toomore sur les décisions de hello et tooconsider de facteurs.

1. [AD DS : déployer une application compatible AD DS ne nécessitant pas de connectivité au réseau d’entreprise](#BKMK_CloudOnly)
   
    Par exemple, un service SharePoint accessible sur Internet est déployé sur une machine virtuelle Azure. application Hello a pas de dépendances sur les ressources du réseau d’entreprise. nécessite Windows Server AD DS Hello application mais ne nécessite pas hello d’entreprise Windows Server AD DS.
2. [Services ADFS : Étendre un toohello d’application frontale locale prenant en charge de revendications Internet](#BKMK_CloudOnlyFed)
   
    Par exemple, une application prenant en charge les revendications qui a été correctement déployé localement et utilisée par les utilisateurs d’entreprise doit toobecome accessible à partir de hello Internet. application Hello doit toobe accessible directement via hello Internet par les partenaires commerciaux à l’aide de leurs propres identités d’entreprise et par les utilisateurs existants.
3. [Les services AD DS : Déployer une application de AD DS-compatible avec Windows Server qui nécessite le réseau d’entreprise de connectivité toohello](#BKMK_HybridExt)
   
    Par exemple, une application compatible LDAP qui prend en charge l’authentification Windows intégrée et utilise Windows Server AD DS en tant que référentiel pour les données de profil utilisateur et de configuration est déployée sur une machine virtuelle Azure. Il est souhaitable de hello de tooleverage application hello existantes d’entreprise Windows Server AD DS et fournir l’authentification unique. application Hello n’est pas en charge les revendications.

### <a name="BKMK_CloudOnly"></a>1. AD DS : déployer une application compatible AD DS ne nécessitant pas de connectivité au réseau d’entreprise
![Déploiement AD DS dans le cloud seulement](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**Figure 1**

#### <a name="description"></a>Description
SharePoint est déployé sur une machine virtuelle Azure et l’application hello a pas de dépendances sur les ressources du réseau d’entreprise. Hello application n’a besoin de domaine Active Directory mais ne *pas* nécessitent hello d’entreprise Windows Server AD DS. Aucune approbation Kerberos ou fédérée n’est requise, car les utilisateurs sont configurés automatiquement via l’application hello dans domaine hello de domaine Active Directory qui est également hébergé dans le cloud hello sur des machines virtuelles.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considérations sur le scénario et la façon dont les domaines technologiques appliquent toohello scénario
* [Topologie du réseau](#BKMK_NetworkTopology): créez un réseau virtuel Azure sans connectivité intersite (également appelée connectivité site à site).
* [Configuration du déploiement du contrôleur de domaine](#BKMK_DeploymentConfig): déployez un nouveau contrôleur de domaine dans une nouvelle forêt Windows Server Active Directory à un seul domaine. Celui-ci doit être déployé en même temps que le serveur DNS Windows de hello.
* [Topologie de site Active Directory Windows Server](#BKMK_ADSiteTopology): site d’Active Directory Windows Server utilisez hello par défaut (tous les ordinateurs seront dans Default-First-Site-Name).
* [Adressage IP et DNS](#BKMK_IPAddressDNS):
  
  * Définissez une adresse IP statique pour hello contrôleur de domaine à l’aide d’applet de commande Set-AzureStaticVNetIP Azure PowerShell hello.
  * Installez et configurez le serveur DNS Windows sur les contrôleurs de domaine hello sur Azure.
  * Configurer les propriétés de réseau virtuel hello avec le nom de hello et l’adresse IP hello machine virtuelle qui héberge les rôles de serveur de contrôleur de domaine et DNS hello.
* [Catalogue global](#BKMK_GC): hello premier contrôleur de domaine dans la forêt de hello doit être un serveur de catalogue global. Contrôleurs de domaine supplémentaires doivent également être configurés en tant que catalogues globaux car dans une forêt à domaine unique, catalogue global de hello ne requiert aucun travail supplémentaire hello contrôleur de domaine.
* [Placement de la base de données hello de domaine Active Directory et SYSVOL](#BKMK_PlaceDB): ajouter un tooDCs de disque de données en cours d’exécution en tant que machines virtuelles Azure dans la base de données de commandes toostore hello Windows Server Active Directory, les journaux et SYSVOL.
* [Sauvegarde et restauration](#BKMK_BUR): déterminer où vous souhaitez toostore sauvegardes d’état du système. Si nécessaire, ajoutez un autre disque toohello machine virtuelle du contrôleur de domaine toostore des sauvegardes de données.

### <a name="BKMK_CloudOnlyFed"></a>2 ADFS : étendre un toohello d’application frontale locale prenant en charge de revendications Internet
![Fédération avec connectivité intersite](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**Figure 2**

#### <a name="description"></a>Description
Une application prenant en charge les revendications qui a été correctement déployé localement et utilisée par les utilisateurs de l’entreprise toobecome de besoins accessible directement à partir de hello Internet. application Hello sert un web frontal tooa base de données SQL dans laquelle il stocke des données. Hello serveurs SQL Server utilisés par l’application hello est également situés sur le réseau d’entreprise de hello. Deux serveurs de STS Windows Server AD FS et un équilibreur de charge ont été déployés localement tooprovide accès toohello d’entreprise, les utilisateurs. Hello application doit maintenant toobe accessible directement sur hello Internet par les partenaires commerciaux à l’aide de leurs propres identités d’entreprise et par les utilisateurs existants.

Dans un effort toosimplify et hello satisfait les besoins de déploiement et la configuration de cette nouvelle exigence, il est décidé que deux autres web frontaux et deux serveurs de proxy ADFS Windows Server être installé sur les machines virtuelles. Toutes les quatre machines virtuelles sera exposée directement toohello Internet et réseau local de connectivité toohello à l’aide de la fonctionnalité VPN de site à site du réseau virtuel Azure sera fournie.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considérations sur le scénario et la façon dont les domaines technologiques appliquent toohello scénario
* [Topologie du réseau](#BKMK_NetworkTopology) : créez un réseau virtuel Azure et [configurez la connectivité intersite](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Pour chacun des certificats de Windows Server AD FS hello, assurez-vous que hello URL définie dans le modèle de certificat hello et les certificats obtenus hello peuvent être atteint par les instances de hello ADFS Windows Server s’exécutant sur Azure. Cette opération peut nécessiter tooparts de connectivité entre différents locaux de votre infrastructure à clé publique. Pour exemple, si le point de terminaison de CRL hello est basé sur LDAP et exclusivement hébergé localement, puis la connectivité intersite sera requis. Si ce n’est pas souhaitable, il peut être nécessaire toouse les certificats émis par une autorité de certification dont la liste CRL est accessible sur Internet de hello.
  > 
  > 
* [Configuration des services cloud](#BKMK_CloudSvcConfig): assurez-vous d’avoir deux services cloud pour fournir deux adresses IP virtuelles à équilibrage de charge. l’adresse IP virtuelle Hello premier service cloud sera dirigée toohello les machines virtuelles sur les ports 80 et 443 de deux proxy ADFS Windows Server. Hello proxy d’ADFS Windows Server Active Directory que seront des machines virtuelles configurées adresseIP toopoint toohello de hello local équilibreur de charge que fronts hello Windows Server AD FS STS. l’adresse IP virtuelle du service du cloud de deuxième Hello sera VMs dirigée toohello deux exécutant hello web frontal sur les ports 80 et 443. Configurez une sonde personnalisée tooensure hello-équilibreur de charge dirige uniquement le trafic toofunctioning ADFS Windows Server proxy et serveur web frontal machines virtuelles.
* [Configuration du serveur de fédération](#BKMK_FedSrvConfig): configurez ADFS Windows Server comme un federation server (STS) toogenerate de sécurité des jetons pour la forêt Active Directory Windows Server hello créée dans le cloud de hello. Relations d’approbation de fédération revendications fournisseur avec hello différents partenaires de que vous souhaitez tooaccept des identités à partir et configurer des relations d’approbation de partie de confiance tiers avec hello différentes applications vous souhaitez que les jetons toogenerate à.
  
    Dans la plupart des scénarios, les serveurs de proxy Windows Server AD FS sont déployés dans une fonctionnalité sur Internet pour des raisons de sécurité, tandis que leurs homologues de fédération Windows Server AD FS restent isolés d’une connectivité directe à Internet. Quelle que soit votre scénario de déploiement, vous devez configurer votre service cloud avec une adresse IP virtuelle qui fournira une adresse IP exposée publiquement et le port qui est en mesure de solde de tooload sur des vos deux instances de Windows Server AD FS STS ou instances de proxy.
* [Configuration de haute disponibilité de Windows Server AD FS](#BKMK_ADFSHighAvail): il est conseillé de toodeploy une batterie de serveurs ADFS Windows Server avec au moins deux serveurs pour le basculement et l’équilibrage de charge. Vous souhaitez tooconsider à l’aide de hello de base de données interne Windows (WID) pour les données de configuration de Windows Server AD FS et hello interne équilibrage de charge la capacité de Azure toodistribute les demandes entrantes sur les serveurs hello dans la batterie de serveurs hello.

Pour plus d’informations, consultez hello [Guide de déploiement d’AD DS](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. Les services AD DS : Déployer une application de AD DS-compatible avec Windows Server qui nécessite le réseau d’entreprise de connectivité toohello
![Déploiement AD DS dans différents locaux](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**Figure 3**

#### <a name="description"></a>Description
Une application compatible LDAP est déployée sur une machine virtuelle Azure. Elle prend en charge l’authentification Windows intégrée et utilise Windows Server AD DS comme référentiel pour les données de profil utilisateur et de configuration. objectif de Hello hello de tooleverage application hello existantes d’entreprise Windows Server AD DS et fournir l’authentification unique. application Hello n’est pas en charge les revendications. Les utilisateurs doivent également tooaccess hello application directement depuis hello Internet. toooptimize pour des performances et de coûts, il est décidé que les deux contrôleurs de domaine supplémentaires qui font partie du domaine de l’entreprise hello être déployés en même temps que l’application hello sur Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considérations sur le scénario et la façon dont les domaines technologiques appliquent toohello scénario
* [Topologie du réseau](#BKMK_NetworkTopology) : créez un réseau virtuel Azure avec [une connectivité intersite](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Méthode d’installation](#BKMK_InstallMethod): déployer des contrôleurs de domaine réplica hello domaine d’entreprise Windows Server Active Directory. Pour un contrôleur de domaine réplica, vous pouvez installer Windows Server AD DS sur hello machine virtuelle, et éventuellement hello installer à partir du média fonctionnalité tooreduce hello montant d’utilisation de données qui doivent toobe répliquées toohello nouveau contrôleur de domaine lors de l’installation. Pour obtenir un didacticiel, consultez [Installation d’un contrôleur de domaine Active Directory réplica dans Azure](active-directory-install-replica-active-directory-domain-controller.md). Même si vous utilisez IFM, il peut être plus efficace toobuild hello, contrôleur de domaine virtuel local et déplacer du cloud de toohello de disque dur virtuel (VHD) ensemble hello au lieu de répliquer de domaine Active Directory lors de l’installation. Pour la sécurité, il est recommandé de supprimer hello VHD hello sur un réseau local une fois qu’il a été copié tooAzure.
* [Topologie du site Windows Server Active Directory](#BKMK_ADSiteTopology): créez un nouveau site Azure dans les sites et services Active Directory. Créer un objet de Windows Server Active Directory sous-réseau toorepresent hello réseau virtuel Azure et ajoutez hello sous-réseau toohello site. Créer un lien de site qui inclut le nouveau site d’Azure hello et site hello dans le hello réseau virtuel Azure de point de terminaison VPN se trouve dans l’ordre toocontrol et optimiser tooand de trafic Active Directory Windows Server à partir d’Azure.
* [Adressage IP et DNS](#BKMK_IPAddressDNS):
  
  * Définissez une adresse IP statique pour hello contrôleur de domaine à l’aide d’applet de commande Set-AzureStaticVNetIP Azure PowerShell hello.
  * Installez et configurez le serveur DNS Windows sur les contrôleurs de domaine hello sur Azure.
  * Configurer les propriétés de réseau virtuel hello avec le nom de hello et l’adresse IP hello machine virtuelle qui héberge les rôles de serveur de contrôleur de domaine et DNS hello.
* [Contrôleurs de domaine géolocalisés](#BKMK_DistributedDCs): configurez les réseaux virtuels supplémentaires si nécessaire. Si votre topologie de site Active Directory nécessite des contrôleurs de domaine dans les zones géographiques différentes qui correspondent toodifferent Azure régions, que vous voulez que les sites d’Active Directory toocreate en conséquence.
* [Les contrôleurs de domaine en lecture seule](#BKMK_RODC): vous pouvez déployer un RODC Bonjour site Azure, selon vos conditions requises pour effectuer les opérations d’écriture sur hello hello et contrôleur de domaine de compatibilité des applications et services site hello avec RODC. Pour plus d’informations sur la compatibilité des applications, consultez hello [guide de compatibilité de domaine en lecture seule contrôleurs application](https://technet.microsoft.com/library/cc755190).
* [Catalogue global](#BKMK_GC): des catalogues globaux sont nécessaires tooservice les demandes d’ouverture de session dans les forêts. Si vous ne déployez pas de catalogue global dans hello site Azure, vous engagerez des coûts de trafic sortant comme les demandes d’authentification entraînent des requêtes dans d’autres sites. toominimize que le trafic, vous pouvez activer l’appartenance au groupe universel de mise en cache pour hello site Azure dans les Services et les Sites Active Directory.
  
    Si vous déployez un catalogue global, configurer des liens de site et les coûts de liens de site afin que le GC hello Bonjour Azure site n’est pas recommandée en tant qu’une contrôleur de domaine source par d’autres catalogues globaux qui doivent tooreplicate hello les mêmes partitions partielles de domaine.
* [Placement de la base de données hello de domaine Active Directory et SYSVOL](#BKMK_PlaceDB): ajouter un tooDCs de disque de données en cours d’exécution sur des machines virtuelles Azure dans la base de données de commandes toostore hello Windows Server Active Directory, les journaux et SYSVOL.
* [Sauvegarde et restauration](#BKMK_BUR): déterminer où vous souhaitez toostore sauvegardes d’état du système. Si nécessaire, ajoutez un autre disque toohello machine virtuelle du contrôleur de domaine toostore des sauvegardes de données.

## <a name="deployment-decisions-and-factors"></a>Facteurs et décisions relatifs au déploiement
Le tableau suivant résume les domaines technologiques hello Windows Server Active Directory qui sont affectés dans hello précédant les scénarios et hello tooconsider de décisions correspondant, avec le détail de toomore des liens ci-dessous. Certains domaines technologiques peuvent ne pas être scénario de déploiement tooevery applicables, et certains domaines technologiques peuvent être le scénario de déploiement tooa plus critique que d’autres.

Par exemple, si vous déployez un contrôleur de domaine réplica sur un réseau virtuel et votre forêt dispose d’un seul domaine, puis en choisissant toodeploy un serveur de catalogue global dans ce cas Impossible de scénario de déploiement toohello critique, car il ne crée pas de réplication supplémentaire configuration requise. Sur hello autre part, si hello forêt possède plusieurs domaines, puis hello décision toodeploy un catalogue global sur un réseau virtuel peut affecter la bande passante disponible, performances, l’authentification, recherches Active directory et ainsi de suite.

| Domaine technologique Windows Server Active Directory | Décisions | Facteurs |
| --- | --- | --- |
| [Topologie du réseau](#BKMK_NetworkTopology) |Devez-vous créer un réseau virtuel ? |<li>Configuration requise tooaccess ressources d’entreprise</li> <li>Authentification</li> <li>Account Management</li> |
| [Configuration du déploiement du contrôleur de domaine](#BKMK_DeploymentConfig) |<li>Déployer une forêt distincte sans aucune approbation ?</li> <li>Déployer une nouvelle forêt avec fédération ?</li> <li>Déployer une nouvelle forêt avec approbation de forêt Windows Server Active Directory ou Kerberos ?</li> <li>Étendre la forêt d’entreprise en déployant un contrôleur de domaine réplica ?</li> <li>Étendre la forêt d’entreprise en déployant un nouveau domaine enfant ou une arborescence de domaine ?</li> |<li>Sécurité</li> <li>Conformité</li> <li>Coût</li> <li>Résilience et tolérance de pannes</li> <li>Compatibilité des applications</li> |
| [Topologie du site Windows Server Active Directory](#BKMK_ADSiteTopology) |Comment configurer des liens de sites, sites et sous-réseaux avec le trafic de réseau virtuel Azure toooptimize et réduire les coûts ? |<li>Définitions de site et de sous-réseau</li> <li>Propriétés du lien de site et notification de modification</li> <li>Compression de la réplication</li> |
| [Adressage IP et DNS](#BKMK_IPAddressDNS) |Comment tooconfigure adresses IP et la résolution de noms ? |<li>Utilisez hello d’utilisation hello applet de commande Set-AzureStaticVNetIP tooassign une adresse IP statique</li> <li>Installer le serveur DNS Windows Server et de configurer les propriétés de réseau virtuel hello avec le nom de hello et l’adresse IP hello machine virtuelle qui héberge les rôles de serveur de contrôleur de domaine et DNS hello</li> |
| [Contrôleurs de domaine géolocalisés](#BKMK_DistributedDCs) |Comment tooDCs tooreplicate sur différentes des réseaux virtuels ? |Si votre topologie de site Active Directory nécessite des contrôleurs de domaine dans les zones géographiques correspondant toodifferent Azure régions, que vous voulez que les sites d’Active Directory toocreate en conséquence. [Configuration réseau toovirtual de réseau virtuel connectivité](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate entre les contrôleurs de domaine sur des réseaux virtuels distincts. |
| [Contrôleurs de domaine en lecture seule](#BKMK_RODC) |Utilisez des contrôleurs de domaine en lecture seule ou en écriture ? |<li>Filtrage des attributs HBI/PII</li> <li>Filtrage des secrets</li> <li>Limiter le trafic sortant</li> |
| [Catalogue global](#BKMK_GC) |Installer un catalogue global ? |<li>Pour une forêt à un seul domaine, configurez tous les contrôleurs de domaine en tant que catalogues globaux</li> <li>Pour une forêt à plusieurs domaines, les catalogues globaux sont requis pour l’authentification</li> |
| [Méthode d’installation](#BKMK_InstallMethod) |Comment tooinstall contrôleur de domaine dans Azure ? |Au choix :  <li>Installation d’AD DS à l’aide de Windows PowerShell ou Dcpromo</li> <li>Déplacer le disque dur virtuel d’un contrôleur de domaine virtuel local</li> |
| [Placement de la base de données hello de domaine Active Directory et SYSVOL](#BKMK_PlaceDB) |Où la base de données toostore de domaine Active Directory, ouvre une session et SYSVOL ? |Modifier les valeurs par défaut de Dcpromo.exe Ces fichiers Active Directory critiques *doivent* être placés sur des disques de données Azure plutôt que sur des disques de système d’exploitation qui implémentent le cache d’écriture. |
| [Sauvegarde et restauration](#BKMK_BUR) |Comment toosafeguard et restaurer les données ? |Créer des sauvegardes d’états du système |
| [Configuration du serveur de fédération](#BKMK_FedSrvConfig) |<li>Déployer une nouvelle forêt avec fédération dans le cloud de hello ?</li> <li>Déployer AD FS localement et exposer un proxy dans le cloud de hello ?</li> |<li>Sécurité</li> <li>Conformité</li> <li>Coût</li> <li>Tooapplications d’accès par des partenaires commerciaux</li> |
| [Configuration des services cloud](#BKMK_CloudSvcConfig) |Un service cloud est déployé implicitement hello la première fois que vous créez une machine virtuelle. Avez-vous besoin de services de cloud supplémentaire toodeploy ? |<li>Une ou plusieurs machines virtuelles requièrent une exposition directe toohello Internet ?</li> <li> Service de hello a-t-il besoin d’équilibrage de charge ?</li> |
| [Configuration requise du serveur de fédération pour l’adressage IP privé et public (adresse IP dynamique et adresse IP virtuelle)](#BKMK_FedReqVIPDIP) |<li>Instance de hello ADFS Windows Server doit-elle toobe directement accessible depuis hello Internet ?</li> <li>Application hello est déployée dans le cloud de hello nécessite sa propre adresse IP d’exposés à Internet et le port ?</li> |Créer un service cloud pour chaque adresse IP virtuelle requise par votre déploiement |
| [Configuration de la haute disponibilité de Windows Server AD FS](#BKMK_ADFSHighAvail) |<li>Combien y a-t-il de nœuds dans ma batterie de serveurs Windows Server AD FS ?</li> <li>Toodeploy le nombre de nœuds dans ma batterie de serveurs Windows Server AD FS proxy ?</li> |Résilience et tolérance de pannes |

### <a name="BKMK_NetworkTopology"></a>Topologie du réseau
Cohérence des adresses IP ordre toomeet hello et la configuration requise du DNS de domaine Active Directory, il est nécessaire toofirst créer un [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md) et attacher votre tooit de machines virtuelles. Lors de sa création, vous devez décider si toooptionally étendre la connectivité tooyour local d’entreprise réseau qui connecte de façon transparente Azure virtual machines machines tooon-site, cela est possible à l’aide de technologies VPN classiques et requiert qu’un point de terminaison VPN être exposé sur bord hello hello réseau d’entreprise. Autrement dit, hello VPN est lancée à partir du réseau d’entreprise toohello Azure, pas vice versa.

Notez que des frais supplémentaires s’appliquent lors de l’extension d’un réseau virtuel tooyour sur réseau local au-delà des frais standard hello qui s’appliquent tooeach machine virtuelle. Plus précisément, il existe des frais pour le temps processeur de passerelle de réseau virtuel Azure hello et pour le trafic sortant hello générés par chaque machine virtuelle qui communique avec les machines locales sur hello VPN. Pour plus d’informations sur les frais de trafic réseau, voir [Aperçu rapide de la tarification Azure](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Configuration du déploiement du contrôleur de domaine
méthode Hello vous configurez hello contrôleur de domaine dépend des exigences de hello hello de service vous souhaitez toorun sur Azure. Par exemple, vous pouvez déployer une nouvelle forêt, isolée à partir de votre propre forêt d’entreprise, pour tester une preuve de concept, une nouvelle application ou un autre projet à court terme qui nécessite des services d’annuaire, mais les ressources de l’entreprise toointernal pas spécifiques un accès.

Un avantage, une forêt isolée avec que ne réplique pas les contrôleurs de domaine des locaux contrôleurs de domaine, ce qui entraîne un trafic réseau moins sortant généré par le système hello lui-même, ainsi que les coûts. Pour plus d’informations sur les frais de trafic réseau, voir [Aperçu rapide de la tarification Azure](http://azure.microsoft.com/pricing/).

Autre exemple, supposons que vous avez des exigences de confidentialité pour un service, mais le service de hello dépend d’accès tooyour interne Windows Server Active Directory. Si vous êtes autorisé toohost des données pour le service hello dans le cloud de hello, vous pouvez déployer un nouveau domaine enfant pour votre forêt interne sur Azure. Dans ce cas, vous pouvez déployer un contrôleur de domaine pour hello nouveau domaine enfant (sans catalogue global de hello dans les problèmes de confidentialité d’ordre toohelp adresse). Ce scénario, combiné au déploiement d’un contrôleur de domaine réplica, nécessite un réseau virtuel pour la connectivité avec vos contrôleurs de domaine locaux.

Si vous créez une nouvelle forêt, choisissez si toouse [approbation Active Directory](https://technet.microsoft.com/library/cc771397) ou [approbations de fédération](https://technet.microsoft.com/library/dd807036). Équilibrer les besoins hello dictées par la compatibilité, de sécurité, de conformité, de coût et de résilience. Par exemple, tootake parti de [l’authentification sélective](https://technet.microsoft.com/library/cc755844) vous pouvez choisir toodeploy une nouvelle forêt sur Azure et créer une approbation de Windows Server Active Directory entre les forêts de local hello et hello cloud. Toutefois, si l’application hello est prenant en charge les revendications, vous pouvez déployer des approbations de fédération au lieu d’approbations de forêt Active Directory. Un autre facteur est hello coût tooeither répliquer davantage de données en étendant votre service cloud toohello de Windows Server Active Directory ou générer plus de trafic à la suite de l’authentification et de la charge de la requête.

Les exigences de disponibilité et de tolérance de pannes ont également une répercussion sur votre choix. Par exemple, si le lien de hello est interrompue, applications qui exploitent une approbation Kerberos ou une approbation de fédération sont probablement entièrement arrêtées, sauf si vous avez déployé une infrastructure suffisante sur Azure. Autres configurations de déploiement tels que les contrôleurs de domaine réplica (accessible en écriture ou en lecture seule) augmenter la probabilité de hello d’être en mesure de tootolerate pannes de lien.

### <a name="BKMK_ADSiteTopology"></a>Topologie du site Windows Server Active Directory
Vous devez toocorrectly définir des sites et des liens de sites dans l’ordre toooptimize du trafic et réduisent les coûts. Les sites, liens de sites et les sous-réseaux affectent la topologie de réplication hello entre les contrôleurs de domaine et les flux hello du trafic d’authentification. Envisagez hello suivant les frais liés au trafic puis déployer et configurer des contrôleurs de domaine selon les exigences de toohello de votre scénario de déploiement :

* Il existe des frais nominaux par heure pour la passerelle hello lui-même :
  
  * Elle peut être démarrée et arrêtée selon vos besoins.
  * En cas d’arrêt, les machines virtuelles Azure sont isolées hello réseau d’entreprise
* Le trafic entrant est gratuit.
* Le trafic sortant est facturé, en fonction de trop[Azure tarification en un coup de œil](http://azure.microsoft.com/pricing/). Vous pouvez optimiser les propriétés de lien de site entre des sites locaux et les sites du cloud hello comme suit :
  
  * Si vous utilisez plusieurs réseaux virtuels, configurer des liens de sites hello et leurs coûts convenablement tooprevent de domaine Active Directory à partir de la hiérarchisation hello Azure de site sur un qui peut fournir des mêmes niveaux de service sans frais hello. Vous pouvez également envisager de désactiver le pont hello tous les sites option lien (relier) (qui est activée par défaut). Cela garantit que seuls les sites connectés directement sont répliqués avec un autre. Contrôleurs de domaine dans les sites connectés de manière transitive ne sont plus en mesure de tooreplicate directement entre eux, mais ils doivent répliquer via un ou plusieurs sites courants. Si les sites intermédiaires hello deviennent indisponibles pour une raison quelconque, la réplication entre contrôleurs de domaine dans les sites connectés de manière transitive ne produira pas même si la connectivité entre les sites hello est disponible. Enfin, où les sections du comportement de la réplication transitive restent souhaitables, créez site ponts entre liens de contenant hello approprié liens de sites et des sites, tels que local, sites de réseau d’entreprise.
  * [Configurer les coûts de lien de site](https://technet.microsoft.com/library/cc794882) tooavoid correctement le trafic imprévu. Par exemple, si **essayez de Site le plus proche suivant** est activé, vérifiez que réseau virtuel hello sites ne sont pas hello ensuite le plus proche en augmentant le coût de l’objet lien de sites hello qui se connecte toohello arrière de site Azure hello hello réseau d’entreprise.
  * Configurer le lien de sites [intervalles](https://technet.microsoft.com/library/cc794878) et [planifications](https://technet.microsoft.com/library/cc816906) selon les exigences de tooconsistency et taux de modifications de l’objet. Alignez la planification des réplications avec la tolérance de latence. Contrôleurs de domaine répliquent uniquement hello dernier état d’une valeur, afin de l’intervalle de réplication hello décroissant peut enregistrer les coûts s’il existe un taux de modification d’objet suffisante.
* Si la réduction des coûts est une priorité, vérifiez que la réplication est planifiée et que la notification de modification n’est pas activée. Il s’agit de configuration par défaut de hello lors de la réplication entre sites. Cela n’est pas important si vous déployez un RODC sur un réseau virtuel, car hello RODC pas répliquer les modifications sortantes. Mais si vous déployez un contrôleur de domaine accessible en écriture, vous devez vous assurer de lien de sites hello n’est pas configuré tooreplicate les mises à jour à une fréquence inutile. Si vous déployez un serveur de catalogue global (GC), assurez-vous que chaque site qui contient un catalogue global réplique les partitions de domaine à partir d’une contrôleur de domaine dans un site qui est connecté avec un lien de site source ou de liens de sites qui ont un coût inférieur à hello GC dans Bienvenue site Azure.
* Il est possible de toofurther réduire le trafic réseau généré par la réplication entre les sites en modifiant l’algorithme de compression de réplication hello. algorithme de compression Hello est contrôlé par l’algorithme de compression HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator hello REG_DWORD Registre entrée. Hello par défaut est 3, qui met en corrélation toohello algorithme de compression Xpress. Vous pouvez modifier hello valeur too2, quelles modifications hello tooMSZip d’algorithme. Dans la plupart des cas, cela augmentera la compression de hello, mais il le fait à frais hello d’utilisation du processeur. Pour plus d’informations, voir [How Active Directory replication topology works](https://technet.microsoft.com/library/cc755994)(Fonctionnement de la topologie de réplication Active Directory).

### <a name="BKMK_IPAddressDNS"></a>Adressage IP et DNS
Par défaut, des « adresses avec bail DHCP » sont allouées aux machines virtuelles Azure. Étant donné que les adresses dynamiques de réseau virtuel Azure persistent avec une machine virtuelle pour la durée de vie hello de machine virtuelle de hello, hello de Windows Server AD DS sont requise.

Par conséquent, lorsque vous utilisez une adresse dynamique sur Azure, vous utilisez en fait à l’aide d’une adresse IP statique, car elle est routable pendant un bail de hello hello et période hello de bail de hello est égal toohello de durée de vie du service de cloud hello.

Toutefois, une adresse dynamique hello est désallouée si hello machine virtuelle est arrêtée. adresse IP du hello tooprevent de désallocation, vous pouvez [utiliser Set-AzureStaticVNetIP tooassign une adresse IP statique](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Résolution de noms, déployez votre propre (ou optimisez votre) l’infrastructure de serveur DNS ; DNS fourni par Azure ne répond pas aux hello avancé des besoins de résolution de nom de domaine Active Directory. Par exemple, il ne prend pas en charge les enregistrements SRV dynamiques, et ainsi de suite. La résolution de noms est un élément de configuration critique pour les contrôleurs de domaine et les clients joints au domaine. Les contrôleurs de domaine doivent être capables d’inscrire des enregistrements de ressource et de résoudre d’autres enregistrements de ressource de contrôleurs de domaine.
Pour des raisons de performances et tolérance de panne, il est service de DNS Windows Server hello tooinstall optimale sur les contrôleurs de domaine hello s’exécutant sur Azure. Puis configurez les propriétés du réseau virtuel Azure hello avec le nom de hello et l’adresse IP du serveur DNS de hello. Quand démarrer d’autres ordinateurs virtuels sur le réseau virtuel de hello, leurs paramètres de résolution client DNS seront configurés avec le serveur DNS dans le cadre de l’allocation d’adresses IP dynamique hello.

> [!NOTE]
> Vous ne peut pas joindre le domaine de Windows Server AD DS, Active Directory local ordinateurs tooa qui est hébergé sur Azure directement via Internet de hello. Bonjour les exigences de ports pour Active Directory et l’opération de jonction de domaine hello rendent ports nécessaires de toodirectly peu pratique exposent hello et en réalité, un ensemble toohello de contrôleur de domaine Internet.
> 
> 

Les machines virtuelles inscrivent leur nom DNS automatiquement au démarrage ou lors d’une modification de nom.

Pour plus d’informations sur cet exemple et un autre exemple qui montre comment tooprovision hello première machine virtuelle et installer les services AD DS sur celle-ci, consultez [installer une nouvelle forêt Active Directory sur Microsoft Azure](active-directory-new-forest-virtual-machine.md). Pour plus d’informations sur l’utilisation de Windows PowerShell, voir [Installer Azure PowerShell](/powershell/azureps-cmdlets-docs) et [Azure Management Cmdlet](/powershell/module/azurerm.compute/#virtual_machines) (Applets de commande de gestion Azure).

### <a name="BKMK_DistributedDCs"></a>Contrôleurs de domaine géolocalisés
Azure présente des avantages lors de l’hébergement de plusieurs contrôleurs de domaine sur différents réseaux virtuels :

* Tolérance de pannes sur plusieurs sites
* Bureaux de toobranch proximité physique (latence inférieure)

Pour plus d’informations sur la configuration d’une communication directe entre les réseaux virtuels, consultez [configurer la connectivité de réseau virtuel toovirtual réseau](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Contrôleurs de domaine en lecture seule
Vous devez toochoose si toodeploy en lecture-seule ou en écriture les contrôleurs de domaine. Vous pouvez être tenté toodeploy RODC car vous n’aurez contrôle physique sur eux, mais RODC est conçu toobe déployé dans des emplacements où leur sécurité physique est menacée, notamment des filiales.

Azure ne présente pas hello risque de sécurité physique d’une filiale, mais RODC peut-être se toobe plus rentables, car les fonctionnalités hello qu’ils fournissent sont bien adaptées toothese environnements et ce pour des raisons très différentes. Par exemple, RODC ont aucune réplication sortante et sont tooselectively en mesure de remplir les secrets (mots de passe). Sur l’inconvénient de hello, l’absence de ces secrets hello peut nécessiter le trafic sortant de la demande toovalidate leur un ordinateur ou un utilisateur s’authentifie. Toutefois, il est possible de pré-renseigner et mettre en cache les secrets de manière sélective.

RODC fournit un avantage supplémentaire en autour HBI et PII, car vous pouvez ajouter des attributs qui contiennent des données sensibles toohello RODC filtré ensemble d’attributs (FAS). Hello FAS est un jeu d’attributs qui ne sont pas répliquées tooRODCs personnalisable. Vous pouvez utiliser hello FAS par précaution au cas où vous ne sont pas autorisées ou que vous ne voulez pas que toostore PII ou HBI sur Azure. Pour plus d’informations, voir [RODC filtered attribute set (jeu d’attributs filtré du contrôleur de domaine accessible en lecture seule)[(https://technet.microsoft.com/library/cc753459)].

Assurez-vous que les applications seront compatibles avec RODC vous envisagez de toouse. Nombreuses applications Active Directory Windows Server fonctionnent correctement avec RODC, mais certaines applications peuvent être inefficaces ou échouer si elles n’ont pas accès tooa contrôleur de domaine accessible en écriture. Pour plus d’informations, voir [Compatibilité des applications avec les contrôleurs de domaine en lecture seule](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Catalogue global
Vous devez toochoose si tooinstall un catalogue global (GC). Dans une forêt de domaine unique, vous devez configurer tous les contrôleurs de domaine comme des serveurs de catalogue global. Cela n’augmente pas les coûts car aucun trafic de réplication supplémentaire n’est généré.

Dans une forêt de plusieurs domaines, les catalogues globaux sont appartenances au groupe universel de tooexpand nécessaire pendant le processus d’authentification hello. Si vous ne déployez pas de catalogue global, les charges de travail sur le réseau virtuel de hello qui authentifient auprès d’un contrôleur de domaine sur Azure génèreront indirectement le trafic de l’authentification sortante tooquery catalogues globaux locaux lors de chaque tentative d’authentification.

les coûts de Hello associés aux catalogues globaux sont moins prédictibles, car ils hébergent chaque domaine (en partie). Si la charge de travail hello héberge un service connecté à Internet et authentifie les utilisateurs par rapport à Windows Server AD DS, les coûts de hello peuvent être totalement imprévisibles. toohelp réduire les requêtes de catalogue global en dehors du site de cloud hello lors de l’authentification, vous pouvez [activer le cache d’appartenance au groupe universel](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Méthode d’installation
Vous devez toochoose comment tooinstall hello contrôleurs de domaine sur le réseau virtuel de hello :

* Promouvoir de nouveaux contrôleurs de domaine. Pour plus d’informations, voir [Installation d’une nouvelle forêt Active Directory sur un réseau virtuel Azure](active-directory-new-forest-virtual-machine.md).
* Déplacer hello disque dur virtuel d’un nuage de toohello de contrôleur de domaine virtuel local. Dans ce cas, vous devez vous assurer que hello local virtuel contrôleur de domaine est « déplacé, « pas « copiées » ou « clonés ».

Utiliser uniquement les machines virtuelles pour les contrôleurs de domaine (comme tooAzure opposés « web » ou « travailleur » machines virtuelles de rôle). Elles sont durables et la durabilité de l’état d’un contrôleur de domaine est essentielle. Les machines virtuelles Azure sont conçues pour des charges de travail telles que des contrôleurs de domaine.

N’utilisez SYSPREP toodeploy ou cloner des contrôleurs de domaine. possibilité de Hello tooclone contrôleurs de domaine est uniquement disponible à compter de Windows Server 2012. Hello fonctionnalité de clonage nécessite la prise en charge de VMGenerationID dans l’hyperviseur sous-jacent de hello. Hyper-V dans Windows Server 2012 et les réseaux virtuels Azure prennent tous deux en charge VMGenerationID, tout comme les fournisseurs de logiciels de virtualisation tiers.

### <a name="BKMK_PlaceDB"></a>Placement de la base de données hello de domaine Active Directory et SYSVOL
Sélectionnez où toolocate hello la base de données de domaine Active Directory, les journaux et SYSVOL. Ils doivent être déployés sur des disques de données Azure.

> [!NOTE]
> Disques de données Azure sont limitées too1 to.
> 
> 

Par défaut, les disques de données ne mettent pas les écritures en cache. Les lecteurs de disque de données qui sont attaché tooa machine virtuelle utilisent le cache à double écriture. Permet de cache à double écriture que hello écriture est validée toodurable stockage Azure avant la fin du point de vue hello du système d’exploitation de la machine virtuelle hello transaction de hello. Il fournit la durabilité, à des frais de hello d’écritures légèrement plus lentes.

Ceci est important pour le domaine Active Directory, car le disque en cache d’écriture invalide les hypothèses effectuées par hello contrôleur de domaine. Windows Server AD DS tente toodisable cache d’écriture, mais c’est toohello disque e/s système toohonor il. Cache d’écriture toodisable échec peut, dans certaines circonstances, introduire une restauration USN résultant en attente d’objets et autres problèmes.

Comme meilleure pratique pour les contrôleurs de domaine virtuels, procédez comme hello suivant :

* Définir hello préférences de Cache hôte sur le disque de données Azure hello pour aucun. Cela évite les problèmes de cache d’écriture pour les opérations AD DS.
* Stocker hello de base de données, journaux et SYSVOL sur hello soit les données mêmes disque ou des disques de données distincts. En règle générale, il s’agit d’un disque distinct à partir du disque hello utilisé pour le système d’exploitation de hello lui-même. clé à retenir Hello est cette base de données de domaine Active Directory Windows Server hello et SYSVOL ne doit pas être stocké sur un disque de système d’exploitation Azure. Par défaut, hello AD DS processus d’installation installe ces composants dans le dossier % SystemRoot%, ce qui n’est pas recommandée pour Azure.

### <a name="BKMK_BUR"></a>Sauvegarde et restauration
Soyez attentif à ce qui est pris en charge ou non dans le cadre de la sauvegarde et de la restauration des contrôleurs de domaine, en particulier ceux qui sont exécutés sur une machine virtuelle. Voir [Observations sur la sauvegarde et la restauration des contrôleurs de domaine virtualisés](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Créez des sauvegardes d’état en utilisant seulement des logiciels de sauvegarde compatibles avec les exigences de sauvegarde de Windows Server AD DS, telles que Sauvegarde Windows Server.

Ne copiez ou ne clonez pas les fichiers des disques durs virtuels des contrôleurs de domaine au lieu d’effectuer des sauvegardes régulières. Si une restauration doit être effectuée, vous introduirez des bulles USN en utilisant pour cela des disque durs virtuels clonés ou copiés sans Windows Server 2012 et un hyperviseur pris en charge.

### <a name="BKMK_FedSrvConfig"></a>Configuration du serveur de fédération
Hello configuration des serveurs de fédération ADFS Windows Server (STS) dépend en partie que hello applications que vous souhaitez toodeploy sur Azure doivent tooaccess des ressources sur votre réseau local.

Si les applications hello remplit hello suivant des critères, vous pouvez déployer des applications hello de manière isolée à partir de votre réseau local.

* Elles acceptent les jetons de sécurité SAML.
* Ils sont toohello peuvent être exposée Internet
* Elles n’accèdent pas aux ressources locales.

Dans ce cas, configurez les STS Windows Server AD FS comme suit :

1. Configurez une forêt à domaine unique isolée sur Azure.
2. Fournir un accès fédéré toohello forêt en configurant une batterie de serveurs de fédération Windows Server AD FS.
3. Configurer les services ADFS Windows Server (batterie de serveurs de fédération et batterie de proxy de serveur de fédération) dans la forêt locale de hello.
4. Établir une relation d’approbation de fédération entre hello sur site et des instances Azure des services ADFS Windows Server.

Sur hello autre part, si les applications de hello requièrent tooon local d’accéder aux ressources, vous pouvez configurer Windows Server AD FS avec une application hello sur Azure comme suit :

1. Configurez la connectivité entre les réseaux locaux et Azure.
2. Configurer une batterie de serveurs de fédération ADFS Windows Server dans la forêt locale de hello.
3. Configurez une batterie de serveurs proxy de fédération Windows Server AD FS sur Azure.

Cette configuration a l’avantage hello de réduire l’exposition de hello de ressources locales, tooconfiguring similaire ADFS Windows Server avec des applications dans un réseau de périmètre.

Notez que dans les deux cas, vous pouvez établir des relations d’approbation avec d’autres fournisseurs d’identité, si une collaboration d’entreprise à entreprise est requise.

### <a name="BKMK_CloudSvcConfig"></a>Configuration des services cloud
Services de cloud computing sont nécessaires si vous souhaitez tooexpose une machine virtuelle directement toohello Internet ou tooexpose une côté Internet équilibrée application. Cela est possible car chaque service cloud propose une seule adresse IP virtuelle configurable.

### <a name="BKMK_FedReqVIPDIP"></a>Configuration requise du serveur de fédération pour l’adressage IP privé et public (adresse IP dynamique et adresse IP virtuelle)
Chaque machine virtuelle Azure reçoit une adresse IP dynamique. Une adresse IP dynamique est une adresse privée accessible uniquement dans Azure. Dans la plupart des cas, toutefois, il sera nécessaire tooconfigure une adresse IP virtuelle pour vos déploiements de Windows Server AD FS. adresse IP virtuelle de Hello est nécessaire tooexpose toohello de points de terminaison ADFS Windows Server Internet et sera utilisé par les clients et les partenaires fédérés pour l’authentification et la gestion continue. Une adresse IP virtuelle est une propriété d’un service cloud qui contient une ou plusieurs machines virtuelles Azure. Si l’application prenant en charge les revendications hello est déployée sur Azure et Windows Server AD FS est exposés à Internet et le partage de ports courants, chacune requiert une adresse IP virtuelle lui est propre, et il sera donc nécessaire toocreate un seul service cloud pour l’application hello et un seconde pour les services ADFS Windows Server.

Pour les définitions de l’adresse IP virtuelle hello termes du contrat et une adresse IP dynamique, consultez [termes et définitions](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Configuration de la haute disponibilité de Windows Server AD FS
Bien qu’il soit les services de fédération autonome ADFS Windows Server toodeploy possibles, il est recommandé de toodeploy une batterie de serveurs au moins deux nœuds pour le service STS AD FS et proxys pour les environnements de production.

Consultez [considérations sur la topologie AD FS 2.0 déploiement](https://technet.microsoft.com/library/gg982489) Bonjour [AD FS 2.0 Design Guide](https://technet.microsoft.com/library/dd807036) toodecide options de configuration de déploiement mieux adaptées à vos besoins.

> [!NOTE]
> Commande tooget l’équilibrage de charge pour les points de terminaison Windows Server AD FS sur Azure, configurez tous les membres de la batterie de serveurs ADFS Windows Server de hello Bonjour même service cloud et utiliser hello équilibrage de charge la fonctionnalité d’Azure pour HTTP (80 par défaut) et les ports HTTPS (443 par défaut). Pour plus d’informations, voir [Sonde d’équilibrage de charge Azure](https://msdn.microsoft.com/library/azure/jj151530).
> L’équilibrage de la charge réseau (NLB) de Windows Server n’est pas pris en charge sur Azure.
> 
> 

