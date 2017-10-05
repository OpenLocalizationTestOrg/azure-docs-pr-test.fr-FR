---
title: "Afficher les affectations d’accès aux ressources Azure | Microsoft Docs"
description: "Affichez et gérez toutes les affectations de contrôle d’accès en fonction du rôle des utilisateurs ou groupes sur le Portail Azure"
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
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="4c152-103">Afficher les affectations d’accès des utilisateurs et des groupes sur le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4c152-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c152-104">Gérer l’accès par utilisateur ou par groupe</span><span class="sxs-lookup"><span data-stu-id="4c152-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="4c152-105">Gérer l’accès par ressource</span><span class="sxs-lookup"><span data-stu-id="4c152-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="4c152-106">Avec le contrôle d’accès en fonction du rôle (RBAC), intégré à Azure Active Directory (Azure AD), vous pouvez gérer l’accès à vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4c152-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="4c152-107">Les accès affectés avec le RBAC sont précis car il existe deux façons de restreindre les autorisations :</span><span class="sxs-lookup"><span data-stu-id="4c152-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="4c152-108">**Étendue :** les affectations de rôles RBAC sont limitées à un abonnement, à un groupe de ressources ou à une ressource donnés.</span><span class="sxs-lookup"><span data-stu-id="4c152-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="4c152-109">Un utilisateur ayant accès à une ressource en particulier ne peut pas accéder aux autres ressources du même abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c152-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="4c152-110">**Rôle :** au sein de l’affectation d’étendue, l’accès est encore restreint par l’affectation d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="4c152-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="4c152-111">Les rôles peuvent être de haut niveau, comme propriétaire, ou spécifiques, comme lecteur de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4c152-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="4c152-112">Les rôles peuvent être affectés au sein de l’abonnement, du groupe de ressources ou de la ressource qui constitue l’étendue de l’affectation.</span><span class="sxs-lookup"><span data-stu-id="4c152-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="4c152-113">Mais vous pouvez afficher toutes les affectations d’accès d’un groupe ou d’un utilisateur donné en un seul et même endroit.</span><span class="sxs-lookup"><span data-stu-id="4c152-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="4c152-114">Vous pouvez avoir jusqu’à 2000 attributions de rôles dans chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c152-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="4c152-115">Pour en savoir plus, consultez [Utiliser les affectations de rôle pour gérer l’accès à vos ressources d’abonnement Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4c152-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="4c152-116">Afficher les affectations d’accès</span><span class="sxs-lookup"><span data-stu-id="4c152-116">View access assignments</span></span>
<span data-ttu-id="4c152-117">Pour rechercher les affectations d’accès d’un utilisateur ou d’un groupe en particulier, commencez dans Azure Active Directory sur le [Portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c152-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="4c152-118">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c152-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="4c152-119">Si cette option n’est pas visible dans votre liste de navigation, sélectionnez **Plus de services**, puis faites défiler vers le bas jusqu’à **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c152-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="4c152-120">Sélectionnez **Utilisateurs et groupes**, puis **Tous les utilisateurs** ou **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="4c152-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="4c152-121">Pour cet exemple, nous nous concentrons sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4c152-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="4c152-122">![Gérer les utilisateurs et les groupes dans Azure Active Directory - capture d’écran](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="4c152-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="4c152-123">Recherchez l’utilisateur par nom ou par nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4c152-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="4c152-124">Sélectionnez **Ressources Azure** sur le panneau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4c152-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="4c152-125">Toutes les affectations d’accès de cet utilisateur s’affichent.</span><span class="sxs-lookup"><span data-stu-id="4c152-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="4c152-126">Autorisations de lecture pour afficher les affectations</span><span class="sxs-lookup"><span data-stu-id="4c152-126">Read permissions to view assignments</span></span>
<span data-ttu-id="4c152-127">Cette page affiche uniquement les affectations d’accès que vous êtes autorisé à lire.</span><span class="sxs-lookup"><span data-stu-id="4c152-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="4c152-128">Par exemple, vous avez un accès en lecture à l’abonnement A et vous allez sur le panneau des ressources Azure pour consulter les affectations d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4c152-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="4c152-129">Vous pouvez voir ses affectations d’accès pour l’abonnement A, mais vous ne pouvez pas voir qu’il a également des affectations d’accès dans l’abonnement B.</span><span class="sxs-lookup"><span data-stu-id="4c152-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="4c152-130">Supprimer des affectations d’accès</span><span class="sxs-lookup"><span data-stu-id="4c152-130">Delete access assignments</span></span>
<span data-ttu-id="4c152-131">Sur ce panneau, vous pouvez supprimer les affectations d’accès affectées directement à un utilisateur ou un groupe.</span><span class="sxs-lookup"><span data-stu-id="4c152-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="4c152-132">Si l’affectation d’accès a été héritée d’un groupe parent, vous devez accéder à la ressource ou l’abonnement et y gérer l’affectation.</span><span class="sxs-lookup"><span data-stu-id="4c152-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="4c152-133">Dans la liste de toutes les affectations d’accès d’un utilisateur ou d’un groupe, sélectionnez celle que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="4c152-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="4c152-134">Sélectionnez **Supprimer**, puis **Oui** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="4c152-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="4c152-135">![Supprimer l’affectation de l’accès - capture d’écran](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="4c152-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c152-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c152-136">Next steps</span></span>

* <span data-ttu-id="4c152-137">Familiarisez-vous avec le contrôle d’accès en fonction du rôle afin [d’Utiliser les affectations de rôle pour gérer l’accès à vos ressources d’abonnement Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4c152-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="4c152-138">Consultez les [rôles RBAC intégrés](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="4c152-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

