---
title: aaaAzure Active Directory FAQ | Documents Microsoft
description: "Forum aux questions sur Active Directory Azure répond aux questions sur comment accéder à application tooaccess Azure et Azure Active Directory et gestion de mot de passe."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Forum Aux Questions sur Azure Active Directory
Azure Active Directory (Azure AD) est une solution IDaaS (Identity as a Service) complète qui couvre tous les aspects de l’identité, la gestion des accès et la sécurité.

Pour plus d’informations, consultez [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Accédez à Azure et à Azure Active Directory
**Q : Pourquoi puis-je « aucun abonnement ne trouvé » lors de le tooaccess Azure AD Bonjour portail classique Azure ?**

**R :** tooaccess hello portail Azure classic, chaque utilisateur a besoin d’autorisations avec un abonnement Azure. Si vous avez un abonnement Office 365 ou Azure AD, passez trop[http://aka.ms/accessAAD](http://aka.ms/accessAAD) pour une étape d’activation. Sinon, vous devez tooactivate gratuitement [compte Azure](https://azure.microsoft.com/pricing/free-trial/) ou un abonnement payant.

Pour plus d'informations, consultez les pages suivantes :

* [Association des abonnements Azure avec Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gérer le répertoire hello pour votre abonnement Office 365 dans Azure](active-directory-manage-o365-subscription.md)

- - -
**Q : quelle est la relation hello entre AD Azure, Office 365 et Azure ?**

**R :** Azure AD vous fournit des fonctionnalités courantes des identités et des accès tooall des services web. Si vous utilisez Office 365, Microsoft Azure, Intune, ou d’autres personnes, vous êtes déjà à l’aide d’Azure AD toohelp désactiver la gestion de l’authentification et l’accès pour tous ces services.

Tous les utilisateurs qui sont configurés de toouse des services web sont définies en tant que comptes d’utilisateur dans une ou plusieurs instances d’Azure AD. Vous pouvez configurer ces comptes pour des fonctionnalités Azure AD gratuites, par exemple l’accès aux applications cloud.

Les services Azure AD payants comme Enterprise Mobility + Security complètent d’autres services web comme Office 365 et Microsoft Azure avec des solutions avancées de gestion et de sécurité à l’échelle de l’entreprise.
- - -
**Q : Pourquoi puis-je connecter toohello portail Azure mais pas hello portail classique Azure ?**

**R :** hello portail Azure ne nécessite pas un abonnement valide, et portail classique de hello nécessite un abonnement valide.  Si vous n’avez pas d’un abonnement, vous ne peut pas se connecter dans le portail classique de toohello.
- - -
**Q : quelles sont les différences de hello entre l’administrateur de l’abonnement et l’administrateur d’annuaire ?**

**R :** par défaut, vous êtes affecté rôle d’administrateur de l’abonnement hello lorsque vous vous inscrivez pour Azure. Un administrateur de l’abonnement peut utiliser un compte Microsoft ou un travail ou compte scolaire à partir du répertoire hello hello abonnement Azure est associé.  Ce rôle est services autorisés toomanage Bonjour portail Azure.

Si d’autres utilisateurs doivent toosign dans et accéder aux services en utilisant hello même abonnement, vous pouvez les ajouter en tant que coadministrateurs. Ce rôle a hello même des privilèges d’accès en tant qu’administrateur de service hello, mais vous ne pouvez pas modifier l’association de hello de répertoires de tooAzure d’abonnements.  Pour plus d’informations sur les administrateurs d’abonnements, consultez [comment tooadd ou modifier les rôles administrateur Azure](../billing-add-change-azure-subscription-administrator.md) et [les abonnements Azure sont associés à Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Azure AD a un ensemble différent de répertoire de hello toomanage admin rôles et fonctionnalités liées à identité.  Ces administrateurs ont accès toovarious fonctionnalités Bonjour portail Azure ou hello portail Azure classic. rôle de l’administrateur Hello détermine les opérations possibles, telles que créer ou modifier des utilisateurs, attribuer des rôles d’administrateur tooothers, réinitialiser les mots de passe utilisateur, gérer les licences utilisateur ou gérer les domaines.  Pour plus d’informations sur les administrateurs de répertoires Azure AD et leurs rôles, consultez [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md).

Par ailleurs, les services Azure AD payants comme Enterprise Mobility + Security complètent d’autres services web, tels qu’Office 365 et Microsoft Azure, avec des solutions avancées de gestion et de sécurité à l’échelle de l’entreprise.

- - -
**Q : Existe-t-il un rapport qui indique la date d’expiration de mes licences utilisateur Azure AD ?**

**R :** Non.  Ce n’est pas le cas pour l’instant.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Prise en main d’Azure AD hybride


**Q : Comment quitter un client quand je suis ajouté comme collaborateur ?**

**R :** lorsque vous sont ajoutés client de l’organisation tooanother comme un collaborateur, vous pouvez utiliser hello « client du sélecteur » dans tooswitch droite supérieure de hello entre les clients.  Actuellement, il n’existe aucun hello tooleave de façon invitation d’organisation, et Microsoft travaille sur la fourniture de cette fonctionnalité.  Jusqu'à ce que cette fonctionnalité est disponible, vous pouvez demander à hello inviter organisation tooremove vous à partir de leur client.
- - -
**Q : Comment puis-je connecter mon tooAzure de répertoire Active Directory local ?**

**R :** vous pouvez vous connecter à votre tooAzure de répertoire local AD à l’aide d’Azure AD Connect.

Pour plus d’informations, consultez [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).

- - -
**Q : Comment configurer l’authentification unique entre mon annuaire local et mes applications cloud ?**

**R :** vous ne devez tooset haut session unique (SSO) entre votre annuaire local et le Azure AD. Tant que vous accédez à vos applications cloud via Azure AD, service de hello lecteurs automatiquement vos utilisateurs toocorrectly s’authentifier avec leurs informations d’identification locales.

L’implémentation du SSO à partir de l’emplacement local peut être facilement mise en œuvre à l’aide de solutions de fédération telles que les services de fédération Active Directory (AD FS) ou en configurant la synchronisation du hachage de mot de passe. Vous pouvez facilement déployer les deux options à l’aide d’Assistant de configuration hello Azure AD Connect.

Pour plus d’informations, consultez [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).

- - -
**Q : Azure AD fournit-il un portail en libre-service aux utilisateurs de mon organisation ?**

**R :** Oui, Azure AD vous offre hello [panneau d’accès Azure AD](http://myapps.microsoft.com) pour utilisateur libre-service et d’accès aux applications. Si vous êtes un client Office 365, vous pouvez trouver un grand nombre de hello mêmes fonctionnalités dans le portail de hello Office 365.

Pour plus d’informations, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

- - -
**Q : Azure AD m’aide-t-il à gérer mon infrastructure locale ?**

**R :** Oui. Bonjour Azure AD Premium edition vous offre Azure AD Connect Health. Azure AD Connect Health vous permet de surveiller et d’obtenir un aperçu de votre identité locale hello infrastructure et les services de synchronisation.  

Pour plus d’informations, consultez [surveiller votre identité infrastructure et la synchronisation services locaux dans le cloud de hello](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Gestion des mots de passe
**Q : Puis-je utiliser l’écriture différée de mot de passe Azure AD sans synchronisation de mot de passe ? (Dans ce scénario, est-il possible toouse Azure AD réinitialisation de mot de passe libre-service (SSPR) avec le mot de passe pas de magasin et d’écriture différée des mots de passe dans le cloud de hello ?)**

**R :** vous n’avez pas besoin toosynchronize votre Active Directory des mots de passe tooAzure AD tooenable en écriture différée. Dans un environnement fédéré, Azure AD-session unique (SSO) s’appuie sur utilisateur de hello tooauthenticate hello locale active. Ce scénario ne nécessite pas de toobe de mot de passe local hello suivie dans Azure AD.

- - -
**Q : combien de temps faut-il pour un toobe de mot de passe mis à jour tooActive annuaire local ?**

**R :** L’écriture différée de mot de passe fonctionne en temps réel.

Pour en savoir plus, voir [Prise en main de la gestion de mot de passe](active-directory-passwords-getting-started.md).

- - -
**Q : Puis-je utiliser l’écriture différée de mot de passe avec des mots de passe gérés par un administrateur ?**

**R :** Oui, si vous disposez d’un mot de passe en écriture différée activée, les opérations de mot de passe hello effectuées par un administrateur sont réécrits environnement local de tooyour.  

Pour obtenir des réponses plus liés toopassword des questions, consultez [gestion de mot de passe de questions fréquemment posées](active-directory-passwords-faq.md).
- - -
**Q : que puis-je faire si je ne parviens pas à mémoriser mon mot de passe existant Office 365/Azure AD lors de la tentative de toochange mon mot de passe ?**

**R :** Pour ce type de situation, plusieurs options s’offrent à vous.  Utilisez la réinitialisation de mot de passe en libre-service si elle est disponible.  Le fonctionnement de la réinitialisation de mot de passe en libre-service dépend de la façon dont elle est configurée.  Pour plus d’informations, consultez [comment un mot de passe hello réinitialisation portail travail](active-directory-passwords-best-practices.md).

Pour les utilisateurs d’Office 365, votre administrateur peut réinitialiser un mot de passe hello à l’aide de hello étapes [réinitialiser les mots de passe utilisateur](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Pour les comptes Azure AD, administrateurs peuvent réinitialiser les mots de passe à l’aide de valeurs hello suivantes :

- [Réinitialiser les comptes Bonjour portail Azure](active-directory-users-reset-password-azure-portal.md)
- [Réinitialiser les comptes dans le portail classique de hello](active-directory-create-users-reset-password.md)
- [Utiliser PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Sécurité
**Q : Les comptes sont-ils verrouillés après un nombre spécifique de tentatives infructueuses, ou une stratégie plus élaborée est-elle utilisée ?**</br>
Nous utilisons un compte de toolock stratégie plus sophistiquées.  Cela est basée sur IP hello de demande de hello et mots de passe hello entrés. Durée Hello du verrouillage de hello augmente également en fonction de probabilité hello qu’il s’agit d’une attaque.  

**Q : certains mots de passe (communs) refusés par hello messages « ce mot de passe a été utilisé réduire fois », cela fait référence toopasswords utilisé dans active directory en cours de hello ?**</br>
Cela fait référence toopasswords global communs, tels que toutes les variantes de « Password » et « 123456 ».

**Q : Une demande de connexion émanant de sources douteuses (botnets, point de terminaison Tor) sera-t-elle bloquée dans un client B2C ou nécessite-t-elle un client d’une édition De base ou Premium ?**</br>
Nous disposons d’une passerelle qui filtre les demandes et offre une certaine protection contre les botnets. Elle s’applique à tous les clients B2C.

## <a name="application-access"></a>Accès aux applications
**Q : Où puis-je trouver une liste des applications qui sont déjà intégrées à Azure AD et leurs fonctionnalités ?**

**R :** Azure AD offre plus de 2 600 applications pré-intégrées développées par Microsoft, des fournisseurs de services d’application et des partenaires. Toutes les applications pré-intégrées prennent en charge l’authentification unique (SSO). L’authentification unique vous permet d’utiliser vos informations d’identification d’organisation de tooaccess vos applications. Certaines applications de hello prennent également en charge l’annulation du déploiement et de mise en service automatisée.

Pour obtenir une liste complète des applications pré-intégrées de hello, consultez hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**Q : que se passe-t-il si hello application qu'ai-je besoin n’est pas dans le marketplace d’Azure AD hello ?**

**R :** Azure AD Premium vous permet d’ajouter et de configurer n’importe quelle application. Vous pouvez configurer, selon les fonctionnalités de votre application et vos préférences, l’authentification unique et l’approvisionnement automatisé.  

Pour plus d'informations, consultez les pages suivantes :

* [Configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello](active-directory-saas-custom-apps.md)
* [SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications](active-directory-scim-provisioning.md)

- - -
**Q : comment les utilisateurs s’en tooapplications à l’aide d’Azure AD ?**

**R :** Azure AD offre plusieurs moyens pour les utilisateurs tooview et accéder à leurs applications, telles que :

* volet d’accès Hello Azure AD
* Lanceur d’applications Hello Office 365
* Applications toofederated connexion directe
* Des liens profonds toofederated, basé sur le mot de passe, ou les applications existantes

Pour plus d’informations, consultez [déploiement d’Azure AD intégré applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**Q : quelles sont les façons hello Azure AD permet une authentification et tooapplications de l’authentification uniques ?**

**R :** Azure AD prend en charge de nombreux protocoles standardisés pour l’authentification et l’autorisation, tels que SAML 2.0, OpenID Connect, OAuth 2.0 et WS-Federation. Azure AD prend également en charge la mise en coffre du mot de passe et les fonctionnalités d’authentification automatisées pour les applications qui prennent uniquement en charge l’authentification basée sur les formulaires.  

Pour plus d'informations, consultez les pages suivantes :

* [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md)
* [Protocoles d’authentification Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Fonctionnement de l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**Q : Puis-je ajouter des applications si l’exécution s’effectue en local ?**

**R :** Proxy d’Application Azure AD fournit vous avec un accès facile et sécurisé aux applications web tooon local que vous choisissez. Vous pouvez accéder à ces applications Bonjour même façon que vous accédez à votre logiciel comme un service (SaaS) les applications dans Azure AD. Il n’est pas nécessaire pour une connexion VPN ou toochange votre infrastructure réseau.  

Pour plus d’informations, consultez [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).

- - -
**Q : Comment faire pour imposer l’authentification multifacteur aux utilisateurs qui accèdent à une application spécifique ?**

**R :** L’accès conditionnel Azure AD vous permet d’affecter une stratégie d’accès unique à chaque application. Dans votre stratégie, vous pouvez exiger l’authentification multifacteur toujours, ou lorsque les utilisateurs ne sont pas connectés toohello les réseau local.  

Pour plus d’informations, consultez [sécurisation de l’accès tooOffice 365 et d’autres applications connectées tooAzure Active Directory](active-directory-conditional-access.md).

- - -
**Q : Qu’est-ce que l’approvisionnement automatique des utilisateurs pour les applications SaaS ?**

**R :** création de hello tooautomate utilisent Azure AD, la maintenance et la suppression des identités des utilisateurs dans le nombre d’applications SaaS populaires cloud.

Pour plus d’informations, consultez [automatiser la configuration de l’utilisateur et l’annulation de tooSaaS des applications avec Azure Active Directory](active-directory-saas-app-provisioning.md).

- - -
**Q : Puis-je configurer une connexion LDAP sécurisée avec Azure AD ?**

**R :** Non. Azure AD ne prend pas en charge le protocole LDAP de hello.
