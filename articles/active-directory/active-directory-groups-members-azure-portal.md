---
title: "Gérer les membres des groupes dans Azure Active Directory | Microsoft Docs"
description: "Comment ajouter ou supprimer des utilisateurs et des appareils dans un groupe d’Azure Active Directory"
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
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="28753-103">Gérer l’appartenance à un groupe des utilisateurs dans votre client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28753-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="28753-104">Cet article explique comment gérer les membres d’un groupe dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28753-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="28753-105">Comment trouver les membres et les gérer ?</span><span class="sxs-lookup"><span data-stu-id="28753-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="28753-106">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="28753-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="28753-107">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="28753-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="28753-109">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="28753-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Ouvrir le panneau de groupes](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="28753-111">Dans le panneau **Utilisateurs et groupes - Tous les groupes** , sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="28753-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="28753-112">Dans le panneau **Groupe - *NomGroupe*** , sélectionnez **Membres**.</span><span class="sxs-lookup"><span data-stu-id="28753-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Ouverture du panneau Membres](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="28753-114">Pour ajouter des membres au groupe, dans le panneau **Groupe - Membres**, sélectionnez **Ajouter des membres**.</span><span class="sxs-lookup"><span data-stu-id="28753-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Commande Ajouter des membres](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="28753-116">Dans le panneau **Membres**, sélectionnez un ou plusieurs utilisateurs ou appareils à ajouter au groupe, puis cliquez sur le **Sélectionner** en bas du panneau pour les ajouter au groupe.</span><span class="sxs-lookup"><span data-stu-id="28753-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="28753-117">La zone **Utilisateur** filtre l’affichage en fonction de la correspondance de votre entrée avec une partie ou l’intégralité d’un nom d’utilisateur ou d’appareil.</span><span class="sxs-lookup"><span data-stu-id="28753-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="28753-118">Dans cette zone aucun caractère générique n’est accepté.</span><span class="sxs-lookup"><span data-stu-id="28753-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="28753-119">Pour supprimer des membres du groupe, dans le panneau **Groupe - Membres** , sélectionnez un membre.</span><span class="sxs-lookup"><span data-stu-id="28753-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="28753-120">Dans le panneau ***NomMembre***, sélectionnez la commande **Supprimer**, puis confirmez votre choix dans l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="28753-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Commande Supprimer des membres](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="28753-122">Lorsque vous avez terminé la modification des membres du groupe, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="28753-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="28753-123">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28753-123">Additional information</span></span>
<span data-ttu-id="28753-124">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28753-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="28753-125">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="28753-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="28753-126">Création d’un nouveau groupe et ajout de membres</span><span class="sxs-lookup"><span data-stu-id="28753-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="28753-127">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="28753-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="28753-128">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="28753-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="28753-129">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="28753-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
