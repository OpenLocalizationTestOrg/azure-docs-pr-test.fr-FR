---
title: "gestion de session aaaSingle pour les applications d’entreprise Bonjour Azure Active Directory | Documents Microsoft"
description: "Découvrez comment toomanage l’authentification unique pour les applications d’entreprise à l’aide de hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Gestion de l’authentification unique pour les applications d’entreprise
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-enterprise-apps-manage-sso.md)
> * [portail Azure Classic](active-directory-sso-integrate-saas-apps.md)
> 

Cet article décrit comment toouse hello [portail Azure](https://portal.azure.com) toomanage unique paramètres d’authentification pour les applications d’entreprise. Les applications d’entreprise sont des applications qui sont déployées et utilisées au sein de votre organisation. Cet article s’applique en particulier les tooapps qui ont été ajoutés à partir de hello [Galerie d’applications Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Recherche de vos applications dans le portail de hello
Toutes les applications d’entreprise qui sont configurées pour l’authentification unique peuvent être affichées et gérées dans hello portail Azure. Vous trouverez les applications Hello Bonjour **plus Services** &gt; **des Applications d’entreprise** section du portail de hello. 

![Panneau Applications d’entreprise][1]

Sélectionnez **toutes les applications** tooview une liste de toutes les applications qui ont été configurés. La sélection d’une application charge panneau des ressources hello pour cette application, où les rapports peuvent être affichés pour cette application et divers paramètres peuvent être gérés.

toomanage unique paramètres d’authentification, sélectionnez **l’authentification unique**.

![Panneau de ressources d’application][2]

## <a name="single-sign-on-modes"></a>Modes d’authentification unique
Hello **l’authentification unique** panneau commence par un **Mode** menu, ce qui permet de hello toobe de mode d’authentification unique configurée. les options disponibles Hello sont les suivantes :

* **L’authentification basée sur les SAML** -cette option est disponible si l’application hello prend en charge complète unique authentification fédérée avec Azure Active Directory à l’aide du protocole de hello SAML 2.0.
* **Password-based sign on** (Authentification par mot de passe) : cette option est disponible si Azure AD prend en charge le remplissage de formulaire de mot de passe pour cette application.
* **Lié signe sur** -anciennement « Existant single sign-on », cette option permet aux administrateurs tooplace une application toothis de lien dans le Lanceur d’applications de leur utilisateur du panneau d’accès Azure AD ou Office 365.

Pour plus d’informations sur ces modes, voir [Fonctionnement de l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Authentification basée sur SAML
Hello **basé sur SAML authentification** option affiche un panneau est divisé en quatre sections :

### <a name="domains-and-urls"></a>Domains and URLs (Domaines et URL)
Il s’agit où tous les détails sur le domaine de l’application hello et URL sont ajoutées tooyour Windows Azure AD. Toutes les entrées requises toomake travail de l’authentification unique app s’affichent directement sur l’écran hello, tandis que toutes les entrées facultatives peuvent être affichées en sélectionnant hello **afficher les paramètres d’URL avancés** case à cocher. la liste complète des entrées prises en charge Hello inclut :

* **URL de connexion** – où l’utilisateur de hello accède dans toosign toothis application. Si application hello est service configuré tooperform unique initiée par le fournisseur de session, lorsqu’un utilisateur navigue toothis URL, le fournisseur de services hello hello nécessaire signe et la redirection tooAzure AD tooauthenticate hello utilisateur dans. Si ce champ est renseigné, Azure AD utilisera cette application de hello toolaunch URL à partir d’Office 365 et hello panneau d’accès Azure AD. Si ce champ est omis, Azure AD effectue à la place le fournisseur d’identité-authentification lorsque hello application est lancée à partir d’Office 365, hello panneau d’accès Azure AD, ou à partir de hello Azure AD unique initiée par l’authentification URL.
* **Identificateur** -cet URI doit identifier de façon unique application hello pour le simple ouverture de session est configurée. Valeur hello que Azure AD envoie tooapplication arrière comme hello paramètre Audience du jeton SAML de hello et application hello est attendu toovalidate il. Cette valeur apparaît également comme hello ID d’entité dans les métadonnées SAML fournie par l’application hello.
* **URL de réponse** -URL de réponse hello est alors application hello attend le jeton SAML de hello tooreceive. C’est également référencé tooas hello Service ACS (Assertion Consumer) URL. Une fois que ceux-ci ont été entrées, cliquez sur Suivant tooproceed toohello prochain écran. Cet écran fournit des informations sur le besoins de toobe configuré sur tooenable de côté application hello tooaccept un jeton SAML à partir d’Azure AD.
* **État du relais** -état du relais hello est un paramètre optionnel qui peut aider à savoir application hello où tooredirect hello utilisateur une fois l’authentification est terminée. En général, la valeur de hello est une URL valide au niveau de l’application hello, toutefois, certaines applications utilisent ce champ différemment (voir l’authentification unique de l’application hello sur la documentation pour plus d’informations). état du relais Hello capacité tooset hello est une nouvelle fonctionnalité qui est unique toohello de nouveau portail Azure.

### <a name="user-attributes"></a>Attributs utilisateur
Il s’agit où administrateurs peuvent afficher et modifier les attributs de hello sont envoyés dans le jeton SAML de hello Azure AD émet toohello application chaque fois qu’ils se connecter.

Hello uniquement l’attribut modifiable pris en charge est hello **identificateur de l’utilisateur** attribut. valeur Hello de cet attribut est un champ de hello dans Azure AD, qui identifie de façon unique chaque utilisateur au sein de l’application hello. Par exemple, si l’application hello a été déployée à l’aide de hello « adresse de messagerie » comme nom d’utilisateur hello et un identificateur unique, puis hello serait être valeur toohello « user.mail » champ dans Azure AD.

### <a name="saml-signing-certificate"></a>Certificat de signature SAML
Cette section affiche les détails de hello du certificat hello que Azure AD utilise les jetons SAML toosign hello émis application toohello que chaque utilisateur hello s’authentifie. Il permet de propriétés hello de hello actuel certificat toobe inspecté, y compris la date d’expiration de hello.

### <a name="application-configuration"></a>Configuration de l’application
Hello finale présente documentation de hello et/ou les contrôles requis tooconfigure hello application toouse Azure Active Directory comme fournisseur d’identité.

Hello **configurer l’Application** menu volant fournit les nouvelles instructions concises, incorporées pour la configuration d’application hello. Il s’agit d’une autre nouvelle fonctionnalité unique toohello nouveau portail Azure.

> [!NOTE]
> Pour obtenir un exemple complet de documentation incorporée, consultez application de Salesforce.com hello. De la documentation est ajoutée en continu pour d’autres applications.
> 
> 

![Documents incorporés][3]

## <a name="password-based-sign-on"></a>Password-based sign on
Si l’application hello prises en charge, en sélectionnant hello basée sur mot de passe en mode d’authentification unique et en sélectionnant **enregistrer** instantanément configure toodo mot de passe de l’authentification unique. Pour plus d’informations sur le déploiement de l’authentification unique par mot de passe, voir [Fonctionnement de l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Password-based sign on][4]

## <a name="linked-sign-on"></a>Linked sign on
Si l’application hello prises en charge, en sélectionnant le mode d’authentification unique hello lié vous permet de tooenter hello URL hello panneau d’accès Azure AD ou Office 365 tooredirect toowhen utilisateurs cliquez sur cette application. Pour plus d’informations sur l’authentification unique liée (précédemment appelée Authentification unique existante), voir [Fonctionnement de l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Authentification liée][5]

##<a name="feedback"></a>Commentaires

Nous espérons que vous le souhaitez à l’aide de hello amélioration de l’expérience d’Azure AD. Gardez les commentaires hello à venir ! Valider des idées pour améliorer et vos commentaires Bonjour **portail d’administration** section de notre [forum de commentaires](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Nous sommes très heureux sur la création de tous les jours, nouveautés et utiliser votre tooshape des conseils et définir ce que nous créons ensuite.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
