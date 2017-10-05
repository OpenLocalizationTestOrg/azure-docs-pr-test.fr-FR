---
title: "Flux de travail d’approbation Azure Privileged Identity Management (PIM) | Microsoft Docs"
description: "En savoir plus sur les flux de travail d’approbation dans Privileged Identity Management (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="14a28-103">Approbations (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="14a28-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="14a28-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="14a28-104">Overview</span></span>

<span data-ttu-id="14a28-105">Grâce aux approbations Privileged Identity Management, vous pouvez configurer des rôles afin de demander une approbation d’activation, et choisir un ou plusieurs utilisateurs ou groupes comme approbateurs délégués.</span><span class="sxs-lookup"><span data-stu-id="14a28-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="14a28-106">Poursuivez pour découvrir comment configurer des rôles et sélectionner des approbateurs.</span><span class="sxs-lookup"><span data-stu-id="14a28-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="14a28-107">N’oubliez pas que cette fonctionnalité est en cours de développement et que vous pouvez rencontrer des bugs.</span><span class="sxs-lookup"><span data-stu-id="14a28-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="14a28-108">La fonctionnalité, y compris le texte et les conventions d’affectation de noms, peut être modifiée et ne doit pas être considérée comme finale.</span><span class="sxs-lookup"><span data-stu-id="14a28-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="14a28-109">Terminologie clé</span><span class="sxs-lookup"><span data-stu-id="14a28-109">Key Terminology</span></span>

<span data-ttu-id="14a28-110">*Utilisateur de rôle éligible* : un utilisateur de rôle éligible est un utilisateur au sein de votre organisation affecté à un rôle Azure AD comme éligible (le rôle requiert une activation).</span><span class="sxs-lookup"><span data-stu-id="14a28-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="14a28-111">*Approbateur délégué* : un approbateur délégué est une ou plusieurs personnes ou groupes au sein de votre Azure AD responsables de l’approbation des demandes d’activation de rôle.</span><span class="sxs-lookup"><span data-stu-id="14a28-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="14a28-112">Scénarios</span><span class="sxs-lookup"><span data-stu-id="14a28-112">Scenarios</span></span>

<span data-ttu-id="14a28-113">La version préliminaire privée prend en charge les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="14a28-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="14a28-114">**En tant qu’Administrateur de rôle privilégié (PRA), vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="14a28-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="14a28-115">activer l’approbation pour des rôles spécifiques</span><span class="sxs-lookup"><span data-stu-id="14a28-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="14a28-116">spécifier les utilisateurs et/ou groupes approbateurs pour approuver des demandes</span><span class="sxs-lookup"><span data-stu-id="14a28-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="14a28-117">afficher l’historique des demandes et approbations pour tous les rôles privilégiés</span><span class="sxs-lookup"><span data-stu-id="14a28-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="14a28-118">**En tant d’approbateur désigné, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="14a28-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="14a28-119">afficher les approbations (demandes) en attente</span><span class="sxs-lookup"><span data-stu-id="14a28-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="14a28-120">approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)</span><span class="sxs-lookup"><span data-stu-id="14a28-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="14a28-121">justifier mon approbation/rejet</span><span class="sxs-lookup"><span data-stu-id="14a28-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="14a28-122">**En tant qu’un utilisateur de rôle éligible, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="14a28-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="14a28-123">demander l’activation d’un rôle qui nécessite une approbation</span><span class="sxs-lookup"><span data-stu-id="14a28-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="14a28-124">afficher l’état de votre demande d’activation</span><span class="sxs-lookup"><span data-stu-id="14a28-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="14a28-125">exécuter la tâche dans Azure AD si l’activation a été approuvée</span><span class="sxs-lookup"><span data-stu-id="14a28-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="14a28-126">Navigation</span><span class="sxs-lookup"><span data-stu-id="14a28-126">Navigation</span></span>

