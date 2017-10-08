---
title: "aaaAn affecté application n’apparaît pas dans le volet d’accès hello | Documents Microsoft"
description: "Résoudre les problèmes de la raison pour laquelle une application n’apparaît pas dans le volet d’accès de hello"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>Une application attribuée n’apparaît pas dans le volet d’accès hello

Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à. Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello. application Hello doit être configurée correctement et toohello attribué ou un utilisateur de hello de groupe est un membre de l’application de hello toosee Bonjour panneau d’accès.

type Hello d’applications peut s’agir d’un utilisateur se situent dans hello suivant des catégories :

-   Applications Office 365

-   Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération

-   Applications à authentification unique (SSO) par mot de passe

-   Applications avec solutions d’authentification unique (SSO) existantes

## <a name="general-issues-toocheck-first"></a>Général émet toocheck tout d’abord

-   Si une application vient d’être ajoutée tooa utilisateur, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si l’application hello est ajoutée.

-   Si une licence vient d’être supprimée d’un utilisateur ou un utilisateur hello le groupe est que membre de ce peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe hello pour toobe des modifications apportée. Prévoyez du temps supplémentaire avant de vous connecter en hello panneau d’accès.

## <a name="problems-related-tooapplication-configuration"></a>Configuration de tooapplication connexes des problèmes

Une application n’apparaît peut-être pas dans le volet d’accès d’un utilisateur en raison d’une mauvaise configuration. Voici quelques méthodes que vous pourrez résoudre les problèmes de configuration connexes tooapplication de problèmes :

