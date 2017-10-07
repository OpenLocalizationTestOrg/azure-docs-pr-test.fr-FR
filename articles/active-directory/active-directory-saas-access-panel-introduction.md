---
title: "aaaWhat est le volet d’accès hello dans Azure Active Directory ? | Microsoft Docs"
description: "Découvrez comment toouse les variations de hello aux tooaccess du Panneau de configuration (navigateur web, application Android, application iPhone et iPad) les applications SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Quel est le volet d’accès hello ?

volet d’accès Hello est un portail web. Il permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory tooview et démarrer les applications cloud un administrateur Azure AD lui a accordé l’accès à. Vous pouvez également utiliser des groupes en libre-service et les fonctionnalités de gestion des applications via le volet d’accès hello.

volet d’accès Hello est distinct de hello portail Azure et n’apporte pas toohave un abonnement Azure.

![Volet d'accès][1]

volet d’accès Hello permet tooedit certains de vos paramètres de profil, y compris hello possibilité :

- Modifier hello de mot de passe associé à un compte professionnel ou scolaire

- Modifier les paramètres de réinitialisation de mot de passe

- Modifier le contact et préférences paramètres connexes toomulti-authentification (pour les comptes qui ont été toouse requis par un administrateur)

- Afficher les détails de compte tels que l’ID d’utilisateur, l’adresse e-mail de secours, les numéros de téléphone mobile et de bureau et les appareils

- Afficher et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à. Pour plus d’informations sur le volet d’accès hello du point de vue des utilisateurs hello, reportez-vous à l’aide du volet d’accès hello. 

- Gérer les groupes en libre-service. Plus spécifiquement, hello peut créer et gérer des groupes de sécurité et l’appartenance aux groupes de sécurité de demande dans Azure AD. Pour plus d’informations, consultez [Gestion de groupe libre-service pour les utilisateurs dans Azure AD](active-directory-accessmanagement-self-service-group-management.md) et [Gérer vos groupes](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>L’accès au panneau d’accès hello

Vous pouvez accéder à panneau d’accès hello en visitant hello suivant des URL dans un navigateur web :`http://myapps.microsoft.com`

Si vous avez marque personnalisée est configurée pour votre page de connexion, vous pouvez charger cette marque en ajoutant la fin de toohello de domaine de votre organisation de hello URL :`http://myapps.microsoft.com/<your domain>.com`

Dans ce cas, vous pouvez utiliser n’importe quel nom de domaine actif ou vérifié ayant été configuré dans votre portail Azure.

![Nom de domaine Jouets Wingtip][2]  

Vous devez toodistribute hello URL tooall les utilisateurs qui pourront se connecter dans tooapplications qui sont intégrées à Azure AD.

## <a name="authentication"></a>Authentification

volet d’accès tooreach hello, vous devez être authentifié dans Azure AD via un compte professionnel ou scolaire. Vous pouvez être authentifié tooAzure AD directement. En guise d’alternative, si une organisation a configuré la fédération à l’aide des services Active Directory Federation Services (AD FS) ou d’autres technologies, vous pouvez être authentifié par Windows Server Active Directory.

Si vous avez un abonnement à Azure ou Office 365 et que vous avez utilisé hello portail Azure ou une application Office 365, vous pouvez voir la liste des applications hello sans signer de nouveau. Si vous ne sont pas authentifiés vous êtes invité à toosign dans à l’aide de nom d’utilisateur hello et le mot de passe pour votre compte dans Azure AD. Si votre organisation a configuré la fédération, il suffit de taper le nom d’utilisateur hello.

Lorsque vous êtes authentifié, vous pouvez interagir avec les applications hello que votre administrateur a intégré à Active de hello. toolearn toointegrate des applications avec Azure AD, voir [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Configuration requise du navigateur web

Au minimum, volet d’accès hello nécessite un navigateur qui prend en charge JavaScript et a activé les CSS. Pour hello toobe d’utilisateur connecté tooapplications par l’intermédiaire d’un mot de passe-session unique (SSO), l’extension volet d’accès hello doit être installée dans votre navigateur. extension de Hello est téléchargée automatiquement lorsque vous sélectionnez une application qui est configurée pour l’authentification unique de mot de passe.

extension de panneau d’accès Hello est actuellement disponible pour les navigateurs Internet Explorer 8 et versions ultérieures, Edge, Chrome et Firefox.

## <a name="mobile-app-support"></a>Prise en charge des applications mobiles

équipe Azure Active Directory de Hello publie hello mon application mobile d’applications. Lorsque vous installez application hello, vous pouvez signer dans les applications SSO toopassword sur des appareils iOS et Android.

> [!NOTE]
> Vous pouvez signer dans tooapplications qui prennent en charge la fédération avec Azure AD (notamment Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 et plus de 70 autres) sur pratiquement n’importe quel navigateur web, sur n’importe quel appareil, sans avoir besoin d’une application de plug-in ou mobile. Tous les autres [accéder au panneau de configuration expériences](https://myapps.microsoft.com/) également nécessitent hello mon toobe d’application mobile applications utilisée sur un appareil mobile.
>
>

### <a name="my-apps-for-android"></a>My Apps pour Android

My Apps pour Android est prise en charge sur n’importe quel appareil Android exécutant Android version 4.1 et ultérieures.  
Il est disponible dans hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![My Apps pour Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>My Apps pour iPhone et iPad

My Apps pour iOS est prise en charge sur n’importe quel iPhone ou iPad exécutant iOS version 7 et ultérieures.  
Il est disponible dans hello [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![My Apps pour iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Managed Browser pour My apps

Mes applications est également intégré hello Intune Managed Browser. Hello Intune Managed Browser pour les appareils iOS et Android joue un rôle clé pour garantir la sécurisation des données sur les appareils mobiles. Il vous permet d’afficher et de parcourir des pages web pouvant contenir des informations d’entreprise, et fournit une expérience de navigation web sécurisée.  
Vous trouverez un accès rapide toomy applications sur votre page d’accueil de Managed Browser et dans vos favoris, ce qui vous donne moins clique tooreach toute application que vous souhaitez tooaccess.

Il est disponible dans hello [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) et [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Managed Browser pour My apps][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Conseils pour l’expérience utilisateur de test hello

Si vous êtes un administrateur Azure et que vous êtes connecté toohello portail Azure en utilisant un compte dans le répertoire de hello, vous êtes automatiquement connecté dans le volet d’accès toohello en tant que votre compte actuel. Dans ce cas, vous pouvez voir toutes les applications qui ont été attribuées tooyou.

**tootest comme un *différents* compte d’utilisateur :**

1. Cliquez sur le menu d’utilisateur hello dans le coin supérieur droit de hello de hello portail Azure ou le volet d’accès hello et sélectionnez **se déconnecter**. 
2. Accédez toohello [volet d’accès](http://myapps.microsoft.com).
3. Sur hello-page de connexion, le nom d’utilisateur de type hello et mot de passe de compte hello dans votre annuaire, vous souhaitez tootest.


## <a name="starting-applications"></a>Démarrage des applications

Plusieurs types d’applications peuvent apparaître dans le volet d’accès hello.

### <a name="office-365-applications"></a>Applications Office 365

Si votre organisation utilise les applications Office 365 et vous sont concédés sous licence pour les applications de hello Office 365 apparaissent dans le volet d’accès.

Lorsque vous cliquez sur une vignette d’application pour une application Office 365, vous êtes redirigé toohello application et connecté automatiquement.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération

Votre administrateur peut ajouter des applications de hello section Active Directory du portail Azure de hello lorsque le mode d’authentification unique de hello défini trop**Azure AD Single Sign-On**. Vous pouvez uniquement afficher ces applications si votre administrateur a explicitement accordé le qu'accès toohello applications.

Lorsque vous cliquez sur une vignette pour l’une de ces applications, vous êtes redirigé et connecté automatiquement toohello application.

### <a name="password-based-sso-without-identity-provisioning"></a>Authentification unique avec mot de passe sans approvisionnement d’identité

Votre administrateur peut ajouter des applications de hello section Active Directory du portail Azure de hello lorsque le mode d’authentification unique de hello défini trop**mot de passe Single Sign-On**. Tous les utilisateurs dans le répertoire de hello peuvent voir toutes les applications qui ont été configurées dans ce mode.

Hello première fois, vous cliquez sur une vignette pour l’une de ces applications, vous êtes invité à tooinstall hello SSO de mot de passe du plug-in pour Internet Explorer ou Chrome. installation de Hello peut nécessiter vous toorestart votre navigateur web. Lorsque vous revenez toohello volet d’accès puis cliquez sur vignette de l’application hello là encore, vous êtes invité à entrer un nom d’utilisateur et un mot de passe pour l’application hello. Lorsque vous avez entré votre nom d’utilisateur et un mot de passe, ces informations d’identification sont stockées en toute sécurité et liés tooyour compte dans Azure AD.

Hello prochaine sur la vignette de l’application hello, vous êtes automatiquement connecté toohello application.  
Vous ne de disposer de tooenter vos informations d’identification à nouveau et ou installer hello SSO de mot de passe du plug-in.

Si vos informations d’identification ont été modifiés dans hello cible les applications tierces, vous devez également mettre à jour vos informations d’identification sont stockées dans Azure AD. 

**informations d’identification de tooupdate :**

1. Sélectionnez l’icône hello sur la vignette de l’application hello.
2. Sélectionnez **mettre à jour les informations d’identification** tooreenter hello utilisateur et mot de passe hello application.


### <a name="password-based-sso-with-identity-provisioning"></a>Authentification unique avec mot de passe avec approvisionnement d’identité

Votre administrateur peut ajouter des applications de hello **Active Directory** section Hello portail Azure avec le mode d’authentification unique hello défini trop**mot de passe Single Sign-On**, ainsi que de l’approvisionnement d’identité.

Hello première fois, vous cliquez sur une vignette de l’une de ces applications, vous êtes invité à tooinstall hello **mot de passe SSO de plug-in pour Internet Explorer ou Chrome**. installation de Hello peut nécessiter vous toorestart votre navigateur web.  
Lorsque vous revenez toohello volet d’accès puis cliquez sur vignette de l’application hello là encore, vous êtes automatiquement connecté toohello application.

Certaines applications peuvent nécessiter vous toochange votre mot de passe hello première connectez-vous. Si vos informations d’identification ont été modifiés dans hello cible les applications tierces, vous devez également mettre à jour les informations d’identification de hello sont stockées dans Azure AD. 

**informations d’identification de tooupdate :**

1. Sélectionnez l’icône hello sur la vignette de l’application hello.
2. Sélectionnez **mettre à jour les informations d’identification** tooreenter hello utilisateur et mot de passe hello application.


### <a name="application-with-existing-sso-solutions"></a>Application avec solutions d’authentification unique (SSO) existantes

tooconfigure l’authentification unique pour une application, hello portail Azure fournit une troisième option appelée **existant Single Sign-On**. Cette option permet à votre administrateur de toocreate une application tooan de lien et le placer dans le volet d’accès hello pour les utilisateurs sélectionnés.

Par exemple, si une application est configurée tooauthenticate utilisateurs à l’aide des services AD FS 2.0, votre administrateur peut utiliser hello **existant Single Sign-On** option toocreate un tooit lien sur le volet d’accès hello. Lorsque vous accédez à des liens de hello, vous êtes authentifié via AD FS 2.0 ou de toute application de hello solution SSO existante fournit.


## <a name="next-steps"></a>Étapes suivantes

- toosee une liste de toutes les rubriques qui sont associées tooapplication management, consultez hello [index de l’article pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md).
 
- toolearn toointegrate une application SaaS dans Azure AD, voir hello [liste des didacticiels sur la façon des applications SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn savoir plus sur la gestion des applications avec Azure AD, consultez hello [introduction toosingle d’authentification et la gestion des accès de l’application avec Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn savoir plus sur la configuration de l’utilisateur, consultez [automatiser la configuration de l’utilisateur et la mise hors service des applications de tooSaaS](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
