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
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="24f87-104">Gérer des groupes toowhich qu'un groupe appartient dans votre locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24f87-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="24f87-105">Les groupes peuvent contenir d’autres groupes dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24f87-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="24f87-106">Voici comment toomanage ces appartenances.</span><span class="sxs-lookup"><span data-stu-id="24f87-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="24f87-107">Comment trouver les groupes de hello de que mon groupe est membre ?</span><span class="sxs-lookup"><span data-stu-id="24f87-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="24f87-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="24f87-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="24f87-109">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="24f87-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="24f87-111">Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="24f87-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="24f87-113">Sur hello **utilisateurs et groupes - tous les groupes** panneau, sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="24f87-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="24f87-114">Sur hello **groupe - *groupname***  panneau, sélectionnez **appartenances au groupe**.</span><span class="sxs-lookup"><span data-stu-id="24f87-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Panneau des appartenances au groupe Ouverture hello](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="24f87-116">tooadd votre groupe en tant que membre d’un autre groupe, sur hello **de groupe - appartenances au groupe** panneau, sélectionnez hello **ajouter** commande.</span><span class="sxs-lookup"><span data-stu-id="24f87-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="24f87-117">Sélectionnez un groupe de hello **sélectionner un groupe** panneau, puis sélectionnez hello **sélectionnez** bouton bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="24f87-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="24f87-118">Vous pouvez ajouter votre groupe d’un groupe tooonly à la fois.</span><span class="sxs-lookup"><span data-stu-id="24f87-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="24f87-119">Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance.</span><span class="sxs-lookup"><span data-stu-id="24f87-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="24f87-120">Dans cette zone aucun caractère générique n’est accepté.</span><span class="sxs-lookup"><span data-stu-id="24f87-120">No wildcard characters are accepted in that box.</span></span>

   ![Ajouter une appartenance à un groupe](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="24f87-122">tooremove votre groupe en tant que membre d’un autre groupe, sur hello **de groupe - appartenances** panneau, sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="24f87-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="24f87-123">Sur hello ***groupname*** panneau, sélectionnez hello **supprimer** de commandes et confirmez votre choix à l’invite de hello.</span><span class="sxs-lookup"><span data-stu-id="24f87-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Commande Supprimer des appartenances](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="24f87-125">Lorsque vous avez terminé de modifier les appartenances aux groupes de votre groupe, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="24f87-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="24f87-126">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="24f87-126">Additional information</span></span>
<span data-ttu-id="24f87-127">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24f87-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="24f87-128">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="24f87-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="24f87-129">Création d’un nouveau groupe et ajout de membres</span><span class="sxs-lookup"><span data-stu-id="24f87-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="24f87-130">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="24f87-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="24f87-131">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="24f87-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="24f87-132">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="24f87-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
