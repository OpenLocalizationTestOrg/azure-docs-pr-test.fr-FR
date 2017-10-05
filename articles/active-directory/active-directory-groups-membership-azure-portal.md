---
title: "Gérer les groupes dont votre groupe fait partie dans Azure Active Directory | Microsoft Docs"
description: "Les groupes peuvent contenir d’autres groupes dans Azure Active Directory. Voici comment gérer ces adhésions."
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="e9e36-104">Gérer les groupes auxquels un groupe appartient dans votre client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9e36-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="e9e36-105">Les groupes peuvent contenir d’autres groupes dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9e36-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="e9e36-106">Voici comment gérer ces adhésions.</span><span class="sxs-lookup"><span data-stu-id="e9e36-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="e9e36-107">Comment trouver les groupes dont mon groupe est membre ?</span><span class="sxs-lookup"><span data-stu-id="e9e36-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="e9e36-108">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="e9e36-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e9e36-109">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="e9e36-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="e9e36-111">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="e9e36-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Ouvrir le panneau de groupes](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="e9e36-113">Dans le panneau **Utilisateurs et groupes - Tous les groupes** , sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="e9e36-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="e9e36-114">Dans le panneau **Groupe - *Nom_groupe*** , sélectionnez **Appartenances aux groupes**.</span><span class="sxs-lookup"><span data-stu-id="e9e36-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Ouverture du panneau Appartenances aux groupes](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="e9e36-116">Pour ajouter votre groupe en tant que membre d’un autre groupe, dans le panneau **Groupe - Appartenances aux groupes**, sélectionnez la commande **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e9e36-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="e9e36-117">Sélectionnez un groupe à partir du panneau **Sélectionner un groupe**, puis cliquez sur le bouton **Sélectionner** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="e9e36-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="e9e36-118">Vous pouvez ajouter votre groupe à un seul groupe à la fois.</span><span class="sxs-lookup"><span data-stu-id="e9e36-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="e9e36-119">La zone **Utilisateur** filtre l’affichage en fonction de la correspondance de votre entrée avec une partie ou l’intégralité d’un nom d’utilisateur ou d’appareil.</span><span class="sxs-lookup"><span data-stu-id="e9e36-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="e9e36-120">Dans cette zone aucun caractère générique n’est accepté.</span><span class="sxs-lookup"><span data-stu-id="e9e36-120">No wildcard characters are accepted in that box.</span></span>

   ![Ajouter une appartenance à un groupe](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="e9e36-122">Pour supprimer votre groupe en tant que membre d’un autre groupe, dans le panneau **Groupe - Appartenances aux groupes** , sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="e9e36-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="e9e36-123">Dans le panneau ***NomGroupe***, sélectionnez la commande **Supprimer**, puis confirmez votre choix dans l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="e9e36-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Commande Supprimer des appartenances](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="e9e36-125">Lorsque vous avez terminé de modifier les appartenances aux groupes de votre groupe, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e9e36-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e9e36-126">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e9e36-126">Additional information</span></span>
<span data-ttu-id="e9e36-127">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9e36-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e9e36-128">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="e9e36-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e9e36-129">Création d’un nouveau groupe et ajout de membres</span><span class="sxs-lookup"><span data-stu-id="e9e36-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="e9e36-130">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="e9e36-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e9e36-131">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="e9e36-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="e9e36-132">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="e9e36-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
