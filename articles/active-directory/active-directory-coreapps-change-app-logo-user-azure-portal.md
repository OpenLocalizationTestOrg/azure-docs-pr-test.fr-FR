---
title: "aaaChange hello nom ou un logo d’une application d’entreprise dans Active Directory de Azure | Documents Microsoft"
description: "Comment toochange hello nom ou un logo pour une application d’entreprise personnalisés dans Azure Active Directory"
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
ms.openlocfilehash: b660e1f0f6c7ffd626e17e2e3399e7169f6e8bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="69203-103">Modifier le nom hello ou un logo d’une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69203-103">Change hello name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="69203-104">Il est le nom de hello toochange simple ou un logo pour une application d’entreprise personnalisés dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69203-104">It's easy toochange hello name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="69203-105">Vous devez disposer de toomake des autorisations appropriées hello de ces modifications, et vous devez être créateur hello d’application personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="69203-105">You must have hello appropriate permissions toomake these changes, and you must be hello creator of hello custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="69203-106">Comment modifier le nom ou le logo d’une application d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="69203-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="69203-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="69203-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="69203-108">Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="69203-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="69203-109">Sur hello **Azure Active Directory - *nom_répertoire***  blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="69203-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="69203-111">Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="69203-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="69203-112">Vous verrez une liste d’applications hello que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="69203-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="69203-113">Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="69203-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="69203-114">Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="69203-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![En sélectionnant la commande de propriétés hello](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="69203-116">Sur hello ***appname*** **-propriétés** panneau, recherchez un toouse de fichier en tant que nouveau logo ou modifier le nom de l’application hello, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="69203-116">On hello ***appname*** **- Properties** blade, browse for a file toouse as a new logo, or edit hello app name, or both.</span></span>

    ![Modification de commande de logo ou nameproperties application hello](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="69203-118">Sélectionnez hello **enregistrer** commande.</span><span class="sxs-lookup"><span data-stu-id="69203-118">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69203-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69203-119">Next steps</span></span>
* [<span data-ttu-id="69203-120">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="69203-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="69203-121">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="69203-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="69203-122">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69203-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="69203-123">Désactiver les connexions utilisateur pour une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="69203-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
