---
title: "aaaRemove une affectation d’utilisateur ou un groupe à partir d’une application d’entreprise dans Active Directory de Azure | Documents Microsoft"
description: "Comment tooremove hello accéder à l’affectation d’un utilisateur ou un groupe à partir d’une application d’entreprise dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="b6cee-103">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6cee-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="b6cee-104">Il est facile tooremove un utilisateur ou un groupe d’être assignée tooone d’accès de vos applications d’entreprise dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6cee-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b6cee-105">Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="b6cee-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="b6cee-106">Comment supprimer une affectation d’utilisateur ou de groupe ?</span><span class="sxs-lookup"><span data-stu-id="b6cee-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="b6cee-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="b6cee-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="b6cee-108">Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="b6cee-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="b6cee-109">Sur hello **Azure Active Directory - *nom_répertoire***  blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b6cee-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="b6cee-111">Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b6cee-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="b6cee-112">Vous verrez une liste d’applications hello que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="b6cee-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="b6cee-113">Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="b6cee-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="b6cee-114">Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b6cee-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Sélection d’utilisateurs ou groupes](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="b6cee-116">Sur hello ***appname*** **-utilisateur et l’affectation du groupe** panneau, sélectionnez une des autres utilisateurs ou groupes, puis hello **supprimer** commande.</span><span class="sxs-lookup"><span data-stu-id="b6cee-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="b6cee-117">Confirmer votre décision à l’invite de hello.</span><span class="sxs-lookup"><span data-stu-id="b6cee-117">Confirm your decision at hello prompt.</span></span>

    ![En sélectionnant la commande de suppression hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="b6cee-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6cee-119">Next steps</span></span>
* [<span data-ttu-id="b6cee-120">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="b6cee-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b6cee-121">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="b6cee-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="b6cee-122">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="b6cee-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="b6cee-123">Modifier le nom hello ou un logo d’une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="b6cee-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
