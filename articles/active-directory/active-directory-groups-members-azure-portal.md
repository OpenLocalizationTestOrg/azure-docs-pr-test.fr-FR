---
title: "aaaManage hello membres d’un groupe dans Azure Active Directory | Documents Microsoft"
description: "Comment tooadd ou supprimer des utilisateurs et des périphériques d’un groupe dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Gérer l’appartenance à un groupe des utilisateurs dans votre client Azure Active Directory
Cet article explique comment toomanage hello membres d’un groupe dans Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Comment rechercher des membres hello et les gérer ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Sur hello **utilisateurs et groupes - tous les groupes** panneau, sélectionnez un groupe.
5. Sur hello **groupe - *groupname***  panneau, sélectionnez **membres**.

   ![Panneau de membres hello ouverture](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. tooadd membres toohello groupe hello **- groupe de membres** panneau, sélectionnez **ajouter des membres**.

   ![Commande Ajouter des membres](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Sur hello **membres** panneau, sélectionnez une ou plus d’utilisateurs ou périphériques tooadd toohello et sélectionnez hello **sélectionnez** bouton bas hello hello panneau tooadd les toohello groupe. Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance. Dans cette zone aucun caractère générique n’est accepté.
8. tooremove les membres de groupe hello hello **- groupe de membres** panneau, sélectionnez un membre.
9. Sur hello ***membername*** panneau, sélectionnez hello **supprimer** de commandes et confirmez votre choix à l’invite de hello.

   ![Commande Supprimer des membres](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Lorsque vous avez terminé la modification des membres du groupe de hello, sélectionnez **enregistrer**.

## <a name="additional-information"></a>Informations supplémentaires
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Création d’un nouveau groupe et ajout de membres](active-directory-groups-create-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer l’appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
