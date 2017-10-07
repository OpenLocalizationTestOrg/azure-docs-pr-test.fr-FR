---
title: aaaSecurity meilleures pratiques pour IaaS les charges de travail dans Azure | Documents Microsoft
description: " la migration des charges de travail tooAzure IaaS Hello met opportunités tooreevaluate nos conceptions "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Meilleures pratiques de sécurité pour les charges de travail IaaS dans Azure

Comme vous avez démarré réfléchir à l’infrastructure de tooAzure déplacement des charges de travail en tant que service (IaaS), vous aurez probablement compris que quelques points sont familiers. Vous disposez peut-être déjà d’une expérience de sécurisation d’environnements virtuels. Lorsque vous déplacez tooAzure IaaS, vous pouvez appliquer vos connaissances en matière de sécurisation des environnements virtuels et utiliser un nouvel ensemble d’options toohelp de sécuriser vos ressources.

Nous pouvons commencer en disant que nous devons nous pas attendre toobring ressources locales en tant que tooAzure un à un. Hello nouveaux défis et nouvelles options de hello mettre opportunité tooreevaluate existant deigns, d’outils et de processus.

Votre responsable de la sécurité est basée sur le type hello du service cloud. Hello graphique suivant résume solde hello de responsabilité de Microsoft et vous :


![Domaines de responsabilité](./media/azure-security-iaas/sec-cloudstack-new.png)


Nous aborderons certaines options hello disponibles dans Azure qui peut vous aider à répondre aux exigences de sécurité de votre organisation. N’oubliez pas que les exigences de sécurité peuvent varier selon les types de charges de travail. Aucune de ces meilleures pratiques ne peut à elle seule sécuriser vos systèmes. Comme tout autre élément dans la sécurité, vous disposez des options appropriées de toochoose hello et voir comment les solutions hello peuvent se complètent mutuellement en remplissant les écarts.

## <a name="use-privileged-access-workstations"></a>Utiliser des stations de travail d’accès privilégié

Les organisations sont souvent victimes toocyberattacks, car les administrateurs effectuer des actions lors de l’utilisation de comptes avec des droits élevés. Généralement, leur intention n’est pas de nuire mais, simplement, la configuration et les processus existants le permettent. La plupart de ces utilisateurs hello, risques de ces actions à partir d’un point de vue conceptuel, toujours choisir toodo les.

Effectuer diverses tâches telles que la vérification de la messagerie et de navigation hello Internet semblent assez inoffensive. Mais ils peuvent exposer toocompromise de comptes avec élévation de privilèges par malveillants acteurs qui peuvent utiliser les activités de navigation, des messages électroniques spécialement ou autres techniques toogain accès tooyour enterprise. Nous recommandons vivement d’utiliser hello de stations de gestion sécurisée pour l’exécution de toutes les tâches d’administration Azure, comme un moyen de réduire la compromission de tooaccidental d’exposition.

Les stations de travail d’accès privilégié (PAW) fournissent un système d’exploitation dédié aux tâches sensibles, et protégé contre les attaques Internet et les vecteurs de menaces. Séparation de ces tâches sensibles et les comptes de hello utilisation quotidienne des stations de travail et périphériques offre une protection renforcée à partir des attaques d’hameçonnage, application et des vulnérabilités du système d’exploitation, différentes attaques d’emprunt d’identité et vol des informations d’identification telles que de la séquence de touches journalisation, Pass-the-Hash et Pass-the-Ticket.

Hello privilégiées approche est une extension de hello bien établi et recommandé pratique toouse affectés de manière individuelle d’administration d’un compte distinct à partir d’un compte d’utilisateur standard. Une approche PAW fournit une station de travail digne de confiance pour ces comptes sensibles.

