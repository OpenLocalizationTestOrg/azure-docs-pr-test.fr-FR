---
title: "portail aaaAzure pour les stratégies de ressources | Documents Microsoft"
description: "Décrit comment toouse toocreate portail Azure et de gérer les stratégies du Gestionnaire de ressources. Les stratégies peuvent être appliquées à des groupes d’abonnement ou une ressource hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="b7d46-104">Utilisez tooassign portail Azure et de gérer les stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="b7d46-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="b7d46-105">Hello portail Azure permet les abonnements et vous tooassign stratégies tooresource groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="b7d46-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="b7d46-106">l’interface utilisateur Hello permet stratégie de hello tooselect facile que vous souhaitez tooassign et spécifiez des valeurs de paramètre pour cette stratégie de paramètres de stratégie toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="b7d46-107">tooassign une stratégie via le portail de hello, définition de stratégie hello doit déjà exister dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7d46-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="b7d46-108">Votre abonnement a plusieurs définitions des stratégies intégrées qui sont prêtes pour vous tooassign tooresource groupes ou des abonnements.</span><span class="sxs-lookup"><span data-stu-id="b7d46-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="b7d46-109">Vous voyez ces stratégies intégrées et les stratégies personnalisées que vous avez défini lors de l’utilisation de stratégies de portail tooassign hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="b7d46-110">Pour une présentation toopolicies et comment toodefine personnalisés stratégie, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b7d46-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="b7d46-111">Toutes les ressources enfants héritent des stratégies.</span><span class="sxs-lookup"><span data-stu-id="b7d46-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="b7d46-112">Donc, si une stratégie est un groupe de ressources appliquée tooa, ressources de hello tooall applicable dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b7d46-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="b7d46-113">Dans cet article, le terme de hello **étendue** fait référence le groupe de ressources toohello ou d’un abonnement qui est affectée à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="b7d46-114">Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).</span><span class="sxs-lookup"><span data-stu-id="b7d46-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="b7d46-115">Attribution d’une stratégie</span><span class="sxs-lookup"><span data-stu-id="b7d46-115">Assign a policy</span></span>

1. <span data-ttu-id="b7d46-116">tooassign un tooeither stratégie un groupe de ressources ou un abonnement, sélectionnez ce groupe de ressources ou d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7d46-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="b7d46-117">Dans paramètres de hello, sélectionnez **stratégies**.</span><span class="sxs-lookup"><span data-stu-id="b7d46-117">In hello settings, select **Policies**.</span></span>

   ![sélectionner des stratégies](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="b7d46-119">toocreate une attribution de stratégie pour cette étendue, sélectionnez **ajouter affectation**.</span><span class="sxs-lookup"><span data-stu-id="b7d46-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![ajouter une affectation](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="b7d46-121">Sélectionnez la stratégie hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="b7d46-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="b7d46-122">Même si vous n’avez ajouté aucun abonnement de tooyour de définitions de stratégie, vous consultez stratégies hello intégrées qui sont disponibles pour l’assignation.</span><span class="sxs-lookup"><span data-stu-id="b7d46-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="b7d46-123">Ces stratégies intégrées couvrent de nombreux scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="b7d46-123">These built-in policies cover many common scenarios.</span></span>

   ![sélectionner une définition](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="b7d46-125">Après avoir sélectionné une stratégie, vous consultez une description de la stratégie de hello et tous les paramètres pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b7d46-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="b7d46-126">Par exemple, hello image suivante montre hello **autorisée emplacements** paramètre, qui est requis pour la stratégie hello qui restreint les emplacements disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![afficher des paramètres](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="b7d46-128">Interface utilisateur de hello, sélectionnez toospecify de valeurs hello pour les paramètres de stratégie hello (par exemple, les emplacements de hello qui peuvent être utilisés pour le déploiement).</span><span class="sxs-lookup"><span data-stu-id="b7d46-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![sélectionner les valeurs des paramètres](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="b7d46-130">Fournir des valeurs pour hello autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="b7d46-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="b7d46-131">étendue de Hello est automatiquement attribué en fonction de panneau hello sélectionnée lors du démarrage d’attribution de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="b7d46-132">Cliquez sur **OK** quand vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="b7d46-132">Select **OK** when done.</span></span>

   ![définir les paramètres](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="b7d46-134">Vous avez attribué hello stratégie toohello spécifié étendue.</span><span class="sxs-lookup"><span data-stu-id="b7d46-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="b7d46-135">Afficher les affectations de stratégies</span><span class="sxs-lookup"><span data-stu-id="b7d46-135">View policy assignments</span></span>

<span data-ttu-id="b7d46-136">Après avoir attribué une stratégie, il apparaît dans la liste hello de stratégies pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="b7d46-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="b7d46-137">Hello **détails** onglet affiche un résumé de l’attribution de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![afficher les détails](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="b7d46-139">Hello **règle d’affectation** onglet affiche hello JSON pour la définition de la stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![afficher une règle d’affectation](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="b7d46-141">Modifier une affectation de stratégie existante</span><span class="sxs-lookup"><span data-stu-id="b7d46-141">Change an existing policy assignment</span></span>

<span data-ttu-id="b7d46-142">toochange une stratégie, sélectionnez **modifier l’affectation** ou **supprimer**</span><span class="sxs-lookup"><span data-stu-id="b7d46-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![modifier ou supprimer une affectation](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="b7d46-144">Affecter des stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="b7d46-144">Assign custom policies</span></span>

<span data-ttu-id="b7d46-145">Si vous avez défini des stratégies personnalisées dans votre abonnement, ces stratégies sont disponibles pour l’assignation via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b7d46-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="b7d46-146">Ces stratégies ont le préfixe **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="b7d46-146">Those policies are prefaced with **[Custom]**</span></span>

![stratégies personnalisées](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="b7d46-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7d46-148">Next steps</span></span>
* <span data-ttu-id="b7d46-149">toolearn sur la syntaxe JSON hello pour définir des stratégies, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b7d46-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="b7d46-150">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b7d46-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="b7d46-151">schéma de stratégie Hello est publiée à [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="b7d46-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

