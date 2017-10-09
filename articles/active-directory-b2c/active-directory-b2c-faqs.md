---
title: Forum aux questions (FAQ) - Azure AD B2C | Microsoft Docs
description: Forum aux questions sur Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C : Forum aux questions (FAQ) 
Cette page répond aux questions fréquemment posées sur hello B2C d’Azure Active Directory (Azure AD). N'hésitez pas à la consulter pour vous tenir au courant des mises à jour.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>Puis-je utiliser les fonctionnalités d’Azure AD B2C dans mon client Azure AD existant, basé sur les employés ?
Azure AD et Azure AD B2C sont des offres de produits distincts et ne peut pas coexister dans hello même client.  Un locataire Azure AD représente une organisation.  Un locataire Azure AD B2C représente une collection de toobe identités utilisée avec les applications de confiance.  Avec les stratégies personnalisées (en version préliminaire publique), Azure AD B2C peut fédérer tooAzure AD permettant l’authentification des employés dans une organisation.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Puis-je utiliser connexion sociale Azure AD B2C tooprovide (Facebook et Google +) dans Office 365 ?
Azure AD B2C ne peut pas être des utilisateurs tooauthenticate utilisé pour Microsoft Office 365.  Azure AD est la solution Microsoft pour la gestion des applications de tooSaaS accès employé et il comporte des fonctionnalités conçues à cet effet, telles que l’accès conditionnel et de licence.  Azure AD B2C fournit une plateforme de gestion des identités et des accès pour la création d’applications web et mobiles.  Lorsque Azure AD B2C est un locataire Azure AD de tooan toofederate configuré, locataire Azure AD de hello gère tooapplications accès employé qui s’appuient sur Azure AD B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Que sont les comptes locaux dans Azure AD B2C ? En quoi sont-ils différents des comptes professionnels ou scolaires dans Azure AD ?
Dans un locataire Azure AD, les utilisateurs qui appartiennent toohello locataire connectez-vous avec une adresse de messagerie sous forme de hello `<xyz>@<tenant domain>`.  Hello `<tenant domain>` est un des hello vérifié domaines Bonjour locataire ou hello initiales `<...>.onmicrosoft.com` domaine. Ce type de compte est un compte professionnel ou scolaire.

Dans un locataire Azure AD B2C, la plupart des applications souhaitez utilisateur de hello dans toosign avec n’importe quelle adresse de messagerie arbitraire (par exemple, joe@comcast.net, bob@gmail.com, sarah@contoso.com, ou jim@live.com). Ce type de compte est un compte local.  Nous prenons également en charge les noms d’utilisateur arbitraires en tant que comptes locaux (par exemple joe, bob, sarah ou jim). Vous pouvez choisir un de ces deux types de compte local en configurant Azure AD B2C Bonjour portail Azure.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Quels fournisseurs d’identité sociaux prenez-vous en charge maintenant ? Ceux qui voulez-vous planifier toosupport Bonjour futures ?
Nous prenons actuellement en charge Facebook, Google+, LinkedIn, Amazon, Twitter (aperçu), WeChat (aperçu), Weibo (aperçu) et QQ (aperçu). Nous ajouterons la prise en charge d’autres fournisseurs d’identité sociaux populaires en fonction de la demande des clients.

