---
title: "aaaRemove une affectation d’utilisateur ou un groupe à partir d’une application d’entreprise dans Active Directory de Azure | Documents Microsoft"
description: "Comment tooremove hello accéder à l’affectation d’un utilisateur ou un groupe à partir d’une application d’entreprise dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans Azure Active Directory
Il est facile tooremove un utilisateur ou un groupe d’être assignée tooone d’accès de vos applications d’entreprise dans Azure Active Directory (Azure AD). Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Comment supprimer une affectation d’utilisateur ou de groupe ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.
3. Sur hello **Azure Active Directory - *nom_répertoire***  blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **des applications d’entreprise**.

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**. Vous verrez une liste d’applications hello que vous pouvez gérer.
5. Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.
6. Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **utilisateurs et groupes**.

    ![Sélection d’utilisateurs ou groupes](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Sur hello ***appname*** **-utilisateur et l’affectation du groupe** panneau, sélectionnez une des autres utilisateurs ou groupes, puis hello **supprimer** commande. Confirmer votre décision à l’invite de hello.

    ![En sélectionnant la commande de suppression hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Étapes suivantes
* [Voir tous mes groupes](active-directory-groups-view-azure-portal.md)
* [Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)
* [Désactiver les connexions utilisateur pour une application d’entreprise](active-directory-coreapps-disable-app-azure-portal.md)
* [Modifier le nom hello ou un logo d’une application d’entreprise](active-directory-coreapps-change-app-logo-user-azure-portal.md)
