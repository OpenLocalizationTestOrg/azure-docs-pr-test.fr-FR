---
title: aaaAzure Active Directory de preuve de concept manuel blocs de construction | Documents Microsoft
description: "Explorer et implémenter rapidement des scénarios de gestion des identités et des accès"
services: active-directory
keywords: azure active directory, manuel, preuve de concept, POC
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Manuel de preuve de concept Azure Active Directory : Blocs de construction

## <a name="catalog-of-roles"></a>Catalogue des rôles

| Rôle | Description | Responsabilité de la preuve de concept (PoC) |
| --- | --- | --- |
| **Équipe Architecture d’identités/Développement** | Cette équipe est généralement hello une qui conçoit hello solution implémente des prototypes, lecteurs des approbations et enfin transmet toooperations | Fournir des environnements hello et de hello celles de l’évaluation hello différents scénarios du point de vue hello facilité de gestion |
| **Équipe des opérations d’identité locale** | Gère hello identité différentes sources locales : les forêts Active Directory, annuaires LDAP, RH et fournisseurs d’identité de fédération. | Fournir tooon local d’accéder aux ressources nécessaires pour hello scénarios de preuve de concept.<br/>Elle doit intervenir aussi peu que possible|
| **Propriétaires techniques des applications** | Propriétaires de techniques de hello différentes applications et services cloud qui seront intègrent à Azure AD | Fournir des informations sur les applications IaaS (éventuellement, instances de test) |
| **Administrateur général Azure AD** | Gère la configuration de hello Azure AD | Fournissent des informations d’identification de service de synchronisation tooconfigure hello. Généralement hello même équipe que l’Architecture d’identité au cours de la preuve de concept, mais distinctes au cours de la phase d’exploitation hello|
| **Équipe de base de données** | Propriétaires de l’infrastructure de base de données hello | Fournir l’environnement tooSQL d’accès (AD FS ou Azure AD Connect) pour la préparation de scénario spécifique.<br/>Elle doit intervenir aussi peu que possible |
| **Équipe réseau** | Propriétaires de l’infrastructure de réseau hello | Fournir l’accès requis au niveau du réseau hello pour la synchronisation de hello sources de données de serveurs tooproperly accès hello et services de cloud computing (règles de pare-feu, ports ouverts, les règles IPSec etc.). |
| **Équipe de sécurité** | Définit la stratégie de sécurité hello et analyse les rapports de sécurité à partir de diverses sources de suivi des résultats. | Fournir des scénarios d’évaluation de sécurité cibles |

## <a name="common-prerequisites-for-all-building-blocks"></a>Configuration requise commune à tous les blocs de construction

Voici quelques conditions préalables pour toute POC avec Azure AD Premium.