Azure AD B2C a également ajouté la prise en charge des [stratégies personnalisées](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Ces [des stratégies personnalisées](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) autoriser un toocreate développeur leur propre stratégie qu’avec n’importe quel fournisseur d’identité qui prend en charge [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) ou SAML. 

Bien démarrer avec les stratégies personnalisées en consultant notre [pack de démarrage des stratégies personnalisées](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Configurer les étendues toogather plus d’informations sur les consommateurs à partir de différents fournisseurs d’identité sociaux ?
Non, mais cette fonctionnalité est sur notre feuille de route. les étendues de valeur par défaut Hello utilisées pour notre jeu pris en charge des fournisseurs d’identité sociaux sont :

* Facebook : e-mail
* Google+ : e-mail
* Compte Microsoft : profil de messagerie openid
* Amazon : profil
* LinkedIn : r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Mon application a-t-il toobe s’exécuter sur Azure pour qu’il fonctionne avec Azure AD B2C
Non, vous pouvez héberger votre application n’importe où (dans le cloud de hello ou localement). Tout ce dont il a besoin toointeract avec Azure AD B2C est hello toosend de capacité et de recevoir des requêtes HTTP sur les points de terminaison accessibles publiquement.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Je dispose de plusieurs locataires Azure AD B2C. Comment puis-je gérer les sur hello portail Azure ?
Avant d’ouvrir « B2C d’AD Azure » dans le menu de gauche hello Hello portail Azure, vous devez passer à l’annuaire de hello vraiment toomanage.  Changer de répertoire en cliquant sur votre identité dans hello coin supérieur droit hello portail Azure, puis sélectionnez un répertoire dans hello de liste déroulante qui s’affiche.  Pour obtenir des images, consultez [accédez tooAzure AD B2C paramètres](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Comment personnaliser les messages de vérification (hello contenu et hello » à partir de : « champ) envoyées par Azure AD B2C ?
Vous pouvez utiliser hello [fonctionnalité de marque de société](../active-directory/active-directory-add-company-branding.md) contenu de hello toocustomize des courriers électroniques de vérification. Plus précisément, ces deux éléments de messagerie de hello peuvent être personnalisés :

* **Logo de bannière**: indiqué à hello en bas à droite.
* **Couleur d’arrière-plan**: indiqué en haut de hello.

    ![Capture d’écran d’un e-mail de vérification personnalisée](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

signature de courrier électronique Hello contient le nom du locataire hello B2C que vous avez fourni lors de la création de client de hello B2C. Vous pouvez modifier le nom de hello à l’aide de ces instructions :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) comme hello administrateur de l’abonnement.
1. Accédez tooyour B2C locataire.
1. Cliquez sur hello **configurer** onglet.
1. Hello de modification **nom** champ sous hello **propriétés Active** section.
1. Cliquez sur **enregistrer** bas hello de page de hello.

Il n’existe actuellement aucune hello toochange de façon » à partir de : » de la messagerie de hello. Voter [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) vous êtes intéressé personnalisation corps hello de courrier électronique de vérification hello.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Comment puis-je migrer mes noms d’utilisateur existants, les mots de passe et les profils à partir de mon tooAzure de base de données Active Directory B2C ?
Vous pouvez utiliser hello API Azure AD Graph toowrite votre outil de migration. Consultez hello [exemple d’API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) pour plus d’informations.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Quelle stratégie de mot de passe est utilisée pour les comptes locaux dans Azure AD B2C ?
Hello, stratégie de mot de passe Azure AD B2C pour les comptes locaux est basée sur la stratégie de hello pour Azure AD. AD B2C Azure de l’inscription, inscription ou de connexion et mot de passe réinitialisé force de mot de passe « fort » stratégies utilise hello et n’expire jamais les mots de passe. Hello de lecture [stratégie de mot de passe Azure AD](https://msdn.microsoft.com/library/azure/jj943764.aspx) pour plus d’informations.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>Puis-je utiliser Azure AD Connect toomigrate identités qui sont stockées sur mon tooAzure d’Active Directory sur site AD B2C ?
Non, Azure AD Connect n’est pas conçue toowork avec Azure Active Directory B2C. Envisagez d’utiliser hello [API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) pour la migration de l’utilisateur.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Mon application peut-elle ouvrir des pages Azure Active Directory B2C dans un iFrame ?
Non, pour des raisons de sécurité, les pages Azure AD B2C ne peuvent pas être ouvertes dans un iFrame.  Notre service communique avec hello navigateur tooprohibit iFrames.  Hello Communauté de la sécurité en général et hello spécification OAUTH2, déconseillons d’utiliser les iFrames des expériences d’identité en raison du risque de toohello de levage de clic.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Azure AD B2C fonctionne-t-il avec les systèmes CRM, tels que Microsoft Dynamics ?
L’intégration avec le portail Microsoft Dynamics 365 est disponible.  Consultez [toouse configuration Dynamics 365 portail Azure AD B2C pour l’authentification](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C fonctionne-t-il avec SharePoint localement 2016 ou version antérieure ?
Azure AD B2C n’est pas conçu pour hello SharePoint externe partenaire scénario de partage ; consultez [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) à la place.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Dois-je utiliser Azure AD B2C ou B2B toomanage les identités externes ?
Lisez cet article sur [les identités externes](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn plus d’informations sur l’application hello approprié des scénarios d’identité externe tooyour fonctionnalités.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Quelles sont les fonctionnalités de création de rapports et d’audit proposées par Azure AD B2C ? Sont qu'elles même hello comme dans Azure AD Premium ?
Non, Azure AD B2C ne prend pas en charge hello même ensemble de rapports en tant qu’Azure AD Premium. Toutefois, de nombreux points communs existent :

* Hello-in rapports fournissent un enregistrement de chaque connectez-vous avec les détails réduites.
* Rapports d’audit sont disponibles dans le portail Azure, sous Azure Active Directory de hello > des journaux d’Audit de l’activité > Choisissez un B2C et appliquer des filtres comme vous le souhaitez. Les activités d’administration et d’application sont traitées. 
* Un rapport d’utilisation, couvrant le nombre d’utilisateurs, le nombre de connexions et le volume de MFA est disponible via [l’API de création de rapports](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api).

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Puis-je localiser hello l’interface utilisateur de pages pris en charge par Azure AD B2C ? Quelles sont les langues prises en charge ?
Oui.  Découvrez la [personnalisation linguistique](active-directory-b2c-reference-language-customization.md), qui est en préversion publique.  Nous fournissons des traductions pour 36 langues, et vous pouvez remplacer n’importe quel toosuit de chaîne de vos besoins.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Puis-je utiliser mes propres URL dans les pages d’inscription et de connexion présentées par Azure AD B2C ? Par exemple, puis modifier les URL de hello de login.microsoftonline.com toologin.contoso.com ?
Pas actuellement. Cette fonctionnalité est sur notre feuille de route. Vérification de votre domaine Bonjour **domaines** onglet hello portail Azure classic ne remplissent pas cet objectif.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Comment supprimer mon client Azure AD B2C ?
Suivez ces étapes toodelete votre locataire Azure AD B2C :

1. Suivez ces étapes trop[accédez tooAzure AD B2C paramètres](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
1. Accédez toohello **Applications**, **fournisseurs d’identité**, et **toutes les stratégies** et supprimer toutes les entrées de hello dans chacun d’eux.
1. Maintenant vous connecter à toohello [portail Azure classic](https://manage.windowsazure.com/) comme hello administrateur de l’abonnement. (Utilisez hello même travail ou scolaire compte ou hello du même compte Microsoft que vous avez utilisé toosign pour Azure.)
1. Accédez d’extension d’Active Directory toohello sur hello gauche, puis cliquez sur votre client B2C.
1. Cliquez sur hello **utilisateurs** onglet.
1. Sélectionnez chaque utilisateur à son tour (exclude hello administrateur d’abonnement utilisateur vous êtes actuellement connecté en tant que). Cliquez sur **supprimer** bas hello, puis cliquez sur la page de hello **Oui** lorsque vous y êtes invité.
1. Cliquez sur hello **Applications** onglet.
1. Sélectionnez **Applications que ma société possède** Bonjour **afficher** champ de liste déroulante et cliquez sur hello case à cocher.
1. Une application a appelé **b2c-extensions-app**. Cliquez sur **supprimer** bas hello, puis cliquez sur la page de hello **Oui** lorsque vous y êtes invité.
1. Accédez à nouveau les extension d’Active Directory toohello et sélectionnez votre locataire B2C.
1. Cliquez sur **supprimer** bas hello de page de hello. processus de hello toocomplete, suivez les instructions sur l’écran hello hello.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Puis-je obtenir Azure AD B2C dans le cadre d’Enterprise Mobility Suite ?
Non, Azure AD B2C est un service Azure avec paiement à l’utilisation et ne fait pas partie d’Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Comment signaler des problèmes avec Azure AD B2C ?
Consultez [Azure Active Directory B2C : dépôt de demandes de support](active-directory-b2c-support.md).
