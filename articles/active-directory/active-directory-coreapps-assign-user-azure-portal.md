---
title: "aaaAssign une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory | Documents Microsoft"
description: "Comment tooselect un tooassign d’application d’entreprise un tooit utilisateur ou un groupe dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory
Il est facile tooassign un utilisateur ou un groupe tooyour entreprise dans Azure Active Directory (Azure AD). Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Comment attribuer des applications d’entreprise tooan utilisateur accès ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez Azure Active Directory dans la zone de texte hello et sélectionnez **entrée**.
3. Sur hello **Azure Active Directory - *nom_répertoire***  blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **des applications d’entreprise**.

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**. Vous verrez une liste d’applications hello que vous pouvez gérer.
5. Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.
6. Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **utilisateurs et groupes**.

    ![En sélectionnant hello toutes les commandes d’applications](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. Sur hello ***appname*** **-utilisateur et l’affectation du groupe** panneau, sélectionnez hello **ajouter** commande.
8. Sur hello **ajouter l’affectation** panneau, sélectionnez **utilisateurs et groupes**.

    ![Affecter une application toohello utilisateur ou un groupe](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. Sur hello **utilisateurs et groupes** panneau, sélectionnez un ou plusieurs utilisateurs ou les groupes à partir de hello liste et sélectionnez hello **sélectionnez** bouton bas hello du Panneau de hello.
10. Sur hello **ajouter l’affectation** panneau, sélectionnez **rôle**. Ensuite, sous hello **sélectionner un rôle** panneau, sélectionnez un toohello tooapply de rôle sélectionné d’utilisateurs ou des groupes, puis sélectionnez hello **OK** bouton bas hello du Panneau de hello.
11. Sur hello **ajouter l’affectation** panneau, sélectionnez hello **affecter** bouton bas hello du Panneau de hello. Hello affecté les utilisateurs ou groupes ont les autorisations hello définies par le rôle sélectionné de hello pour cette application d’entreprise.

## <a name="next-steps"></a>Étapes suivantes
* [Voir tous mes groupes](active-directory-groups-view-azure-portal.md)
* [Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Désactiver les connexions utilisateur pour une application d’entreprise](active-directory-coreapps-disable-app-azure-portal.md)
* [Modifier le nom hello ou un logo d’une application d’entreprise](active-directory-coreapps-change-app-logo-user-azure-portal.md)
