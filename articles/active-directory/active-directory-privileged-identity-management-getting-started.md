---
title: "Prise en main d’Azure AD Privileged Identity Management | Microsoft Docs"
description: "Découvrez comment gérer des identités privilégiées avec l’application Azure Active Directory Privileged Identity Management dans le portail Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="5b088-103">Commencer à utiliser Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="5b088-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="5b088-104">Avec Azure Active Directory (AD) Privileged Identity Management, vous pouvez gérer, contrôler et surveiller l’accès au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5b088-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="5b088-105">Cette étendue inclut l’accès aux ressources dans Azure AD et d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="5b088-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="5b088-106">Cet article vous indique comment ajouter l'application Azure AD PIM à votre tableau de bord du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b088-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="5b088-107">Ajout de l’application Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="5b088-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="5b088-108">Avant d'utiliser Azure AD Privileged Identity Management, vous devez ajouter l'application à votre tableau de bord du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b088-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="5b088-109">Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur général de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="5b088-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="5b088-110">Si votre organisation possède plusieurs répertoires, sélectionnez votre nom d’utilisateur dans le coin supérieur droit du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b088-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="5b088-111">Sélectionnez l’annuaire dans lequel vous souhaitez utiliser PIM.</span><span class="sxs-lookup"><span data-stu-id="5b088-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="5b088-112">Sélectionnez **Plus de services** et utilisez la zone de texte Filtre pour rechercher **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="5b088-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="5b088-113">Cochez **Épingler au tableau de bord**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5b088-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="5b088-114">L’application Privileged Identity Management s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5b088-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="5b088-115">Si vous êtes la première personne à utiliser Azure AD Privileged Identity Management dans votre annuaire, les rôles **Administrateur de sécurité** et **Administrateur de rôle privilégié** vous sont automatiquement attribués pour cet annuaire.</span><span class="sxs-lookup"><span data-stu-id="5b088-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="5b088-116">Seuls les administrateurs de rôle privilégié peuvent gérer les attributions de rôles d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5b088-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="5b088-117">En outre, vous pouvez choisir d’exécuter [l’Assistant Sécurité.](active-directory-privileged-identity-management-security-wizard.md)</span><span class="sxs-lookup"><span data-stu-id="5b088-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="5b088-118">qui vous guide tout au long du processus de découverte et d’attribution.</span><span class="sxs-lookup"><span data-stu-id="5b088-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="5b088-119">Accédez à vos tâches</span><span class="sxs-lookup"><span data-stu-id="5b088-119">Navigate to your tasks</span></span>
<span data-ttu-id="5b088-120">Une fois Azure AD Privileged Identity Management configuré, le panneau de navigation s’affiche chaque fois que vous ouvrez l’application.</span><span class="sxs-lookup"><span data-stu-id="5b088-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="5b088-121">Utilisez ce panneau pour accomplir vos tâches de gestion des identités.</span><span class="sxs-lookup"><span data-stu-id="5b088-121">Use this blade to accomplish your identity management tasks.</span></span>

![Tâches de niveau supérieur pour PIM - capture d’écran](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="5b088-123">**Mes rôles** vous permet d’accéder à une liste des rôles qui vous sont assignés.</span><span class="sxs-lookup"><span data-stu-id="5b088-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="5b088-124">C’est dans cette section que vous activez tous les rôles auxquels vous êtes éligible.</span><span class="sxs-lookup"><span data-stu-id="5b088-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="5b088-125">**Approuver des demandes (préversion)** affiche la liste des demandes d’activation en attente effectuées par les utilisateurs dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="5b088-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="5b088-126">En savoir plus.</span><span class="sxs-lookup"><span data-stu-id="5b088-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="5b088-127">**En attente de demandes (préversion)** affiche toutes les demandes en attente d’activation.</span><span class="sxs-lookup"><span data-stu-id="5b088-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="5b088-128">**Revoir l’accès** vous permet d’accéder aux révisions d’accès en attente que vous devez effectuer pour vous-même ou pour un tiers.</span><span class="sxs-lookup"><span data-stu-id="5b088-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="5b088-129">**Rôles d'annuaire Azure AD**, situé dans la section 'Gérer' est le tableau de bord utilisé par les administrateurs de rôles privilégiés pour gérer les affectations de rôle, modifier les paramètres d’activation de rôle, réaliser les révisions d’accès et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="5b088-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="5b088-130">Les options de ce tableau de bord sont désactivées pour toutes les personnes qui ne sont pas des administrateurs de rôle privilégié.</span><span class="sxs-lookup"><span data-stu-id="5b088-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b088-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b088-131">Next steps</span></span>
<span data-ttu-id="5b088-132">La [vue d’ensemble Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) inclut plus de détails sur la manière de gérer un accès administrateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5b088-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
