---
title: "Modifier le nom ou le logo d’une application d’entreprise dans Azure Active Directory | Microsoft Docs"
description: "Comment modifier le nom ou le logo d’une application d’entreprise personnalisée dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="d1ff8-103">Modifier le nom ou le logo d’une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1ff8-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="d1ff8-104">Il est facile de modifier le nom ou le logo d’une application d’entreprise personnalisée dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1ff8-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d1ff8-105">Vous devez disposer des autorisations appropriées pour effectuer ces modifications, et vous devez être le créateur de l’application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="d1ff8-106">Comment modifier le nom ou le logo d’une application d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="d1ff8-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="d1ff8-107">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d1ff8-108">Sélectionnez **Plus de services**, saisissez **Azure Active Directory** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="d1ff8-109">Dans le panneau **Azure Active Directory - *Nom_répertoire*** (autrement dit, le panneau Azure AD correspondant au répertoire que vous gérez), sélectionnez **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="d1ff8-111">Dans le panneau **Applications d’entreprise**, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="d1ff8-112">Vous verrez une liste des applications que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="d1ff8-113">Sur le panneau **Applications d’entreprise - Toutes les applications** , sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="d1ff8-114">Dans le panneau ***NomApplication*** (autrement dit, le panneau avec le nom de l’application sélectionnée dans le titre), sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Sélection de la commande Propriétés](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="d1ff8-116">Dans le panneau ***nom_application*** **- Propriétés**, accédez à un fichier à utiliser en tant que nouveau logo ou modifiez le nom de l’application, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="d1ff8-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Modification du logo de l’application ou de la commande PropriétésNom](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="d1ff8-118">Sélectionnez la commande **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d1ff8-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1ff8-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1ff8-119">Next steps</span></span>
* [<span data-ttu-id="d1ff8-120">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="d1ff8-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d1ff8-121">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="d1ff8-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="d1ff8-122">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1ff8-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="d1ff8-123">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="d1ff8-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