| Conditions préalables | les ressources |
| --- | --- |
| Locataire Azure AD défini avec un abonnement Azure valide | [Comment tooget Azure Active Directory de client](active-directory-howto-tenant.md)<br/>**Remarque :** si vous disposez déjà d’un environnement avec des licences Azure AD Premium, vous pouvez obtenir un abonnement de cap zéro en naviguant toohttps://aka.ms/accessaad <br/>En savoir plus : https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ et https://technet.microsoft.com/library/dn832618.aspx |
| Domaines définis et vérifiés | [Ajouter un tooAzure de nom de domaine personnalisé Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Remarque :** certaines charges de travail telles que Power BI peut avoir configuré un client azure AD sous hello couvre. toocheck si un domaine donné est associé tooa client, accédez à toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Si vous obtenez une réponse correcte, puis hello déjà attribué tooa client et reprendre le peut être nécessaire. Dans ce cas, contactez Microsoft pour obtenir des instructions supplémentaires. En savoir plus sur les options de prise de contrôle hello au : [What ' s Inscription libre-service à Azure ?](active-directory-self-service-signup.md) |
| Essai Azure AD Premium ou EMS activé | [Azure Active Directory Premium gratuit pendant un mois](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Vous avez affecté des licences Azure AD Premium ou EMS tooPoC utilisateurs | [License yourself and your users in Azure Active Directory (Accorder une licence à vos utilisateurs et à vous-même dans Azure Active Directory)](active-directory-licensing-get-started-azure-portal.md) |
| Informations d’identification de l’administrateur général Azure AD | [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Facultatif, mais vivement recommandé : environnement de laboratoire parallèle comme solution de secours | [Conditions préalables pour Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Synchronisation des répertoires - Synchronisation du code de hachage de mots de passe (PHS) - Nouvelle installation

Rapprocher temps tooComplete : une heure pour 1 000 utilisateurs

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Serveur tooRun Azure AD Connect | [Conditions préalables pour Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Ciblez les utilisateurs de preuve de concept, Bonjour même domaine et une partie d’un groupe de sécurité et d’unité d’organisation | [Installation personnalisée d’Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD connecter fonctionnalités nécessaires pour hello preuve de concept sont identifiés. | [Connecter Active Directory à Azure Active Directory - Configuration de fonctionnalités de synchronisation](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Vous disposez des informations d’identification nécessaires pour les environnements locaux et cloud  | [Autorisations et comptes Azure AD Connect](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Télécharger la version la plus récente d’Azure AD Connect hello | [Téléchargez Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Installer Azure AD Connect avec chemin d’accès la plus simple de hello : Express <br/>1. Filtrer les temps de Cycle de synchronisation toohello cible unité d’organisation toominimize hello<br/>2. Choisissez le jeu de cibles d’utilisateurs dans le groupe local de hello.<br/>3. Déployer des fonctionnalités hello nécessaires par hello autres thèmes de preuve de concept | [Azure AD Connect : Installation personnalisée : Filtrage domaine et unité organisationnelle](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect : Installation personnalisée : Filtrage de synchronisation basé sur les groupes](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect : Intégration de vos identités locales avec Azure Active Directory : Configuration de fonctionnalités de synchronisation](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Ouvrez hello Azure AD Connect, l’interface utilisateur et de voir hello en cours d’exécution profils terminée (importation, synchronisation et l’exportation) | [Planificateur Azure AD Connect Sync](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Ouvrez hello [portail de gestion Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), accédez Panneau de « Tous les utilisateurs » toohello, ajouter à la colonne « Source d’autorité » et voir les utilisateurs hello apparaissent, marqué correctement comme provenant de « Windows Server Active Directory » | [Portail de gestion Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Considérations

1. Examiner les considérations sur la sécurité de synchronisation du hachage de mot de passe hello [ici](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Si la synchronisation du hachage de mot de passe pour les utilisateurs de production pilote est définitivement pas une option, envisagez de hello suivant alternatives :
   * Créer des utilisateurs de test dans le domaine de production hello. Assurez-vous de ne synchroniser aucun autre compte.
   * Déplacement tooan UAT environnement
2.  Si vous souhaitez toopursue fédération, il est judicieux les coûts de hello toounderstand associé à une solution fédérée fournisseur d’identité locale au-delà de la preuve de concept de hello et mesure contre hello avantages vous recherchez :
    * Il est critique hello afin que vous ayez toodesign pour la haute disponibilité
    * Il s’agit d’un service local que vous devez toocapacity plan
    * Il s’agit d’un service local vous devez toomonitor/mettre à jour/correctifs

En savoir plus : [Présentation de l’identité Office 365 et d’Azure Active Directory - Identité fédérée](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Personnalisation

Rapprocher temps tooComplete : 15 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Ressources (Images, Logos, etc.) ; Pour une meilleure visualisation faites vraiment actifs de hello hello recommandée. | [Ajouter des logos tooyour-page de connexion Bonjour Azure Active Directory de la société](active-directory-branding-custom-signon-azure-portal.md) |
| Facultatif : Si l’environnement de hello possède un serveur ADFS, accéder au thème toocustomize toohello server | [Personnalisation de la connexion utilisateur AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Expérience de connexion client ordinateur tooperform par l’utilisateur |  |
| Facultatif : Les appareils mobiles toovalidate expérience |  |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Accédez tooAzure AD portail de gestion | [Portail de gestion Azure AD - Marque de société](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Télécharger les ressources hello pour la page de connexion hello (logo de héros, petit logo, étiquettes, etc.). Si vous le souhaitez si vous avez AD FS, aligner hello actifs mêmes avec des pages de connexion AD FS | [Ajouter des logos tooyour se connecter et pages du volet d’accès de la société : éléments personnalisables](active-directory-add-company-branding.md) |
| Attendez quelques minutes pour toofully prennent effet hello modification |  |
| Connectez-vous avec hello preuve de concept utilisateur d’informations d’identification toohttps://myapps.microsoft.com |  |
| Confirmer hello apparence dans le navigateur | [Ajouter des logos tooyour se connecter et pages du volet d’accès de la société](active-directory-add-company-branding.md) |
| Si vous le souhaitez, confirmez hello apparence dans d’autres périphériques |  |

### <a name="considerations"></a>Considérations

Si hello ancien apparence reste après la personnalisation de hello vider le cache du client de navigateur hello, puis recommencez l’opération de hello.

## <a name="group-based-licensing"></a>Gestion des licences par groupe

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Tous les utilisateurs POC font partie d’un groupe de sécurité (cloud ou local) | [Créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Panneau toolicenses accédez dans le portail de gestion Azure AD | [Portail de gestion Azure AD : Licences](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Affecter le groupe de sécurité toohello hello licences avec des utilisateurs de la preuve de concept. | [Affecter le groupe de tooa de licences d’utilisateurs dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Considérations

En cas de problèmes éventuels, consultez trop[scénarios, limitations et problèmes connus liés à l’aide du Gestionnaire de licences toomanage groupes dans Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Configuration de l’authentification unique fédérée SaaS

Rapprocher temps tooComplete : 60 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Environnement de hello SaaS disponible de l’application de test. Dans ce guide, nous prenons pour exemple ServiceNow.<br/>Nous vous recommandons vivement de toouse un friction de toominimize test instance sur la navigation dans les mappages et qualité des données existantes. | Accédez toohttps://developer.servicenow.com/app.do# ! / home toostart hello consistant à une instance de test de mise en route |
| Console de gestion administration accès toohello ServiceNow | [Didacticiel : Intégration d’Azure Active Directory à ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Ensemble de la cible d’utilisateurs tooassign hello application. Un groupe de sécurité contenant des utilisateurs de preuve de concept hello est recommandé. <br/>Si la création du groupe hello n’est pas faisable, puis affecter des utilisateurs de hello toodirectly toohello application hello preuve de concept | [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Partager des acteurs de didacticiel tooall hello à partir de la Documentation de Microsoft  | [Didacticiel : Intégration d’Azure Active Directory à ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Définir une réunion de travail et suivez les étapes du didacticiel hello avec chaque acteur. | [Didacticiel : Intégration d’Azure Active Directory à ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Affectez hello application toohello groupe identifié dans hello conditions préalables. Si hello preuve de concept a accès conditionnel dans la portée de hello, vous pouvez reviendrons ultérieurement et ajouter l’authentification Multifacteur et similaires. <br/>Notez que ceci lancera Bonjour processus de déploiement (si configuré) |  [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Utiliser AD Azure management Portal tooadd ServiceNow Application à partir de la galerie| [Portail de gestion Azure AD : Applications d’entreprise](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Nouveautés relatives à la gestion des applications d’entreprise dans Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| Dans le panneau « Authentification unique » de l’application ServiceNow, activez « Authentification basée sur SAML » |  |
| Complétez les champs URL de connexion et Identificateur avec votre URL ServiceNow<br/>Case à cocher hello trop « activer un nouveau certificat »<br/>et enregistrez les paramètres |  |
| Ouvrez Panneau « Configurer ServiceNow » sous hello hello panneau tooview personnalisé des instructions pour vous tooconfigure ServiceNow |  |
| Suivez les instructions tooconfigure ServiceNow |  |
| Dans le panneau Approvisionnement de l’application ServiceNow, activez l’approvisionnement Automatique | [La gestion de compte d’utilisateur de configuration pour les applications d’entreprise dans le nouveau portail de Azure hello](active-directory-enterprise-apps-manage-provisioning.md) |
| Patientez quelques minutes pour que la configuration se termine.  Bonjour attendant, vous pouvez vérifier dans hello rapports de configuration |  |
| Connectez-vous à toohttps://myapps.microsoft.com/ en tant qu’un utilisateur de test qui a accès | [Nouveautés hello panneau d’accès](active-directory-saas-access-panel-introduction.md) |
| Cliquez sur la vignette hello pour application hello qui vient d’être créée. Confirmez l’accès |  |
| Si vous le souhaitez, vous pouvez vérifier les rapports d’utilisation application hello. Notez une latence, donc vous devez toowait certains types de trafic temps toosee hello dans les rapports de hello. | [Rapports d’activité de connexion dans le portail d’Azure Active Directory hello : l’utilisation des applications managées](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Stratégies de rétention des rapports Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considérations

1. Au-dessus de [didacticiel](active-directory-saas-servicenow-tutorial.md) désigne l’expérience de gestion tooold Azure AD. Mais la POC repose sur l’expérience [Démarrage rapide](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away).
2. Si l’application cible de hello n’est pas présente dans la galerie de hello, vous pouvez utiliser « Apportez votre propre application ». Pour en savoir plus : [Découvrez les nouveautés en matière de gestion des applications d’entreprise dans Azure Active Directory : Ajout d’applications personnalisées à partir d’un seul emplacement](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Configuration de l’authentification unique par mot de passe SaaS

Rapprocher temps tooComplete : 15 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Environnement de test pour les applications SaaS. HipChat et Twitter sont des exemples d’authentification unique par mot de passe. Pour toute autre application, vous devez hello des URL exacte de page hello avec html-formulaire de connexion. | [Twitter sur la Place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat sur la Place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Tester des comptes pour les applications hello. | [S’inscrire sur Twitter](https://twitter.com/signup?lang=en)<br/>[S’inscrire gratuitement sur HipChat](https://www.hipchat.com/sign_up) |
| Ensemble de la cible d’utilisateurs tooassign hello application. Une sécurité groupe contenu hello utilisateurs est recommandé. | [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Hello de toodeploy ordinateur local administrateur accès tooa Extension volet d’accès pour Internet Explorer, Chrome ou Firefox | [Extension du volet d’accès pour IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extension du volet d’accès pour Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extension du volet d’accès pour Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Installer l’extension du navigateur hello | [Extension du volet d’accès pour IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extension du volet d’accès pour Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extension du volet d’accès pour Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurez l’application à partir de la galerie | [Nouveautés de la gestion des applications de l’entreprise dans Active Directory de Azure : galerie d’applications nouvelles et améliorées de hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurez l’authentification unique par mot de passe | [La gestion de l’authentification unique pour les applications d’entreprise dans le nouveau portail de Azure hello : l’authentification basée sur mot de passe](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Affectez hello application toohello groupe identifié dans hello conditions préalables | [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Connectez-vous à toohttps://myapps.microsoft.com/ en tant qu’un utilisateur de test qui a accès |  |
| Cliquez sur la vignette hello pour application hello qui vient d’être créée. | [Nouveautés hello volet d’accès ? : l’authentification avec un mot de passe sans approvisionnement d’identité](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Fournissez les informations d’identification des applications hello | [Nouveautés hello volet d’accès ? : l’authentification avec un mot de passe sans approvisionnement d’identité](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Fermez le navigateur de hello et de connexion de répétition hello. Cette fois-ci hello doit s’afficher application de toohello un accès transparent. |  |
| Si vous le souhaitez, vous pouvez vérifier les rapports d’utilisation application hello. Notez une latence, donc vous devez toowait certains types de trafic temps toosee hello dans les rapports de hello. | [Rapports d’activité de connexion dans le portail d’Azure Active Directory hello : l’utilisation des applications managées](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Stratégies de rétention des rapports Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considérations

Si l’application cible de hello n’est pas présente dans la galerie de hello, vous pouvez utiliser « Apportez votre propre application ». Pour en savoir plus : [Découvrez les nouveautés en matière de gestion des applications d’entreprise dans Azure Active Directory : Ajout d’applications personnalisées à partir d’un seul emplacement](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Gardez Bonjour esprit suivant les exigences :
   * L’application doit avoir une URL de connexion connue
   * Hello-page de connexion doit contenir un formulaire HTML avec un plusieurs champs de texte extensions du navigateur hello peuvent remplir automatiquement la zone. Au minimum de hello, elle doit contenir le nom d’utilisateur et mot de passe.

## <a name="saas-shared-accounts-configuration"></a>Configuration des comptes partagés SaaS

Rapprocher temps tooComplete : 30 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Hello la liste des applications cibles et hello URL de connexion exacts avance. Par exemple, vous pouvez utiliser Twitter. | [Twitter sur la Place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[S’inscrire sur Twitter](https://twitter.com/signup?lang=en) |
| Informations d’identification partagées pour cette application SaaS. | [Partage de comptes à l’aide d’Azure AD](active-directory-sharing-accounts.md)<br/>[Version préliminaire de la substitution automatisée du mot de passe Azure AD pour Facebook, Twitter et LinkedIn ! - Blog Enterprise Mobility and Security] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/ ) |
| Informations d’identification pour au moins deux membres de l’équipe qui ont accès hello même compte. Ils doivent faire partie d’un groupe de sécurité. | [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Hello de toodeploy ordinateur local administrateur accès tooa Extension volet d’accès pour Internet Explorer, Chrome ou Firefox | [Extension du volet d’accès pour IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extension du volet d’accès pour Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extension du volet d’accès pour Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Installer l’extension du navigateur hello | [Extension du volet d’accès pour IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extension du volet d’accès pour Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extension du volet d’accès pour Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurez l’application à partir de la galerie | [Nouveautés de la gestion des applications de l’entreprise dans Active Directory de Azure : galerie d’applications nouvelles et améliorées de hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurez l’authentification unique par mot de passe | [La gestion de l’authentification unique pour les applications d’entreprise dans le nouveau portail de Azure hello : l’authentification basée sur mot de passe](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Affectez hello application toohello groupe identifié dans les conditions préalables de hello lors de leur attribuer des informations d’identification | [Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Connectez-vous en tant qu’utilisateurs différents, cette application d’accès comme hello **même compte partagé.**  |  |
| Si vous le souhaitez, vous pouvez vérifier les rapports d’utilisation application hello. Notez une latence, donc vous devez toowait certains types de trafic temps toosee hello dans les rapports de hello. | [Rapports d’activité de connexion dans le portail d’Azure Active Directory hello : l’utilisation des applications managées](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Stratégies de rétention des rapports Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Considérations

Si l’application cible de hello n’est pas présente dans la galerie de hello, vous pouvez utiliser « Apportez votre propre application ». Pour en savoir plus : [Découvrez les nouveautés en matière de gestion des applications d’entreprise dans Azure Active Directory : Ajout d’applications personnalisées à partir d’un seul emplacement](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Gardez Bonjour esprit suivant les exigences :
   * L’application doit avoir une URL de connexion connue
   * Hello-page de connexion doit contenir un formulaire HTML avec un plusieurs champs de texte extensions du navigateur hello peuvent remplir automatiquement la zone. Au minimum de hello, elle doit contenir le nom d’utilisateur et mot de passe.

## <a name="app-proxy-configuration"></a>Configuration du proxy d’application

Rapprocher temps tooComplete : 20 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Abonnement Microsoft Azure AD de base ou Premium, et annuaire Azure AD pour lequel vous êtes administrateur général | [Éditions d’Azure Active Directory](active-directory-editions.md) |
| Une application web hébergée localement que vous aimeriez tooconfigure pour l’accès à distance |  |
| Un serveur exécutant Windows Server 2012 R2 ou Windows 8.1 ou version ultérieure, sur lequel vous pouvez installer hello connecteur Proxy d’Application | [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md) |
| S’il existe un pare-feu dans le chemin d’accès de hello, assurez-vous qu’il est ouvert afin que hello que connecteur peut rendre HTTPS (TCP) demande toohello le Proxy d’Application | [Activer le Proxy d’Application Bonjour Azure portal : conditions préalables du Proxy d’Application](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Si votre organisation utilise le proxy serveurs tooconnect toohello internet, prenez examiner hello blog post travail avec des serveurs proxy locaux existants pour des détails sur la façon de tooconfigure les | [Travailler avec des serveurs proxy locaux existants](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Installation d’un connecteur sur le serveur de hello | [Activer le Proxy d’Application Bonjour Azure portal : installer et inscrire hello connecteur](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Publier l’application locale de hello dans Azure AD en tant qu’une application de Proxy d’Application | [Publier des applications avec le Proxy d’application Azure AD](application-proxy-publish-azure-portal.md) |
| Affectez des utilisateurs de test | [Publier des applications avec le proxy d’application Azure AD : Ajouter un utilisateur de test](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Si vous le souhaitez, vous pouvez configurer une expérience d’authentification unique pour vos utilisateurs | [Fournir l’authentification unique à l’aide du proxy d’application Azure AD](application-proxy-sso-azure-portal.md) |
| Désignée comme application de test en vous connectant portail tooMyApps en tant qu’utilisateur | https://myapps.microsoft.com |

### <a name="considerations"></a>Considérations

1. Pendant que nous vous suggérons de placer le connecteur de hello dans votre réseau d’entreprise, il existe le cas lorsque vous verrez le placer dans le cloud de hello de meilleures performances. En savoir plus : [Considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure Active Directory](application-proxy-network-topology-considerations.md)
2. Pour plus de détails sur la sécurité et pour savoir comment il fournit une solution d’accès à distance sécurisé par le seul maintien des connexions sortantes, consultez : [Considérations de sécurité pour l’accès aux applications à distance à l’aide du proxy d’application Azure AD](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Configuration du connecteur LDAP générique

Rapprocher temps tooComplete : 60 minutes

> [!IMPORTANT]
> Cette configuration avancée suppose d’avoir quelques connaissances concernant FIM/MIM. En production, nous vous recommandons de soumettre au [Support Premier](https://support.microsoft.com/premier) toutes les questions liées à cette configuration.

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Azure AD Connect installé et configuré | Bloc de construction : [Synchronisation des répertoires - Synchronisation du code de hachage de mots de passe](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Instance ADLDS répondant aux exigences | [Référence technique de connecteur LDAP générique : vue d’ensemble de hello connecteur LDAP générique](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Liste des charges de travail dont les utilisateurs se servent et attributs associés à ces charges de travail | [Synchronisation Azure AD Connect : attributs synchronisés tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Étapes

| Étape | les ressources |
| --- | --- |
| Ajoutez un connecteur LDAP générique | [Référence technique au connecteur LDAP générique : Créer un connecteur](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Créez des profils d’exécution pour le connecteur créé (importation complète, importation d’écart, synchronisation complète, synchronisation d’écart, exportation) | [Create a Management Agent Run Profile (Créer un profil d’exécution d’agent de gestion)](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [À l’aide de connecteurs avec hello Azure AD Connect Sync Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Exécutez le profil d’importation complète et vérifiez la présence d’objets dans l’espace de connecteur | [Search for a Connector Space Object (Rechercher un objet d’espace de connecteur)](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[À l’aide de connecteurs avec hello Sync Service Manager de Azure AD Connect : espace de connecteur de recherche](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Créez des règles de synchronisation afin que les objets de métaverse aient les attributs nécessaires pour les charges de travail | [Synchronisation Azure AD Connect : meilleures pratiques pour la modification de configuration par défaut de hello : modifie les règles tooSynchronization](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect Sync : Présentation de l’approvisionnement déclaratif](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect Sync : Présentation des expressions d’approvisionnement déclaratif](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Démarrez le cycle de synchronisation complète | [Synchronisation Azure AD Connect : planificateur : démarrez le Planificateur de hello](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| En cas de problème, procédez au dépannage | [Résoudre les problèmes d’un objet qui ne se synchronise pas tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Vérifiez, qu’utilisateur LDAP peut se connecter et accéder à application hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Considérations

> [!IMPORTANT]
> Cette configuration avancée suppose d’avoir quelques connaissances concernant FIM/MIM. En production, nous vous recommandons de soumettre au [Support Premier](https://support.microsoft.com/premier) toutes les questions liées à cette configuration.

## <a name="groups---delegated-ownership"></a>Groupes : propriété déléguée

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| L’application SaaS (authentification unique fédérée ou authentification unique par mot de passe) a déjà été configurée | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) |
| Groupe de cloud qui a accès toohello application #1 est identifié | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) <br/>[Créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Informations d’identification pour le propriétaire du groupe hello sont disponibles | [Gérer les accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md) |
| Informations d’identification pour les applications l’accès aux hello hello information worker a été identifiée. | [Nouveautés hello panneau d’accès](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Identifie le groupe hello qui a reçu l’accès toohello application et configurer le propriétaire hello de donnée groupe| [Gérer les paramètres de hello pour un groupe dans Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Connectez-vous en tant que propriétaire du groupe hello, consultez l’appartenance au groupe de hello dans l’onglet groupes du panneau d’accès | [Gérer l’accès aux ressources avec les groupes Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Ajouter le travailleur hello souhaité tootest |  |
| Connectez-vous en tant que travailleur hello, confirmez la vignette de hello est disponible | [Nouveautés hello panneau d’accès](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Considérations

Si l’application hello a activé l’attribution, vous devrez peut-être toowait quelques minutes pour hello toocomplete de configuration avant d’accéder à application hello en tant que travailleur hello.

## <a name="saas-and-identity-lifecycle"></a>SaaS et cycle de vie des identités

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| L’application SaaS (authentification unique fédérée ou authentification unique par mot de passe) a déjà été configurée | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) |
| Groupe de cloud qui a accès toohello application #1 est identifié | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) <br/>[Créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Informations d’identification pour les applications l’accès aux hello hello information worker a été identifiée. | [Nouveautés hello panneau d’accès](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Supprimer utilisateur hello à partir de l’application hello de groupe hello est trop affecté| [Gérer l’appartenance à un groupe des utilisateurs dans votre client Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Attendez quelques minutes que l’approvisionnement soit annulé | [Approvisionnement automatique des utilisateurs pour les applications SaaS dans Azure AD : Comment fonctionne l’approvisionnement automatique ?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Dans une session de navigateur distincte, connectez-vous en tant que portail d’applications hello information worker toomy et confirmez cette vignette est manquante | http://myapps.microsoft.com |


### <a name="considerations"></a>Considérations

Extrapoler hello preuve de concept scénario tooleavers et/ou des scénarios de congé. Si l’utilisateur de hello obtient désactivé dans Active Directory local ou supprimé, il n’est plus un toolog de façon toohello application SaaS.

## <a name="self-service-access-tooapplication-management"></a>Self tooApplication d’accès au Service Management

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Identifier les utilisateurs de preuve de concept qui demandent l’accès toohello applications, en tant que partie du groupe de sécurité hello | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) |
| Application cible déployée | Bloc de construction : [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Atteindre le panneau des Applications tooEnterprise dans le portail de gestion Azure AD | [Portail de gestion Azure AD : Applications d’entreprise](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Configurez l’application à partir des conditions préalables avec le libre-service | [Nouveautés en matière de gestion des applications d’entreprise dans Azure Active Directory : Configuration de l’accès aux applications en libre-service](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Connectez-vous en tant que portail d’applications toomy hello information worker | http://myapps.microsoft.com |
| Notez « + ajouter une application » situé du maître d’opérations de page de hello. Utiliser tooget accès toohello application |  |

### <a name="considerations"></a>Considérations

applications Hello choisies peuvent avoir la mise en service des exigences, afin de passer immédiatement toohello application peut entraîner des erreurs. Si l’application hello choisie prend en charge la mise en service avec azure ad et il est configuré, vous pouvez utiliser cela comme un flux entier hello tooshow opportunité tooend de fin de travail. Consultez le bloc de construction hello pour [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) pour obtenir des recommandations supplémentaires

## <a name="self-service-password-reset"></a>Réinitialisation de mot de passe en libre-service

Rapprocher temps tooComplete : 15 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Activez la gestion des mots de passe en libre-service dans votre locataire. | [Réinitialisation de mot de passe Azure Active Directory pour les administrateurs informatiques](active-directory-passwords.md) |
| Activer les mots de passe toomanage d’écriture différée de mot de passe du site. Cela nécessite des versions spécifiques d’Azure AD Connect | [Configuration requise pour l’écriture différée de mot de passe](active-directory-passwords-writeback.md) |
| Identifiez les utilisateurs de preuve de concept de hello qui utilise cette fonctionnalité et assurez-vous qu’ils sont membres d’un groupe de sécurité. les utilisateurs de Hello doivent être des capacités de hello showcase non-administrateurs toofully | [Personnaliser : La gestion du mot de passe AD Azure : restreindre l’accès toopassword réinitialisation](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Accédez tooAzure AD portail de gestion : mot de passe réinitialisé | [Portail de gestion Azure AD : Réinitialisation du mot de passe](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Déterminer la stratégie de réinitialisation du mot de passe hello. Pour des raisons de preuve de concept, vous pouvez utiliser un appel téléphonique et Q & r. Il est recommandé de tooenable d’enregistrement toobe est requis sur le journal dans le panneau de configuration tooaccess |  |
| Déconnectez-vous et reconnectez-vous en tant que professionnel de l’information |  |
| Fournir des données de réinitialisation du mot de passe libre-service hello comme configuré par l’étape 2 | http://aka.ms/ssprsetup |
| Navigateur de hello fermer |  |
| Redémarrer les processus de connexion hello en tant que travailleur hello utilisé à l’étape 4 |  |
| Réinitialiser le mot de passe hello | [Mettre à jour votre mot de passe : Réinitialiser mon mot de passe](active-directory-passwords-update-your-own-password.md) |
| Essayez de vous connecter avec votre nouveau mot de passe tooAzure AD, ainsi que les ressources locales tooon |  |

### <a name="considerations"></a>Considérations

1. Si la mise à niveau hello Azure AD Connect va toocause friction, puis envisagez d’utiliser il par rapport aux comptes de cloud ou rendre une démonstration par rapport à un environnement distinct
2. les administrateurs de Hello présenter une stratégie différente et hello admin à l’aide de mot de passe de compte tooreset hello peut altérer hello preuve de concept et prêter à confusion. Assurez-vous que vous utilisez une opération de réinitialisation utilisateur normal compte tootest hello


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure Multi-Factor Authentication avec les appels téléphoniques

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Identifiez les utilisateurs qui se serviront de l’authentification MFA  |  |
| Utilisez un téléphone disposant d’une bonne réception pour la demande MFA  | [Présentation d'Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Accédez trop panneau « Utilisateurs et groupes » dans le portail de gestion Azure AD | [Portail de gestion Azure AD : Utilisateurs et groupes](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Sélectionnez le panneau Tous les utilisateurs |  |
| Dans le haut hello bouton de choisir « Authentification multifacteur » de la barre | URL directe du portail MFA Azure : https://aka.ms/mfaportal |
| Dans les paramètres de « User » hello sélectionnez utilisateurs hello et les activer pour l’authentification Multifacteur | [États d’utilisateur dans Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Connectez-vous en tant qu’utilisateur de preuve de concept hello et parcourez les processus de preuve hello  |  |

### <a name="considerations"></a>Considérations

1. les étapes de ce bloc de construction définir explicitement l’authentification Multifacteur pour un utilisateur sur toutes les connexions Hello preuve de concept. Il existe d’autres outils, tels que l’accès conditionnel et la protection d’identité, qui sollicitent l’authentification MFA sur plusieurs scénarios ciblés. Il s’agit d’un élément tooconsider lors du déplacement de la preuve de concept tooproduction.
2. étapes de preuve de concept Hello dans ce bloc de construction sont explicitement à l’aide des appels téléphoniques en tant que méthode d’authentification Multifacteur pour la correspondance à la rapidité de hello. Lorsque vous passez des tooproduction de preuve de concept, nous vous recommandons d’utiliser des applications telles que hello [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) comme votre second facteur, chaque fois que possible.
En savoir plus : [DRAFT NIST Special Publication 800-63B (Publication spéciale NIST 800-63B - version préliminaire)](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Accès conditionnel MFA pour les applications SaaS

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Identifier les utilisateurs une preuve de concept tootarget stratégie hello. Ces utilisateurs doivent être dans une stratégie de sécurité groupe tooscope hello accès conditionnel | [Configuration de l’authentification unique fédérée SaaS](#saas-federated-sso-configuration) |
| L’application SaaS a déjà été configurée |  |
| Les utilisateurs de preuve de concept sont déjà attribués toohello application |  |
| Utilisateur de preuve de concept toohello informations d’identification sont disponibles |  |
| L’utilisateur POC est inscrit pour l’authentification MFA. Utilisation d’un téléphone disposant d’une bonne réception | http://aka.ms/ssprsetup |
| Périphérique de réseau interne de hello. Adresse IP configurée dans la plage d’adresses internes de hello | Recherchez votre adresse IP : https://www.bing.com/search?q=what%27s+my+ip |
| Périphérique réseau externe de hello (peut être d’un téléphone à l’aide d’un réseau mobile du transporteur hello) |  |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Accédez tooAzure AD portail de gestion : panneau d’accès conditionnel | [Portail de gestion Azure AD : Accès conditionnel](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Créez une stratégie d’accès conditionnel :<br/>- Ciblez les utilisateurs POC sous Utilisateurs et groupes<br/>- Ciblez l’application POC sous Applications cloud<br/>- Ciblez tous les emplacements, à l’exception des emplacements approuvés, sous Conditions > Emplacements **Remarque :** les adresses IP de confiance sont configurées dans le [portail MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>- Demandez l’authentification MFA sous Autoriser | [Prise en main de l’accès conditionnel dans Azure Active Directory : Configuration de la stratégie](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Accédez à l’application à partir de l’intérieur du réseau d’entreprise | [Prise en main avec un accès conditionnel dans Azure Active Directory : hello stratégie de test](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Accédez à l’application à partir du réseau public | [Prise en main avec un accès conditionnel dans Azure Active Directory : hello stratégie de test](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Considérations

Si vous utilisez la fédération, vous pouvez utiliser Bonjour local fournisseur d’identité (IdP) toocommunicate Bonjour intérieur/extérieur état du réseau d’entreprise avec les revendications. Vous pouvez utiliser cette technique sans avoir de liste de hello toomanage d’adresses IP qui peuvent être complexes tooassess et gérer dans les grandes entreprises. Dans cette configuration, vous devez prendre en compte scénario de « network itinérance » hello (un utilisateur de journalisation à partir du réseau interne de hello et lors de commutateurs connectés emplacements, par exemple, un cybercafé) et assurez-vous que vous comprenez les implications en matière de hello. En savoir plus : [Sécurisation des ressources de cloud avec le serveur Azure Multi-Factor Authentication et AD FS : Adresses IP de confiance pour les utilisateurs fédérés](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

Rapprocher temps tooComplete : 15 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | Ressources |
| --- | --- |
| Identifier hello administrateur global qui faire partie de hello preuve de concept pour PIM | [Commencer à utiliser Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Identifier hello administrateur global qui deviendra hello administrateur de sécurité | [Commencer à utiliser Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Rôles d’administrateur différent dans Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Facultatif : Vérifiez si les administrateurs globaux hello ont e-mail accéder aux notifications par courrier électronique de tooexercise dans PIM | [Nouveautés d’Azure AD Privileged Identity Management ? : configurer les paramètres de l’activation de rôle hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Toohttps://portal.azure.com connexion en tant qu’un administrateur global (GA) et le panneau PIM hello d’amorçage. Hello administrateur Global qui effectue cette étape est amorcée en tant qu’administrateur de sécurité hello.  Appelons cet acteur GA1 | [À l’aide de l’Assistant sécurité hello dans Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Identifier un administrateur global hello et les déplacer de tooeligible permanente. Ce doit être un administrateur distinct de hello celui utilisé à l’étape 1 pour plus de clarté. Appelons cet acteur GA2 | [Azure AD Privileged Identity Management : Comment tooadd ou supprimer un rôle d’utilisateur](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Nouveautés d’Azure AD Privileged Identity Management ? : configurer les paramètres de l’activation de rôle hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Maintenant, connectez-vous en tant que GA2 toohttps://portal.azure.com et essayez de modifier les « Paramètres utilisateur ». Certaines options sont grisées. | |
| Dans un nouvel onglet Bonjour même session comme l’étape 3, accédez toohttps://portal.azure.com maintenant et ajouter hello PIM panneau toohello tableau de bord. | [Comment tooactivate ou désactiver les rôles dans Azure AD Privileged Identity Management : ajouter hello Privileged Identity Management application](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Rôle d’administrateur général de demande d’activation toohello | [Comment tooactivate ou désactiver les rôles dans Azure AD Privileged Identity Management : activer un rôle](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Si GA2 ne s’est jamais inscrit pour l’authentification MFA, l’inscription pour l’authentification Azure MFA est requise |  |
| Revenir en arrière toohello les onglet d’origine à l’étape 3 et cliquez sur le bouton d’actualisation hello dans le navigateur de hello. Notez que vous avez maintenant accès toochange « Paramètres utilisateur » | |
| Si vous le souhaitez, si vos administrateurs généraux ont messagerie activée, vous pouvez vérifier GA1 et de GA2 la boîte de réception et consultez notification hello du rôle hello en cours d’activation |  |
| 8 Vérifiez l’historique des audits hello et observez hello rapport tooconfirm hello une élévation de GA2 est affichée. | [Qu’est-ce qu’Azure AD Privileged Identity Management ? : Passer en revue les activités de rôle](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Considérations

Cette fonctionnalité fait partie d’Azure AD Premium P2 et/ou EMS E5

## <a name="discovering-risk-events"></a>Détecter les événements à risque

Rapprocher temps tooComplete : 20 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Appareil avec navigateur Tor téléchargé et installé | [Téléchargez le navigateur Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Connexion hello toodo accès tooPOC utilisateur | [Manuel d’Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Étapes

| Étape | les ressources |
| --- | --- |
| Ouvrez le navigateur Tor | [Téléchargez le navigateur Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Connectez-vous à toohttps://myapps.microsoft.com avec un compte d’utilisateur de preuve de concept de hello | [Manuel d’Azure Active Directory Identity Protection : Simulation des événements à risque](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Patientez entre 5 et 7 minutes |  |
| Connectez-vous en tant qu’un administrateur global de toohttps://portal.azure.com et ouvrir le panneau de Protection de l’identité de hello | https://aka.ms/aadipgetstarted |
| Panneau des événements risque hello ouvert. Une entrée doit s’afficher sous Connexions depuis des adresses IP anonymes  | [Manuel d’Azure Active Directory Identity Protection : Simulation des événements à risque](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Considérations

Cette fonctionnalité fait partie d’Azure AD Premium P2 et/ou EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Déployer des stratégies de risque de connexion

Rapprocher temps tooComplete : 10 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Appareil avec navigateur Tor téléchargé et installé | [Téléchargez le navigateur Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Accès en tant qu’une preuve de concept toodo hello connexion de l’utilisateur de test |  |
| L’utilisateur POC est inscrit avec une authentification MFA. Assurez-vous que toouse un téléphone doté d’une bonne réception | Bloc de construction : [Azure Multi-Factor Authentication avec les appels téléphoniques](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Connectez-vous en tant qu’un administrateur global de toohttps://portal.azure.com et ouvrez le panneau de Protection de l’identité de hello | https://aka.ms/aadipgetstarted |
| Activez une stratégie en matière de risque à la connexion de la manière suivante :<br/>- Affectée à : utilisateur POC<br/>- Conditions : Risque à la connexion moyen ou élevé (une connexion à partir d’un emplacement anonyme est associée à un niveau de risque moyen)<br/>- Contrôles : demandez l’authentification MFA | [Manuel d’Azure Active Directory Identity Protection : Risque à la connexion](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Ouvrez le navigateur Tor | [Téléchargez le navigateur Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Connectez-vous à toohttps://myapps.microsoft.com avec hello compte d’utilisateur de preuve de concept |  |
| Hello d’avis stimulation d’authentification Multifacteur | [Expériences de connexion avec Azure AD Identity Protection : Récupération de connexion à risque](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Considérations

Cette fonctionnalité fait partie d’Azure AD Premium P2 et/ou EMS E5. toolearn plus sur les événements à risque, visitez : [événements à risque Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Configurer l’authentification par certificat

Rapprocher temps toocomplete : 20 minutes

### <a name="pre-requisites"></a>Conditions préalables

| Conditions préalables | les ressources |
| --- | --- |
| Appareil avec certificat utilisateur alloué (Windows, iOS ou Android) à partir de la PKI d’entreprise | [Déployer des certificats d’utilisateur](https://msdn.microsoft.com/library/cc770857.aspx) |
| Domaine Azure AD fédéré avec ADFS | [Fédération avec Azure AD Connect](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Vue d’ensemble des services de certificats Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Pour les appareils iOS sur lesquels l’application Microsoft Authenticator est installée | [Prise en main hello Microsoft Authenticator application](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Étapes

| Étape | Ressources |
| --- | --- |
| Activez l’authentification de certificat sur ADFS | [Configurer des stratégies d’authentification : tooconfigure l’authentification principale globale dans Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Facultatif : Activez l’authentification par certificat dans Azure AD pour les clients Exchange Active Sync | [Bien démarrer avec l’authentification par certificat dans Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Accédez tooAccess Panneau de configuration et de s’authentifier à l’aide du certificat de l’utilisateur | https://myapps.microsoft.com |

### <a name="considerations"></a>Considérations

toolearn plus sur les réserves de ce déploiement, visitez : [ADFS : l’authentification par certificat auprès d’Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> La possession du certificat utilisateur doit être protégée. Soit par la gestion des appareils ou avec un code confidentiel dans le cas des cartes à puce.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
