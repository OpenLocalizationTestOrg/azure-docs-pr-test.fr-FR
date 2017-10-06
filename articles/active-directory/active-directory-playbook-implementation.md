---
title: "aaaAzure manuel d’implémentation d’Active Directory preuve de concept | Documents Microsoft"
description: "Explorer et implémenter rapidement des scénarios de gestion des identités et des accès"
services: active-directory
keywords: azure active directory, manuel, preuve de concept, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Manuel de preuve de concept Azure Active Directory : Implémentation

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - synchronisation AD tooAzure AD 

Une identité hybride est foundation hello pour la plupart des clients d’entreprise hello ayant déjà un répertoire local. Hello but ici est toointentionally diminue la durée qu’ici en tant que valeur de hello tooshow possible des scénarios réels d’identité et accès hello. 

| Scénario | Blocs de construction| 
| --- | --- |  
| [Extension de votre service cloud de toohello d’identité](#extending-your-on-premises-identity-to-the-cloud) | [Synchronisation des répertoires - synchronisation du code de hachage de mots de passe](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Remarque** : cette étape est facultative si vous disposez déjà de DirSync/ADSync ou de versions antérieures d’Azure AD Connect. Certains scénarios de ce guide peuvent nécessiter une version plus récente d’Azure AD Connect.  <br/>[Personnalisation](active-directory-playbook-building-blocks.md#branding) | 
| [Affecter des licences Azure AD avec des groupes](#assigning-azure-ad-licenses-using-groups) | [Gestion des licences par groupe](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Extension de votre service cloud de toohello d’identité 

1. Bob est l’administrateur Active Directory de hello chez Contoso. Il obtient l’identité de tooenable de spécification de hello en tant que service pour un ensemble d’utilisateurs. Après l’exécution de l’Assistant Azure AD Connect, hello l’identité des utilisateurs cibles hello disponibles dans le cloud de hello. 
2. Bob demande Julie, un des utilisateurs cibles de hello, tooaccess hello volet d’accès Azure Active Directory et vérifiez qu’elle peut s’authentifier. Julie voit une page de connexion personnalisée et un panneau d’accès vide, prêt à activer l’accès aux applications futures.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Affecter des licences Azure AD avec des groupes 

1. Bob hello un administrateur Global Azure AD et souhaite tooallocate Azure AD licences tooa ensemble spécifique d’utilisateurs dans le cadre du déploiement initial de hello d’Azure AD.
2. Bob crée un groupe pour hello utilisateurs pilotes. 
3. Bob affecte le groupe de toohello hello licences
4. Julie, un des travailleurs de l’information hello, est ajoutée le groupe de sécurité toohello dans le cadre de ses fonctions de travail
5. Après un certain temps, Julie a licence d’accès toohello Azure AD premium. Cela permet plusieurs scénarios de preuve de concept hello plus tard.

## <a name="theme---lots-of-apps-one-identity"></a>Thème : un grand nombre d’applications, une seule identité

| Scénario | Blocs de construction| 
| --- | --- |  
| [Intégrer des applications SaaS : authentification unique fédérée](#integrate-saas-applications---federated-sso) | [Configuration de l’authentification unique fédérée SaaS](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Groupes : propriété déléguée](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Intégrer des applications SaaS : authentification unique par mot de passe](#integrate-saas-applications---password-sso) | [Configuration de l’authentification unique par mot de passe SaaS](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [Authentification unique et événements du cycle de vie des identités](#sso-and-identity-lifecycle-events) | [SaaS et cycle de vie des identités](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Sécuriser les comptes d’accès tooShared](#secure-access-to-shared-accounts) | [Configuration des comptes partagés SaaS](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Sécuriser les Applications tooOn local de l’accès à distance](#secure-remote-access-to-on-premises-applications) | [Configuration du proxy d’application](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [Synchroniser les identités LDAP tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [Configuration du connecteur LDAP générique](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Intégrer des applications SaaS : authentification unique fédérée 

1. Bob est hello un administrateur Global Azure AD et reçoit une demande d’hello Marketing service tooenable accès tootheir Instance ServiceNow. Bob recherche didacticiel hello dans la documentation d’Azure AD et suit et délégués hello attribution d’utilisateurs tooKevin d’application toohello, head hello de l’équipe Marketing. 
2. Kevin se connecte en tant que propriétaire hello des droits de ServiceNow et assigne Julie toohello application. Kevin remarque également que le profil de Julie a été créé automatiquement dans ServiceNow
3. Julie est un travailleur de l’information dans le service de Marketing hello. Il ouvre une session dans tooazure AD et recherche toutes les applications SaaS lui est affecté tooin myapps portal. À partir de là, elle obtient en toute transparence tooServiceNow d’accès.
4. service de Marketing Hello veut tooaudit ayant accédé à ServiceNow. Marc télécharge un rapport d’activité et le partage avec Kevin par e-mail.  

### <a name="sso-and-identity-lifecycle-events"></a>Authentification unique et événements du cycle de vie des identités

1. Julie prend un congé, et par la stratégie d’entreprise hello local compte Active Directory est désactivée temporaire. Julie maintenant ne peut pas se connecter tooAzure AD et par conséquent ne peut pas accéder à ServiceNow. 
2. Julie effectue un mouvement latéral de Marketing tooSales. Kevin supprime son accès de ServiceNow. Julie se connecte hello ad azure myapps et elle ne détecte plus hello ServiceNow vignette. Après 10 minutes, Kevin confirme que le compte de Julie a été désactivé à partir de la console de gestion de ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Intégrer des applications SaaS : authentification unique par mot de passe

1. Bob configure accès tooAtlassian HipChat. HipChat a tooSusie d’accès intégration et accordez à l’authentification unique de mot de passe
2. Julie toohello myapps portail se connecte et voit une hello toodownload de lien extension du navigateur Internet Explorer de AD Azure, qui elle télécharge
3. En cliquant sur le lien, elle est invitée à saisir ses informations d’identification (son nom d’utilisateur et son mot de passe) HipChat. Il s’agit d’une opération unique, et après l’exécution de cette dernière, elle a accès tooHipChat
4. Quelques jours plus tard, Julie ouvre le portail myapps et clique de nouveau sur HipChat. Cette fois-ci, elle obtient un accès transparent
5. Kevin, propriétaire de l’application hello HipChat, veut tooaudit ayant accédé application hello. Marc télécharge un rapport d’audit et le partage avec Kevin par e-mail. 

### <a name="secure-access-tooshared-accounts"></a>Sécuriser les comptes d’accès tooShared 

1. Bob est le handle de Twitter toosecure ressources en stockage sous-utilisées hello partagé pour les membres de l’équipe de vente hello. Il ajoute Twitter comme une application SSO et lui affecte le groupe de sécurité toohello Hello équipe de vente. Il a été donné hello informations d’identification toohello partagé compte et qu’il lui fournit dans le système de hello. 
2. Partage des informations d’identification Twitter n’est plus approuvé en raison de personnes toomultiple savoir. Bob permet la substitution automatique de mot de passe hello Twitter.
3. Julie, un membre de l’équipe de vente hello se connecte toohello myapps portal et voit une hello toodownload de lien extension du navigateur Internet Explorer de AD Azure. Elle l’installe.
4. Lorsque vous cliquez sur elle get accèdent directement à tooTwitter. Elle ne connaît pas le mot de passe hello.
5. Arnold fait également partie de l’équipe de vente hello. Il a hello même expérience de Julie dans les étapes 3 et 4
6. service des ventes Hello veut tooaudit ayant accédé à Twitter. Marc télécharge un rapport d’activité et le partage avec Kevin par e-mail. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Sécuriser les Applications tooOn local de l’accès à distance

1. Bob, hello Azure AD un administrateur Global, a reçu de nombreuses demandes tooenable employés tooaccess utile plusieurs ressources locales, par exemple, application de dépenses hello, tout en travaillant à distance. Il suit hello [documentation de Proxy d’Application](active-directory-application-proxy-enable.md) tooinstall un connecteur et publier des dépenses sous la forme d’une application de Proxy d’Application. 
2. Bob partage les URL de l’application hello externe dépenses avec Julie, un des employés de hello qui a besoin d’accéder à distance. Elle accède au lien de hello et après l’authentification AAD, elle est en mesure de tooaccess hello dépenses application et continuer toobe productif lors à distance. 
3. Bob continue toopublish supplémentaires des applications locales à l’aide de hello même processus et donnant accès toousers en fonction des besoins. Il ajoute des conditions d’accès et l’authentification multifacteur pour hello des applications plus sensibles qu’il publie, tooensure une sécurité supplémentaire.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>Synchroniser les identités LDAP tooAzure AD

1. La société de Marc repose sur une infrastructure d’identité complexe. La plupart des utilisateurs de hello est conservée à l’intérieur de Windows Server Active Directory Domain Services (ADDS). Certains d’entre eux sont gérés par le système RH dans Active Directory Lightweight Directory Services (ADLDS).
2. Bob est chargé de l’activation de l’accès des applications de tooSaaS pour tous les utilisateurs (également ces pas présent dans AD DS).
3. Bob configure données toopull connecteur LDAP générique ADLDS dans Azure AD Connect.
4. Bob crée des règles de synchronisation pour les utilisateurs LDAP sont remplies dans le métaverse et tooAzure AD
5. Julie est un utilisateur LDAP ; elle accède à son application SaaS à l’aide de son identité synchronisée



> [!IMPORTANT] 
> Cette configuration avancée suppose d’avoir quelques connaissances de FIM/MIM. En production, nous vous recommandons de soumettre au [Support Premier](https://support.microsoft.com/premier) toutes les questions concernant cette configuration.



## <a name="theme---increase-your-security"></a>Thème : augmenter la sécurité 

| Scénario | Blocs de construction| 
| --- | --- |  
| [Sécuriser l’accès au compte Administrateur](#secure-administrator-account-access) | [Azure MFA avec appels téléphoniques](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Accès sécurisé pour les applications](#secure-access-to-applications) | [Accès conditionnel pour les applications SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Activer l’administration juste-à-temps](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Protéger les identités en fonction du risque](#protect-identities-based-on-risk) | [Détecter les événements à risque](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Déployer des stratégies de risque de connexion](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [S’authentifier sans mots de passe avec l’authentification par certificat](#authenticate-without-passwords-using-certificate-based-authentication) | [Configurer l’authentification par certificat](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Sécuriser l’accès au compte Administrateur

1. Bob est hello administrateur général de Azure AD. Il a identifié Stuart en tant que coadministrateur du service de hello. 
2. Bob configure le compte de Stuart tooalways nécessitent posture de sécurité de l’authentification Multifacteur tooimprove hello
3. Stuart consigne dans toohello portail Azure et que les mentions qu’il doit tooregister sa connexion hello toocontinue numérique de téléphone
4. Les connexions suivantes à partir de Stuart sont désormais protégées avec l’authentification multifacteur et qu’il est désormais un appel téléphonique de tooverify son identité.

### <a name="secure-access-tooapplications"></a>Sécuriser l’accès tooapplications

1. Kevin est propriétaire de l’entreprise hello de ServiceNow. société de Hello veut maintenant ces toologin utilisateurs avec l’authentification Multifacteur lors de l’accès réseau en dehors de l’entreprise hello.
2. Bob, notre administrateur général Azure AD, ajoute un accès conditionnel stratégie toohello ServiceNow application tooenable l’authentification Multifacteur pour l’accès externe
3. Julie, notre travailleur de l’information, se connecte mon portail d’applications et clique sur la vignette de ServiceNow hello. Elle doit désormais se connecter avec l’authentification multifacteur.

### <a name="enable-just-in-time-jit-administration"></a>Activer l’administration juste-à-temps (JIT)

1. Marc et Pierre sont les administrateurs globaux d’Azure Active Directory. Ils veulent des rôles de gestion tooenable JIT accès toohello et également tookeep des enregistrements sur l’utilisation de hello de hello privilégié des rôles.
2. Bob permet PIM dans le locataire Azure AD de hello et devient l’administrateur de la sécurité hello. Il remplace lui-même et appartenance au rôle Administrateur général de Stuart tooeligible permanente.
3. Bob et Stuart exigent que l’activation de leur rôle via hello portail Azure avant les passe tooAzure AD Configuration. 

### <a name="protect-identities-based-on-risk"></a>Protéger les identités en fonction du risque 

1. Julie, une employée de l’information, tente de se connecter à partir d’un navigateur tor. 
2. Bob vérifie le tableau de bord hello Azure AD identity protection et voit la connexion de Julie à partir d’une adresse IP anonyme. l’équipe de sécurité Hello veut toochallenge telle accède à des utilisateurs avec l’authentification Multifacteur
3. Bob permet à Azure AD Identity Protection stratégie toochallenge l’authentification Multifacteur pour les événements de risque moyen ou élevé
4. Le temps passe et Julie se connecte de nouveau à partir du navigateur Tor. Cette fois, elle s’affiche hello stimulation d’authentification Multifacteur

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>S’authentifier sans mots de passe avec l’authentification par certificat

1. Marc est l’administrateur global d’une institution financière qui interdit l’utilisation de mots de passe comme facteur d’authentification pour l’accès à ses applications.
2. Marc active et met en œuvre l’authentification par certificat sur ADFS et Azure AD
3. Julie alors que l’accès à application est invité tooauthenticate à l’aide du certificat

## <a name="theme---scale-with-self-service"></a>Thème : mettre à l’échelle avec le libre-service

| Scénario | Blocs de construction| 
| --- | --- |  
| [Réinitialisation de mot de passe en libre-service](#self-service-password-reset) | [Réinitialisation de mot de passe en libre-service](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Self tooApplications d’accès au Service](#self-service-access-to-applications) | [Self tooApplications d’accès au Service](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Réinitialisation de mot de passe en libre-service 

1. Bob est hello Azure AD Global admin et permet de gestion de mot de passe de Service Self tooa sous-ensemble d’utilisateurs, y compris Julie. 
2. Julie consigne dans toomyapps portal et voir un message de tooregister ses informations de sécurité pour les événements de réinitialisation de mot de passe futures.
3. Après quelques jours, Julie oublie son mot de passe et le réinitialise via le portail Azure AD

### <a name="self-service-access-tooapplications"></a>Self tooApplications d’accès au Service 

1. Kevin est propriétaire de l’entreprise hello de ServiceNow. Il souhaite que les utilisateurs trop « inscrire » pour celle-ci à la demande, au lieu de les ajouter à la fois
2. Bob, notre administrateur général Azure AD, modifie hello ServiceNow application tooenable demandes du libre-service
3. Julie, notre travailleur de l’information, se connecte mon portail d’applications et les clics hello bouton « Ajouter d’autres applications » et voient parmi hello recommandé d’applications ServiceNow. Elle accède portal d’applications toomy précédent, puis voir hello ServiceNow application.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]