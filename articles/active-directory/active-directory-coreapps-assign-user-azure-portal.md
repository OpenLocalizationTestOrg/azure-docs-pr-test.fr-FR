---
title: "aaaAssign une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory | Documents Microsoft"
description: "Comment tooselect un tooassign d’application d’entreprise un tooit utilisateur ou un groupe dans Azure Active Directory"
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
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="e3f92-103">Affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3f92-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="e3f92-104">Il est facile tooassign un utilisateur ou un groupe tooyour entreprise dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3f92-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e3f92-105">Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="e3f92-106">Comment attribuer des applications d’entreprise tooan utilisateur accès ?</span><span class="sxs-lookup"><span data-stu-id="e3f92-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="e3f92-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e3f92-108">Sélectionnez **davantage de services**, entrez Azure Active Directory dans la zone de texte hello et sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="e3f92-109">Sur hello **Azure Active Directory - *nom_répertoire***  blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="e3f92-111">Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="e3f92-112">Vous verrez une liste d’applications hello que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="e3f92-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="e3f92-113">Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="e3f92-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="e3f92-114">Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![En sélectionnant hello toutes les commandes d’applications](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="e3f92-116">Sur hello ***appname*** **-utilisateur et l’affectation du groupe** panneau, sélectionnez hello **ajouter** commande.</span><span class="sxs-lookup"><span data-stu-id="e3f92-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="e3f92-117">Sur hello **ajouter l’affectation** panneau, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Affecter une application toohello utilisateur ou un groupe](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="e3f92-119">Sur hello **utilisateurs et groupes** panneau, sélectionnez un ou plusieurs utilisateurs ou les groupes à partir de hello liste et sélectionnez hello **sélectionnez** bouton bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="e3f92-120">Sur hello **ajouter l’affectation** panneau, sélectionnez **rôle**.</span><span class="sxs-lookup"><span data-stu-id="e3f92-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="e3f92-121">Ensuite, sous hello **sélectionner un rôle** panneau, sélectionnez un toohello tooapply de rôle sélectionné d’utilisateurs ou des groupes, puis sélectionnez hello **OK** bouton bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="e3f92-122">Sur hello **ajouter l’affectation** panneau, sélectionnez hello **affecter** bouton bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="e3f92-123">Hello affecté les utilisateurs ou groupes ont les autorisations hello définies par le rôle sélectionné de hello pour cette application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="e3f92-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3f92-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3f92-124">Next steps</span></span>
* [<span data-ttu-id="e3f92-125">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="e3f92-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e3f92-126">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3f92-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="e3f92-127">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="e3f92-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="e3f92-128">Modifier le nom hello ou un logo d’une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="e3f92-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
