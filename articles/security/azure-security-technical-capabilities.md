---
title: "fonctionnalités techniques de sécurité aaaAzure | Documents Microsoft"
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
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Fonctionnalités techniques de la sécurité Azure

les clients Azure tooassist actuels et futurs comprendre et utiliser hello différentes fonctionnalités liées à la sécurité disponibles dans et environnantes hello plateforme Azure, Microsoft a développé une série de livres blancs, les vues d’ensemble de la sécurité, les meilleures pratiques, et Listes de contrôle. les rubriques de Hello en termes de largeur et la profondeur de plage et sont régulièrement mises à jour. Ce document fait partie de cette série tel qu’indiqué dans la section abstraite de hello ci-dessous. Des informations complémentaires sur cette série consacrée à la sécurité Azure sont mises à votre disposition à cette adresse (URL).

## <a name="azure-platform"></a>Plateforme Azure

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) est une plateforme cloud, composée de services d’infrastructure et d’application, avec des services de données intégrés et une analytique poussée, ainsi que des outils et des services de développement, tous hébergés dans les centres de données du cloud public de Microsoft. Clients utiliser Azure avec de nombreux scénarios, à partir de la base calcul, de mise en réseau et de stockage, toomobile et application des services web, les scénarios de cloud toofull comme Internet des objets et les différentes capacités et peuvent être utilisés avec les technologies open source et déployés en tant que hybride le cloud ou hébergé dans le centre de données d’un client. Azure fournit des technologies de cloud comme blocs de construction toohelp sociétés réduire les coûts, innover rapidement et gérer des systèmes de façon proactive. Lorsque vous générez sur, ou que vous migrez fournisseur de cloud de tooa de ressources informatiques, vous recourez tooprotect des capacités de cette organisation vos applications et les données avec les services hello et contrôles hello ils sécurisent hello toomanage vos ressources de cloud.

Microsoft Azure est hello uniquement informatique fournisseur de cloud qui offre une plateforme sécurisée et cohérente, application et infrastructure-as-a-service pour toowork équipes de leurs compétences de cloud computing différent et les niveaux de complexité du projet, avec des données intégrées services et analytique ouvrent intelligence à partir de données partout où il existe entre les plateformes Microsoft et non-Microsoft, ouvrez infrastructures et outils, en fournissant des choix pour l’intégration de cloud avec locaux ainsi déployer les services cloud Azure dans centres de données sur site. Dans le cadre de hello Cloud approuvé de Microsoft, les clients s’appuient sur Azure pour la sécurité de pointe, la fiabilité, de conformité, confidentialité et hello vaste réseau de personnes, les partenaires et les organisations de toosupport de processus dans le cloud de hello.

Avec Microsoft Azure, vous pouvez :

- Accélérer l’innovation avec le cloud de hello.

- Obtenir des insights pour dynamiser les décisions et les applications métier.

- Créer sans limite et déployer où que vous soyez.

- Protéger vos activités.

## <a name="scope"></a>Scope

