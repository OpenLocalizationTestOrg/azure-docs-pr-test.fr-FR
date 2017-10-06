---
title: "aaaHow tooconfigure fédéré l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Comment tooconfigure fédéré l’authentification unique pour un existant Galerie d’Azure AD application et utilisez didacticiels tooget va rapidement"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure fédéré l’authentification unique pour une application de la galerie d’Azure AD

Toutes les applications dans la galerie de hello Azure AD activé avec la fonctionnalité d’authentification unique de l’entreprise a un didacticiel pas à pas disponible. Vous pouvez accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir des instructions détaillées.

## <a name="overview-of-steps-required"></a>Vue d’ensemble des étapes requises
tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application-from-the-azure-ad-gallery)

-   [Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Récupérer le certificat et les métadonnées Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Affecter des utilisateurs toohello application](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

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

Après une courte période de temps, vous être Panneau de configuration de l’application en mesure de toosee hello.

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurer l’authentification unique pour une application à partir de la galerie d’Azure AD hello

tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**.

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

   1. Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

13. Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello. En outre, vous a hello les URL des métadonnées et le certificat requis toosetup SSO avec l’application hello.

14. Cliquez sur **enregistrer** configuration de hello toosave.

15. Affecter des utilisateurs toohello application.

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello

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

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Télécharger des métadonnées Azure AD hello ou certificat

métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  *  Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications**.

6.  Sélectionnez l’application hello que vous avez configuré l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne. En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.

Azure AD ne fournit pas une URL de métadonnées hello tooget. Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.

## <a name="assign-users-toohello-application"></a>Affecter des utilisateurs toohello application

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

Après une courte période de temps, les utilisateurs de hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Personnalisation des revendications SAML hello envoyé tooan application

toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)



