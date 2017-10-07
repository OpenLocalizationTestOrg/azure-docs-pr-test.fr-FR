---
title: aaaProblems connecter tooa application Microsoft | Documents Microsoft
description: "Résoudre les problèmes courants rencontrés lors de la connexion toofirst Microsoft Applications tierces à l’aide d’Azure AD (par exemple, Office 365)"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problèmes de connexion tooa application Microsoft

Les applications Microsoft (comme Office 365 Exchange, SharePoint, Yammer, etc.) sont affectées et gérées un peu différemment des applications SaaS tierces et des autres applications que vous intégrez à Azure AD pour l’authentification unique.

Il existe trois manières principales qu’un utilisateur peut obtenir l’accès tooa-Microsoft a publié l’application.

-   Pour les applications dans hello Office 365 ou d’autres suites de tests payants, utilisateurs sont autorisés à accéder via **l’attribution de licence** soit directement tootheir compte d’utilisateur ou via un groupe à l’aide de notre capacité d’affectation basée sur le groupe de licences.

-   Pour les applications que Microsoft ou un tiers publie librement pour toute personne toouse, les utilisateurs peuvent accéder via **consentement de l’utilisateur**. This0 signifie qu’ils application toohello avec leur compte Azure AD ou votre école de connexion et permettent de jeu de toosome limitée accès toohave de données sur son compte.

-   Pour les applications que Microsoft ou un tiers 3e publie librement pour toute personne toouse, les utilisateurs peuvent également être accordés l’accès via **consentement de l’administrateur**. Cela signifie qu’un administrateur a déterminé l’application hello peut être utilisée par tous les membres de l’organisation de hello, afin qu’ils application toohello avec un compte d’administrateur Global de connexion et accorder tooeveryone d’accès dans l’organisation de hello.

