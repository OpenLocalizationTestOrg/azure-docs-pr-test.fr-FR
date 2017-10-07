---
title: "aaaHow tooconfigure mot de passe l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Comment tooconfigure une application pour sécuriser basée sur mot de passe de session unique lorsqu’il est déjà répertorié dans hello Galerie d’applications Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie d’Azure AD

Lorsque vous ajoutez une application à partir de hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), vous pouvez hello comment vous souhaitez que votre toosign d’utilisateurs dans l’application de toothat. Vous pouvez configurer ce choix à tout moment en sélectionnant hello **Single Sign-on** élément de navigation sur une Application d’entreprise Bonjour [Azure Portal](https://portal.azure.com/).

Un des tooyou disponibles des méthodes d’authentification unique de hello est hello [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option. Il s’agit d’un excellent moyen de tooget démarré l’intégration d’applications dans Azure AD rapidement et vous permet de :

-   Activer **l’authentification unique pour vos utilisateurs** en stocker en toute sécurité et en relisant les noms d’utilisateur et mots de passe pour l’application hello que vous avez intégré à Azure AD

-   **Prend en charge les applications qui requièrent plusieurs champs de connexion** pour les applications qui nécessitent toosign champs plus que nom d’utilisateur et mot de passe dans

-   **Personnaliser les étiquettes hello** des champs d’entrée hello nom d’utilisateur et mot de passe, les utilisateurs voient sur hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lorsqu’ils entrent leurs informations d’identification

-   Autoriser votre **utilisateurs** tooprovide leurs noms d’utilisateur et les mots de passe pour les comptes d’application existants qu’ils tapent dans manuellement sur hello [Application panneau d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Autoriser un **membre du groupe d’activités hello** toospecify hello noms et mots de passe assigné tooa utilisateur à l’aide de hello [accès à l’Application libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) fonctionnalité

-   Autoriser un **administrateur** toospecify hello noms et mots de passe utilisateur de tooa à l’aide des informations d’identification de la mise à jour hello fonction si [affectation d’un utilisateur de l’application tooan](#assign-a-user-to-an-application-directly)

-   Autoriser un **administrateur** toospecify hello partagé utilisateur ou mot de passe utilisé par un groupe de personnes à l’aide des informations d’identification de la mise à jour hello fonction si [attribution d’une application tooan de groupe](#assign-an-application-to-a-group-directly)

Ci-dessous décrit comment vous pouvez activer [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application qui est déjà hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

## <a name="overview-of-steps-required"></a>Vue d’ensemble des étapes requises
tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#add-an-application-from-the-azure-ad-gallery)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application-for-password-single-sign-on)

-   [Affecter tooa utilisateur de l’application hello ou un groupe](#assign-the-application-to-a-user-or-a-group)

    -   [Attribuer un utilisateur de l’application tooan directement](#assign-a-user-to-an-application-directly)

    -   [Affecter un groupe d’applications tooa directement](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

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

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurer une application hello pour mot de passe l’authentification unique

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

9.  [Affecter des utilisateurs toohello application](#assign-a-user-to-an-application-directly).

10. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

## <a name="assign-a-user-tooan-application-directly"></a>Attribuer un utilisateur de l’application tooan directement

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

## <a name="assign-an-application-tooa-group-directly"></a>Affecter un groupe d’applications tooa directement

tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :

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

10. Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.

Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)
