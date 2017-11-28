---
title: "Stratégies de ressources sur le portail Azure | Microsoft Docs"
description: "Explique comment utiliser le portail Azure pour créer et gérer des stratégies Resource Manager. Les stratégies peuvent être appliquées au niveau de l’abonnement ou des groupes de ressources."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="9e09b-104">Utiliser le portail Azure pour attribuer et gérer les stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="9e09b-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="9e09b-105">Le portail vous permet d’affecter des stratégies de ressource pour les abonnements et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="9e09b-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="9e09b-106">L’interface utilisateur facilite la sélection de la stratégie que vous souhaitez affecter, puis la spécification des valeurs de paramètre pour cette stratégie afin de personnaliser les paramètres de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e09b-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="9e09b-107">Pour affecter une stratégie via le portail, la définition de stratégie doit déjà exister dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e09b-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="9e09b-108">Votre abonnement a plusieurs définitions de stratégie intégrées qui sont prêtes à être affectées à des groupes de ressources ou des abonnements.</span><span class="sxs-lookup"><span data-stu-id="9e09b-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="9e09b-109">Vous voyez ces stratégies intégrées et les stratégies personnalisées que vous avez définies lors de l’utilisation du portail pour affecter des stratégies.</span><span class="sxs-lookup"><span data-stu-id="9e09b-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="9e09b-110">Pour une introduction aux stratégies et à la définition de stratégies personnalisées, consultez la page [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9e09b-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="9e09b-111">Toutes les ressources enfants héritent des stratégies.</span><span class="sxs-lookup"><span data-stu-id="9e09b-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="9e09b-112">Ainsi, si une stratégie est appliquée à un groupe de ressources, elle est applicable à toutes les ressources appartenant à ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9e09b-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="9e09b-113">Dans cet article, le terme **étendue** fait référence au groupe de ressources ou à l’abonnement affecté à la stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e09b-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="9e09b-114">Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).</span><span class="sxs-lookup"><span data-stu-id="9e09b-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="9e09b-115">Attribution d’une stratégie</span><span class="sxs-lookup"><span data-stu-id="9e09b-115">Assign a policy</span></span>

1. <span data-ttu-id="9e09b-116">Pour affecter une stratégie à un groupe de ressources ou un abonnement, sélectionnez ce groupe de ressources ou abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e09b-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="9e09b-117">Dans les paramètres, sélectionnez **Stratégies**.</span><span class="sxs-lookup"><span data-stu-id="9e09b-117">In the settings, select **Policies**.</span></span>

   ![sélectionner des stratégies](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="9e09b-119">Pour créer une affectation de stratégie pour cette étendue, sélectionnez **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9e09b-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![ajouter une affectation](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="9e09b-121">Sélectionnez la stratégie que vous souhaitez affecter.</span><span class="sxs-lookup"><span data-stu-id="9e09b-121">Select the policy you want to assign.</span></span> <span data-ttu-id="9e09b-122">Même si vous n’avez pas ajouté de définitions de stratégie à votre abonnement, vous voyez les stratégies intégrées qui sont disponibles pour affectation.</span><span class="sxs-lookup"><span data-stu-id="9e09b-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="9e09b-123">Ces stratégies intégrées couvrent de nombreux scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="9e09b-123">These built-in policies cover many common scenarios.</span></span>

   ![sélectionner une définition](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="9e09b-125">Après avoir sélectionné une stratégie, vous voyez une description de la stratégie et ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="9e09b-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="9e09b-126">Par exemple, l’illustration suivante montre le paramètre **Emplacements autorisés**, qui est requis pour la stratégie qui restreint les emplacements disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e09b-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![afficher des paramètres](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="9e09b-128">Via l’interface utilisateur, sélectionnez les valeurs à spécifier pour les paramètres de stratégie (par exemple, les emplacements qui peuvent être utilisés pour le déploiement).</span><span class="sxs-lookup"><span data-stu-id="9e09b-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![sélectionner les valeurs des paramètres](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="9e09b-130">Fournissez des valeurs pour les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="9e09b-130">Provide values for the other parameters.</span></span> <span data-ttu-id="9e09b-131">L’étendue est automatiquement affectée selon le panneau sélectionné lors du démarrage de l’affectation de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e09b-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="9e09b-132">Cliquez sur **OK** quand vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="9e09b-132">Select **OK** when done.</span></span>

   ![définir les paramètres](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="9e09b-134">Vous avez affecté la stratégie à l’étendue spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9e09b-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="9e09b-135">Afficher les affectations de stratégies</span><span class="sxs-lookup"><span data-stu-id="9e09b-135">View policy assignments</span></span>

<span data-ttu-id="9e09b-136">Après avoir attribué une stratégie, elle s’affiche dans la liste des stratégies pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="9e09b-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="9e09b-137">L’onglet **Détails** affiche un résumé de l’affectation de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e09b-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![afficher les détails](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="9e09b-139">L’onglet **Règle d’affectation** affiche le code JSON pour la définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e09b-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![afficher une règle d’affectation](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="9e09b-141">Modifier une affectation de stratégie existante</span><span class="sxs-lookup"><span data-stu-id="9e09b-141">Change an existing policy assignment</span></span>

<span data-ttu-id="9e09b-142">Pour modifier une stratégie, sélectionnez **Modifier l’affectation** ou **Supprimer**</span><span class="sxs-lookup"><span data-stu-id="9e09b-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![modifier ou supprimer une affectation](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="9e09b-144">Affecter des stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="9e09b-144">Assign custom policies</span></span>

<span data-ttu-id="9e09b-145">Si vous avez défini des stratégies personnalisées dans votre abonnement, ces stratégies sont disponibles pour affectation via le portail.</span><span class="sxs-lookup"><span data-stu-id="9e09b-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="9e09b-146">Ces stratégies ont le préfixe **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="9e09b-146">Those policies are prefaced with **[Custom]**</span></span>

![stratégies personnalisées](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="9e09b-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e09b-148">Next steps</span></span>
* <span data-ttu-id="9e09b-149">Pour en savoir plus sur la syntaxe JSON pour définir des stratégies, consultez la [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9e09b-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="9e09b-150">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9e09b-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="9e09b-151">Le schéma de stratégie est publié à l’adresse [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="9e09b-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

