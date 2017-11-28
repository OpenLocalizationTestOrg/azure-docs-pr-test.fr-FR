---
title: "aaaManage hello membres d’un groupe dans Azure Active Directory | Documents Microsoft"
description: "Comment tooadd ou supprimer des utilisateurs et des périphériques d’un groupe dans Azure Active Directory"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="d6202-103">Gérer l’appartenance à un groupe des utilisateurs dans votre client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6202-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="d6202-104">Cet article explique comment toomanage hello membres d’un groupe dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6202-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="d6202-105">Comment rechercher des membres hello et les gérer ?</span><span class="sxs-lookup"><span data-stu-id="d6202-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="d6202-106">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="d6202-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="d6202-107">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d6202-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="d6202-109">Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6202-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="d6202-111">Sur hello **utilisateurs et groupes - tous les groupes** panneau, sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="d6202-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="d6202-112">Sur hello **groupe - *groupname***  panneau, sélectionnez **membres**.</span><span class="sxs-lookup"><span data-stu-id="d6202-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Panneau de membres hello ouverture](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="d6202-114">tooadd membres toohello groupe hello **- groupe de membres** panneau, sélectionnez **ajouter des membres**.</span><span class="sxs-lookup"><span data-stu-id="d6202-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Commande Ajouter des membres](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="d6202-116">Sur hello **membres** panneau, sélectionnez une ou plus d’utilisateurs ou périphériques tooadd toohello et sélectionnez hello **sélectionnez** bouton bas hello hello panneau tooadd les toohello groupe.</span><span class="sxs-lookup"><span data-stu-id="d6202-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="d6202-117">Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance.</span><span class="sxs-lookup"><span data-stu-id="d6202-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="d6202-118">Dans cette zone aucun caractère générique n’est accepté.</span><span class="sxs-lookup"><span data-stu-id="d6202-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="d6202-119">tooremove les membres de groupe hello hello **- groupe de membres** panneau, sélectionnez un membre.</span><span class="sxs-lookup"><span data-stu-id="d6202-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="d6202-120">Sur hello ***membername*** panneau, sélectionnez hello **supprimer** de commandes et confirmez votre choix à l’invite de hello.</span><span class="sxs-lookup"><span data-stu-id="d6202-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Commande Supprimer des membres](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="d6202-122">Lorsque vous avez terminé la modification des membres du groupe de hello, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6202-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="d6202-123">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d6202-123">Additional information</span></span>
<span data-ttu-id="d6202-124">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6202-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="d6202-125">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="d6202-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d6202-126">Création d’un nouveau groupe et ajout de membres</span><span class="sxs-lookup"><span data-stu-id="d6202-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="d6202-127">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="d6202-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="d6202-128">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="d6202-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="d6202-129">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="d6202-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
