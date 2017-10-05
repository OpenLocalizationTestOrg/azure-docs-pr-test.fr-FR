---
title: "Démarrage d’une révision d’accès | Microsoft Docs"
description: "Découvrez comment créer une révision d'accès pour les identités privilégiées avec l’application Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="21ff0-103">Comment démarrer une révision de l’accès dans Azure AD Privileged Identity Management ?</span><span class="sxs-lookup"><span data-stu-id="21ff0-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="21ff0-104">Les attributions de rôles deviennent « obsolètes » lorsque les utilisateurs bénéficient d’un accès privilégié dont ils n’ont plus besoin.</span><span class="sxs-lookup"><span data-stu-id="21ff0-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="21ff0-105">Pour réduire les risques associés à ces affectations de rôles « obsolètes », les administrateurs de rôle privilégié doivent régulièrement réviser les rôles qui ont été donnés aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="21ff0-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="21ff0-106">Ce document décrit les étapes de démarrage d’une révision d’accès dans Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="21ff0-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="21ff0-107">Démarrage d’une révision d’accès</span><span class="sxs-lookup"><span data-stu-id="21ff0-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="21ff0-108">Si vous n’avez pas ajouté l’application PIM à votre tableau de bord dans le Portail Azure, consultez les étapes dans [Prise en main d’Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="21ff0-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="21ff0-109">Dans la page principale de l’application PIM, vous pouvez démarrer une révision d’accès de trois façons différentes :</span><span class="sxs-lookup"><span data-stu-id="21ff0-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="21ff0-110">**Révisions d’accès** > **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="21ff0-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="21ff0-111">**Rôles** > bouton **Révision**</span><span class="sxs-lookup"><span data-stu-id="21ff0-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="21ff0-112">Sélectionnez le rôle spécifique à réviser dans la liste des rôles > bouton **Révision**.</span><span class="sxs-lookup"><span data-stu-id="21ff0-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="21ff0-113">Lorsque vous cliquez sur le bouton **Révision**, le panneau **Démarrer une vérification d’accès** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="21ff0-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="21ff0-114">Dans ce panneau, vous allez configurer la révision avec un nom et une limite de temps, choisir un rôle à réviser, et nommer la personne qui effectuera la révision.</span><span class="sxs-lookup"><span data-stu-id="21ff0-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Démarrage d’une vérification d’accès - capture d’écran][1]

### <a name="configure-the-review"></a><span data-ttu-id="21ff0-116">Configuration de la révision</span><span class="sxs-lookup"><span data-stu-id="21ff0-116">Configure the review</span></span>
<span data-ttu-id="21ff0-117">Pour créer une révision d’accès, vous devez la nommer et définir une date de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="21ff0-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Configuration d’une révision - capture d’écran][2]

<span data-ttu-id="21ff0-119">Prévoyez une période suffisamment longue pour permettre aux utilisateurs de terminer la révision.</span><span class="sxs-lookup"><span data-stu-id="21ff0-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="21ff0-120">Si vous avez terminé avant la date de fin, vous pouvez toujours arrêter la révision plus tôt.</span><span class="sxs-lookup"><span data-stu-id="21ff0-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="21ff0-121">Sélection d’un rôle à réviser</span><span class="sxs-lookup"><span data-stu-id="21ff0-121">Choose a role to review</span></span>
<span data-ttu-id="21ff0-122">Chaque révision se concentre sur un seul rôle.</span><span class="sxs-lookup"><span data-stu-id="21ff0-122">Each review focuses on only one role.</span></span> <span data-ttu-id="21ff0-123">À moins d’avoir démarré la révision d’accès à partir d’un panneau de rôle spécifique, vous devez maintenant choisir un rôle.</span><span class="sxs-lookup"><span data-stu-id="21ff0-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="21ff0-124">Navigation vers **Réviser une appartenance à un rôle**</span><span class="sxs-lookup"><span data-stu-id="21ff0-124">Navigate to **Review role membership**</span></span>
   
    ![Réviser une appartenance à un rôle - capture d’écran][3]
2. <span data-ttu-id="21ff0-126">Choisissez un rôle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="21ff0-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="21ff0-127">Désignez la personne qui effectuera la révision</span><span class="sxs-lookup"><span data-stu-id="21ff0-127">Decide who will perform the review</span></span>
<span data-ttu-id="21ff0-128">Il existe trois options pour effectuer une révision.</span><span class="sxs-lookup"><span data-stu-id="21ff0-128">There are three options for performing a review.</span></span> <span data-ttu-id="21ff0-129">Vous pouvez affecter la révision à quelqu’un d’autre, vous pouvez la faire vous-même ou vous pouvez demander à chaque utilisateur de réviser son propre accès.</span><span class="sxs-lookup"><span data-stu-id="21ff0-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="21ff0-130">Navigation vers **Sélectionner des réviseurs**</span><span class="sxs-lookup"><span data-stu-id="21ff0-130">Navigate to **Select reviewers**</span></span>
   
    ![Sélection des réviseurs - capture d’écran][4]
2. <span data-ttu-id="21ff0-132">Choisissez l'une des options :</span><span class="sxs-lookup"><span data-stu-id="21ff0-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="21ff0-133">**Sélectionnez le réviseur**: utilisez cette option lorsque vous ne savez pas qui a besoin de l’accès.</span><span class="sxs-lookup"><span data-stu-id="21ff0-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="21ff0-134">Avec cette option, vous pouvez affecter la révision à un propriétaire de ressource ou un responsable de groupe.</span><span class="sxs-lookup"><span data-stu-id="21ff0-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="21ff0-135">**Moi**: utile si vous souhaitez un aperçu du fonctionnement des révisions d’accès ou effectuer une révision à la place de personnes qui ne peuvent pas le faire.</span><span class="sxs-lookup"><span data-stu-id="21ff0-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="21ff0-136">**Auto-révision par les membres du rôle**: utilisez cette option pour demander aux utilisateurs de réviser leurs propres affectations de rôles.</span><span class="sxs-lookup"><span data-stu-id="21ff0-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="21ff0-137">Démarrage d’une révision</span><span class="sxs-lookup"><span data-stu-id="21ff0-137">Start the review</span></span>
<span data-ttu-id="21ff0-138">Enfin, vous pouvez obliger les utilisateurs à indiquer le motif pour lequel ils approuvent leur accès.</span><span class="sxs-lookup"><span data-stu-id="21ff0-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="21ff0-139">Ajoutez une description de la révision si vous le souhaitez, puis sélectionnez **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="21ff0-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="21ff0-140">Assurez-vous d’informer vos utilisateurs qu’une révision d’accès les attend, puis montrez-leur [comment exécuter une révision d’accès](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="21ff0-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="21ff0-141">Gestion de la révision d’accès</span><span class="sxs-lookup"><span data-stu-id="21ff0-141">Manage the access review</span></span>
<span data-ttu-id="21ff0-142">Vous pouvez suivre la progression des révisions des réviseurs dans le tableau de bord Azure AD PIM, dans la section des révisions d'accès.</span><span class="sxs-lookup"><span data-stu-id="21ff0-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="21ff0-143">Aucun droit d’accès ne sera modifié dans le répertoire avant que [la révision ne soit terminée](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="21ff0-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="21ff0-144">Tant que la période de révision n’est pas terminée, vous pouvez rappeler aux utilisateurs d’effectuer leur révision, ou arrêter la révision au début de la section des révisions d’accès.</span><span class="sxs-lookup"><span data-stu-id="21ff0-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="21ff0-145">Sommaire PIM</span><span class="sxs-lookup"><span data-stu-id="21ff0-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
