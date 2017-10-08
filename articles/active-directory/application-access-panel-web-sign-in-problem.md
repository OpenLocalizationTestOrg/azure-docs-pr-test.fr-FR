---
title: "aaaProblem de signature dans le site Web du panneau d’accès toohello | Documents Microsoft"
description: "Problèmes de tootroubleshoot de conseils que vous pouvez rencontrer lors de la tentative de toosign dans toouse hello panneau d’accès"
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Problème de connexion dans le site Web du panneau d’accès toohello

Hello volet d’accès est un portail web qui permet à un utilisateur qui dispose d’une entreprise ou école administrateur de compte dans Azure Active Directory (Azure AD) tooview et lancer les applications cloud qui hello Azure AD lui a accordé l’accès à. Un utilisateur disposant des éditions d’Azure AD permet également de groupes en libre-service et les fonctionnalités de gestion d’application via hello panneau d’accès. Hello volet d’accès est séparé hello portail Azure et ne requiert pas d’utilisateurs toohave un abonnement Azure.

Les utilisateurs peuvent se connecter toohello volet d’accès s’ils ont un compte professionnel ou scolaire dans Azure AD.

-   Les utilisateurs peuvent être authentifiés par Azure AD directement.

-   Les utilisateurs peuvent être authentifiés à l’aide d’Active Directory Federation Services (ADFS).

-   Les utilisateurs peuvent être authentifiés par Windows Server Active Directory.

Si un utilisateur dispose d’un abonnement pour Azure ou Office 365 et à l’aide hello portail Azure ou une application Office 365, ils serez en mesure de toouse hello volet d’accès en toute transparence sans avoir besoin de toosign de nouveau. Les utilisateurs qui ne sont pas authentifiés être demandée toosign dans à l’aide de nom d’utilisateur hello et le mot de passe de leur compte dans Azure AD. Si l’organisation de hello a configuré la fédération, il suffit de taper le nom d’utilisateur hello.

## <a name="general-issues-toocheck-first"></a>Général émet toocheck tout d’abord 

-   Assurez-vous que la signature de l’utilisateur de hello dans toohello **Corrigez-la**: <https://myapps.microsoft.com>

-   Assurez-vous que navigateur de l’utilisateur hello a ajouté hello URL tooits **sites de confiance**

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


## <a name="problems-with-hello-users-account"></a>Problèmes avec le compte d’utilisateur hello

Accès toohello volet d’accès peut être bloqué en raison du problème de tooa avec un compte d’utilisateur hello. Voici quelques méthodes pour vous aider à résoudre les problèmes avec les utilisateurs et leurs paramètres de compte :

-   [Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Vérifier l’état du compte d’un utilisateur](#check-a-users-account-status)

-   [Réinitialiser le mot de passe d’un utilisateur](#reset-a-users-password)

-   [Activer la réinitialisation du mot de passe libre-service](#enable-self-service-password-reset)

-   [Vérifier l’état Multi-Factor Authentication d’un utilisateur](#check-a-users-multi-factor-authentication-status)

-   [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info)

-   [Vérifier les appartenances d’un utilisateur à des groupes](#check-a-users-group-memberships)

-   [Vérifier les licences affectées à un utilisateur](#check-a-users-assigned-licenses)

-   [Affecter une licence à un utilisateur](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory

toocheck si un compte d’utilisateur est présent, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Vérifiez les propriétés de hello de hello utilisateur objet toobe assurer qu’elles apparaîtront comme prévu et aucune donnée n’est manquante.

### <a name="check-a-users-account-status"></a>Vérifier l’état du compte d’un utilisateur

toocheck un utilisateur état du compte, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Profil**.

8.  Sous **paramètres** vous assurer que **bloc connectez-vous** est défini trop**non**.

### <a name="reset-a-users-password"></a>Réinitialiser le mot de passe d’un utilisateur

tooreset un mot de passe, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur hello **réinitialisation de mot de passe** bouton en haut de hello du panneau d’utilisateur hello.

8.  Cliquez sur hello **réinitialisation de mot de passe** bouton sur hello **réinitialisation de mot de passe** panneau s’affiche.

9.  Hello de copie **mot de passe temporaire** ou **Entrez un nouveau mot de passe** pour l’utilisateur de hello.

10. Communiquer ce nouvel utilisateur toohello de mot de passe, ils requis toochange ce mot de passe lors de sa prochaine connexion tooAzure Active Directory.

### <a name="enable-self-service-password-reset"></a>Activer la réinitialisation du mot de passe libre-service

tooenable le mot de passe libre-service de réinitialisation, suivez les étapes de déploiement hello ci-dessous :

-   [Activer les utilisateurs tooreset leurs mots de passe Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Activer les utilisateurs tooreset ou de modifier leurs mots de passe Active Directory local](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Vérifier l’état Multi-Factor Authentication d’un utilisateur

toocheck un utilisateur multi-Factor de l’état d’authentification, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  Cliquez sur hello **multi-Factor Authentication** bouton en haut de hello du panneau des hello.

7.  Une fois hello **portail d’Administration de l’authentification multifacteur** charges, assurez-vous que vous êtes sur hello **utilisateurs** onglet.

8.  Rechercher les utilisateur hello dans liste hello des utilisateurs par la recherche, le filtrage ou le tri.

9.  Utilisateur hello SELECT à partir de la liste de hello des utilisateurs et **activer**, **désactiver**, ou **appliquer** authentification multifacteur selon vos besoins.

   >[!NOTE]
   >Si un utilisateur est dans un **appliqué** d’état, vous pouvez les définir trop**désactivé** temporairement toolet replacer dans son compte. Une fois qu’ils sont dans, vous pouvez ensuite modifier leur état trop**activé** toorequire à nouveau les toore-s’inscrire leurs informations de contact lors de sa prochaine connexion. Ou bien, vous pouvez suivre les étapes de hello Bonjour [vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info) tooverify ou définir ces données pour eux.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Vérifier les informations de contact de l’authentification d’un utilisateur

toocheck utilisée pour l’authentification multifacteur, l’accès conditionnel, Protection d’identité et réinitialisation du mot de passe, des informations de contact de l’authentification de l’utilisateur suit hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Profil**.

8.  Faites défiler la liste trop**les informations de contact d’authentification**.

9.  **Révision** les données de salutation inscrit pour l’utilisateur de hello et de mise à jour en fonction des besoins.

### <a name="check-a-users-group-memberships"></a>Vérifier les appartenances d’un utilisateur à des groupes

de toocheck un utilisateur appartenance aux groupes, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **groupes** toosee qui regroupe les utilisateur hello est membre.

### <a name="check-a-users-assigned-licenses"></a>Vérifier les licences affectées à un utilisateur

toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.

### <a name="assign-a-user-a-license"></a>Affecter une licence à un utilisateur 

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

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si ces étapes de dépannage ne résolvent pas le problème de hello

Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)

-   ID client

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)