-   [Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [Comment tooconfigure fédéré l’authentification unique pour une application non-galerie](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [Comment tooconfigure un mot de passe une seule application d’authentification pour une application de la galerie Azure AD](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [Comment tooconfigure un mot de passe une seule application d’authentification pour une application non-galerie](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD

Toutes les applications dans la galerie d’Azure AD hello activé avec la fonctionnalité Enterprise Single Sign-On a un didacticiel pas à pas disponible. Vous pouvez accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application-from-the-azure-ad-gallery)

-   [Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Récupérer le certificat et les métadonnées Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.

6.  Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.

7.  Sélectionnez hello application tooconfigure pour l’authentification unique.

8.  Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.

9.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurer l’authentification unique pour une application à partir de la galerie d’Azure AD hello

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

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

   2. Cliquez sur **Enregistrer**. Vous consultez hello nouvel attribut dans la table de hello.

13. Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello. En outre, vous a hello les URL des métadonnées et le certificat requis toosetup SSO avec l’application hello.

14. Cliquez sur **enregistrer** configuration de hello toosave.

15. Affecter des utilisateurs toohello application.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello

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

   2. Cliquez sur **Enregistrer**. Vous verrez hello nouvel attribut dans la table de hello.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Télécharger des métadonnées Azure AD hello ou certificat

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

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Comment tooconfigure fédéré l’authentification unique pour une application non-galerie

tooconfigure une application non-galerie, vous devez toohave Azure AD premium et l’application hello prend en charge SAML 2.0. Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)](#configuring-single-sign-on)

-   [Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Récupérer le certificat et les métadonnées Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)

tooconfigure l’authentification unique pour une application qui n’est pas dans la galerie d’Azure AD hello, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.

6.  Cliquez sur **application Non-gallery** Bonjour **ajouter votre propre application** section.

7.  Entrez le nom hello de l’application hello Bonjour **nom** zone de texte.

8.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

9.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

10. Sélectionnez **SAML-authentification** Bonjour **Mode** liste déroulante.

11. Entrez les valeurs hello requis dans **URL et domaine.** Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.

   1. application de hello tooconfigure en tant que l’authentification unique initiée par les fournisseurs d’identité, entrez hello URL de réponse et hello identificateur.

   2.  **Facultatif :** application hello tooconfigure authentifications uniques initiées, hello signe sur l’URL, il est obligatoire.

12. Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.

13. **Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   1. Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   2. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

14. Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello. Possède également Azure AD URL et le certificat requis pour l’application hello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello

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

   2. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Télécharger des métadonnées Azure AD hello ou certificat

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

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application-from-the-azure-ad-gallery)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.

6.  Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.

7.  Sélectionnez hello application tooconfigure pour l’authentification unique.

8.  Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.

9.  Cliquez sur **ajouter** bouton, l’application de hello tooadd.

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurer une application hello pour mot de passe l’authentification unique

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

9.  [Affecter des utilisateurs toohello application](#how-to-assign-a-user-to-an-application-directly).

10. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application ne figurant pas dans la galerie](#add-a-non-gallery-application)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>Ajouter une application ne figurant pas dans la galerie

tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**.

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.

6.  Cliquez sur **Application ne figurant pas dans la galerie**.

7.  Entrez le nom hello de votre application Bonjour **nom** zone de texte. Sélectionnez **Ajouter.**

Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurer une application hello pour mot de passe l’authentification unique

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

    1.  Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Mode de sélection hello **mot de passe de session.**

9.  Entrez hello **URL de connexion**. Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour. Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.

10. [Affecter des utilisateurs toohello application](#how-to-assign-a-user-to-an-application-directly).

11. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

## <a name="problems-related-tooassigning-applications-toousers"></a>Des problèmes connexes tooassigning applications toousers

Un utilisateur ne peut pas s’agir d’une application dans leur volet d’accès, car ils ne sont pas affectés toohello application. Voici certains toocheck façons :

-   [Vérifiez si un utilisateur est affecté toohello application](#check-if-a-user-is-assigned-to-the-application)

-   [Comment tooassign directement une application de tooan utilisateur](#how-to-assign-a-user-to-an-application-directly)

-   [Vérifiez si un utilisateur est assigné tooa licence liées toohello application](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [Comment tooassign un utilisateur tooa de licence](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>Vérifiez si un utilisateur est affecté toohello application

toocheck si un utilisateur est assigné toohello application, procédez comme suit hello :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

6.  **Recherche** pour nom hello de l’application hello en question.

7.  Sélectionnez **Utilisateurs et groupes**.

8.  Vérifiez toosee si votre utilisateur est affecté toohello application.

   * Si ce n’est pas hello comme suit dans « comment tooassign directement une application de tooan utilisateur » toodo donc.

### <a name="how-tooassign-a-user-tooan-application-directly"></a>Comment tooassign directement une application de tooan utilisateur

tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global**.

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

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Vérifier si un utilisateur est sous licence toohello application relative

toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.

  * Si l’utilisateur de hello est attribué une licence Office tooan Ceci activer premier tiers Office applications tooappear sur hello panneau d’accès de l’utilisateur.

### <a name="how-tooassign-a-user-a-license"></a>Comment tooassign un utilisateur une licence 

tooassign un utilisateur tooa de licences, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.

8.  Cliquez sur hello **affecter** bouton.

9.  Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.

10. **Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits. Cliquez sur **OK** lorsque l’opération est terminée.

11. Cliquez sur hello **affecter** bouton tooassign ces utilisateur toothis de licences.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Des problèmes connexes tooassigning applications toogroups

Un utilisateur peut s’agir d’une application dans leur volet d’accès car ils font partie d’un groupe auquel a été attribué application hello. Voici certains toocheck façons :

-   [Vérifier les appartenances d’un utilisateur à des groupes](#check-a-users-group-memberships)

-   [Comment tooassign un tooa application groupe directement](#how-to-assign-an-application-to-a-group-directly)

-   [Vérifiez si un utilisateur fait partie du groupe tooa licence attribuée](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [Comment tooassign un tooa un groupe de licences](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>Vérifier les appartenances d’un utilisateur à des groupes

toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Groupes**.

8.  Vérifiez toosee si l’utilisateur fait partie d’une application toohello de groupe affecté.

  * Si vous souhaitez utilisateur de hello tooremove à partir du groupe de hello, **cliquez sur la ligne hello** hello groupe d’et sélectionnez Supprimer.

### <a name="how-tooassign-an-application-tooa-group-directly"></a>Comment tooassign un tooa application groupe directement

tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global**.

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.

7.  Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.

9.  Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.

10. Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.

Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>Vérifiez si un utilisateur fait partie du groupe tooa licence attribuée

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Groupes**.

8.  Cliquez sur ligne hello d’un groupe spécifique.

9.  Cliquez sur **licences** toosee quel groupe hello de licences a affecté tooit.

   * Si le groupe de hello est attribué une licence Office tooan sur que ceci peut activer certaine tooappear d’applications de premier tiers Office hello panneau d’accès de l’utilisateur.

### <a name="how-tooassign-a-license-tooa-group"></a>Comment tooassign un tooa un groupe de licences

tooassign un groupe tooa de licences, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les groupes**.

6.  **Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.

8.  Cliquez sur hello **affecter** bouton.

9.  Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.

10. **Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits. Cliquez sur **OK** lorsque l’opération est terminée.

11. Cliquez sur hello **affecter** bouton tooassign ces toothis de groupe de licences. Cette opération peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe de hello.

>[!NOTE]
>toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence. 
>
>

## <a name="next-steps"></a>Étapes suivantes
[Ajouter de nouveaux utilisateurs tooAzure Active Directory](active-directory-users-create-azure-portal.md)