Pour obtenir plus d’informations et des instructions d’implémentation, consultez [Stations de travail d’accès privilégié](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Utiliser l’authentification multifacteur

Bonjour précédentes, votre réseau de périmètre a été utilisé toocontrol, accéder aux données toocorporate. Dans un monde privilégie le cloud, mobiles en premier, identité est le plan de contrôle hello : vous l’utilisez toocontrol des services de tooIaaS d’accès à partir de n’importe quel appareil. Vous utilisez également tooget visibilité et un aperçu de comment et où vos données sont utilisées. Protection des identités numériques de hello de vos utilisateurs Azure d’est la pierre angulaire de hello de la protection de vos abonnements à partir de l’usurpation d’identité et autres méfaits.

Une des étapes plus avantageux de hello que vous pouvez prendre toosecure un compte est l’authentification à deux facteurs tooenable. Authentification à deux facteurs est un moyen de l’authentification à l’aide d’un élément dans le mot de passe outre tooa. Il permet d’atténuer les risques hello d’accès par une personne qui gère les tooget par quelqu'un d’autre mot de passe.

[L’authentification multifacteur Azure](../multi-factor-authentication/multi-factor-authentication.md) vous aide à protéger l’accès toodata et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une authentification forte via diverses options de vérification simples : appel téléphonique, SMS, notification sur l’application mobile. Les utilisateurs choisissent la méthode hello qu’ils préfèrent.

toouse de façon plus simple Hello multi-Factor Authentication est l’application mobile de hello Authenticator de Microsoft qui peut être utilisée sur les périphériques mobiles exécutant Windows, iOS et Android. Avec la version la plus récente de Windows 10 et l’intégration de hello de locale d’Active Directory avec Azure Active Directory (Azure AD), hello [Windows Hello for Business](../active-directory/active-directory-azureadjoin-passport-deployment.md) peut être utilisé pour les ressources tooAzure d’authentification unique transparente. Dans ce cas, les appareils Windows 10 de hello sont utilisé comme second facteur d’hello pour l’authentification.

Pour les comptes qui gèrent votre abonnement Azure et pour les comptes qui peuvent se connecter les machines toovirtual, à l’aide de l’authentification multifacteur vous donne un niveau de sécurité beaucoup plu que d’utiliser uniquement un mot de passe. D’autres formes d’authentification à deux facteurs peuvent fonctionner tout aussi bien, mais elles risquent d’être plus complexes à déployer si elles ne sont pas déjà en production.

Hello capture d’écran suivante montre certaines des options de hello disponibles pour l’authentification multifacteur Azure :

![Options de Multi-Factor Authentication](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Limiter et contraindre l’accès administrateur

Il est extrêmement important de sécuriser les comptes hello qui peuvent gérer votre abonnement Azure. compromettre un de ces comptes Hello inverse valeur hello hello toutes les autres étapes que vous pouvez effectuer la confidentialité de tooensure hello et l’intégrité de vos données. Récemment illustrée par hello [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) fuite d’informations confidentielles, les attaques internes présentent un toohello immense menace de sécurité globale de toutes les organisations.

Évaluer particuliers pour les droits d’administration en toothese similaire des critères suivants :

- Effectue-t-elle des tâches nécessitant des privilèges administratifs ?
- La fréquence à laquelle les tâches de hello sont effectuées ?
- Y a-t-il une raison spécifique pourquoi hello ne peut pas être exécutées par un autre administrateur de leur part ?

Documenter tous les autres privilèges de hello toogranting connus autres approches et pourquoi chaque n’est pas acceptable.

Utilisez Hello d’administration juste-à-temps empêche l’existence de hello inutiles de comptes avec des droits élevés pendant les périodes quand ces droits ne sont pas nécessaires. Les comptes disposent de plus de droits pendant une période limitée afin que les administrateurs puissent effectuer leurs tâches. Ensuite, ces droits sont supprimés à fin hello d’un travail d’équipe, ou lorsqu’une tâche est terminée.

Vous pouvez utiliser [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, analyse et contrôle d’accès de votre organisation. Il vous permet de tenir compte des actions hello qui utilisent les personnes de votre organisation. Il apporte également administration juste-à-temps tooAzure AD en introduisant concept hello des administrateurs éligible. Ceux-ci sont des personnes qui ont des comptes avec toobe potentielle de hello accordé des droits d’administrateur. Ces types d’utilisateurs peuvent suivre un processus d’activation et se voir accorder des droits d’administrateur pour une durée limitée.


## <a name="use-devtest-labs"></a>Utiliser DevTest Labs

À l’aide d’Azure pour les laboratoires et des environnements de développement permet de prendre des organisations toogain de test et développement de retards de rangement hello prenant qui présente les approvisionnements en matériel. Malheureusement, un manque de connaissance de Azure ou un toohelp désir accélérer son adoption peut provoquer des toobe d’administrateur hello trop permissif avec attribution des droits. Ce risque peut exposer involontairement hello organisation toointernal attaques. Certains utilisateurs peuvent alors disposer de droits d’accès bien supérieurs à ce qu’ils devraient avoir.

Hello [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) service utilise [du contrôle d’accès](../active-directory/role-based-access-control-what-is.md) (RBAC). À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe dans des rôles qui accordent uniquement le niveau de hello d’accès nécessaires pour les utilisateurs toodo leurs tâches. RBAC est fourni avec des rôles prédéfinis (propriétaire, utilisateur de labo et collaborateur). Vous pouvez même utiliser ces partenaires de rôles tooassign droits tooexternal et simplifier considérablement la collaboration.

DevTest Labs utilise RBAC, il est possible de toocreate supplémentaire, [des rôles personnalisés](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs simplifie non seulement la gestion hello des autorisations, il simplifie hello d’obtention des environnements configurés. Cela vous permet également de traiter les autres défis types des équipes qui travaillent sur des environnements de développement et de test. Il requiert une préparation, mais dans à long terme hello, il sera simplifier les choses pour votre équipe.

Voici certaines des fonctionnalités d’Azure DevTest Labs :

- Le contrôle administratif des hello options toousers disponibles. administrateur de Hello peut gérer les éléments tels que les tailles de machine virtuelle autorisées, nombre maximal de machines virtuelles, et lorsque les ordinateurs virtuels sont démarrés et arrêter de manière centralisée.
- Automatisation de la création de l’environnement de laboratoire
- Suivi des coûts
- Distribution simplifiée des machines virtuelles pour un travail collaboratif temporaire
- Libre-service qui permet aux utilisateurs tooprovision leurs laboratoires à l’aide de modèles.
- Gestion et limitation de la consommation

![À l’aide de DevTest Labs toocreate un laboratoire](./media/azure-security-iaas/devtestlabs.png)

Sans coût supplémentaire est associé à l’utilisation de hello de DevTest Labs. Création de Hello d’ateliers pratiques, des stratégies, des modèles et des artefacts est gratuite. Vous payez pour hello uniquement les ressources Azure utilisés dans vos travaux, tels que les ordinateurs virtuels, des comptes de stockage et des réseaux virtuels.



## <a name="control-and-limit-endpoint-access"></a>Contrôler et limiter l’accès aux points de terminaison

Hébergement des ateliers pratiques ou des systèmes de production dans Azure signifie que vos systèmes doivent toobe accessible à partir de hello Internet. Par défaut, un ordinateur virtuel Windows est accessible à partir de hello Internet le port RDP hello et une machine virtuelle Linux a port SSH de hello ouvert. Mesures de points de terminaison toolimit exposé est nécessaire toominimize hello tout accès non autorisé.

Technologies dans Azure peuvent vous aider à limiter les points de terminaison d’administration de la toothose de hello accès. Vous pouvez notamment utiliser les [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) (NSG) dans Azure. Lorsque vous utilisez Azure Resource Manager pour le déploiement, groupes de sécurité réseau limitent l’accès de hello à partir de tous les réseaux toojust hello gestion des points de terminaison (RDP ou SSH). Lorsque vous pensez NSG, pensez listes de contrôle d'accès (ACL) du routeur. Vous pouvez les utiliser tootightly contrôle hello réseau la communication entre différents segments de vos réseaux Azure. Il s’agit des réseaux toocreating similaires dans des réseaux de périmètre ou d’autres réseaux isolés. Ils n’inspectent pas le trafic de hello, mais ils aident à avec la segmentation de réseau.


Dans Azure, vous pouvez configurer un [VPN de site à site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) à partir de votre réseau local. Un VPN de site à site étend votre service cloud toohello de réseau. Cela vous donne une autre opportunité toouse groupes de sécurité réseau, car vous pouvez également modifier hello toonot de groupes de sécurité réseau autoriser l’accès en tout lieu autre que le réseau local de hello. Vous pouvez imposer que l’administration est effectuée en premier toohello de connexion réseau Azure via VPN.

option de VPN de site à site Hello peut être très intéressante dans les cas où vous hébergez des systèmes de production sont étroitement intégrés à vos ressources locales dans Azure.

Vous pouvez également utiliser hello [point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) option disponible dans les situations où vous souhaitez toomanage les systèmes qui ne doive accéder aux ressources locales tooon. Ces systèmes peuvent être isolés dans leur propre réseau virtuel Azure. Les administrateurs peuvent VPN dans hello Azure hébergé environnement à partir de leur station de travail d’administration.

>[!NOTE]
>Vous pouvez utiliser soit hello de tooreconfigure option VPN qu'accès toomanagement points de terminaison à partir de hello Internet des ACL sur toonot de groupes de sécurité réseau hello.

Une autre option intéressante consiste à envisager un déploiement de type [Passerelle des services Bureau à distance](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md). Vous pouvez utiliser ce déploiement toosecurely connecter les serveurs de bureau tooRemote via HTTPS, lors de l’application plus contrôle les connexions de toothose.

Les fonctionnalités que vous devriez accès tooinclude :

- Administrateur des options toorequests de connexions toolimit à partir de systèmes spécifiques.
- Authentification de carte à puce ou Azure Multi-Factor Authentication
- Contrôle sur les systèmes, une personne peut se connecter à passerelle de hello toovia.
- Contrôle de la redirection des appareils et des disques

## <a name="use-a-key-management-solution"></a>Utiliser une solution de gestion des clés

Gestion de clés sécurisée est tooprotecting essentiels des données dans le cloud de hello. Avec [Azure Key Vault](../key-vault/key-vault-whatis.md), vous pouvez stocker en toute sécurité des clés de chiffrement et des secrets (tels que les mots de passe) dans des modules de sécurité matériels (HSM). Pour une meilleure garantie, vous pouvez importer ou générer des clés HSM.

Microsoft traite vos clés dans des modules de sécurité matériels validés selon la norme « FIPS 140-2 Level 2 » (matériel et microprogramme). Surveillez et auditez l’utilisation des clés avec la journalisation Azure : envoyez les journaux dans Azure ou votre système SIEM (Security Information and Event Management) pour bénéficier d’une analyse et d’une détection des menaces supplémentaires.

Toute personne disposant d’un abonnement Azure peut créer et utiliser des coffres de clés. Bien que Key Vault procure des avantages aux développeurs et aux administrateurs de sécurité, il peut être implémenté et géré par l’administrateur responsable de la gestion des services Azure dans une organisation.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Chiffrer les disques virtuels et le stockage des disques

[Le chiffrement des disques Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) adresses hello risque de vol de données ou l’exposition à partir de tout accès non autorisé qui est effectué par le déplacement d’un disque. disque de Hello peut être attachés tooanother le système comme un moyen de contourner les autres contrôles de sécurité. Utilisation du chiffrement de disque [BitLocker](https://technet.microsoft.com/library/hh831713) dans Windows et d’exploration de données-Crypt Linux tooencrypt système d’exploitation et lecteurs de données. Le chiffrement des disques Azure s’intègre avec le coffre de clés toocontrol et gérer des clés de chiffrement hello. Il est disponible pour des machines virtuelles standard et des machines virtuelles avec stockage premium.

Pour plus d’informations, voir [Azure Disk Encryption pour machines virtuelles Windows et Linux IaaS](azure-security-disk-encryption.md).

Le [chiffrement des services de stockage Azure](../storage/common/storage-service-encryption.md) vous aide à protéger vos données au repos. Il est activé au niveau de compte de stockage hello. Il chiffre les données au fur et à mesure de leur écriture dans nos centres de données ; elles sont déchiffrées automatiquement lorsque vous y accédez. Il prend en charge hello les scénarios suivants :

- Chiffrement des objets blob de blocs, des objets blob d’ajout et des objets blob de pages
- Chiffrement des disques durs virtuels et des modèles archivés mis tooAzure du site
- Chiffrement du système d’exploitation et des disques de données sous-jacents pour les machines virtuelles IaaS créées à l’aide de vos disques durs virtuels

Avant de passer au chiffrement du Stockage Azure, tenez compte de deux limitations :

- Il n’est pas disponible sur les comptes de stockage Classic.
- Il ne crypte les données écrites qu’une fois le chiffrement activé.

## <a name="use-a-centralized-security-management-system"></a>Utiliser un système de gestion centralisée de la sécurité

Vos serveurs doivent toobe surveillé pour la mise à jour corrective, configuration, les événements et les activités qui pourraient être considérées comme des problèmes de sécurité. tooaddress celles concerne, vous pouvez utiliser [centre de sécurité](https://azure.microsoft.com/services/security-center/) et [Operations Management Suite de sécurité et conformité](https://azure.microsoft.com/services/security-center/). Ces deux options Aller au-delà de la configuration de hello hello système d’exploitation. Elles fournissent également l’analyse de configuration hello Hello sous-jacent d’infrastructure, tels que la configuration du réseau et l’utilisation de l’appliance virtuelle.

## <a name="manage-operating-systems"></a>Gérer les systèmes d’exploitation

Dans un déploiement IaaS, vous êtes chargé pour la gestion de hello des systèmes hello que vous déployez, tout comme n’importe quel autre serveur ou station de travail dans votre environnement. Mise à jour corrective, renforcement de la sécurité, attribution des droits et toute autre activité liées maintenance toohello de votre système sont toujours de votre responsabilité. Pour les systèmes qui sont étroitement intégrés avec vos ressources locales, vous pourriez toouse hello les mêmes outils et procédures que vous êtes à l’aide locale pour les éléments tels que les antivirus, contre les logiciels malveillants, la mise à jour corrective et la sauvegarde.

### <a name="harden-systems"></a>Sécurisation renforcée
Tous les ordinateurs virtuels dans Azure IaaS doit être renforcées afin qu’ils exposent uniquement service points de terminaison qui sont requis pour les applications de hello qui sont installées. Pour les machines virtuelles Windows, suivez les recommandations de hello publiés par Microsoft en tant que lignes de base pour hello [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) solution.

Security Compliance Manager est un outil gratuit. Vous pouvez l’utiliser tooquickly configurer et gérer vos bureaux, le centre de données traditionnel et le cloud public et privé à l’aide de la stratégie de groupe et de System Center Configuration Manager.

Security Compliance Manager fournit des stratégies prêtes à l’emploi et des packs de configuration de gestion de la configuration souhaitée testés. Ces lignes de base sont basées sur les recommandations [Instructions de sécurité Microsoft](https://technet.microsoft.com/en-us/library/cc184906.aspx) et les meilleures pratiques du secteur. Ils vous aident à gérer les dérives de configuration, à respecter les exigences de conformité et à réduire les menaces de sécurité.

Vous pouvez utiliser la configuration actuelle de Security Compliance Manager tooimport hello de vos ordinateurs à l’aide de deux méthodes différentes. Tout d’abord, vous pouvez importer des stratégies de groupe Active Directory. Ensuite, vous pouvez importer la configuration hello de « golden master » machine de référence à l’aide de hello [LocalGPO outil](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback la stratégie de groupe local de hello. Vous pouvez ensuite importer stratégie de groupe locale hello dans Security Compliance Manager.

Comparer les normes tooindustry meilleures pratiques pour les personnaliser et créer de nouvelles stratégies et les packs de configuration de gestion de Configuration souhaitée. Les lignes de base ont été publiées pour tous les systèmes d’exploitation pris en charge, y compris la Mise à jour anniversaire Windows 10 et Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Installer et gérer des logiciels anti-programme malveillant

Pour les environnements hébergés séparément à partir de votre environnement de production, vous pouvez utiliser un toohelp d’extension de logiciel anti-programme malveillant protéger vos machines virtuelles et services de cloud computing. Elle s’intègre avec [Azure Security Center](../security-center/security-center-intro.md).


Le [logiciel anti-programme malveillant Microsoft](azure-security-antimalware.md) inclut des fonctionnalités telles que la protection en temps réel, l’analyse planifiée, la correction des logiciels malveillants, la mise à jour des signatures, la mise à jour des moteurs, les rapports d’exemples, la collecte d’événements d’exclusion et la [prise en charge de PowerShell](https://msdn.microsoft.com/library/dn771715.aspx).

![Logiciel anti-programme malveillant Azure](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Installer les mises à jour de sécurité plus récente hello
Certaines charges de travail première hello que les clients déplacent tooAzure sont ateliers pratiques et les systèmes externes. Si vos ordinateurs virtuels hébergés par Azure héberger des applications ou services qui doivent toohello accessible de toobe Internet, soyez vigilant sur la mise à jour corrective. Correctif logiciel au-delà de système d’exploitation de hello. Des vulnérabilités non corrigées sur les applications tierces peuvent également provoquer des tooproblems qui peut être évitée si la gestion des correctifs efficace est en place.

### <a name="deploy-and-test-a-backup-solution"></a>Déployer et tester une solution de sauvegarde

Tout comme les mises à jour de sécurité, une sauvegarde doit toobe gérée hello même façon que vous gérez de toute autre opération. Cela est vrai pour les systèmes qui font partie de votre environnement de production extension toohello cloud. Systèmes de test et développement doivent respecter les stratégies de sauvegarde qui fournissent des fonctions de restauration qui sont les utilisateurs toowhat similaires ont pris l’habitude de, en fonction de leur expérience avec les environnements sur site.

Les charges de production déplacé tooAzure doivent intégrer des solutions de sauvegarde existantes lorsque cela est possible. Vous pouvez également utiliser [Azure Backup](../backup/backup-azure-arm-vms.md) toohelp répondre à vos besoins.


## <a name="monitor"></a>Surveiller

[Centre de sécurité](../security-center/security-center-intro.md) fournit l’évaluation continue de l’état de la sécurité de vos ressources Azure hello tooidentify éventuelles failles de sécurité. Une liste de recommandations vous guide tout au long des processus de hello de la configuration de contrôles nécessaires.

Voici quelques exemples :

- Configuration du logiciel anti-programme malveillant toohelp identifier et supprimer les logiciels malveillants.
- Configuration de sécurité et groupes de règles toocontrol trafic toovirtual ordinateurs du réseau.
- Configuration des pare-feu d’applications web toohelp vous défendre contre des attaques qui ciblent vos applications web.
- Déploiement de mises à jour système manquantes
- Adressage des configurations de système d’exploitation qui ne correspondent pas hello recommandé de lignes de base.

Hello image suivante présente certaines des options hello que vous pouvez activer dans le centre de sécurité.

![Stratégies Azure Security Center](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et dans le cloud. Operations Management Suite étant implémenté sous la forme d’un service cloud, elle peut être déployée rapidement et avec un investissement minimal en ressources d’infrastructure.

Les nouvelles fonctionnalités sont fournies automatiquement, ce qui vous permet d’économiser sur les coûts de mise à niveau et de maintenance. Operations Management Suite s’intègre également avec System Center Operations Manager. Il a toohelp différents composants vous de mieux gérer vos charges de travail Azure, y compris un [sécurité et conformité](../operations-management-suite/oms-security-getting-started.md) module.

Vous pouvez utiliser les fonctionnalités de sécurité et conformité hello dans les informations de tooview Operations Management Suite sur vos ressources. informations de Hello sont organisées en quatre catégories principales :

- **Domaines de sécurité** : explorez davantage les enregistrements de sécurité au fil du temps. Accédez aux évaluations des logiciels malveillants, mises à jour des évaluations, informations de sécurité réseau, informations d’identité et d’accès, et ordinateurs avec des événements de sécurité. Tirer parti du tableau de bord de centre de sécurité Azure toohello accès rapide.
- **Problèmes importants**: rapidement identifier le numéro de hello de problèmes actifs et hello gravité de ces problèmes.
- **Détections (version préliminaire)** : identifiez les modèles d’attaque en visualisant les alertes de sécurité au fur et à mesure qu’elles affectent vos ressources.
- **La menace d’intelligence**: identifier les attaques modèles en affichant le nombre total de hello de serveurs avec trafic IP malveillant sortant, hello contre les menaces type et une carte qui montre la provenance des ces adresses IP.
- **Requêtes de sécurité courantes**: voir une liste de sécurité les plus courantes hello des requêtes que vous pouvez utiliser toomonitor votre environnement. Lorsque vous cliquez sur une de ces requêtes, hello **recherche** panneau s’ouvre et affiche les résultats de hello pour cette requête.

Hello capture d’écran suivante montre un exemple d’information de hello Operations Management Suite peut afficher.

![Instructions de sécurité de base pour Operations Management Suite](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Étapes suivantes


* [Blog de l’équipe de sécurité Azure](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Centre de réponse aux problèmes de sécurité Microsoft](https://technet.microsoft.com/library/dn440717.aspx)
* [Meilleures pratiques et tendances Azure relatives à la sécurité](security-best-practices-and-patterns.md)
