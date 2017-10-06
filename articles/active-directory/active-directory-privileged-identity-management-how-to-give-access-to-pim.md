---
title: "aaaHow toogive accès tooPrivileged Identity Management - Azure | Documents Microsoft"
description: "Découvrez comment toousers de rôles tooadd avec hello extension d’Azure Active Directory Privileged Identity Management afin de pouvoir gérer PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="fdb70-103">En donnant accès toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="fdb70-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="fdb70-104">administrateur général de Hello qui permet à Azure AD Privileged Identity Management (PIM) pour une organisation automatiquement les attributions de rôle et accédez aux tooPIM.</span><span class="sxs-lookup"><span data-stu-id="fdb70-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="fdb70-105">Aucune autre personne ne dispose d’un accès en écriture par défaut, y compris les autres administrateurs généraux.</span><span class="sxs-lookup"><span data-stu-id="fdb70-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="fdb70-106">Autres administrateurs globaux, les administrateurs de sécurité et les lecteurs de sécurité ont accès en lecture seule tooAzure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="fdb70-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="fdb70-107">toogive accès tooPIM, hello premier utilisateur peut assigner à d’autres toohello **administrateur du rôle privilégié** rôle.</span><span class="sxs-lookup"><span data-stu-id="fdb70-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="fdb70-108">Cette affectation doit être effectuée depuis PIM proprement dit et ne peut pas être modifiée via PowerShell ou d’autres portails.</span><span class="sxs-lookup"><span data-stu-id="fdb70-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb70-109">La gestion d’Azure AD PIM requiert l’authentification Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="fdb70-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="fdb70-110">Les comptes Microsoft ne pouvant pas s’inscrire pour l’authentification Azure MFA, un utilisateur qui se connecte avec un compte Microsoft ne peut pas accéder à Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="fdb70-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="fdb70-111">Vérifiez qu’il y a toujours au moins deux utilisateurs dans un rôle d’administrateur de rôle privilégié, au cas où un utilisateur serait verrouillé ou son compte supprimé.</span><span class="sxs-lookup"><span data-stu-id="fdb70-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="fdb70-112">Permettre à un autre utilisateur de l’accès toomanage PIM</span><span class="sxs-lookup"><span data-stu-id="fdb70-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="fdb70-113">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello **Azure AD Privileged Identity Management** application sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="fdb70-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="fdb70-114">Sélectionnez **Gérer les rôles privilégiés** > **Administrateur de rôle privilégié** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fdb70-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Ajout d’administrateur de rôle privilégié - capture d’écran][1]
3. <span data-ttu-id="fdb70-116">Sur le panneau de hello ajouter les utilisateurs gérés, l’étape 1 est déjà terminée.</span><span class="sxs-lookup"><span data-stu-id="fdb70-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="fdb70-117">L’étape 2, sélectionnez **sélectionnez utilisateurs** et de recherche pour l’utilisateur de hello souhaité tooadd.</span><span class="sxs-lookup"><span data-stu-id="fdb70-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Sélection des utilisateurs - capture d’écran][2]
4. <span data-ttu-id="fdb70-119">Sélectionnez un utilisateur de hello hello résultats de recherche, puis cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="fdb70-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="fdb70-120">Cliquez sur **OK** toosave votre sélection.</span><span class="sxs-lookup"><span data-stu-id="fdb70-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="fdb70-121">utilisateur Hello que vous avez sélectionné s’affiche dans la liste hello des administrateurs de rôle privilégié.</span><span class="sxs-lookup"><span data-stu-id="fdb70-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="fdb70-122">Chaque fois que vous affectez une nouvelle toosomeone de rôle, ils sont automatiquement configurés en tant que rôle de hello tooactivate éligible.</span><span class="sxs-lookup"><span data-stu-id="fdb70-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="fdb70-123">Si vous souhaitez toomake permanentes dans le rôle de hello, cliquez sur utilisateur hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="fdb70-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="fdb70-124">Sélectionnez **rendre l’autorisation** dans le menu d’informations utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="fdb70-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="fdb70-125">Envoyer à un lien utilisateur de hello trop[prise en main d’Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fdb70-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="fdb70-126">Supprimez les droits d'accès d'un autre utilisateur pour la gestion de PIM</span><span class="sxs-lookup"><span data-stu-id="fdb70-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="fdb70-127">Avant de supprimer un utilisateur du rôle d’administrateur hello rôle privilégié, assurez-vous toujours qu’il y aura toujours deux utilisateurs affectés tooit.</span><span class="sxs-lookup"><span data-stu-id="fdb70-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="fdb70-128">Dans le tableau de bord PIM hello, cliquez sur le rôle de hello **administrateur du rôle privilégié**.</span><span class="sxs-lookup"><span data-stu-id="fdb70-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="fdb70-129">liste Hello d’utilisateurs actuellement dans ce rôle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fdb70-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="fdb70-130">Cliquez sur l’utilisateur hello dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="fdb70-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="fdb70-131">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fdb70-131">Click on **Remove**.</span></span>  <span data-ttu-id="fdb70-132">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fdb70-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="fdb70-133">Cliquez sur **Oui** utilisateur de hello tooremove du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="fdb70-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="fdb70-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fdb70-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
