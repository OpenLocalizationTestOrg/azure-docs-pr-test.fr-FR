---
title: "workflows d’approbation de la gestion Privileged Identity aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="ab1ac-103">Approbations (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="ab1ac-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="ab1ac-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ab1ac-104">Overview</span></span>

<span data-ttu-id="ab1ac-105">Avec des approbations pour Privileged Identity Management, vous pouvez configurer l’approbation toorequire rôles pour l’activation et choisissez un ou plusieurs utilisateurs ou groupes approbateurs comme délégués.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="ab1ac-106">Poursuivez votre lecture toolearn comment tooconfigure rôles et de sélectionner les approbateurs.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="ab1ac-107">N’oubliez pas que cette fonctionnalité est en cours de développement et que vous pouvez rencontrer des bugs.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="ab1ac-108">fonctionnalité de Hello, y compris le texte et les conventions d’affectation de noms sont susceptibles de changer et ne doivent pas être considérés finales.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="ab1ac-109">Terminologie clé</span><span class="sxs-lookup"><span data-stu-id="ab1ac-109">Key Terminology</span></span>

<span data-ttu-id="ab1ac-110">*Utilisateur rôle éligible* – un utilisateur éligible rôle est un utilisateur au sein de votre organisation qui a été attribué rôle tooan Azure AD comme éligibles (rôle nécessite l’activation).</span><span class="sxs-lookup"><span data-stu-id="ab1ac-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="ab1ac-111">*Approbateur délégué* : un approbateur délégué est une ou plusieurs personnes ou groupes au sein de votre Azure AD responsables de l’approbation des demandes d’activation de rôle.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="ab1ac-112">Scénarios</span><span class="sxs-lookup"><span data-stu-id="ab1ac-112">Scenarios</span></span>

<span data-ttu-id="ab1ac-113">version préliminaire limitée de Hello prend en charge hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="ab1ac-114">**En tant qu’Administrateur de rôle privilégié (PRA), vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="ab1ac-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="ab1ac-115">activer l’approbation pour des rôles spécifiques</span><span class="sxs-lookup"><span data-stu-id="ab1ac-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="ab1ac-116">spécifier les demandes de tooapprove les utilisateurs et/ou groupes approbateur</span><span class="sxs-lookup"><span data-stu-id="ab1ac-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="ab1ac-117">afficher l’historique des demandes et approbations pour tous les rôles privilégiés</span><span class="sxs-lookup"><span data-stu-id="ab1ac-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="ab1ac-118">**En tant d’approbateur désigné, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="ab1ac-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="ab1ac-119">afficher les approbations (demandes) en attente</span><span class="sxs-lookup"><span data-stu-id="ab1ac-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="ab1ac-120">approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)</span><span class="sxs-lookup"><span data-stu-id="ab1ac-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="ab1ac-121">justifier mon approbation/rejet</span><span class="sxs-lookup"><span data-stu-id="ab1ac-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="ab1ac-122">**En tant qu’un utilisateur de rôle éligible, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="ab1ac-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="ab1ac-123">demander l’activation d’un rôle qui nécessite une approbation</span><span class="sxs-lookup"><span data-stu-id="ab1ac-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="ab1ac-124">afficher l’état de votre demande de tooactivate hello</span><span class="sxs-lookup"><span data-stu-id="ab1ac-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="ab1ac-125">exécuter la tâche dans Azure AD si l’activation a été approuvée</span><span class="sxs-lookup"><span data-stu-id="ab1ac-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="ab1ac-126">Navigation</span><span class="sxs-lookup"><span data-stu-id="ab1ac-126">Navigation</span></span>

<span data-ttu-id="ab1ac-127">Nous avons mis à jour les approbations de hello navigation toosupport</span><span class="sxs-lookup"><span data-stu-id="ab1ac-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="ab1ac-128">page d’accueil par défaut Hello fournit tooinformation un accès aisé à propos de PIM et hello nouvelle documentation approbations.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="ab1ac-129">Nous avons également ajouté une nouvelle section pour tous les utilisateurs de PIM, « Mon historique d’audit ».</span><span class="sxs-lookup"><span data-stu-id="ab1ac-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="ab1ac-130">Vous trouverez ici identité de tooyour applique toutes les hello plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="ab1ac-131">Cela inclut toutes les demandes en attente et terminées, les décisions sur les demandes hello vous résolvez et toutes vos activations rôle passées dans un emplacement pratique.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="ab1ac-132">Activer l’approbation pour des rôles spécifiques</span><span class="sxs-lookup"><span data-stu-id="ab1ac-132">Enable approval for specific roles</span></span>

