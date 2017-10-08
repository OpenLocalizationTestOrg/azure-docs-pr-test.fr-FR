---
title: "aaaHow toostart une vérification de l’accès | Documents Microsoft"
description: "Découvrez comment toocreate un accès à examiner pour les identités privilégiées avec hello application d’Azure Privileged Identity Management."
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="e8c20-103">Comment toostart un accès passez en revue dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e8c20-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e8c20-104">Les attributions de rôles deviennent « obsolètes » lorsque les utilisateurs bénéficient d’un accès privilégié dont ils n’ont plus besoin.</span><span class="sxs-lookup"><span data-stu-id="e8c20-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="e8c20-105">Dans l’ordre tooreduce hello risque est associé à ces attributions de rôles obsolètes, les administrateurs de rôle privilégié doivent examiner régulièrement de rôles hello auxquelles les utilisateurs ont été attribuées.</span><span class="sxs-lookup"><span data-stu-id="e8c20-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="e8c20-106">Ce document décrit les étapes de hello pour démarrer une vérification de l’accès dans Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="e8c20-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="e8c20-107">Démarrage d’une révision d’accès</span><span class="sxs-lookup"><span data-stu-id="e8c20-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="e8c20-108">Si vous n’avez pas ajouté le tableau de bord tooyour hello PIM application Bonjour portail Azure, consultez les étapes de hello dans [prise en main d’Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="e8c20-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="e8c20-109">À partir de la page principale hello PIM application, Voici trois façons toostart une vérification de l’accès :</span><span class="sxs-lookup"><span data-stu-id="e8c20-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="e8c20-110">**Révisions d’accès** > **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="e8c20-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="e8c20-111">**Rôles** > bouton **Révision**</span><span class="sxs-lookup"><span data-stu-id="e8c20-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="e8c20-112">Sélectionnez hello rôle spécifique toobe vérifiés à partir de la liste de rôles hello > **révision** bouton</span><span class="sxs-lookup"><span data-stu-id="e8c20-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="e8c20-113">Lorsque vous cliquez sur hello **Examinez** bouton, hello **démarrer une vérification de l’accès** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e8c20-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="e8c20-114">Dans ce panneau, vous êtes continu tooconfigure hello revue avec un nom de délai d’exécution, choisissez un rôle tooreview et décidez qui effectuera la révision de hello.</span><span class="sxs-lookup"><span data-stu-id="e8c20-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Démarrage d’une vérification d’accès - capture d’écran][1]

### <a name="configure-hello-review"></a><span data-ttu-id="e8c20-116">Configurer la vérification de hello</span><span class="sxs-lookup"><span data-stu-id="e8c20-116">Configure hello review</span></span>
<span data-ttu-id="e8c20-117">Examinez de toocreate d’accès, vous devez tooname et affectez-lui une date de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="e8c20-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Configuration d’une révision - capture d’écran][2]

<span data-ttu-id="e8c20-119">Faites en sorte que longueur hello Hello examiner suffisamment longtemps pour que les utilisateurs toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e8c20-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="e8c20-120">Si vous avez terminé avant la date de fin hello, vous pouvez toujours s’arrêter révision de hello tôt.</span><span class="sxs-lookup"><span data-stu-id="e8c20-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="e8c20-121">Choisissez un rôle tooreview</span><span class="sxs-lookup"><span data-stu-id="e8c20-121">Choose a role tooreview</span></span>
<span data-ttu-id="e8c20-122">Chaque révision se concentre sur un seul rôle.</span><span class="sxs-lookup"><span data-stu-id="e8c20-122">Each review focuses on only one role.</span></span> <span data-ttu-id="e8c20-123">Sauf si vous avez démarré hello vérification de l’accès à partir d’un panneau de rôle spécifique, vous devez maintenant toochoose un rôle.</span><span class="sxs-lookup"><span data-stu-id="e8c20-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="e8c20-124">Accédez trop**consulter l’appartenance au rôle**</span><span class="sxs-lookup"><span data-stu-id="e8c20-124">Navigate too**Review role membership**</span></span>
   
    ![Réviser une appartenance à un rôle - capture d’écran][3]
