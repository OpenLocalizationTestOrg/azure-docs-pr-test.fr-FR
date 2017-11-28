---
title: "Affectation de rôles d’administrateur à un utilisateur dans Azure Active Directory | Microsoft Docs"
description: "Expliquez comment modifier les informations administratives d’un utilisateur dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="42aba-103">Affecter des rôles d’administrateur à un utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42aba-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="42aba-104">Cet article explique comment affecter un rôle d’administration à un utilisateur dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42aba-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="42aba-105">Pour en savoir plus sur l’ajout d’utilisateurs dans votre organisation, consultez [Ajout de nouveaux utilisateurs à Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="42aba-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="42aba-106">Par défaut, les utilisateurs ajoutés ne reçoivent pas d’autorisations d’administrateur, mais vous pouvez leur attribuer des rôles à tout moment.</span><span class="sxs-lookup"><span data-stu-id="42aba-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="42aba-107">Affecter un rôle à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="42aba-107">Assign a role to a user</span></span>
1. <span data-ttu-id="42aba-108">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="42aba-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="42aba-109">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="42aba-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="42aba-111">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42aba-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Ouverture du panneau Tous les utilisateurs](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="42aba-113">Sur le panneau **Utilisateurs et groupes - Tous les utilisateurs** , sélectionnez un utilisateur dans la liste.</span><span class="sxs-lookup"><span data-stu-id="42aba-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="42aba-114">Dans le panneau de l’utilisateur sélectionné, sélectionnez **Rôle d’annuaire**, puis affectez l’utilisateur à un rôle dans la liste **Rôle d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="42aba-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="42aba-115">Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="42aba-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Affectation d’un utilisateur à un rôle](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="42aba-117">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="42aba-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42aba-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42aba-118">Next steps</span></span>
* [<span data-ttu-id="42aba-119">Ajouter un utilisateur</span><span class="sxs-lookup"><span data-stu-id="42aba-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="42aba-120">Réinitialiser le mot de passe d’un utilisateur dans le nouveau portail Azure</span><span class="sxs-lookup"><span data-stu-id="42aba-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="42aba-121">Modifier les informations de travail d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="42aba-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="42aba-122">Gérer les profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="42aba-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="42aba-123">Suppression d’un utilisateur dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="42aba-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
