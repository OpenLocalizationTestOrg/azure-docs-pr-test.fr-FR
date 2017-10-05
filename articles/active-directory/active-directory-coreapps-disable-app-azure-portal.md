---
title: "Désactiver les connexions utilisateur pour une application d’entreprise dans Azure Active Directory | Microsoft Docs"
description: "Comment désactiver une application d’entreprise afin qu’aucun utilisateur ne puisse s’y connecter dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="1387d-103">Désactiver les connexions utilisateur pour une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1387d-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="1387d-104">Il est facile de désactiver une application d’entreprise afin qu’aucun utilisateur ne puisse s’y connecter dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1387d-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1387d-105">Vous devez disposer des autorisations nécessaires pour gérer l’application d’entreprise, et vous devez être l’administrateur général du répertoire.</span><span class="sxs-lookup"><span data-stu-id="1387d-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="1387d-106">Comment désactiver les connexions des utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="1387d-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="1387d-107">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="1387d-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1387d-108">Sélectionnez **Plus de services**, saisissez **Azure Active Directory** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="1387d-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="1387d-109">Dans le panneau **Azure Active Directory** -  ***NomRépertoire*** (autrement dit, le panneau Azure AD du répertoire que vous gérez), sélectionnez **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1387d-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="1387d-111">Dans le panneau **Applications d’entreprise**, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1387d-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="1387d-112">Vous verrez une liste des applications que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="1387d-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="1387d-113">Sur le panneau **Applications d’entreprise - Toutes les applications** , sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="1387d-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="1387d-114">Dans le panneau ***NomApplication*** (autrement dit, le panneau avec le nom de l’application sélectionnée dans le titre), sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="1387d-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Sélection de la commande Toutes les applications](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="1387d-116">Dans le panneau ***NomApplication*** - **Propriétés**, sélectionnez **Non** pour **Activé pour que les utilisateurs se connectent ?**.</span><span class="sxs-lookup"><span data-stu-id="1387d-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="1387d-117">Sélectionnez la commande **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1387d-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1387d-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1387d-118">Next steps</span></span>
* [<span data-ttu-id="1387d-119">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="1387d-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="1387d-120">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="1387d-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="1387d-121">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1387d-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="1387d-122">Modifier le nom ou le logo d’une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1387d-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