2. <span data-ttu-id="e8c20-126">Choisir un rôle à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e8c20-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="e8c20-127">Décider qui effectuera la révision de hello</span><span class="sxs-lookup"><span data-stu-id="e8c20-127">Decide who will perform hello review</span></span>
<span data-ttu-id="e8c20-128">Il existe trois options pour effectuer une révision.</span><span class="sxs-lookup"><span data-stu-id="e8c20-128">There are three options for performing a review.</span></span> <span data-ttu-id="e8c20-129">Vous pouvez affecter hello révision toosomeone toocomplete else, vous pouvez le faire vous-même, ou vous pouvez avoir à chaque utilisateur de consulter leur accès.</span><span class="sxs-lookup"><span data-stu-id="e8c20-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="e8c20-130">Accédez trop**sélectionnez relecteurs**</span><span class="sxs-lookup"><span data-stu-id="e8c20-130">Navigate too**Select reviewers**</span></span>
   
    ![Sélection des réviseurs - capture d’écran][4]
2. <span data-ttu-id="e8c20-132">Choisissez une des options de hello :</span><span class="sxs-lookup"><span data-stu-id="e8c20-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="e8c20-133">**Sélectionnez le réviseur**: utilisez cette option lorsque vous ne savez pas qui a besoin de l’accès.</span><span class="sxs-lookup"><span data-stu-id="e8c20-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="e8c20-134">Avec cette option, vous pouvez affecter un propriétaire de la ressource hello révision tooa ou toocomplete de gestionnaire de groupe.</span><span class="sxs-lookup"><span data-stu-id="e8c20-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="e8c20-135">**Me**: utile si vous souhaitez toopreview comment access passe en revue le travail, ou vous souhaitez tooreview pour le compte de personnes qui ne peuvent pas.</span><span class="sxs-lookup"><span data-stu-id="e8c20-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="e8c20-136">**Les membres d’examiner eux-mêmes**: utilisez cette revue d’utilisateurs option toohave hello leurs attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="e8c20-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="e8c20-137">Démarrer hello révision</span><span class="sxs-lookup"><span data-stu-id="e8c20-137">Start hello review</span></span>
<span data-ttu-id="e8c20-138">Enfin, vous avez toorequire d’option hello les utilisateurs à fournir une raison si elles approuver leur accès.</span><span class="sxs-lookup"><span data-stu-id="e8c20-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="e8c20-139">Ajouter une description de la révision de hello si vous le souhaitez, puis sélectionnez **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="e8c20-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="e8c20-140">Assurez-vous que vous informer vos utilisateurs qu’il existe une vérification de l’accès en attente pour les et les afficher [façon tooperform examiner un accès](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="e8c20-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="e8c20-141">Gérer la vérification de l’accès hello</span><span class="sxs-lookup"><span data-stu-id="e8c20-141">Manage hello access review</span></span>
<span data-ttu-id="e8c20-142">Vous pouvez suivre la progression de hello à mesure que les réviseurs hello effectuent leurs révisions Bonjour du tableau de bord Azure AD PIM, Bonjour accès examine la section.</span><span class="sxs-lookup"><span data-stu-id="e8c20-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="e8c20-143">Aucun droit d’accès ne sera modifiée dans le répertoire hello jusqu'à ce que [se termine de révision de hello](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="e8c20-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="e8c20-144">Jusqu'à ce que la période de révision hello est terminée, vous pouvez rappeler les utilisateurs toocomplete leur révision ou stop hello révision tôt contre tout accès hello section révision.</span><span class="sxs-lookup"><span data-stu-id="e8c20-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="e8c20-145">Sommaire PIM</span><span class="sxs-lookup"><span data-stu-id="e8c20-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
