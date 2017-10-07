---
title: "affectations d’accès de ressource Azure d’aaaView | Documents Microsoft"
description: "Afficher et gérer toutes les affectations de contrôle d’accès en fonction du rôle hello pour tout utilisateur ou groupe Bonjour portail Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Afficher les affectations d’accès des utilisateurs et groupes Bonjour portail Azure
> [!div class="op_single_selector"]
> * [Gérer l’accès par utilisateur ou par groupe](role-based-access-control-manage-assignments.md)
> * [Gérer l’accès par ressource](role-based-access-control-configure.md)

Avec le contrôle d’accès basé sur un rôle (RBAC) Bonjour Azure Active Directory (Azure AD), vous pouvez gérer l’accès tooyour Azure ressources. 

Accès attribué avec RBAC est affinée, car il existe deux façons, vous pouvez limiter les autorisations de hello :

* **Étendue :** attributions de rôles RBAC sont tooa étendue des abonnement spécifique, groupe de ressources ou ressource. Un utilisateur donné accès tooa seule ressource ne peut pas accéder aux autres ressources de hello même abonnement.
* **Rôle :** étendue hello d’affectation de hello, l’accès est restreint davantage par l’attribution d’un rôle. Les rôles peuvent être de haut niveau, comme propriétaire, ou spécifiques, comme lecteur de machines virtuelles.

Rôles peuvent uniquement être attribuées à partir d’abonnement de hello, groupe de ressources ou ressource qui est étendue hello pour l’attribution de hello. Mais vous pouvez afficher toutes les affectations d’accès hello pour un utilisateur donné ou un groupe dans un emplacement unique. Vous pouvez avoir des attributions de rôles too2000 dans chaque abonnement. 

Obtenir plus d’informations sur la façon de trop[utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Afficher les affectations d’accès
toolook les affectations d’accès hello pour un seul utilisateur ou un groupe, démarrer dans Azure Active Directory hello [portail Azure](http://portal.azure.com).

1. Sélectionnez **Azure Active Directory**. Si cette option n’est pas visible dans votre liste de navigation, sélectionnez **plus Services** , puis faites défiler vers le bas toofind **Azure Active Directory**.
2. Sélectionnez **Utilisateurs et groupes**, puis **Tous les utilisateurs** ou **Tous les groupes**. Pour cet exemple, nous nous concentrons sur les utilisateurs.
    ![Gérer les utilisateurs et les groupes dans Azure Active Directory - capture d’écran](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Rechercher un utilisateur hello par nom ou nom d’utilisateur.
4. Sélectionnez **ressources Azure** sur le panneau d’utilisateur hello. Toutes les attributions d’accès hello pour cet utilisateur s’affichent.

### <a name="read-permissions-tooview-assignments"></a>Tooview affectations d’autorisations de lecture
Cette page affiche uniquement les affectations d’accès hello que vous avez l’autorisation tooread. Par exemple, vous avez accès en lecture toosubscription A et accédez toohello ressources Azure panneau toocheck les affectations d’un utilisateur. Vous pouvez voir ses affectations d’accès pour l’abonnement A, mais vous ne pouvez pas voir qu’il a également des affectations d’accès dans l’abonnement B.

## <a name="delete-access-assignments"></a>Supprimer des affectations d’accès
À partir de ce panneau, vous pouvez supprimer les affectations d’accès qui ont été directement affectées tooa utilisateur ou un groupe. Si l’assignation d’accès hello a été héritée d’un groupe parent, vous devez toogo toohello ressource ou un abonnement et gérez l’affectation hello il.

1. Dans liste de hello de toutes les affectations d’accès hello pour un utilisateur ou un groupe, sélectionnez hello une souhaité toodelete.
2. Sélectionnez **supprimer** , puis **Oui** tooconfirm.
    ![Supprimer l’affectation de l’accès - capture d’écran](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Étapes suivantes

* Prise en main le contrôle d’accès en fonction du rôle trop[utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](role-based-access-control-configure.md)
* Consultez hello [rôles intégrés RBAC](role-based-access-built-in-roles.md)

