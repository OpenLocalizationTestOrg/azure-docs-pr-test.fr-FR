---
title: "aaaError sur une page de l’application après l’ouverture de session | Documents Microsoft"
description: "Comment les problèmes de tooresolve avec Azure AD se connectent lors de l’application hello lui-même émet une erreur"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Erreur dans la page d’une application après la connexion

Dans ce scénario, Azure AD a signé utilisateur hello dans mais hello application affiche une erreur interdisant hello utilisateur toosuccessfully terminer hello signe dans le flux. Dans ce scénario, application hello n’accepte pas de problème de réponse hello par Azure AD.

Voici quelques raisons possibles pour lesquelles application hello n’a pas accepté la réponse hello d’Azure AD. Si l’erreur hello dans l’application hello n’est pas assez clair tooknow ce qui est manquant dans la réponse de hello, puis :

-   Si l’application hello est hello Azure AD galerie, vérifiez vous avez suivi toutes les étapes de hello dans l’article de hello [comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Utiliser un outil tel que [Fiddler](http://www.telerik.com/fiddler) toocapture SAML demande, la réponse SAML et jeton SAML.

-   Partager la réponse SAML de hello avec tooknow de fournisseur d’application hello ce qui est manquant.

## <a name="missing-attributes-in-hello-saml-response"></a>Attributs manquants hello réponse SAML

tooadd un attribut dans toobe de configuration d’Azure AD hello envoyé en réponse de hello Azure AD, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur **affichage et modification des attributs de tous les autres utilisateurs sous** hello **attributs utilisateur** hello tooedit de section attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.

   tooadd un attribut :

   * Cliquez sur **Ajouter un attribut**. Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.

   * Cliquez sur **Enregistrer.** Vous consultez hello nouvel attribut dans la table de hello.

9.  Enregistrer la configuration de hello.

Prochaine connexion d’utilisateur de hello dans toohello application, Azure AD envoyer nouvel attribut de hello Bonjour réponse SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>application Hello attend une autre valeur de l’identificateur de l’utilisateur ou d’un format

Hello connectez-vous toohello application échoue car hello réponse SAML manque des attributs tels que les rôles ou application hello attend un autre format d’attribut de EntityID hello.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Ajoutez un attribut dans la configuration de l’application hello Azure AD :

toochange hello valeur d’identificateur de l’utilisateur, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Sous hello **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.

## <a name="change-entityid-user-identifier-format"></a>Changer le format d’EntityID (identificateur d’utilisateur)

Si l’application hello attend un autre format pour l’attribut EntityID de hello. Ensuite, vous n’être tooselect en mesure de hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.

Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest. Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>application Hello attend une méthode de signature différente pour hello réponse SAML

toochange quelles parties du jeton SAML de hello sont signés numériquement par Azure Active Directory. Suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur **afficher les paramètres de signature de certificat avancés** sous hello **le certificat de signature SAML** section.

9.  Sélectionnez hello approprié **Option de signature** attendu par l’application hello :

  * Signer la réponse SAML

  * Signer la réponse et l’assertion SAML

  * Signer l’assertion SAML

Prochaine connexion d’utilisateur de hello dans toohello application, d’authentification Azure AD hello partie de réponse SAML de hello sélectionné.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>application Hello attend hello signature toobe de l’algorithme SHA-1

Par défaut, Azure AD connecte le jeton SAML de hello à l’aide de hello la plupart des algorithme de sécurité. Modifier l’algorithme de connexion hello tooSHA-1 n’est pas recommandée, sauf si requis par l’application hello.

toochange hello algorithme de signature, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

   * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooconfigure l’authentification unique.

7.  Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur **afficher les paramètres de signature de certificat avancés** sous hello **le certificat de signature SAML** section.

9.  Sélectionnez l’algorithme SHA-1, Bonjour **algorithme de signature**.

Prochaine hello utilisateur s’inscrit dans l’application de toohello, d’authentification Azure AD hello jeton SAML utilisant l’algorithme SHA-1.

## <a name="next-steps"></a>Étapes suivantes
[Comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
