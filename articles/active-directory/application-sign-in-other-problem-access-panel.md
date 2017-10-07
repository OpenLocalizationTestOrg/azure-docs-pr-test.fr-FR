---
title: "aaaProblems de signature dans l’application tooan à partir du volet d’accès hello | Documents Microsoft"
description: "Comment les problèmes de tootroubleshoot l’accès à une application à partir de hello panneau d’accès Microsoft Azure AD MyApps.Microsoft.com"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Problèmes de connexion dans l’application tooan à partir du volet d’accès hello

Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à. 

Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello. application Hello doit être configurée correctement et toohello attribué ou un utilisateur de hello de groupe est un membre de l’application de hello toosee Bonjour panneau d’accès.

type Hello d’applications peut s’agir d’un utilisateur se situent dans hello suivant des catégories :

-   Applications Office 365

-   Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération

-   Applications à authentification unique (SSO) par mot de passe

-   Applications avec solutions d’authentification unique (SSO) existantes

## <a name="general-issues-toocheck-first"></a>Général émet toocheck tout d’abord

-   Assurez-vous que votre en utilisant un **navigateur** qui répond aux hello configuration minimale requise pour hello panneau d’accès.

-   Assurez-vous que navigateur de l’utilisateur hello a ajouté des URL hello de hello application tooits **sites de confiance**.

-   Assurez-vous que l’application de hello toocheck est **configuré** correctement.

-   Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions.

-   Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**

-   Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.**

-   Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.

-   Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.

-   S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée.

-   Assurez-vous que tooalso try effacer les cookies de votre navigateur et réessayer toosign dans.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Configuration requise du navigateur de réunion hello panneau d’accès

Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS. toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello. Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.

Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :

-   Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure

-   Edge sur Windows 10 Édition anniversaire ou version ultérieure

-   Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur

-   Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Comment tooinstall hello extension du navigateur de panneau d’accès

tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.

2.  Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.

3.  Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.

4.  En fonction de votre navigateur vous être lien de téléchargement toohello dirigée. **Ajouter** navigateur de tooyour extension hello.

5.  Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.

6.  Une fois l’extension installée, **redémarrez** votre session de navigateur.

7.  Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe

Vous pouvez également télécharger l’extension de hello pour Chrome et le bord à partir de liens directs de hello ci-dessous :

-   [Extension du volet d’accès pour Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extension du volet d’accès pour Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD

Toutes les applications dans la galerie d’Azure AD hello activée avec la fonctionnalité Enterprise Single Sign-On a un didacticiel pas à pas disponible. Vous pouvez accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application)

-   [Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Récupérer le certificat et les métadonnées Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Affecter des utilisateurs toohello application](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau

6.  Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.

7.  Sélectionnez hello application tooconfigure pour l’authentification unique.

8.  Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.

9.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurer l’authentification unique pour une application à partir de la galerie d’Azure AD hello

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Sélectionnez **SAML-authentification** de hello **Mode** liste déroulante.

9.  Entrez les valeurs hello requis dans **URL et domaine.** Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.

   1. application de hello tooconfigure en tant que l’authentification unique initiée par SP, hello signe sur l’URL, il est obligatoire. Pour certaines applications, hello identificateur est également une valeur requise.

   2. application hello tooconfigure initiées IdP, hello URL de réponse qu’il est obligatoire. Pour certaines applications, hello identificateur est également une valeur requise.

10. **Facultatif :** cliquez sur **afficher les paramètres d’URL avancés** si vous souhaitez que les valeurs toosee hello non requis.

11. Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.

12. **Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   1. Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   2. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

13. Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello. En outre, vous a hello les URL des métadonnées et le certificat requis toosetup SSO avec l’application hello.

14. Cliquez sur **enregistrer** configuration de hello toosave.

15. Affecter des utilisateurs toohello application.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello

tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello souhaité tooshow ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante. Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.

    >[!NOTE]
    >Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest. Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.
    >
    >

9.  attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   1. Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   2. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Télécharger des métadonnées Azure AD hello ou certificat

métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne. En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.

    Azure AD ne fournit pas une URL de métadonnées hello tooget. Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Comment tooconfigure fédéré l’authentification unique pour une application non-galerie

tooconfigure une application non-galerie, vous devez toohave Azure AD premium et l’application hello prend en charge SAML 2.0. Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)](#configuring-single-sign-on)

-   [Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Récupérer le certificat et les métadonnées Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)

tooconfigure l’authentification unique pour une application qui n’est pas dans la galerie d’Azure AD hello, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau

6.  Cliquez sur **application Non-gallery** Bonjour **ajouter votre propre application** section

7.  Entrez le nom hello de l’application hello Bonjour **nom** zone de texte.

8.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

9.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

10. Sélectionnez **SAML-authentification** Bonjour **Mode** liste déroulante

11. Entrez les valeurs hello requis dans **URL et domaine.** Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.

  1. application de hello tooconfigure en tant que l’authentification unique initiée par les fournisseurs d’identité, entrez hello URL de réponse et hello identificateur.

  2. **Facultatif :** application hello tooconfigure authentifications uniques initiées, hello signe sur l’URL, il est obligatoire.

12. Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.

13. **Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   1. Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   2. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

14. Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello. Possède également Azure AD URL et le certificat requis pour l’application hello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello

tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante. Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.

   >[!NOTE]
   >Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest. Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.
   >
   >

9.  attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   1. Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   2. Cliquez sur **Enregistrer**. Vous consultez hello nouvel attribut dans la table de hello.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Télécharger des métadonnées Azure AD hello ou certificat

métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne. En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.

    Azure AD ne fournit pas une URL de métadonnées hello tooget. Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau

6.  Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello

7.  Sélectionnez hello application tooconfigure pour l’authentification unique

8.  Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.

9.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurer une application hello pour mot de passe l’authentification unique

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

 * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Mode de sélection hello **mot de passe de session.**

9.  Affecter des utilisateurs toohello application.

10. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application ne figurant pas dans la galerie](#add-a-non-gallery-application)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Ajouter une application ne figurant pas dans la galerie

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau

6.  Cliquez sur **Application ne figurant pas dans la galerie**.

7.  Entrez le nom hello de votre application Bonjour **nom** zone de texte. Sélectionnez **Ajouter.**

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurer une application hello pour mot de passe l’authentification unique

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

 * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Mode de sélection hello **mot de passe de session.**

9.  Entrez hello **URL de connexion**. Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour. Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.

10. Affecter des utilisateurs toohello application.

11. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Comment tooassign directement une application de tooan utilisateur

tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.

7.  Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.

9.  Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.

10. Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.

Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Si ces étapes de dépannage ne pas hello hello résoudre

Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   UPN (adresse e-mail de l’utilisateur)

-   ID de locataire

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)

