---
title: "aaaProblems connecter tooan application Azure AD galerie configurée pour fédéré sur l’authentification unique | Documents Microsoft"
description: "Comment tootroubleshoot problèmes avec application de la galerie de Azure AD configurée pour le mot de passe l’authentification unique"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>Problèmes de connexion tooan application Azure AD galerie configurée pour fédérée l’authentification unique

Hello volet d’accès est un portail web qui permet à un utilisateur qui dispose d’une entreprise ou école administrateur de compte dans Azure Active Directory (Azure AD) tooview et lancer les applications cloud qui hello Azure AD lui a accordé l’accès à. Un utilisateur disposant des éditions d’Azure AD permet également de groupes en libre-service et les fonctionnalités de gestion d’application via hello panneau d’accès. Hello volet d’accès est séparé hello portail Azure et ne requiert pas d’utilisateurs toohave un abonnement Azure.

toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello. Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Configuration requise du navigateur de réunion hello panneau d’accès

Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS. toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello. Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.

Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :

-   Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure

-   Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou version ultérieure

-   Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou version ultérieure, et sur Mac OS X 10.6 ou version ultérieure

>[!NOTE]
>extension de l’authentification unique basée sur le mot de passe Hello deviennent disponibles pour Edge dans Windows 10 lorsque les extensions du navigateur sont pris en charge pour la session.
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Comment tooinstall hello extension du navigateur de panneau d’accès

tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.

2.  Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.

3.  Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.

4.  En fonction de votre navigateur vous être lien de téléchargement toohello dirigée. **Ajouter** navigateur de tooyour extension hello.

5.  Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.

6.  Une fois l’extension installée, **redémarrez** votre session de navigateur.

7.  Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe

Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :

-   [Extension du volet d’accès pour Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extension du volet d’accès pour Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configuration d’une stratégie de groupe pour Internet Explorer

Vous pouvez configurer une stratégie de groupe qui vous tooremotely installer une extension volet d’accès hello pour Internet Explorer sur les ordinateurs de vos utilisateurs.

conditions préalables de Hello sont les suivantes :

-   Vous avez configuré [les Services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), et vous avez joint le domaine de tooyour ordinateurs de vos utilisateurs.

-   Vous devez avoir hello hello « Modifier les paramètres » autorisation tooedit objet de stratégie de groupe (GPO). Par défaut, les membres de hello les groupes de sécurité suivants ont cette autorisation : les administrateurs de domaine, les administrateurs d’entreprise et les propriétaires créateurs de la stratégie de groupe. [En savoir plus](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Suivez le didacticiel de hello [comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) pour obtenir des instructions étape par étape comment tooconfigure hello de stratégie de groupe et déployez-le toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Résoudre les problèmes de hello volet d’accès dans Internet Explorer

Suivez hello [dépannage hello Extension volet d’accès pour Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide pour l’accès d’un outil de diagnostic et des instructions étape par étape sur la configuration de l’extension de hello pour Internet Explorer.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD

tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :

-   [Ajouter une application à partir de la galerie d’Azure AD hello](#_Add_an_application)

-   [Configurer une application hello pour mot de passe l’authentification unique](#configure-the-application-for-password-single-sign-on)

-   [Affecter des utilisateurs toohello application](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Ajouter une application à partir de la galerie d’Azure AD hello

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

9.  [Affecter des utilisateurs toohello application](#_How_to_assign).

10. En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello. Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.

### <a name="assign-users-toohello-application"></a>Affecter des utilisateurs toohello application

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

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a>Si ces résoudre les étapes ne résolvent hello 
Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   UPN (adresse e-mail de l’utilisateur)

-   ID de locataire

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)
