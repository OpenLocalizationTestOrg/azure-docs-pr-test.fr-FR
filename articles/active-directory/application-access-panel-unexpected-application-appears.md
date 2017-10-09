---
title: "applications d’aaaHow apparaissent dans le volet d’accès hello | Documents Microsoft"
description: "Résoudre les problèmes de la raison pour laquelle une application s’affiche dans hello panneau d’accès"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>L’apparence des applications dans le volet d’accès hello

Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à. Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello. Hello admin peut configurer hello toohello utilisateur de l’application directement ou groupe tooa qu'un utilisateur fait partie du résultant dans une application hello figurant sur le panneau d’accès de l’utilisateur hello.

## <a name="general-issues-toocheck-first"></a>Général émet toocheck tout d’abord

-   Si une application vient d’être supprimée d’un utilisateur ou groupe hello utilisateur est membre de, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si l’application hello est supprimée.

-   Si une licence vient d’être supprimée d’un utilisateur ou un utilisateur hello le groupe est que membre de ce peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe hello pour toobe des modifications apportée. Prévoyez du temps supplémentaire avant de vous connecter en hello panneau d’accès.

## <a name="problems-related-tooassigning-applications-toousers"></a>Des problèmes connexes tooassigning applications toousers

Un utilisateur peut s’agir d’une application dans leur volet d’accès, car il avaient été précédemment affecté tooit. Voici certains toocheck façons :

-   [Vérifiez si un utilisateur est affecté toohello application](#check-if-a-user-is-assigned-to-the-application)

-   [Vérifier si un utilisateur est sous licence toohello application relative](#check-if-a-user-is-under-a-license-related-to-the-application)


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

  * Si vous souhaitez que les utilisateurs de hello tooremove à partir de l’application hello, **cliquez sur la ligne hello** de l’utilisateur de hello et sélectionnez **supprimer**.

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

## <a name="problems-related-tooassigning-applications-toogroups"></a>Des problèmes connexes tooassigning applications toogroups

Un utilisateur peut s’agir d’une application dans leur volet d’accès car ils font partie d’un groupe auquel a été attribué application hello. Voici certains toocheck façons :

-   [Vérifier les appartenances d’un utilisateur à des groupes](#check-a-users-group-memberships)

-   [Vérifiez si un utilisateur est membre d’un groupe tooa licence attribué](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Vérifier les appartenances d’un utilisateur à des groupes

toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Groupes.**

8.  Vérifiez toosee si l’utilisateur fait partie d’une application toohello de groupe affecté.

   * Si vous souhaitez utilisateur de hello tooremove à partir du groupe de hello, **cliquez sur la ligne hello** hello groupe d’et sélectionnez Supprimer.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Vérifiez si un utilisateur est membre d’un groupe tooa licence attribué

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Tous les utilisateurs**.

6.  **Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.

7.  Cliquez sur **Groupes.**

8.  Cliquez sur ligne hello d’un groupe spécifique.

9.  Cliquez sur **licences** toosee quel groupe hello de licences a affecté tooit.

  * Si le groupe de hello est attribué une licence Office tooan sur que ceci peut activer certaine tooappear d’applications de premier tiers Office hello panneau d’accès de l’utilisateur.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Si ces étapes de dépannage ne pas hello hello résoudre

Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)

-   ID client

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
