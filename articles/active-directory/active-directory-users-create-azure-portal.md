---
title: "Ajout de nouveaux utilisateurs à Azure Active Directory | Microsoft Docs"
description: "Expliquez comment ajouter de nouveaux utilisateurs, ou comment modifier les informations d’un utilisateur dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="84362-103">Ajout de nouveaux utilisateurs à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84362-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84362-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="84362-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="84362-105">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="84362-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="84362-106">Cet article explique comment ajouter de nouveaux utilisateurs de votre organisation à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84362-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="84362-107">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="84362-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="84362-108">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="84362-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouverture du panneau Utilisateurs et groupes](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="84362-110">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les utilisateurs**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84362-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Sélection de la commande Ajouter](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="84362-112">Entrez les détails de l’utilisateur, dont son **nom** et son **nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="84362-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="84362-113">La partie du nom de domaine du nom d’utilisateur doit être le nom de domaine initial par défaut, « foo.onmicrosoft.com », ou un nom de domaine vérifié, non fédéré, comme « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="84362-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="84362-114">Copiez ou notez d’une autre façon le mot de passe généré de sorte à pouvoir le fournir à l’utilisateur une fois ce processus terminé.</span><span class="sxs-lookup"><span data-stu-id="84362-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="84362-115">Si vous le souhaitez, vous pouvez ouvrir et remplir les informations dans le panneau **Profil**, le panneau **Groupes** ou le panneau **Rôle de répertoire** pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="84362-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="84362-116">Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="84362-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="84362-117">Dans le panneau **Utilisateur**, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="84362-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="84362-118">Distribuez de manière sécurisée le mot de passe généré au nouvel utilisateur afin qu’il puisse se connecter.</span><span class="sxs-lookup"><span data-stu-id="84362-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="84362-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84362-119">Next steps</span></span>
* [<span data-ttu-id="84362-120">Ajouter un utilisateur externe</span><span class="sxs-lookup"><span data-stu-id="84362-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="84362-121">Réinitialiser le mot de passe d’un utilisateur dans le nouveau portail Azure</span><span class="sxs-lookup"><span data-stu-id="84362-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="84362-122">Modifier les informations de travail d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="84362-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="84362-123">Gérer les profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="84362-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="84362-124">Suppression d’un utilisateur dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="84362-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="84362-125">Affecter un utilisateur à un rôle dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="84362-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
