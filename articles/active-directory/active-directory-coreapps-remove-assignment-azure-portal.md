---
title: "Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans Azure Active Directory | Microsoft Docs"
description: "Comment supprimer l’affectation de l’accès à un utilisateur ou à un groupe à une application d’entreprise dans Azure Active Directory"
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
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="8de60-103">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8de60-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="8de60-104">Il est facile de supprimer l’affectation de l’accès à un utilisateur ou un groupe à vos applications d’entreprise dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8de60-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8de60-105">Vous devez disposer des autorisations nécessaires pour gérer l’application d’entreprise, et vous devez être l’administrateur général du répertoire.</span><span class="sxs-lookup"><span data-stu-id="8de60-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="8de60-106">Comment supprimer une affectation d’utilisateur ou de groupe ?</span><span class="sxs-lookup"><span data-stu-id="8de60-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="8de60-107">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="8de60-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8de60-108">Sélectionnez **Plus de services**, saisissez **Azure Active Directory** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="8de60-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="8de60-109">Dans le panneau **Azure Active Directory - *Nom_répertoire*** (autrement dit, le panneau Azure AD correspondant au répertoire que vous gérez), sélectionnez **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8de60-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="8de60-111">Dans le panneau **Applications d’entreprise**, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8de60-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="8de60-112">Vous verrez une liste des applications que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="8de60-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="8de60-113">Sur le panneau **Applications d’entreprise - Toutes les applications** , sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="8de60-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="8de60-114">Dans le panneau ***NomApplication*** (autrement dit, le panneau avec le nom de l’application sélectionnée dans le titre), sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8de60-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Sélection d’utilisateurs ou groupes](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="8de60-116">Sur le panneau ***NomApplication***  **- Affectation d’utilisateur et de groupe**, sélectionnez un ou plusieurs utilisateurs ou groupes, puis sélectionnez la commande **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="8de60-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="8de60-117">Confirmez votre choix dans l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="8de60-117">Confirm your decision at the prompt.</span></span>

    ![Sélection de la commande Supprimer](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="8de60-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8de60-119">Next steps</span></span>
* [<span data-ttu-id="8de60-120">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="8de60-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="8de60-121">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8de60-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="8de60-122">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8de60-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="8de60-123">Modifier le nom ou le logo d’une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8de60-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
