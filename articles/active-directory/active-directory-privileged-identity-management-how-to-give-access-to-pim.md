---
title: "Guide pratique pour donner accès à Privileged Identity Management - Azure | Microsoft Docs"
description: "Découvrez comment ajouter des rôles à des utilisateurs avec l’extension Azure Active Directory Privileged Identity Management pour qu’ils puissent gérer PIM."
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
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="08adb-103">Donner accès à la gestion d’Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="08adb-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="08adb-104">L’administrateur global qui active Azure AD Privileged Identity Management (PIM) pour une organisation obtient automatiquement les affectations de rôles et l’accès à PIM.</span><span class="sxs-lookup"><span data-stu-id="08adb-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="08adb-105">Aucune autre personne ne dispose d’un accès en écriture par défaut, y compris les autres administrateurs généraux.</span><span class="sxs-lookup"><span data-stu-id="08adb-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="08adb-106">Les autres administrateurs généraux, administrateurs de sécurité et les lecteurs de sécurité ont un accès en lecture seule à Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="08adb-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="08adb-107">Pour donner accès à PIM, le premier utilisateur peut affecter les autres au rôle **Administrateur de rôle privilégié** .</span><span class="sxs-lookup"><span data-stu-id="08adb-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="08adb-108">Cette affectation doit être effectuée depuis PIM proprement dit et ne peut pas être modifiée via PowerShell ou d’autres portails.</span><span class="sxs-lookup"><span data-stu-id="08adb-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="08adb-109">La gestion d’Azure AD PIM requiert l’authentification Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="08adb-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="08adb-110">Les comptes Microsoft ne pouvant pas s’inscrire pour l’authentification Azure MFA, un utilisateur qui se connecte avec un compte Microsoft ne peut pas accéder à Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="08adb-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="08adb-111">Vérifiez qu’il y a toujours au moins deux utilisateurs dans un rôle d’administrateur de rôle privilégié, au cas où un utilisateur serait verrouillé ou son compte supprimé.</span><span class="sxs-lookup"><span data-stu-id="08adb-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="08adb-112">Donner accès à un autre utilisateur pour gérer PIM</span><span class="sxs-lookup"><span data-stu-id="08adb-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="08adb-113">Connectez-vous au [portail Azure](https://portal.azure.com/) et sélectionnez l’application **Azure AD Privileged Identity Management** sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="08adb-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="08adb-114">Sélectionnez **Gérer les rôles privilégiés** > **Administrateur de rôle privilégié** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="08adb-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Ajout d’administrateur de rôle privilégié - capture d’écran][1]
3. <span data-ttu-id="08adb-116">Sur le panneau Ajouter les utilisateurs gérés, l’étape 1 est déjà terminée.</span><span class="sxs-lookup"><span data-stu-id="08adb-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="08adb-117">Sélectionnez l’étape 2, **Sélectionner les utilisateurs** et recherchez l’utilisateur que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="08adb-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Sélection des utilisateurs - capture d’écran][2]
4. <span data-ttu-id="08adb-119">Sélectionnez l’utilisateur dans les résultats de la recherche, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="08adb-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="08adb-120">Cliquez sur **OK** pour enregistrer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="08adb-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="08adb-121">L’utilisateur que vous avez sélectionné s’affiche dans la liste des administrateurs de rôle privilégié.</span><span class="sxs-lookup"><span data-stu-id="08adb-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="08adb-122">Chaque fois que vous affectez un nouveau rôle à un utilisateur, celui-ci devient automatiquement éligible pour activer le rôle.</span><span class="sxs-lookup"><span data-stu-id="08adb-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="08adb-123">Si vous souhaitez qu’il conserve le rôle, cliquez sur cet utilisateur dans la liste.</span><span class="sxs-lookup"><span data-stu-id="08adb-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="08adb-124">Sélectionnez **Rendre permanent** dans le menu des informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08adb-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="08adb-125">Envoyez à l'utilisateur un lien vers la ressource [Prise en main d'Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="08adb-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="08adb-126">Supprimez les droits d'accès d'un autre utilisateur pour la gestion de PIM</span><span class="sxs-lookup"><span data-stu-id="08adb-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="08adb-127">Avant de supprimer le rôle d’administrateur de rôle privilégié d’un utilisateur, vérifiez toujours que deux utilisateurs y sont toujours affectés.</span><span class="sxs-lookup"><span data-stu-id="08adb-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="08adb-128">Dans le tableau de bord PIM, cliquez sur le rôle **Administrateur de rôle privilégié**.</span><span class="sxs-lookup"><span data-stu-id="08adb-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="08adb-129">La liste des utilisateurs actuels de ce rôle s'affiche.</span><span class="sxs-lookup"><span data-stu-id="08adb-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="08adb-130">Cliquez sur l’utilisateur dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="08adb-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="08adb-131">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="08adb-131">Click on **Remove**.</span></span>  <span data-ttu-id="08adb-132">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="08adb-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="08adb-133">Cliquez sur **Oui** pour supprimer l’utilisateur du rôle.</span><span class="sxs-lookup"><span data-stu-id="08adb-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="08adb-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08adb-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