<span data-ttu-id="14a28-127">Nous avons mis à jour la navigation pour prendre en charge les approbations</span><span class="sxs-lookup"><span data-stu-id="14a28-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="14a28-128">La page d’accueil par défaut permet d’accéder facilement aux informations sur PIM et à la documentation des nouvelles approbations.</span><span class="sxs-lookup"><span data-stu-id="14a28-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="14a28-129">Nous avons également ajouté une nouvelle section pour tous les utilisateurs de PIM, « Mon historique d’audit ».</span><span class="sxs-lookup"><span data-stu-id="14a28-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="14a28-130">Vous y trouverez toutes les informations relatives à votre identité.</span><span class="sxs-lookup"><span data-stu-id="14a28-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="14a28-131">Celles-ci regroupent dans un emplacement pratique toutes vos demandes en attente et terminées, les décisions que vous avez prises sur les demandes que vous résolvez, et toutes vos activations de rôle passées.</span><span class="sxs-lookup"><span data-stu-id="14a28-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="14a28-132">Activer l’approbation pour des rôles spécifiques</span><span class="sxs-lookup"><span data-stu-id="14a28-132">Enable approval for specific roles</span></span>

<span data-ttu-id="14a28-133">Pour activer l’approbation pour un rôle spécifique, sélectionnez tout d’abord des rôles d’annuaire dans la navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="14a28-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="14a28-134">Rechercher et sélectionner des paramètres dans la navigation de gauche des rôles d’annuaire</span><span class="sxs-lookup"><span data-stu-id="14a28-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="14a28-135">Sélectionner des rôles privilégiés :</span><span class="sxs-lookup"><span data-stu-id="14a28-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="14a28-136">Sélectionnez « Activer » dans la section d’approbation Exiger :</span><span class="sxs-lookup"><span data-stu-id="14a28-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="14a28-137">Une fois activé, le panneau est développé pour afficher les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="14a28-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="14a28-138">Si vous ne spécifiez PAS d’approbateurs, les PRA deviennent les approbateurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="14a28-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="14a28-139">Les PRA doivent approuver TOUTES les demandes d’activation pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="14a28-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="14a28-140">Spécifier les utilisateurs et/ou groupes approbateurs pour approuver des demandes</span><span class="sxs-lookup"><span data-stu-id="14a28-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="14a28-141">Pour déléguer l’approbation, cliquez sur l’option « Sélectionner des approbateurs » :</span><span class="sxs-lookup"><span data-stu-id="14a28-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="14a28-142">Dans le panneau Sélectionner des approbateurs qui s’ouvre, vous pouvez rechercher un utilisateur ou groupe spécifique à l’aide de la barre de recherche située en haut, ou en sélectionnant dans la liste préremplie, puis cliquer sur « Sélectionner » lorsque vous avez terminé :</span><span class="sxs-lookup"><span data-stu-id="14a28-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="14a28-143">Remarque : vous pouvez sélectionner plusieurs utilisateurs ou groupes à la fois.</span><span class="sxs-lookup"><span data-stu-id="14a28-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="14a28-144">Votre sélection apparaît dans la liste des approbateurs sélectionnés comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="14a28-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="14a28-145">Pour supprimer un approbateur, cliquez simplement sur le bouton Supprimer en regard de son nom.</span><span class="sxs-lookup"><span data-stu-id="14a28-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="14a28-146">Pour ajouter des approbateurs supplémentaires, répétez le processus.</span><span class="sxs-lookup"><span data-stu-id="14a28-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="14a28-147">Afficher l’historique des demandes et approbations pour tous les rôles privilégiés</span><span class="sxs-lookup"><span data-stu-id="14a28-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="14a28-148">Pour afficher l’historique des demandes et approbations pour tous les rôles privilégiés, sélectionnez Historique d’audit dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="14a28-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="14a28-149">Vous pouvez trier les données par Action, puis recherchez « Activation approuvée »</span><span class="sxs-lookup"><span data-stu-id="14a28-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="14a28-150">Afficher les approbations (demandes) en attente</span><span class="sxs-lookup"><span data-stu-id="14a28-150">View pending approvals (requests)</span></span>