<span data-ttu-id="ab1ac-133">approbation tooenable pour un rôle spécifique, sélectionnez tout d’abord les rôles d’annuaire à partir du volet de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="ab1ac-134">Recherchez et sélectionnez Paramètres Bonjour de navigation gauche des rôles d’annuaire</span><span class="sxs-lookup"><span data-stu-id="ab1ac-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="ab1ac-135">Sélectionner des rôles privilégiés :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="ab1ac-136">Sélectionnez « Activer » Bonjour nécessitent la section sur l’approbation :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="ab1ac-137">Une fois activé, panneau de hello développera hello tooshow les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="ab1ac-138">Si vous n’effectuez pas spécifiez des approbateurs, hello PRA(s) devenir l’ou les approbateurs hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="ab1ac-139">PRA(s) serait requise tooapprove d’activation de toutes les demandes de ce rôle.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="ab1ac-140">Spécifier les demandes de tooapprove les utilisateurs et/ou groupes approbateur</span><span class="sxs-lookup"><span data-stu-id="ab1ac-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="ab1ac-141">toodelegate approbation, cliquez sur hello option trop « sélectionner les approbateurs » :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="ab1ac-142">Lors du chargement de panneau d’approbateurs sélectionnez hello, vous pouvez rechercher un utilisateur spécifique ou un groupe à l’aide de la barre de recherche hello en haut de hello ou en sélectionnant dans la liste prédéfinie de hello, puis cliquez sur « Select » une fois :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="ab1ac-143">Remarque : vous pouvez sélectionner plusieurs utilisateurs ou groupes à la fois.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="ab1ac-144">La sélection apparaît dans la liste hello des approbateurs sélectionnés comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="ab1ac-145">tooremove un approbateur, cliquez simplement sur le nom de tootheir suivant hello Remove bouton.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="ab1ac-146">approbateurs supplémentaires tooadd, processus de répétition hello.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="ab1ac-147">Afficher l’historique des demandes et approbations pour tous les rôles privilégiés</span><span class="sxs-lookup"><span data-stu-id="ab1ac-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="ab1ac-148">l’historique de demande et d’approbation tooview pour tous les rôles privilégiés, sélectionnez l’historique d’Audit à partir du tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="ab1ac-149">Vous pouvez trier les données de salutation par Action et recherchez « Activation approuvé »</span><span class="sxs-lookup"><span data-stu-id="ab1ac-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="ab1ac-150">Afficher les approbations (demandes) en attente</span><span class="sxs-lookup"><span data-stu-id="ab1ac-150">View pending approvals (requests)</span></span>

<span data-ttu-id="ab1ac-151">En tant qu’approbateur délégué, vous recevez une notification par courrier électronique lorsqu’une demande est en attente d’approbation.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="ab1ac-152">tooview ces demandes dans le portail PIM hello, depuis l’onglet tableau de bord (dans une nouvelle navigation hello) sélectionnez hello » en attente demandes d’approbation » hello la barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="ab1ac-153">Une liste des demandes d’approbation en attente s’affiche ici :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="ab1ac-154">Approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)</span><span class="sxs-lookup"><span data-stu-id="ab1ac-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="ab1ac-155">Vous souhaitez tooapprove ou refusez les demandes de hello, puis cliquez sur le bouton hello dans la barre d’action qui correspond à votre décision :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="ab1ac-156">Justifier mon approbation/rejet</span><span class="sxs-lookup"><span data-stu-id="ab1ac-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="ab1ac-157">Cela ouvre une nouvelle tooapprove de panneau ou refuser plusieurs demandes à la fois.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="ab1ac-158">Entrer une justification de votre choix et cliquez sur Approuver (ou refuser) au bas de hello ou panneau de hello :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="ab1ac-159">Lorsque le processus de demande de hello est terminée, symbole d’état hello reflète la décision (dans cet exemple, la décision de hello est approuver) :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="ab1ac-160">Demander l’activation d’un rôle qui nécessite une approbation</span><span class="sxs-lookup"><span data-stu-id="ab1ac-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="ab1ac-161">Demander l’activation d’un rôle qui nécessite l’approbation peut être lancée à partir de la navigation de PIM ancien hello, ou d’une nouvelle navigation hello, en tant que processus hello pour le reste de l’activation de rôle hello identiques.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="ab1ac-162">Il suffit de sélectionner un rôle à partir de la liste de hello des rôles pour activer :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="ab1ac-163">Si un rôle de privilège requiert Multi-Factor Authentication, vous êtes invité à effectuer la tâche suivante en premier :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="ab1ac-164">Lorsque vous avez terminé, cliquez sur Activer et entrez une justification (si nécessaire) :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="ab1ac-165">demandeur de Hello s’affiche une notification indiquant que hello demande en attente d’approbation :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="ab1ac-166">Afficher l’état de votre demande de tooactivate hello</span><span class="sxs-lookup"><span data-stu-id="ab1ac-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="ab1ac-167">Affichage de l’état de hello d’une demande en attente de tooactivate doit être accessible à partir de la nouvelle navigation.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="ab1ac-168">À partir de la barre de navigation gauche hello, sélectionnez l’onglet de « Mes demandes » hello :</span><span class="sxs-lookup"><span data-stu-id="ab1ac-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="ab1ac-169">état de la demande Hello par défaut est trop « « en attente », mais vous pouvez basculer toosee tous les ou refuser les demandes.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="ab1ac-170">Exécuter la tâche dans Azure AD si l’activation a été approuvée</span><span class="sxs-lookup"><span data-stu-id="ab1ac-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="ab1ac-171">Une fois que hello demande est approuvée, rôle de hello est actif et vous pouvez continuer avec n’importe quel travail qui requiert ce rôle.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="ab1ac-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab1ac-172">Next steps</span></span>

<span data-ttu-id="ab1ac-173">Vos commentaires nous sont précieux toous.</span><span class="sxs-lookup"><span data-stu-id="ab1ac-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="ab1ac-174">Vous pouvez tooshare libre commentaires ou des commentaires nous ici !</span><span class="sxs-lookup"><span data-stu-id="ab1ac-174">Please feel free tooshare comments or feedback with us here!</span></span>
