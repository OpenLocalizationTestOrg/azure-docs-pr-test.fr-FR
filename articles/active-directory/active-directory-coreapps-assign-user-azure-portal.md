---
title: "Affecter un utilisateur ou un groupe à une application d’entreprise dans Azure Active Directory | Microsoft Docs"
description: "Comment sélectionner une application d’entreprise pour affecter un utilisateur ou un groupe dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="1eef9-103">Affecter un utilisateur ou un groupe à une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eef9-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="1eef9-104">Il est facile d’affecter un utilisateur ou un groupe à vos applications d’entreprise dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1eef9-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1eef9-105">Vous devez disposer des autorisations nécessaires pour gérer l’application d’entreprise, et vous devez être l’administrateur général du répertoire.</span><span class="sxs-lookup"><span data-stu-id="1eef9-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="1eef9-106">Comment attribuer l’accès à une application d’entreprise à un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="1eef9-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="1eef9-107">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="1eef9-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1eef9-108">Sélectionnez **Plus de services**, entrez Azure Active Directory dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="1eef9-109">Dans le panneau **Azure Active Directory - *Nom_répertoire*** (autrement dit, le panneau Azure AD correspondant au répertoire que vous gérez), sélectionnez **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="1eef9-111">Dans le panneau **Applications d’entreprise**, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="1eef9-112">Vous verrez une liste des applications que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="1eef9-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="1eef9-113">Sur le panneau **Applications d’entreprise - Toutes les applications** , sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="1eef9-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="1eef9-114">Dans le panneau ***NomApplication*** (autrement dit, le panneau avec le nom de l’application sélectionnée dans le titre), sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Sélection de la commande Toutes les applications](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="1eef9-116">Dans le panneau ***NomApplication*** **- Affectation d’utilisateurs et de groupes**, sélectionnez la commande **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="1eef9-117">Dans le panneau **Ajouter une affectation**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Affecter un utilisateur ou un groupe à l’application](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="1eef9-119">Dans le panneau **Utilisateurs et groupes**, sélectionnez un ou plusieurs utilisateurs ou groupes dans la liste, puis sélectionnez le bouton **Sélectionner** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="1eef9-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="1eef9-120">Dans le panneau **Ajouter une affectation**, sélectionnez **Rôle**.</span><span class="sxs-lookup"><span data-stu-id="1eef9-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="1eef9-121">Puis, dans le panneau **Sélectionner un rôle**, choisissez un rôle à appliquer aux utilisateurs ou groupes sélectionnés, puis cliquez sur le bouton **OK** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="1eef9-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="1eef9-122">Dans le panneau **Ajouter une affectation**, sélectionnez le bouton **Affecter** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="1eef9-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="1eef9-123">Les utilisateurs ou les groupes auront les autorisations définies par le rôle sélectionné pour cette application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="1eef9-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eef9-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1eef9-124">Next steps</span></span>
* [<span data-ttu-id="1eef9-125">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="1eef9-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="1eef9-126">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eef9-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="1eef9-127">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="1eef9-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="1eef9-128">Modifier le nom ou le logo d’une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eef9-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