point central de Hello de ce livre blanc s’applique à des fonctionnalités de sécurité et de fonctionnalités prenant en charge les composants essentiels de Microsoft Azure, à savoir [Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction), [bases de données SQL Microsoft Azure](https://docs.microsoft.com/azure/sql-database/), [Modèle de machine virtuelle de Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/  ), outils de hello et de l’infrastructure de gérer l’ensemble. Ce livre blanc se concentrent sur tooyou disponible de fonctionnalités techniques Microsoft Azure en tant que clients toofulfil leur rôle dans la protection de sécurité de hello et la confidentialité de leurs données.

importance Hello de comprendre ce modèle de gestion partagé est essentielle pour les clients qui migrent toohello cloud. Fournisseurs de cloud offrent des avantages considérables pour les efforts de conformité et de sécurité, mais ces avantages nullement client hello de protéger leurs utilisateurs, les applications et les offres de service.

Pour les solutions IaaS, client de hello est chargé ou a une responsabilité partagée pour la sécurisation et la gestion de système d’exploitation de hello, la configuration du réseau, applications, identité, les clients et données.  Générer des solutions PaaS sur les déploiements IaaS, le client de hello est toujours chargé ou a une responsabilité partagée pour la sécurisation et la gestion des applications, d’identité, les clients et données. Pour les solutions SaaS, Nonetheless, le client de hello continue toobe directeurs. Ils doivent s’assurer que les données sont classées correctement et qu’ils partagent un toomanage responsabilité leurs utilisateurs et des périphériques de point de terminaison.

Ce document ne fournit pas de couverture détaillés de n’importe quel Hello relatives des composants de la plateforme Microsoft Azure comme Sites Web Azure, Azure Active Directory, HDInsight, Media Services et autres services qui sont situent au-dessus des composants principaux de hello. Même si un minimum d’informations générales sont données ici, les lecteurs sont censés connaître les concepts fondamentaux d’Azure, tels que décrits dans les autres documentations de référence fournies par Microsoft et incluses dans les liens indiqués dans ce livre blanc.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Sécurité disponibles fonctionnalités techniques toofulfil (Customer) responsabilité de l’utilisateur - vue d’ensemble

Microsoft Azure fournit des services qui permettent aux clients de répondre aux exigences de conformité, de confidentialité et de sécurité de hello. Bonjour suivants image permet d’expliquer les services Azure différents disponibles pour les utilisateurs toobuild une infrastructure d’application sécurisés et conformes basée sur des normes industrielles.

![Fonctionnalités techniques de sécurité disponibles - Vue d’ensemble](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Gérer et contrôler l’identité et l’accès utilisateur (protection)

Azure vous permet de protéger des informations professionnelles et personnelles en activant vous toomanage identités d’utilisateur et les informations d’identification et contrôler l’accès.

### <a name="azure-active-directory"></a>Azure Active Directory

Identité et accès management solutions aide Microsoft IT protéger tooapplications d’accès et les ressources sur le centre de données d’entreprise hello et dans le cloud de hello, l’activation des niveaux supplémentaires de validation, telles que l’authentification multifacteur et conditionnel stratégies d’accès. En surveillant les activités suspectes via les fonctions avancées de reporting, d’audit et d’alertes de sécurité, vous êtes en mesure de limiter les problèmes de sécurité potentiels. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) fournit toothousands d’authentification unique des applications de cloud (SaaS) et les applications de tooweb d’accès vous exécutez localement.

Avantages de sécurité d’Azure Active Directory (AD) incluent la possibilité de hello :

- Création et gestion d’une identité unique pour chaque utilisateur de l’entreprise hybride, tout en maintenant la synchronisation des utilisateurs, des groupes et des appareils

- Fournir des applications tooyour, y compris des milliers d’applications SaaS pré-intégrées accès avec authentification unique.

- Sécurisation de l’accès aux applications en appliquant une authentification multifacteur basée sur des règles pour les applications aussi bien locales que cloud

- Configurer un accès à distance sécurisé tooon local web applications via le Proxy d’Application Azure AD.

Le [portail Azure Active Directory](http://aad.portal.azure.com/) fait partie du portail Azure. À partir de ce tableau de bord, vous pouvez obtenir une vue d’ensemble de l’état de hello de votre organisation et Explorer facilement la gestion de répertoire de hello, d’utilisateurs ou d’accès à l’application.

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Voici les principales fonctionnalités de gestion des identités Azure :

- Authentification unique

- Authentification multifacteur

- Surveillance de la sécurité, alertes et rapports Machine Learning

- Gestion des identités et des accès des consommateurs

- Inscription des appareils

- Privileged Identity Management

- Identity Protection

#### <a name="single-sign-on"></a>Authentification unique

[L’authentification unique (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) signifie être en mesure de tooaccess toutes les applications de hello et les ressources que vous avez besoin de toodo entreprise, en vous connectant une seule fois à l’aide d’un compte d’utilisateur. Une fois connecté, vous pouvez accéder à toutes les applications hello nécessaires sans être tooauthenticate requis (par exemple, tapez un mot de passe) une deuxième fois.

De nombreuses entreprises s’appuient sur des applications SaaS, comme Office 365, Box et Salesforce, pour accroître la productivité des utilisateurs finaux. Historiquement, tooindividually du personnel informatique créer et mettre à jour des comptes d’utilisateur de chaque application SaaS, et les utilisateurs devaient tooremember un mot de passe pour chaque application SaaS.

[Azure AD s’étend sur site Active Directory dans le cloud de hello](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), l’activation des utilisateurs toouse principal d’organisation compte de connexion uniquement toonot tootheir les appareils joints à un domaine et des ressources d’entreprise, mais également tous les hello web et les applications SaaS nécessaire pour leur travail.

Non seulement les utilisateurs aient toomanage plusieurs ensembles de noms d’utilisateur et mots de passe, l’accès de l’application peut être automatiquement mis en service ou déprovisionnés en fonction des groupes de l’organisation et leur état en tant qu’employé. [Azure AD introduit des contrôles de sécurité et d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) qui permettent de gérer l’accès utilisateur sur les applications SaaS toocentrally.

#### <a name="multi-factor-authentication"></a>Authentification multifacteur

[Azure multi-Factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) est une méthode d’authentification qui nécessite l’utilisation de hello de plusieurs méthodes de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions. [L’authentification Multifacteur permet de protéger](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) accéder toodata et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Cette méthode fournit une authentification forte par le biais de diverses options de vérification : appel téléphonique, SMS, notification par application mobile ou code de vérification et jetons OAuth tiers.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Surveillance de la sécurité, alertes et rapports Machine Learning

Vous pouvez protéger votre entreprise grâce à la surveillance de la sécurité, aux alertes et aux rapports Machine Learning qui identifient les comportements d’accès incohérents. Vous pouvez utiliser l’accès Azure Active Directory et l’utilisation des rapports toogain visibilité intégrité de hello et la sécurité de répertoire de votre organisation. Avec cette information, un administrateur d’annuaire peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.

Bonjour portail Azure classic ou via [portail d’Azure Active directory](http://aad.portal.azure.com/), [rapports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) sont classées en hello suivant façons :

- D’anomalies – ces rapports contiennent des événements que nous avons trouvé toobe anormale de connexion. Notre objectif est toomake vous prenant en charge de cette activité et vous toodecide en mesure de toobe si un événement est suspect.

- Rapports d’application intégrée : fournissent des indications sur l’utilisation des applications du cloud au sein de votre société. Azure Active Directory permet d’intégrer des milliers d'applications du cloud.

- Erreur – ces rapports indiquent des erreurs qui peuvent se produire lors de la configuration des applications tooexternal de comptes.

- Rapports spécifiques à l’utilisateur : affichent les données d’activité relatives aux appareils/connexions d’un utilisateur spécifique.

- Journaux d’activité – contiennent un enregistrement de tous les événements audités dans hello des dernières 24 heures, 7 jours, ou 30 derniers jours et les modifications d’activité de groupe et activité d’inscription et de réinitialisation de mot de passe de la dernière.

#### <a name="consumer-identity-and-access-management"></a>Gestion des identités et des accès des consommateurs

[Azure B2C Active Directory](https://azure.microsoft.com/services/active-directory-b2c/) est un service de gestion des identités hautement disponible, et globaux, pour les applications consommateur qui s’adapte toohundreds de millions d’identités. Le service peut être intégré sur l’ensemble des plateformes web et mobiles. Vos consommateurs peuvent session tooall vos applications par le biais des expériences personnalisables à l’aide de leurs comptes sociaux existants ou en créant de nouvelles informations d’identification.

Bonjour passé, les développeurs d’applications qui voulaient trop[inscription et connexion des consommateurs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) dans leurs applications aurait consigné leur propre code. Et ils aurait utilisé localement bases de données ou des systèmes toostore noms d’utilisateur et mots de passe. Azure B2C Active Directory offre une meilleur moyen toointegrate consommateur gestion des identités dans les applications à l’aide de hello de plate-forme sécurisée basée sur des normes et un grand ensemble de stratégies extensibles à votre organisation.

Lorsque vous utilisez Azure Active Directory B2C, vos consommateurs peuvent s’inscrire auprès de vos applications à l’aide de leurs comptes sociaux existants (Facebook, Google, Amazon, LinkedIn) ou en créant des informations d’identification (adresse de messagerie et mot de passe, ou nom d’utilisateur et mot de passe).

Enregistrement de l’appareil

[L’inscription de périphérique Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) Foundation hello pour des périphériques [accès conditionnel](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) scénarios. Lorsqu’un appareil est inscrit, Azure Active Directory Device Registration fournit appareil hello avec une identité qui est le périphérique de hello tooauthenticate utilisé lors de la hello utilisateur se connecte. Hello authentifié dispositif et attributs hello du périphérique de hello, peuvent ensuite être des stratégies d’accès conditionnel tooenforce utilisé pour les applications qui sont hébergées dans le cloud de hello et sur site.

Lorsque vous associez un [gestion des appareils mobiles (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) solution comme Intune, les attributs d’appareil hello dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil de hello. Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité.

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) vous permet de gérer, contrôler et surveiller vos identités privilégiées et accéder aux tooresources dans Azure AD, ainsi que d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.

Parfois, les utilisateurs doivent toocarry opérations nécessitant des privilèges dans les ressources Azure ou Office 365 ou d’autres applications SaaS. Cela signifie souvent que les organisations ont toogive les privilèges permanentes d’accès dans Azure AD. C’est un risque de sécurité croissant pour les ressources hébergées dans le cloud, car les entreprises ne peuvent pas suffisamment surveiller ce que ces utilisateurs font avec leurs privilèges d'administrateur. En outre, si un compte d’utilisateur disposant d’un accès privilégié est compromis, cette seule faille peut affecter sa sécurité globale sur le cloud. Azure AD Privileged Identity Management permet tooresolve ce risque.

Grâce à Azure AD Privileged Identity Management, vous pouvez :

- Identifier les utilisateurs qui ont un rôle d’administrateur dans Azure AD

- Activer à la demande « juste à temps » d’un accès administratif tooMicrosoft Online Services comme Office 365 et Intune

- Obtenir des rapports sur l'historique des accès administrateur et sur les modifications apportées aux affectations de l'administrateur

- Recevoir des alertes sur le rôle privilégié de tooa d’accès

#### <a name="identity-protection"></a>Identity Protection

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) est un service de sécurité offrant une vue centralisée des événements à risque et des vulnérabilités potentielles qui affectent les identités de votre organisation. Identity Protection utilise des fonctionnalités existantes de détection des anomalies d’Azure Active Directory (disponibles via les rapports d’activités anormales d’Azure AD) et introduit de nouveaux types d’événements à risque capables de détecter les anomalies en temps réel.

## <a name="secured-resource-access-in-azure"></a>Accès des ressources sécurisées dans Azure

Le contrôle des accès dans Azure s’envisage d’abord dans une perspective de facturation. propriétaire Hello d’un compte Azure, accédé en visitant hello [centre des comptes Azure](https://account.windowsazure.com/subscriptions), est hello administrateur de compte. Les abonnements sont un conteneur pour la facturation, mais ils constituent également une limite de sécurité : chaque abonnement a un Service (administrateur) qui peut ajouter, supprimer et modifier des ressources Azure dans cet abonnement à l’aide de hello [portail Azure classic](https://manage.windowsazure.com/). SA valeur par défaut de Hello d’un nouvel abonnement est hello AA, mais hello AA peut modifier SA hello Bonjour centre des comptes Azure.

![Accès des ressources sécurisées dans Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Les abonnements sont également associés à un répertoire. répertoire de Hello définit un ensemble d’utilisateurs. Ceux-ci peuvent être des utilisateurs d’entreprise ou établissement scolaire ayant créé le répertoire de hello hello, ou ils peuvent être des utilisateurs externes (autrement dit, Microsoft Accounts). Les abonnements sont accessibles par un sous-ensemble de ces utilisateurs d’annuaire qui ont été définis en tant que Service administrateur (SA) ou de Coadministrateur (CA) ; Bonjour seule exception est que, pour des raisons légales, Accounts Microsoft (anciennement Windows Live ID) peuvent être affectés comme administrateur de service ou autorité de certification sans être présents dans le répertoire de hello.

Orientée sécurité doit se concentrent sur fournir aux employés les autorisations exactes hello que dont ils ont besoin. Trop d’autorisations peuvent exposer un tooattackers de compte. Si le nombre d’autorisations est trop faible, les employés ne peuvent pas effectuer leur travail efficacement. Le [contrôle d’accès en fonction du rôle (RBAC) dans Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permet de résoudre ce problème en offrant une gestion précise de l’accès pour Azure.

![Accès des ressources sécurisées ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail. Plutôt que de donner à tous des autorisations illimitées au sein de votre abonnement ou de vos ressources Azure, vous pouvez autoriser uniquement certaines actions. Par exemple, un employé d’utiliser RBAC toolet gérer des ordinateurs virtuels dans un abonnement, tandis que l’autre peut gérer les bases de données SQL dans hello même abonnement.

![Accès des ressources sécurisées dans Azure (RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Chiffrement et sécurité des données dans Azure (protection)

Une option de protection de toodata hello clés dans le cloud de hello est la gestion des comptes pour les états possibles de hello dans vos données susceptibles de se produire, et les contrôles sont disponibles pour cet état. Pour le chiffrement et la sécurité des données Azure recommandations hello être autour hello suivant des États de données.

- Au repos : cela inclut tous les objets de stockage, conteneurs et types d’informations présents de manière statique sur un support physique, qu’il s’agisse d’un disque magnétique ou d’un disque optique.

- En Transit : Lorsque données sont transférées entre des composants, des emplacements ou des programmes, tels que sur le réseau de hello, à travers un bus de service (à partir de local toocloud et vice versa, y compris les connexions hybrides tels que ExpressRoute), ou au cours d’une entrée/sortie processus, il est considéré comme étant en mouvement.

### <a name="encryption--rest"></a>Chiffrement au repos

tooachieve chiffrement au repos suivants de hello :

Prend en charge au moins un des hello recommandé de modèles de chiffrement détaillées dans hello table tooencrypt données suivantes.

| Modèles de chiffrement |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Chiffrement serveur | Chiffrement serveur | Chiffrement serveur | Chiffrement client
| Chiffrement côté serveur à l’aide de clés gérés par le service | Chiffrement côté serveur à l’aide de clés gérées par le client dans Azure Key Vault | Chiffrement côté serveur à l’aide de clés gérés par le client local |
| • Les fournisseurs de Ressources azure effectuer des opérations de chiffrement et le déchiffrement de hello <br> • Microsoft gère les clés de hello <br>Fonctionnalités de cloud complète • | • Les fournisseurs de Ressources azure effectuer des opérations de chiffrement et le déchiffrement de hello<br>• Le client contrôle les clés par le biais d’Azure Key Vault<br>• Fonctionnalité cloud complète | • Les fournisseurs de Ressources azure effectuer des opérations de chiffrement et le déchiffrement de hello <br>• Le client contrôle clés locale <br> • Fonctionnalité cloud complète| • Les services Azure ne peuvent pas voir les données déchiffrées <br>• Les clients conservent les clés localement (ou dans d’autres banques d’informations sécurisées). Les clés ne sont pas disponibles tooAzure services <br>• Fonctionnalité cloud réduite|

### <a name="enabling-encryption-at-rest"></a>Activation du chiffrement au repos

**Identifier tous les emplacements où vos données sont stockées**

objectif Hello du chiffrement au repos est tooencrypt toutes les données. Cela élimine possibilité hello de l’absence des données importantes ou tous les emplacements persistantes. Énumérer toutes les données stockées par votre application. 

> [!Note] 
> Pas simplement « application data » ou « informations d’identification personnelle ', mais toutes les données liées tooapplication notamment compte des métadonnées (mappages d’abonnement, informations de contrat, PII).

Considérez ce qui stocke vous utilisez des données toostore. Par exemple :

- Stockage externe (par exemple, SQL Azure, Document DB, HDInsights, Data Lake, etc.)

- Stockage temporaire (n’importe quel cache local incluant les données du locataire)

- Cache en mémoire (peut être intégrée dans le fichier de page hello.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Tirer parti de chiffrement existante de hello au niveau de prise en charge de rest dans Azure

Pour chaque magasin que vous utilisez, exploiter hello existant de chiffrement prise en charge de Rest.

- Stockage Azure : Voir [Chiffrement du service Stockage Azure pour les données au repos](https://docs.microsoft.com/azure/storage/storage-service-encryption)

- SQL Azure : Voir [Transparent Data Encryption (TDE), SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)

- Machine virtuelle & stockage sur disque local ([Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

Pour le stockage de disque local et de machine virtuelle, utilisez Azure Disk Encryption où il est pris en charge :

IaaS

Services avec des machines virtuelles de IaaS (Windows ou Linux) doivent utiliser [chiffrement de disque Azure](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt les volumes contenant des données client.

PaaS v2

Services qui s’exécutent sur PaaS v2 à l’aide de l’infrastructure de Service permettre utiliser le chiffrement des disques Azure pour tooencrypt d’ensemble d’échelle de Machine virtuelle [mise] leurs ordinateurs virtuels v2 de PaaS.

PaaS v1

Actuellement, Azure Disk Encryption n’est pas pris en charge sur PaaS v1. Par conséquent, vous devez utiliser le niveau de l’application tooencrypt de chiffrement de données au repos persistantes.  Cela inclut, mais n’est pas limité aux données d’application, fichiers temporaires, journaux et vidages sur incident.

La plupart des services doit tenter de chiffrement de hello tooleverage d’un fournisseur de ressources de stockage. Certains services ont toodo le chiffrement explicite, par exemple, un rendu persistant le matériel de clé (certificats, racine / maître des clés) doit être stocké dans le coffre de clés.

Si vous prenez en charge le chiffrement côté service avec des clés de gérée par le client doit toobe un moyen pour la clé de hello hello client tooget toous. Hello pris en charge et recommandé moyen toodo en intégrant avec Azure Key Vault (AKV). Dans ce cas, les clients peuvent ajouter et gérer leurs clés dans Azure Key Vault. Un client peut savoir comment toouse AKV via [mise en route avec le coffre de clés](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate avec Azure Key Vault, vous devez ajouter code toorequest une clé à partir de AKV lorsque nécessaire pour le déchiffrement.

- Consultez [Azure Key Vault – étape par étape](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) pour plus d’informations sur la façon de toointegrate avec AKV.

Si vous prenez en charge les clés gérées par le client, vous devez tooprovide une expérience utilisateur pour hello client toospecify le toouse le coffre de clés (ou URI du coffre de clés).

Comme le chiffrement au repos implique le chiffrement des données client et d’infrastructure, hôte hello, perte hello de clés hello toosystem échec ou activité malveillante peut signifier toutes les données chiffrée de hello est perdue. Il est donc essentiel que le chiffrement au niveau de la solution de Rest dispose d’une récupération d’urgence complète récit toosystem résilient échecs et les activités malveillantes.

Les services qui implémentent le chiffrement au repos sont généralement des clés de chiffrement peuvent quand même être toohello ou de données va reste non chiffrés sur le lecteur d’ordinateur hôte hello (par exemple, dans hello fichier d’échange du système d’exploitation hôte de hello.) Par conséquent, les services doivent vérifier leurs services sur le volume hôte hello est chiffré. toofacilitate cette équipe de calcul a activé déploiement hello de chiffrement de l’hôte, qui utilise [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP et extensions toohello DCM et agent tooencrypt hello volume hôte.

La plupart des services sont implémentés sur des machines virtuelles Azure standard. Ces services devraient automatiquement récupérés le[chiffrement de l’hôte](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) lorsque Compute l’active. Pour les services qui s’exécutent dans les clusters gérés par Compute, le chiffrement de l’hôte est activé automatiquement en même temps que Windows Server 2016 est déployé.

### <a name="encryption-in-transit"></a>Chiffrement en transit

La protection des données en transit doit être un aspect essentiel de votre stratégie de protection des données. Étant donné que les données sont déplacées dans les deux sens à partir de nombreux emplacements, recommandation générale de hello est toujours utiliser des données de tooexchange protocoles SSL/TLS sur les différents sites. Dans certains cas, vous souhaiterez peut-être canal de communication entière tooisolate hello entre vos locaux et le cloud infrastructure à l’aide d’un réseau privé virtuel (VPN).

Pour les données qui transitent entre votre infrastructure locale et Azure, vous devez envisager le recours aux dispositifs de protection appropriés, comme HTTPS ou VPN.

Pour les organisations qui ont besoin d’accéder toosecure à partir de plusieurs tooAzure locaux de stations de travail, utilisez [VPN de site à site Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Pour les organisations qui ont besoin d’accéder toosecure à partir d’une station de travail trouve tooAzure local, utilisez [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Les jeux de données volumineux peuvent être transmis par le biais d’une liaison réseau étendu haut débit dédiée, comme [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si vous choisissez toouse ExpressRoute, vous pouvez également chiffrer les données de salutation à l’aide de niveau application hello [SSL/TLS](https://support.microsoft.com/kb/257591) ou d’autres protocoles pour une protection supplémentaire.

Si vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions se produisent via HTTPS. [API REST de stockage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via le protocole HTTPS peut également être utilisé toointeract avec [Azure Storage](https://azure.microsoft.com/services/storage/) et [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/).

Les organisations qui échouent tooprotect des données en transit sont plus vulnérables pour [man in the middle attaques](https://technet.microsoft.com/library/gg195821.aspx), [espionnage](https://technet.microsoft.com/library/gg195641.aspx)et le piratage de session. Ces attaques peuvent être hello première étape de pouvoir accéder aux données de tooconfidential.

Vous pouvez en savoir plus sur option Azure VPN en lisant l’article de hello [planification et conception pour la passerelle VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Application du chiffrement des données au niveau fichier

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de stratégies de chiffrement, d’identité et d’autorisation utilise sécuriser vos fichiers et les messages électroniques. Azure RMS peut fonctionner sur plusieurs appareils (téléphones, tablettes et PC), en protégeant les données au sein de votre organisation et en dehors de cette dernière. Cette fonctionnalité est possible, car Azure RMS ajoute un niveau de protection reste avec les données de salutation, même quand celles-ci quittent les limites de votre organisation.

Lorsque vous utilisez Azure RMS tooprotect vos fichiers, vous utilisez le chiffrement standard avec prise en charge complète de [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Lorsque vous exploitez Azure RMS pour la protection des données, vous disposez d’assurance de hello protection de hello est conservé avec le fichier de hello, même si elle est copiée toostorage qui n’est pas sous contrôle de code hello du service informatique, tel qu’un service de stockage cloud. Hello même se produit pour les fichiers partagés par courrier électronique, hello est protégé en tant qu’un message électronique de tooan pièce jointe, avec des instructions comment tooopen hello protégés pièce jointe.
Lors de la planification pour l’adoption d’Azure RMS, nous recommandons suivant de hello :

- Installer hello [application de partage RMS](https://technet.microsoft.com/library/dn339006.aspx). Cette application s’intègre avec les applications Office en installant un complément Office, afin que les utilisateurs puissent directement protéger leurs fichiers, en toute simplicité.

- Configurer des applications et services toosupport Azure RMS

- Créez des [modèles personnalisés](https://technet.microsoft.com/library/dn642472.aspx) qui reflètent les besoins de votre entreprise (exemple : un modèle portant sur des données ultra-secrètes, qui doit être appliqué à tous les e-mails ultra-secrets).

Les organisations qui sont faibles sur [classification des données](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) et la protection des fichiers peut-être être plus vulnérables toodata fuite. Sans protection de fichiers appropriées, les organisations ne tooobtain en mesure de gagner en visibilité, surveiller les abus et empêcher tout accès malveillant toofiles.

> [!Note]
> Vous pouvez en savoir plus sur Azure RMS, lisez l’article de hello [prise en main d’Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Sécuriser votre application (protection)
Azure est responsable de la sécurisation d’infrastructure de hello et la plateforme que votre application s’exécute sur, mais il est toosecure de votre responsabilité l’application elle-même. En d’autres termes, vous devez toodevelop, déployer et gérer votre code d’application et le contenu de manière sécurisée. Sans cela, votre code d’application ou le contenu peut toujours être toothreats vulnérable.

### <a name="web-application-firewall-waf"></a>Pare-feu d’applications web (WAF)
Le [pare-feu d’applications Web (WAF, Web Application Firewall)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) est une fonctionnalité de [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) qui protège vos applications web de manière centralisée contre les vulnérabilités et exploits courants.

Pare-feu d’applications Web est basé sur les règles de hello [OWASP avoir des ensembles de règles principales](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 ou 2.2.9. Les applications Web sont de plus en plus la cible d’attaques malveillantes qui exploitent des vulnérabilités connues. Communs à ces attaques sont des attaques par injection SQL, l’écriture de scripts entre sites attaques tooname quelques exemples. Prévention de telles attaques dans le code d’application peut être difficile et peut nécessiter rigoureuse maintenance, mise à jour corrective et la surveillance de plusieurs couches de la topologie de l’application hello. Un pare-feu d’applications web centralisé permet de simplifier la gestion de la sécurité et offre une meilleure assurance aux administrateurs de tooapplication contre les menaces ou les intrusions. Une solution WAF peut réagir également de menace pour la sécurité tooa plus rapide par la mise à jour corrective une vulnérabilité connue à un emplacement central par rapport à la sécurisation de chacune des applications web individuelles. Les passerelles d’application existant peuvent être converti tooa web application pare-feu est activé application passerelle facilement.

Parmi le pare-feu d’applications web protège contre les vulnérabilités web courantes hello inclut :

- Protection contre les injections de code SQL

- Protection de l’exécution de script de site à site

- Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)

- Protection contre les violations de protocole HTTP

- Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept

- Protection contre les robots, les crawlers et les scanneurs

- Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)

> [!Note]
> Pour une liste plus détaillée des règles et les protections Voir hello [ensembles de règles de base](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure fournit également plusieurs facile à utiliser les fonctionnalités toohelp sécuriser le trafic entrant et sortant pour votre application. Azure permet aux clients sécuriser leur code d’application en fournissant en externe également fonctionnalité tooscan votre application web pour les vulnérabilités.

- [Sécurisation de votre application web avec plusieurs méthodes d'authentification et d'autorisation](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Configuration de l'authentification Azure Active Directory pour votre application](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Sécuriser le trafic tooyour application en activant le Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Affectation de force de tout le trafic entrant sur la connexion HTTPS](http://microsoftazurewebsitescheatsheet.info/)

  - [Activation du protocole HSTS (Strict Transport Security)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Restreindre l’accès tooyour application en adresse IP du client](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Restreindre l’accès tooyour application par le comportement du client - fréquence de demande et d’accès concurrentiel](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Analyse du code de votre application web pour rechercher les vulnérabilités à l'aide de l'analyse Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [Configurer l’application web des tooyour tooconnect certificats TLS l’authentification mutuelle toorequire client](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Configurer un certificat client pour la connexion à utiliser à partir de votre application de toosecurely tooexternal ressources](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Supprimer les outils de tooavoid d’en-têtes standard de serveur à partir de l’empreinte de votre application](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Connexion sécurisée de votre application aux ressources d'un réseau privé à l'aide d'un VPN de point à site](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Connexion sécurisée de votre application aux ressources d'un réseau privé à l'aide de connexions hybrides](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure App Service utilise hello même solution anti-programme malveillant utilisée par les Services de cloud computing Azure et les ordinateurs virtuels. toolearn à ce sujet plus faire référence tooour [documentation du logiciel anti-programme malveillant](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Sécuriser votre réseau (protection)
Microsoft Azure inclut un toosupport infrastructure de mise en réseau robuste votre application et les exigences de connectivité de service. La connectivité réseau est possible entre les ressources situées dans Azure, entre locaux et Azure hébergé tooand de hello Internet et des ressources et Azure.

Hello [infrastructure réseau Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permet toosecurely vous connecter des ressources Azure tooeach autres avec [des réseaux virtuels (réseaux virtuels)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique d’abonnement de tooyour réseau dédié hello cloud Azure. Vous pouvez connecter des réseaux virtuels tooyour sur des réseaux locaux.

![Sécuriser votre réseau (protection)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Si vous avez besoin de contrôle d’accès au réseau de base (basé sur IP adresse et hello protocoles TCP ou UDP), vous pouvez ensuite utiliser [groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Un groupe de sécurité réseau (NSG) est une base pare-feu de filtrage des paquets avec état et elle active l’accès toocontrol vous selon un [5-tuple](https://www.techopedia.com/definition/28190/5-tuple).

Mise en réseau Azure prend en charge le comportement de routage hello capacité toocustomize hello pour le trafic réseau sur vos réseaux virtuels Azure. Pour cela, vous pouvez configurer les [itinéraires définis par l’utilisateur](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) dans Azure.

[Le tunneling forcé](https://www.petri.com/azure-forced-tunneling) est un mécanisme que vous pouvez utiliser tooensure vos services ne sont pas autorisées tooinitiate un toodevices de connexion sur Internet de hello.

Prend en charge Azure dédié de réseau local de liaison WAN connectivité tooyour et un réseau virtuel Azure avec [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). lien de Hello entre Azure et votre site utilise une connexion dédiée ne passe pas par hello Internet public. Si votre application Windows Azure est en cours d’exécution dans plusieurs centres de données, vous pouvez utiliser [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute demandes d’utilisateurs intelligemment sur les instances de l’application hello. Vous pouvez également acheminer tooservices trafic ne pas en cours d’exécution dans Azure s’ils sont accessibles à partir de hello Internet.

## <a name="virtual-machine-security-protect"></a>Sécurité de la machine virtuelle (protection)

Les [Machines virtuelles Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/) vous permettent de déployer un large éventail de solutions de calcul de façon agile. Avec la prise en charge de Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP et Azure BizTalk Services, vous pouvez déployer des charges de travail et des langages variés sur la plupart des systèmes d’exploitation.

Avec Azure, vous pouvez utiliser [logiciel anti-programme malveillant](https://docs.microsoft.com/azure/security/azure-security-antimalware) provenant de fournisseurs de sécurité telles que Microsoft, Symantec, Trend Micro et Kaspersky tooprotect vos machines virtuelles à partir de fichiers malveillants, de logiciels de publicité et d’autres menaces.

Microsoft Antimalware pour Azure Cloud Services et Virtual Machines offre une fonctionnalité de protection en temps réel qui permet d’identifier et de supprimer les virus, logiciels espions et autres logiciels malveillants. Microsoft Antimalware fournit des alertes configurables vous avertissant lorsque connu tooinstall de tentatives de logiciels malveillants ou indésirables lui-même ou s’exécuter sur vos systèmes Azure.

[Sauvegarde Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) est une solution évolutive qui protège les données de vos applications, sans investissement en capital et avec des frais de fonctionnement minimaux. Les erreurs rencontrées par les applications peuvent endommager vos données et les erreurs humaines peuvent introduire des bogues dans vos applications. Avec Sauvegarde Azure, vos machines virtuelles exécutant Windows et Linux sont protégées.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) aide à coordonner la réplication, le basculement et la récupération des charges de travail et des applications afin qu’elles soient disponibles à partir d’un site secondaire si votre site principal tombe en panne.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Assurer la conformité : Liste des points à vérifier avec une prudence mesurée pour les services cloud (protection)

Microsoft a développé [hello Cloud Services échéance Diligence liste de vérification](https://aka.ms/cloudchecklist.download) observer les organisations de toohelp diligence qu’ils estiment un cloud toohello de déplacement. Il fournit une structure d’une organisation de toute taille et le type — privés entreprises et organisations du secteur public, notamment l’administration à tous les niveaux et les associations : tooidentify leurs performances, service, gestion des données et les objectifs de gouvernance et configuration requise. Ainsi, les offres de hello toocompare des fournisseurs de services de cloud computing différent, finalement formant base hello pour un contrat de service cloud.

liste de vérification Hello fournit une infrastructure qui aligne by-clause avec une nouvelle norme internationale pour les contrats de service cloud, ISO/IEC 19086. Cette norme offre un ensemble unifié règles pour les organisations toohelp les décisions concernant l’adoption du cloud et créer une base commune pour la comparaison des offres de service cloud.

liste de vérification Hello promeut un cloud toohello déplacement soigneusement neufs, fournissant une aide structurée et une approche cohérente et reproductible permettant de choisir un fournisseur de services cloud.

Opter pour le cloud ne relève plus d’un choix purement technologique. Étant donné que les exigences de la liste de vérification aborde tous les aspects d’une organisation, ils servent à tooconvene toutes les clés internes-décideurs : hello directeur informatique et CISO ainsi juridiques, des risques les professionnels de l’administration, d’approvisionnement et de conformité. Cela augmente l’efficacité de hello du processus de prise de décision de hello et les décisions de toutes pièces dans son raisonnement, ce qui réduit la probabilité hello des obstacles imprévus tooadoption.

En outre, hello liste de vérification :

- Expose les rubriques clés pour les décideurs de début de hello du processus d’adoption hello cloud.

- Prend en charge à des discussions de l’entreprise approfondie sur réglementaires et les objectifs de l’organisation hello confidentialité, les informations d’identification personnelle (PII) et sécurité des données.

- Aide les organisations à identifier les problèmes potentiels qui pourraient avoir un impact sur un projet cloud

- Fournit un ensemble cohérent de questions, par hello même terminologie, définitions, métriques et livrables pour chaque fournisseur, le processus de hello toosimplify de la comparaison des offres de fournisseurs de services de cloud computing différent.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Validation de la sécurité des applications et de l’infrastructure Azure (détection)

[Sécurité opérationnelle Azure](https://docs.microsoft.com/azure/security/azure-operational-security) fait référence toohello services, des contrôles et toousers disponibles de fonctionnalités pour protéger leurs données, les applications et les autres composants dans Microsoft Azure.

![Validation de la sécurité (détection)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Sécurité opérationnelle Azure repose sur une infrastructure qui intègre les connaissances hello acquises via une différentes fonctionnalités qui sont tooMicrosoft unique, y compris hello Microsoft du cycle de vie SDL (Security Development), hello Centre de réponse de sécurité Microsoft programme et une connaissance approfondie du paysage des menaces inquiétudes hello.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) est hello solution de gestion informatique pour cloud hybride de hello. Utilisée seule ou hello de tooextend votre déploiement de System Center existant, OMS vous donne une flexibilité maximale et contrôle pour la gestion de votre infrastructure cloud.

![Microsoft Operations Management Suite (OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Avec OMS, vous pouvez gérer n’importe quelle instance dans n’importe quel cloud, notamment local, Azure, AWS, Windows Server, Linux, VMware et OpenStack, à moindre coût par rapport aux solutions concurrentes. Conçu pour le cloud en premier Bonjour, OMS offre une nouvelle toomanaging d’approche votre entreprise est hello plus rapide et plus économique toomeet nouveaux contrats défis et prendre en compte les nouvelles charges de travail, applications et les environnements de cloud.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) assure des services de surveillance pour OMS en collectant les données de ressources gérées et en les regroupant dans un référentiel central. Ces données peuvent inclure des événements, données de performances ou des données personnalisées fournies par le biais hello API. Une fois collectées, les données de salutation sont disponibles pour la génération d’alertes, analyse et l’exportation.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Cette méthode vous permet de tooconsolidate des données à partir de diverses sources, donc vous pouvez combiner des données à partir de vos services Azure avec votre environnement local. Elle sépare clairement collection hello de données de salutation à l’action de hello entreprise sur ces données afin que toutes les actions sont tooall disponibles les types de données.

### <a name="azure-security-center"></a>Azure Security Center

[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) vous aide à vous empêchez, détectez et répondre toothreats avec une meilleure visibilité et contrôler hello la sécurité de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Centre de sécurité analyse l’état de sécurité hello de vos ressources Azure tooidentify éventuelles failles de sécurité. Une liste de recommandations vous guide tout au long des processus de hello de la configuration de contrôles nécessaires.

Voici quelques exemples :

- Configuration du logiciel anti-programme malveillant toohelp identifier et supprimer les logiciels malveillants

- Configuration réseau sécurité et groupes de règles toocontrol trafic tooVMs

- Configuration des pare-feu d’applications web toohelp vous défendre contre des attaques qui ciblent vos applications web

- Déploiement de mises à jour système manquantes

- Adressage des configurations de système d’exploitation qui ne correspondent pas hello recommandé de lignes de base

Centre de sécurité automatiquement collecte, analyse et intègre des données de journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire comme des programmes de logiciel anti-programme malveillant et les pare-feu. Quand des menaces sont détectées, une alerte de sécurité est créée. Voici quelques exemples de détections :

- Des machines virtuelles compromises qui communiquent avec des adresses IP connues comme étant malveillantes

- Des programmes malveillants avancés qui sont détectés à l’aide du rapport d’erreurs Windows

- Des attaques par force brute contre des machines virtuelles

- Des alertes de sécurité de logiciels anti-programme malveillant et de pare-feu intégrés

### <a name="azure-monitor"></a>Azure Monitor

[Moniteur de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) fournit des pointeurs tooinformation sur des types de ressources. Il offre la visualisation, requête, le routage, alertes, à l’échelle automatique et automation sur chaque ressource Azure (journaux de Diagnostic) et les données à partir de hello infrastructure Azure (journal d’activité).

Les applications cloud sont complexes, et se composent de nombreux éléments mobiles. L’analyse fournit des données tooensure que votre application reste opérationnel et en cours d’exécution dans un état sain. Cela permet également vous toostave désactivé des problèmes potentiels ou de dépanner au-delà de celles.

![Moniteur de Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) en outre, vous pouvez utiliser la surveillance données toogain des informations détaillées relatives à votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle.

L’audit de sécurité de votre réseau est essentiel pour détecter ses vulnérabilités et assurer la conformité avec votre modèle de gouvernance réglementaire et de sécurité informatique. Avec l’affichage du groupe de sécurité, vous pouvez récupérer les règles du groupe de sécurité réseau et de sécurité hello configuré, ainsi hello des règles de sécurité efficace. Liste hello de règles, vous pouvez déterminer ss et ports hello ouverts vulnérabilité du réseau.

### <a name="network-watcher"></a>Network Watcher

[Observateur de réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) est un service régional qui vous permet de toomonitor et diagnostiquer des conditions à un niveau de réseau dans, vers et à partir d’Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure. Ce service inclut la capture de paquets, le tronçon saut suivant, la vérification des flux IP, l’affichage de groupe de sécurité, les journaux de flux de groupe de sécurité réseau. Surveillance au niveau du scénario présente une fin tooend des ressources réseau dans l’analyse de ressource contraste tooindividual réseau.

### <a name="storage-analytics"></a>Storage analytics

[Stockage Analytique](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) peut stocker des métriques qui incluent des données de la capacité et les statistiques groupées des transactions sur le service de stockage tooa de demandes. Les transactions sont déclarées au niveau opération hello API ainsi qu’au niveau de service de stockage hello, et la capacité est signalée au niveau de service de stockage hello. Les données de métriques peuvent être des tooanalyze utilisé d’utilisation de service de stockage, diagnostiquer les problèmes avec les demandes effectuées sur le service de stockage hello et les performances de hello tooimprove des applications qui utilisent un service.

### <a name="application-insights"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) est un service extensible de gestion des performances des applications (APM) destiné aux développeurs web sur de multiples plateformes. Utiliser toomonitor votre application web dynamique. Ce service détecte automatiquement les problèmes de performances. Il inclut toohelp d’outils puissants analytique vous diagnostiquez des problèmes et toounderstand faire de ce que les utilisateurs avec votre application. Il est conçu toohelp vous améliorer en permanence les performances et la facilité d’utilisation. Il fonctionne pour les applications sur un large éventail de plateformes, y compris .NET, Node.js et J2EE, hébergé localement ou dans le cloud de hello. Il s’intègre à votre processus devOps et tooa des points de connexion divers outils de développement.

Il analyse les éléments suivants :

- **Taux de demandes, temps de réponse et taux d’échec** : identifiez les pages les plus consultées, à quel moment de la journée, et déterminez où se trouvent vos utilisateurs. Identifiez les pages qui offrent les meilleures performances. Si vos temps de réponse et votre taux d’échec augmentent lorsqu’il y a plus de requêtes, vous avez peut-être un problème de ressources.

- **Taux de dépendance, temps de réponse et taux d’échec** : déterminez si des services externes vous ralentissent.

- **Exceptions** : analyser les statistiques de hello agrégée, ou choisir des instances spécifiques et explorez de trace de la pile hello et requêtes connexes. Les exceptions de serveur et de navigateur sont signalées.

- **Consultations de pages et performances de chargement** : indiquées par le navigateur de vos utilisateurs.

- **Appels AJAX à partir de pages web** : taux, temps de réponse et taux d’échec.

- **Nombre de sessions et d’utilisateurs**.

- **Compteurs de performances** de vos ordinateurs serveurs Windows ou Linux, par exemple le processeur, la mémoire et l’utilisation du réseau.

- **Diagnostics d’hébergement** de Docker ou Azure.

- **Journaux de suivi des diagnostics** de votre application : pour pouvoir mettre en corrélation les événements de suivi avec les demandes.

- **Événements personnalisés et des mesures** que vous écrivez vous-même dans du code client ou serveur hello, tootrack des événements commerciaux tels que des éléments vendus ou jeux a gagné.
infrastructure Hello pour votre application est généralement constitué de nombreux composants – peut-être un ordinateur virtuel, compte de stockage et réseau virtuel, ou une application web, base de données, serveur de base de données et 3 services tiers. Vous ne voyez pas ces composants comme des entités distinctes, mais plutôt comme des parties associées et interdépendantes d’une seule et même entité. Vous souhaitez toodeploy, gérez et surveillez en tant que groupe. [Le Gestionnaire de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) vous permet de toowork des ressources de hello dans votre solution en tant que groupe.

Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources hello pour votre solution dans une opération unique et coordonnée. Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production). Gestionnaire de ressources fournit la sécurité, l’audit et le balisage des fonctionnalités toohelp gérer vos ressources après le déploiement.

**avantages de Hello d’à l’aide du Gestionnaire de ressources**

Resource Manager offre plusieurs avantages :

- Vous pouvez déployer, gérer et surveiller toutes les ressources hello pour votre solution en tant qu’un groupe, au lieu de gérer ces ressources individuellement.

- Vous pouvez à plusieurs reprises déployer votre solution tout au long du cycle de vie de développement hello et avez confiance que vos ressources sont déployées dans un état cohérent.

- Vous pouvez gérer votre infrastructure à l’aide de modèles déclaratifs plutôt que de scripts.

- Vous pouvez définir des dépendances de hello entre les ressources, afin qu’ils sont déployés dans l’ordre correct de hello.

- Vous pouvez appliquer l’accès contrôle tooall services dans votre groupe de ressources, car le contrôle d’accès en fonction du rôle (RBAC) est en mode natif intégré à la plate-forme de gestion hello.

- Vous pouvez appliquer des balises tooresources toologically organiser toutes les ressources hello dans votre abonnement.

- Vous pouvez de clarifier la facturation de votre organisation en consultant les coûts pour un groupe de ressources de partage hello même balise.

> [!Note]
> Le Gestionnaire de ressources fournit un nouveau toodeploy de façon et gérer vos solutions. Si vous avez utilisé hello classiques de déploiement et souhaitez toolearn sur les modifications de hello, consultez [déploiement du Gestionnaire de ressources de présentation et déploiement classique](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur la sécurité, lisez nos rubriques détaillées sur la sécurité :

- [Audit et journalisation](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Cybercrime](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Conception et sécurité opérationnelle](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Chiffrement](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Gestion de l’identité et de l’accès](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Sécurité du réseau](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Gestion des menaces](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