tootroubleshoot votre problème, commencent par Bonjour [zones à problème général avec l’accès aux applications tooconsider](#general-problem-areas-with-application-access-to-consider) , puis lire hello [procédure pas à pas : étapes tootroubleshoot accès aux applications de Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget dans les détails de hello.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Zones à problème général avec l’accès aux applications tooconsider

Voici une liste de hello zones à problème général que vous pouvez Explorer si vous avez une idée d’où toostart, mais nous vous conseillons de lire hello tooget de procédure pas à pas va rapidement : [procédure pas à pas : étapes tootroubleshoot accès de l’Application Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problèmes avec le compte d’utilisateur hello](#problems-with-the-users-account)

-   [Problèmes liés aux groupes](#problems-with-groups)

-   [Problèmes liés aux stratégies d’accès conditionnel](#problems-with-conditional-access-policies)

-   [Problèmes liés au consentement d’application](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Étapes tootroubleshoot accès aux applications de Microsoft

Ci-dessous sont certaines personnes problèmes courants rencontrer quand les utilisateurs ne peuvent pas se connecter tooa application Microsoft.

-   Général émet toocheck tout d’abord

  * Assurez-vous que la signature de l’utilisateur de hello dans toohello **Corrigez-la** et pas une URL de l’application locale.

  * Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**

  * Vérifiez que hello **compte d’utilisateur existe** dans Azure Active Directory. [Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory](#problems-with-the-users-account)

  * Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions. [Vérifier l’état du compte d’un utilisateur](#problems-with-the-users-account)

  * Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.** [Réinitialiser le mot de passe d’un utilisateur](#reset-a-users-password) ou [Activer la réinitialisation du mot de passe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur. [Vérifier l’état Multi-Factor Authentication d’un utilisateur](#check-a-users-multi-factor-authentication-status) ou [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info)

   * Vérifiez qu’une **stratégie d’accès conditionnel** ou qu’une **stratégie de protection d’identité** ne bloque pas l’accès utilisateur. [Vérifier une stratégie d’accès conditionnel](#problems-with-conditional-access-policies) ou [Vérifier la stratégie d’accès conditionnel d’une application spécifique](#check-a-specific-applications-conditional-access-policy) ou [Désactiver une stratégie d’accès conditionnel](#disable-a-specific-conditional-access-policy)

   * S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée. [Vérifier l’état Multi-Factor Authentication d’un utilisateur](#check-a-users-multi-factor-authentication-status) ou [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info)

-   Pour **Microsoft** **les applications qui nécessitent une licence** (comme Office 365), Voici certains problèmes spécifiques de toocheck une fois que vous avez écarté problèmes généraux de hello ci-dessus :

   * S’assurer que hello utilisateur ou a un **licence attribuée.** [Vérifier les licences affectées à un utilisateur](#check-a-users-assigned-licenses) ou [Vérifier les licences affectées à un groupe](#check-a-groups-assigned-licenses)

   * Si la licence hello est **affecté tooa** **groupe statique**, vérifiez que hello **utilisateur est membre** de ce groupe. [Vérifier les appartenances d’un utilisateur à des groupes](#check-a-users-group-memberships)

   * Si la licence hello est **affecté tooa** **groupe dynamique**, vérifiez que hello **règle de groupe dynamique est correctement**. [Vérifier les critères d’appartenance d’un groupe dynamique](#check-a-dynamic-groups-membership-criteria)

   * Si la licence hello est **affecté tooa** **groupe dynamique**, vérifiez ce groupe dynamique hello a **terminé le traitement** son appartenance et ce hello **utilisateur est un membre** (Cela peut prendre un certain temps). [Vérifier les appartenances d’un utilisateur à des groupes](#check-a-users-group-memberships)

   *  Une fois que vous vérifiez que les licences hello sont attribuée, assurez-vous que la licence hello est **ne pas expiré**.

   *  Assurez-vous que la licence hello est **pour l’application hello** ils accèdent.

-   Pour **Microsoft** **les applications qui ne nécessitent pas une licence**, voici quelques autres toocheck choses :

   * Si l’application hello demande **autorisations au niveau de l’utilisateur** (par exemple « accéder à cette boîte aux lettres »), assurez-vous que l’utilisateur hello toohello application s’est connecté et a effectué une **opération d’accord de niveau de l’utilisateur**  application hello de toolet accéder à ses données.

   * Si l’application hello demande **autorisations de niveau administrateur** (par exemple « accéder aux boîtes aux lettres de tous les utilisateurs »), assurez-vous qu’un administrateur général a effectué une **opération d’accord de niveau administrateur sur nom de tous les utilisateurs** dans l’organisation de hello.

## <a name="problems-with-hello-users-account"></a>Problèmes avec le compte d’utilisateur hello

Accès à l’application peut être bloqué en raison du problème de tooa avec un utilisateur qui est attribué toohello application. Voici quelques méthodes pour vous aider à résoudre les problèmes avec les utilisateurs et leurs paramètres de compte :

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

  * **Remarque**: si un utilisateur est dans un **appliqué** d’état, vous pouvez les définir trop**désactivé** temporairement toolet replacer dans son compte. Une fois qu’ils sont dans, vous pouvez ensuite modifier leur état trop**activé** toorequire à nouveau les toore-s’inscrire leurs informations de contact lors de sa prochaine connexion. Ou bien, vous pouvez suivre les étapes de hello Bonjour [vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info) tooverify ou définir ces données pour eux.

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

## <a name="problems-with-groups"></a>Problèmes liés aux groupes

Accès à l’application peut être bloqué en raison du problème de tooa avec un groupe auquel est attribué toohello application. Voici quelques méthodes pour vous aider à résoudre les problèmes liés aux groupes et à l’appartenance :

-   [Vérifier l’appartenance à un groupe](#check-a-groups-membership)

-   [Vérifier les critères d’appartenance d’un groupe dynamique](#check-a-dynamic-groups-membership-criteria)

-   [Vérifier les licences affectées à un groupe](#check-a-groups-assigned-licenses)

-   [Retraiter les licences d’un groupe](#reprocess-a-groups-licenses)

-   [Affecter une licence à un groupe](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Vérifier l’appartenance à un groupe

toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les groupes**.

6.  **Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **membres** liste de hello tooreview d’utilisateurs affectés toothis groupe.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Vérifier les critères d’appartenance d’un groupe dynamique 

toocheck les critères d’appartenance d’un groupe dynamique, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les groupes**.

6.  **Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Règles d’appartenance dynamique**.

8.  Hello de révision **simple** ou **avancées** définie pour ce groupe de règles et vérifiez que cet utilisateur hello souhaité toobe un membre de ce groupe répond à ces critères.

### <a name="check-a-groups-assigned-licenses"></a>Vérifier les licences affectées à un groupe

toocheck un groupe affecté des licences, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les groupes**.

6.  **Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.

### <a name="reprocess-a-groups-licenses"></a>Retraiter les licences d’un groupe

tooreprocess un groupe affecté des licences, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les groupes**.

6.  **Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.

8.  Cliquez sur hello **retraiter** tooensure bouton qui hello les membres du groupe de licences attribuées toothis sont à jour. Cette opération peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe de hello.

   >[!NOTE]
   >toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence. [Affecter une licence à un utilisateur](#problems-with-application-consent)
   >
   >

### <a name="assign-a-group-a-license"></a>Affecter une licence à un groupe

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
   >toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence. [Affecter une licence à un utilisateur](#problems-with-application-consent)
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problèmes liés aux stratégies d’accès conditionnel

### <a name="check-a-specific-conditional-access-policy"></a>Vérifier une stratégie d’accès conditionnel

toocheck ou valider une stratégie d’accès conditionnel unique :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.

5.  Cliquez sur hello **accès conditionnel** élément de navigation.

6.  Cliquez sur stratégie hello vous êtes intéressé par inspection.

7.  Vérifiez la présence de conditions, d’affectations ou d’autres paramètres pouvant bloquer l’accès de l’utilisateur.

   >[!NOTE]
   >Vous souhaiterez peut-être tootemporarily désactiver cette tooensure stratégie qu’il n’affecte pas les signe assurance toodo, hello ensemble **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Vérifier une stratégie d’accès conditionnel d’une application

toocheck ou valider une seule stratégie de l’application actuellement configuré l’accès conditionnel :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.

5.  Cliquez sur **Toutes les applications**.

6.  Recherche de l’application hello vous intéressez, ou hello utilisateur tente de toosign dans tooby application afficher les id de nom ou de l’application.

     >[!NOTE]
     >Si vous ne voyez pas application hello souhaité, cliquez sur hello **filtre** bouton et étendre la portée de hello de liste de hello trop**toutes les applications**. Si vous souhaitez toosee plus de colonnes, cliquez sur hello **colonnes** bouton tooadd des détails supplémentaires pour vos applications.
     >
     >

7.  Cliquez sur hello **accès conditionnel** élément de navigation.

8.  Cliquez sur stratégie hello vous êtes intéressé par inspection.

9.  Vérifiez la présence de conditions, d’affectations ou d’autres paramètres pouvant bloquer l’accès de l’utilisateur.

     >[!NOTE]
     >Vous souhaiterez peut-être tootemporarily désactiver cette tooensure stratégie qu’il n’affecte pas les signe assurance toodo, hello ensemble **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Désactiver une stratégie d’accès conditionnel

toocheck ou valider une stratégie d’accès conditionnel unique :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.

5.  Cliquez sur hello **accès conditionnel** élément de navigation.

6.  Cliquez sur stratégie hello vous êtes intéressé par inspection.

7.  Désactivez hello de stratégie en définissant un hello **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton.

## <a name="problems-with-application-consent"></a>Problèmes liés au consentement d’application

Accès à l’application peut être bloqué, car l’opération de consentement d’autorisations adéquates hello n’a pas eu lieu. Voici quelques méthodes pour résoudre les problèmes de consentement d’application :

-   [Effectuer une opération de consentement de niveau utilisateur](#perform-a-user-level-consent-operation)

-   [Effectuer une opération de consentement de niveau administrateur pour n’importe quelle application](#perform-administrator-level-consent-operation-for-any-application)

-   [Effectuer une opération de consentement de niveau administrateur pour une application à locataire unique](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Effectuer une opération de consentement de niveau administrateur pour une application multilocataire](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Effectuer une opération de consentement de niveau utilisateur

-   Pour des applications compatibles ouvrir connecter d’ID qui demande des autorisations, la navigation d’écran de connexion de l’application toohello effectue une application de toohello utilisateur au niveau de consentement pour l’utilisateur connecté hello.

-   Si vous souhaitez toodo cela par programme, consultez [demander le consentement des utilisateurs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Effectuer une opération de consentement de niveau administrateur pour n’importe quelle application

-   Pour **uniquement les applications développées à l’aide du modèle d’application hello V1**, vous pouvez forcer cette toooccur de niveau de consentement d’administrateur en ajoutant «**? invite = admin\_donner son consentement**« fin toohello d’un URL de connexion de l’application.

-   Pour **toutes les applications développées à l’aide du modèle d’application hello V2**, vous pouvez appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations de hello à partir d’un répertoire administrateur** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Effectuer une opération de consentement de niveau administrateur pour une application à locataire unique

-   Pour **locataire unique applications** qui demande les autorisations (telles que celles vous développez ou que vous possédez dans votre organisation), vous pouvez effectuer une **administratives consentement** opération pour le compte de toutes les les utilisateurs en vous connectant en tant qu’administrateur général et en cliquant sur hello **accorder des autorisations** bouton haut hello hello **Registre de l’Application -&gt; toutes les Applications -&gt; sélectionner une application - &gt; Autorisations requises** panneau.

-   Pour **toutes les applications développées à l’aide de hello V1 ou V2 modèle d’application**, vous pouvez appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations hello à un l’administrateur Active** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Effectuer une opération de consentement de niveau administrateur pour une application multilocataire

-   Pour les **applications multilocataires** qui demandent des autorisations (comme les applications développées par un tiers ou par Microsoft), vous pouvez effectuer une opération de **consentement de niveau administrateur**. Connectez-vous en tant qu’administrateur général et en cliquant sur hello **accorder des autorisations** sous hello **des Applications d’entreprise -&gt; toutes les Applications -&gt; sélectionner une application -&gt; Autorisations** blade (disponible bientôt).

-   Vous pouvez également appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations de hello à un administrateur d’annuaire** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Étapes suivantes
[À l’aide du point de terminaison consentement hello admin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