<span data-ttu-id="14a28-151">En tant qu’approbateur délégué, vous recevez une notification par courrier électronique lorsqu’une demande est en attente d’approbation.</span><span class="sxs-lookup"><span data-stu-id="14a28-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="14a28-152">Pour afficher ces requêtes dans le portail PIM, dans le tableau de bord (dans la nouvelle navigation), sélectionnez l’onglet « Demandes d’approbation en attente » dans la barre de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="14a28-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="14a28-153">Une liste des demandes d’approbation en attente s’affiche ici :</span><span class="sxs-lookup"><span data-stu-id="14a28-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="14a28-154">Approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)</span><span class="sxs-lookup"><span data-stu-id="14a28-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="14a28-155">Sélectionnez les demandes que vous souhaitez approuver ou refuser, puis cliquez sur le bouton dans la barre d’action qui correspond à votre décision :</span><span class="sxs-lookup"><span data-stu-id="14a28-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="14a28-156">Justifier mon approbation/rejet</span><span class="sxs-lookup"><span data-stu-id="14a28-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="14a28-157">Un nouveau panneau s’ouvre, dans lequel vous pouvez approuver ou refuser plusieurs demandes simultanément.</span><span class="sxs-lookup"><span data-stu-id="14a28-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="14a28-158">Entrez une justification de votre choix, puis cliquez sur Approuver (ou Refuser) au bas du panneau :</span><span class="sxs-lookup"><span data-stu-id="14a28-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="14a28-159">Une fois le processus de demande terminé, le symbole d’état reflète la décision que vous avez prise (dans cet exemple, Approuver) :</span><span class="sxs-lookup"><span data-stu-id="14a28-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="14a28-160">Demander l’activation d’un rôle qui nécessite une approbation</span><span class="sxs-lookup"><span data-stu-id="14a28-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="14a28-161">La demande d’activation d’un rôle qui nécessite une approbation peut être effectuée dans l’ancienne navigation de PIM ou dans la nouvelle, car le processus d’activation d’un rôle est identique.</span><span class="sxs-lookup"><span data-stu-id="14a28-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="14a28-162">Sélectionnez simplement un rôle dans la liste des rôles à activer :</span><span class="sxs-lookup"><span data-stu-id="14a28-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="14a28-163">Si un rôle de privilège requiert Multi-Factor Authentication, vous êtes invité à effectuer la tâche suivante en premier :</span><span class="sxs-lookup"><span data-stu-id="14a28-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="14a28-164">Lorsque vous avez terminé, cliquez sur Activer et entrez une justification (si nécessaire) :</span><span class="sxs-lookup"><span data-stu-id="14a28-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="14a28-165">Une notification indiquant que la demande est en attente d’approbation est envoyée au demandeur :</span><span class="sxs-lookup"><span data-stu-id="14a28-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="14a28-166">Afficher l’état de votre demande d’activation</span><span class="sxs-lookup"><span data-stu-id="14a28-166">View the status of your request to activate</span></span>

<span data-ttu-id="14a28-167">L’état d’une demande d’activation en attente doit être consulté à partir de la nouvelle navigation.</span><span class="sxs-lookup"><span data-stu-id="14a28-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="14a28-168">Dans la barre de navigation de gauche, sélectionnez l’onglet « My Requests » (Mes demandes) :</span><span class="sxs-lookup"><span data-stu-id="14a28-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="14a28-169">L’état de la demande par défaut est « En attente », mais vous pouvez basculer pour afficher toutes les demandes ou les demandes refusées.</span><span class="sxs-lookup"><span data-stu-id="14a28-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="14a28-170">Exécuter la tâche dans Azure AD si l’activation a été approuvée</span><span class="sxs-lookup"><span data-stu-id="14a28-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="14a28-171">Une fois la demande approuvée, le rôle est actif et vous pouvez effectuer les tâches qui requièrent ce rôle.</span><span class="sxs-lookup"><span data-stu-id="14a28-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="14a28-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14a28-172">Next steps</span></span>

<span data-ttu-id="14a28-173">Vos commentaires sont précieux pour nous.</span><span class="sxs-lookup"><span data-stu-id="14a28-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="14a28-174">N’hésitez pas à nous faire part ici de vos commentaires !</span><span class="sxs-lookup"><span data-stu-id="14a28-174">Please feel free to share comments or feedback with us here!</span></span>
