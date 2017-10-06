---
title: groupes de hello aaaManage votre groupe appartient tooin Azure Active Directory | Documents Microsoft
description: "Les groupes peuvent contenir d’autres groupes dans Azure Active Directory. Voici comment toomanage ces appartenances."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Gérer des groupes toowhich qu'un groupe appartient dans votre locataire Azure Active Directory
Les groupes peuvent contenir d’autres groupes dans Azure Active Directory. Voici comment toomanage ces appartenances.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Comment trouver les groupes de hello de que mon groupe est membre ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Sur hello **utilisateurs et groupes - tous les groupes** panneau, sélectionnez un groupe.
5. Sur hello **groupe - *groupname***  panneau, sélectionnez **appartenances au groupe**.

   ![Panneau des appartenances au groupe Ouverture hello](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd votre groupe en tant que membre d’un autre groupe, sur hello **de groupe - appartenances au groupe** panneau, sélectionnez hello **ajouter** commande.
7. Sélectionnez un groupe de hello **sélectionner un groupe** panneau, puis sélectionnez hello **sélectionnez** bouton bas hello du Panneau de hello. Vous pouvez ajouter votre groupe d’un groupe tooonly à la fois. Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance. Dans cette zone aucun caractère générique n’est accepté.

   ![Ajouter une appartenance à un groupe](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove votre groupe en tant que membre d’un autre groupe, sur hello **de groupe - appartenances** panneau, sélectionnez un groupe.
9. Sur hello ***groupname*** panneau, sélectionnez hello **supprimer** de commandes et confirmez votre choix à l’invite de hello.

   ![Commande Supprimer des appartenances](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Lorsque vous avez terminé de modifier les appartenances aux groupes de votre groupe, sélectionnez **Enregistrer**.

## <a name="additional-information"></a>Informations supplémentaires
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Création d’un nouveau groupe et ajout de membres](active-directory-groups-create-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer les membres d’un groupe](active-directory-groups-members-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
