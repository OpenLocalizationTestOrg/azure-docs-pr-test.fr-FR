---
title: "aaaCreate un groupe d’utilisateurs dans Azure Active Directory | Documents Microsoft"
description: Comment toocreate un groupe dans Azure Active Directory et ajouter le groupe de membres toohello
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="50b3a-103">Créer un groupe et ajouter des membres dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50b3a-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50b3a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="50b3a-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="50b3a-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="50b3a-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="50b3a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50b3a-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="50b3a-107">Cet article explique comment toocreate et remplir un nouveau groupe dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50b3a-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="50b3a-108">Utilisez une tâche de gestion de tooperform groupe tels que l’attribution des licences ou autorisations nombre tooa d’utilisateurs ou d’appareils à la fois.</span><span class="sxs-lookup"><span data-stu-id="50b3a-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="50b3a-109">Comment créer un groupe ?</span><span class="sxs-lookup"><span data-stu-id="50b3a-109">How do I create a group?</span></span>
1. <span data-ttu-id="50b3a-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="50b3a-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="50b3a-111">Sélectionnez **davantage de services**, entrez **utilisateur et les groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="50b3a-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="50b3a-113">Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="50b3a-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="50b3a-115">Sur hello **utilisateurs et groupes - tous les groupes de** panneau, sélectionnez hello **ajouter** commande.</span><span class="sxs-lookup"><span data-stu-id="50b3a-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![En sélectionnant Ajouter une commande hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="50b3a-117">Sur hello **groupe** panneau, ajouter un nom et une description pour le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="50b3a-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="50b3a-118">tooselect membres tooadd toohello groupe, sélectionnez **affecté** Bonjour **type d’appartenance** zone, puis sélectionnez **membres**.</span><span class="sxs-lookup"><span data-stu-id="50b3a-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="50b3a-119">Pour plus d’informations sur la façon dont toomanage hello dynamiquement l’appartenance d’un groupe, consultez [à l’aide des attributs toocreate des règles pour l’appartenance au groupe avancées](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50b3a-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Sélection de membres tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="50b3a-121">Sur hello **membres** panneau, sélectionnez une ou plus d’utilisateurs ou périphériques tooadd toohello et sélectionnez hello **sélectionnez** bouton bas hello hello panneau tooadd les toohello groupe.</span><span class="sxs-lookup"><span data-stu-id="50b3a-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="50b3a-122">Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance.</span><span class="sxs-lookup"><span data-stu-id="50b3a-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="50b3a-123">Dans cette zone aucun caractère générique n’est accepté.</span><span class="sxs-lookup"><span data-stu-id="50b3a-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="50b3a-124">Lorsque vous avez terminé d’ajouter le groupe de membres toohello, sélectionnez **créer** sur hello **groupe** panneau.</span><span class="sxs-lookup"><span data-stu-id="50b3a-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Confirmation de création du groupe](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="50b3a-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50b3a-126">Next steps</span></span>
<span data-ttu-id="50b3a-127">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50b3a-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="50b3a-128">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="50b3a-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="50b3a-129">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="50b3a-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="50b3a-130">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="50b3a-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="50b3a-131">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="50b3a-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="50b3a-132">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="50b3a-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
