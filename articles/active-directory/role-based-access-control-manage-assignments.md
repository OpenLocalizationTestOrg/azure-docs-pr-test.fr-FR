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
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="0d38c-103">Afficher les affectations d’accès des utilisateurs et groupes Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0d38c-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d38c-104">Gérer l’accès par utilisateur ou par groupe</span><span class="sxs-lookup"><span data-stu-id="0d38c-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="0d38c-105">Gérer l’accès par ressource</span><span class="sxs-lookup"><span data-stu-id="0d38c-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="0d38c-106">Avec le contrôle d’accès basé sur un rôle (RBAC) Bonjour Azure Active Directory (Azure AD), vous pouvez gérer l’accès tooyour Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="0d38c-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="0d38c-107">Accès attribué avec RBAC est affinée, car il existe deux façons, vous pouvez limiter les autorisations de hello :</span><span class="sxs-lookup"><span data-stu-id="0d38c-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="0d38c-108">**Étendue :** attributions de rôles RBAC sont tooa étendue des abonnement spécifique, groupe de ressources ou ressource.</span><span class="sxs-lookup"><span data-stu-id="0d38c-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="0d38c-109">Un utilisateur donné accès tooa seule ressource ne peut pas accéder aux autres ressources de hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d38c-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="0d38c-110">**Rôle :** étendue hello d’affectation de hello, l’accès est restreint davantage par l’attribution d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="0d38c-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="0d38c-111">Les rôles peuvent être de haut niveau, comme propriétaire, ou spécifiques, comme lecteur de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0d38c-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="0d38c-112">Rôles peuvent uniquement être attribuées à partir d’abonnement de hello, groupe de ressources ou ressource qui est étendue hello pour l’attribution de hello.</span><span class="sxs-lookup"><span data-stu-id="0d38c-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="0d38c-113">Mais vous pouvez afficher toutes les affectations d’accès hello pour un utilisateur donné ou un groupe dans un emplacement unique.</span><span class="sxs-lookup"><span data-stu-id="0d38c-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="0d38c-114">Vous pouvez avoir des attributions de rôles too2000 dans chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d38c-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="0d38c-115">Obtenir plus d’informations sur la façon de trop[utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0d38c-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="0d38c-116">Afficher les affectations d’accès</span><span class="sxs-lookup"><span data-stu-id="0d38c-116">View access assignments</span></span>
<span data-ttu-id="0d38c-117">toolook les affectations d’accès hello pour un seul utilisateur ou un groupe, démarrer dans Azure Active Directory hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d38c-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="0d38c-118">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d38c-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="0d38c-119">Si cette option n’est pas visible dans votre liste de navigation, sélectionnez **plus Services** , puis faites défiler vers le bas toofind **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d38c-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="0d38c-120">Sélectionnez **Utilisateurs et groupes**, puis **Tous les utilisateurs** ou **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="0d38c-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="0d38c-121">Pour cet exemple, nous nous concentrons sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0d38c-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="0d38c-122">![Gérer les utilisateurs et les groupes dans Azure Active Directory - capture d’écran](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="0d38c-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="0d38c-123">Rechercher un utilisateur hello par nom ou nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0d38c-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="0d38c-124">Sélectionnez **ressources Azure** sur le panneau d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0d38c-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="0d38c-125">Toutes les attributions d’accès hello pour cet utilisateur s’affichent.</span><span class="sxs-lookup"><span data-stu-id="0d38c-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="0d38c-126">Tooview affectations d’autorisations de lecture</span><span class="sxs-lookup"><span data-stu-id="0d38c-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="0d38c-127">Cette page affiche uniquement les affectations d’accès hello que vous avez l’autorisation tooread.</span><span class="sxs-lookup"><span data-stu-id="0d38c-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="0d38c-128">Par exemple, vous avez accès en lecture toosubscription A et accédez toohello ressources Azure panneau toocheck les affectations d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0d38c-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="0d38c-129">Vous pouvez voir ses affectations d’accès pour l’abonnement A, mais vous ne pouvez pas voir qu’il a également des affectations d’accès dans l’abonnement B.</span><span class="sxs-lookup"><span data-stu-id="0d38c-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="0d38c-130">Supprimer des affectations d’accès</span><span class="sxs-lookup"><span data-stu-id="0d38c-130">Delete access assignments</span></span>
<span data-ttu-id="0d38c-131">À partir de ce panneau, vous pouvez supprimer les affectations d’accès qui ont été directement affectées tooa utilisateur ou un groupe.</span><span class="sxs-lookup"><span data-stu-id="0d38c-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="0d38c-132">Si l’assignation d’accès hello a été héritée d’un groupe parent, vous devez toogo toohello ressource ou un abonnement et gérez l’affectation hello il.</span><span class="sxs-lookup"><span data-stu-id="0d38c-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="0d38c-133">Dans liste de hello de toutes les affectations d’accès hello pour un utilisateur ou un groupe, sélectionnez hello une souhaité toodelete.</span><span class="sxs-lookup"><span data-stu-id="0d38c-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="0d38c-134">Sélectionnez **supprimer** , puis **Oui** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0d38c-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="0d38c-135">![Supprimer l’affectation de l’accès - capture d’écran](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="0d38c-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d38c-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d38c-136">Next steps</span></span>

* <span data-ttu-id="0d38c-137">Prise en main le contrôle d’accès en fonction du rôle trop[utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="0d38c-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="0d38c-138">Consultez hello [rôles intégrés RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0d38c-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

