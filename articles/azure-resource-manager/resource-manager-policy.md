---
title: "Stratégies de ressources Azure | Microsoft Docs"
description: "Explique comment utiliser les stratégies d’Azure Resource Manager afin de garantir la définition de propriétés de ressource cohérentes pendant le déploiement. Les stratégies peuvent être appliquées au niveau de l’abonnement ou des groupes de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="43841-104">Vue d’ensemble des stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="43841-104">Resource policy overview</span></span>
<span data-ttu-id="43841-105">Les stratégies de ressources permettent d’établir des conventions pour les ressources de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="43841-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="43841-106">En définissant des conventions, vous pouvez contrôler les coûts et gérer plus facilement vos ressources.</span><span class="sxs-lookup"><span data-stu-id="43841-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="43841-107">Par exemple, vous pouvez spécifier que seuls certains types de machines virtuelles sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="43841-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="43841-108">Vous pouvez aussi exiger que toutes les ressources soient marquées.</span><span class="sxs-lookup"><span data-stu-id="43841-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="43841-109">Toutes les ressources enfants héritent des stratégies.</span><span class="sxs-lookup"><span data-stu-id="43841-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="43841-110">Ainsi, si une stratégie est appliquée à un groupe de ressources, elle est applicable à toutes les ressources appartenant à ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="43841-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="43841-111">Il y a deux concepts importants à comprendre concernant les stratégies :</span><span class="sxs-lookup"><span data-stu-id="43841-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="43841-112">Définition de stratégie : vous spécifiez à quel moment la stratégie est appliquée et l’action à exécuter.</span><span class="sxs-lookup"><span data-stu-id="43841-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="43841-113">Affectation de stratégie : vous appliquez la définition de stratégie à une étendue (abonnement ou groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="43841-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="43841-114">Cette rubrique porte sur la définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="43841-115">Pour plus d’informations sur l’affectation des stratégies, consultez [Utiliser le portail Azure pour attribuer et gérer les stratégies de ressources](resource-manager-policy-portal.md) ou [Attribuer et gérer les stratégies de ressources via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="43841-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="43841-116">Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).</span><span class="sxs-lookup"><span data-stu-id="43841-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="43841-117">Actuellement, la stratégie n'évalue pas les types de ressources qui ne prennent pas en charge les balises, le type et l'emplacement, par exemple, le type de ressource Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="43841-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="43841-118">Cette prise en charge sera ajoutée prochainement.</span><span class="sxs-lookup"><span data-stu-id="43841-118">This support will be added at a future time.</span></span> <span data-ttu-id="43841-119">Pour éviter des problèmes de compatibilité descendante, vous devriez spécifier explicitement le type lors de la création de stratégies.</span><span class="sxs-lookup"><span data-stu-id="43841-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="43841-120">Par exemple, une stratégie de balises sans spécification des types est appliquée à tous les types.</span><span class="sxs-lookup"><span data-stu-id="43841-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="43841-121">Dans ce cas, le déploiement d’un modèle risque d’échouer s’il existe une ressource imbriquée ne prenant pas en charge les balises, et le type de ressource du déploiement sera ajouté à l’évaluation de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="43841-122">Quelle est la différence avec RBAC ?</span><span class="sxs-lookup"><span data-stu-id="43841-122">How is it different from RBAC?</span></span>
<span data-ttu-id="43841-123">Il existe quelques différences importantes entre la stratégie et le contrôle d’accès en fonction du rôle (RBAC).</span><span class="sxs-lookup"><span data-stu-id="43841-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="43841-124">RBAC porte sur les actions des **utilisateurs** dans différentes étendues.</span><span class="sxs-lookup"><span data-stu-id="43841-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="43841-125">Par exemple, le rôle de contributeur vous est attribué pour un groupe de ressources dans l’étendue de votre choix, ce qui vous permet d’apporter des modifications à ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="43841-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="43841-126">La stratégie se focalise sur les propriétés des **ressources** pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="43841-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="43841-127">Par exemple, vous pouvez utiliser des stratégies pour contrôler les types de ressources qui peuvent être approvisionnées.</span><span class="sxs-lookup"><span data-stu-id="43841-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="43841-128">Vous pouvez aussi restreindre les emplacements auxquels les ressources peuvent être approvisionnées.</span><span class="sxs-lookup"><span data-stu-id="43841-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="43841-129">Contrairement à RBAC, la stratégie est, par défaut, un système explicite d'autorisation et de refus.</span><span class="sxs-lookup"><span data-stu-id="43841-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="43841-130">Pour utiliser des stratégies, vous devez vous authentifier au moyen de RBAC.</span><span class="sxs-lookup"><span data-stu-id="43841-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="43841-131">Plus précisément, votre compte a besoin de :</span><span class="sxs-lookup"><span data-stu-id="43841-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="43841-132">l’autorisation `Microsoft.Authorization/policydefinitions/write` pour définir une stratégie ;</span><span class="sxs-lookup"><span data-stu-id="43841-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="43841-133">l’autorisation `Microsoft.Authorization/policyassignments/write` pour affecter une stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="43841-134">Ces autorisations ne sont pas incluses dans le rôle **Contributeur**.</span><span class="sxs-lookup"><span data-stu-id="43841-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="43841-135">Stratégies prédéfinies</span><span class="sxs-lookup"><span data-stu-id="43841-135">Built-in policies</span></span>

<span data-ttu-id="43841-136">Azure fournit certaines définitions de stratégie intégrées qui peuvent réduire le nombre de stratégies à définir.</span><span class="sxs-lookup"><span data-stu-id="43841-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="43841-137">Avant de procéder à des définitions de stratégie, vous devez vous demander si une stratégie intégrée fournit déjà la définition dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="43841-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="43841-138">Les définitions de stratégie intégrée sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="43841-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="43841-139">Emplacements autorisés</span><span class="sxs-lookup"><span data-stu-id="43841-139">Allowed locations</span></span>
* <span data-ttu-id="43841-140">Types de ressources autorisés</span><span class="sxs-lookup"><span data-stu-id="43841-140">Allowed resource types</span></span>
* <span data-ttu-id="43841-141">Références SKU de compte de stockage autorisées</span><span class="sxs-lookup"><span data-stu-id="43841-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="43841-142">Références SKU de machine virtuelle autorisées</span><span class="sxs-lookup"><span data-stu-id="43841-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="43841-143">Appliquer la valeur par défaut et la balise</span><span class="sxs-lookup"><span data-stu-id="43841-143">Apply tag and default value</span></span>
* <span data-ttu-id="43841-144">Appliquer une balise et une valeur</span><span class="sxs-lookup"><span data-stu-id="43841-144">Enforce tag and value</span></span>
* <span data-ttu-id="43841-145">Types de ressources non autorisés</span><span class="sxs-lookup"><span data-stu-id="43841-145">Not allowed resource types</span></span>
* <span data-ttu-id="43841-146">Nécessitent SQL Server version 12.0</span><span class="sxs-lookup"><span data-stu-id="43841-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="43841-147">Nécessitent le chiffrement du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="43841-147">Require storage account encryption</span></span>

<span data-ttu-id="43841-148">Vous pouvez affecter l’une de ces stratégies par le biais du [portail](resource-manager-policy-portal.md), de [PowerShell](resource-manager-policy-create-assign.md#powershell) ou d’[Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="43841-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="43841-149">Structure de la définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="43841-149">Policy definition structure</span></span>
<span data-ttu-id="43841-150">Vous devez utiliser JSON pour créer une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="43841-151">La définition de stratégie contient des éléments pour :</span><span class="sxs-lookup"><span data-stu-id="43841-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="43841-152">parameters</span><span class="sxs-lookup"><span data-stu-id="43841-152">parameters</span></span>
* <span data-ttu-id="43841-153">le nom d’affichage</span><span class="sxs-lookup"><span data-stu-id="43841-153">display name</span></span>
* <span data-ttu-id="43841-154">description</span><span class="sxs-lookup"><span data-stu-id="43841-154">description</span></span>
* <span data-ttu-id="43841-155">la règle de stratégie</span><span class="sxs-lookup"><span data-stu-id="43841-155">policy rule</span></span>
  * <span data-ttu-id="43841-156">évaluation logique</span><span class="sxs-lookup"><span data-stu-id="43841-156">logical evaluation</span></span>
  * <span data-ttu-id="43841-157">effet</span><span class="sxs-lookup"><span data-stu-id="43841-157">effect</span></span>

<span data-ttu-id="43841-158">L’exemple suivant illustre une stratégie qui limite les emplacements où les ressources sont déployées :</span><span class="sxs-lookup"><span data-stu-id="43841-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="43841-159">Paramètres</span><span class="sxs-lookup"><span data-stu-id="43841-159">Parameters</span></span>
<span data-ttu-id="43841-160">Les paramètres permettent de simplifier la gestion des stratégies en réduisant le nombre de définitions de stratégies.</span><span class="sxs-lookup"><span data-stu-id="43841-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="43841-161">Vous définissez une stratégie pour une propriété de ressource (vous limitez par exemple les emplacements où les ressources peuvent être déployées) et incluez des paramètres dans la définition.</span><span class="sxs-lookup"><span data-stu-id="43841-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="43841-162">Ensuite, vous réutilisez cette définition de stratégie pour différents scénarios en transmettant différentes valeurs (vous spécifiez par exemple un ensemble d’emplacements pour un abonnement) au moment de l’affectation de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="43841-163">Vous déclarez des paramètres lorsque vous créez des définitions de stratégies.</span><span class="sxs-lookup"><span data-stu-id="43841-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="43841-164">Le type d’un paramètre peut être une chaîne ou un tableau.</span><span class="sxs-lookup"><span data-stu-id="43841-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="43841-165">La propriété de métadonnées est utilisée pour des outils comme le Portail Azure pour afficher des informations conviviales.</span><span class="sxs-lookup"><span data-stu-id="43841-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="43841-166">Dans la règle de stratégie, vous référencez des paramètres avec la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="43841-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="43841-167">Nom d’affichage et description</span><span class="sxs-lookup"><span data-stu-id="43841-167">Display name and description</span></span>

<span data-ttu-id="43841-168">Vous utilisez **displayName** et **description** pour distinguer la définition de stratégie et préciser le contexte d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="43841-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="43841-169">Règle de stratégie</span><span class="sxs-lookup"><span data-stu-id="43841-169">Policy rule</span></span>

<span data-ttu-id="43841-170">La règle de stratégie se compose de blocs **if** et **then**.</span><span class="sxs-lookup"><span data-stu-id="43841-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="43841-171">Dans le bloc **if**, vous définissez une ou plusieurs conditions qui spécifient à quel moment la stratégie est mise en œuvre.</span><span class="sxs-lookup"><span data-stu-id="43841-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="43841-172">Vous pouvez appliquer des opérateurs logiques à ces conditions pour définir avec précision le scénario d’une stratégie.</span><span class="sxs-lookup"><span data-stu-id="43841-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="43841-173">Dans le bloc **then**, vous définissez l’effet qui se produit lorsque les conditions de **si** sont remplies.</span><span class="sxs-lookup"><span data-stu-id="43841-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="43841-174">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="43841-174">Logical operators</span></span>
<span data-ttu-id="43841-175">Les opérateurs logiques pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="43841-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="43841-176">La syntaxe **not** inverse le résultat de la condition.</span><span class="sxs-lookup"><span data-stu-id="43841-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="43841-177">La syntaxe **allOf** (semblable à l’opération logique **And**) nécessite que toutes les conditions soient remplies.</span><span class="sxs-lookup"><span data-stu-id="43841-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="43841-178">La syntaxe **anyOf** (semblable à l’opération logique **Of**) nécessite qu’au moins une des conditions soit remplie.</span><span class="sxs-lookup"><span data-stu-id="43841-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="43841-179">Vous pouvez imbriquer des opérateurs logiques.</span><span class="sxs-lookup"><span data-stu-id="43841-179">You can nest logical operators.</span></span> <span data-ttu-id="43841-180">L’exemple suivant illustre une opération **not** imbriquée dans une opération **allOf**.</span><span class="sxs-lookup"><span data-stu-id="43841-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="43841-181">Conditions</span><span class="sxs-lookup"><span data-stu-id="43841-181">Conditions</span></span>
<span data-ttu-id="43841-182">La condition évalue si un **champ** répond à certains critères.</span><span class="sxs-lookup"><span data-stu-id="43841-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="43841-183">Les conditions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="43841-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="43841-184">Lorsque vous utilisez la condition **like**, vous pouvez utiliser un caractère générique (*) dans la valeur.</span><span class="sxs-lookup"><span data-stu-id="43841-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="43841-185">Lorsque vous utilisez la condition de **correspondance**, indiquez `#` pour représenter un chiffre, `?` pour une lettre et tout autre caractère pour représenter ce caractère réel.</span><span class="sxs-lookup"><span data-stu-id="43841-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="43841-186">Pour obtenir des exemples, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="43841-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="43841-187">Champs</span><span class="sxs-lookup"><span data-stu-id="43841-187">Fields</span></span>
<span data-ttu-id="43841-188">Les conditions sont formées à partir de champs.</span><span class="sxs-lookup"><span data-stu-id="43841-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="43841-189">Un champ représente des propriétés dans la charge utile de la requête de ressource qui est utilisée pour décrire l'état de la ressource.</span><span class="sxs-lookup"><span data-stu-id="43841-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="43841-190">Les champs suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="43841-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="43841-191">alias de propriété : pour en obtenir la liste, consultez [Alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="43841-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="43841-192">Résultat</span><span class="sxs-lookup"><span data-stu-id="43841-192">Effect</span></span>
<span data-ttu-id="43841-193">La stratégie prend en charge trois types d’effet : `deny`, `audit` et `append`.</span><span class="sxs-lookup"><span data-stu-id="43841-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="43841-194">**deny** génère un événement dans le journal d’audit et fait échouer la requête.</span><span class="sxs-lookup"><span data-stu-id="43841-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="43841-195">**audit** génère un événement d’avertissement dans le journal d’audit, mais ne fait pas échouer la requête.</span><span class="sxs-lookup"><span data-stu-id="43841-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="43841-196">**append** ajoute l’ensemble de champs défini à la requête.</span><span class="sxs-lookup"><span data-stu-id="43841-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="43841-197">Pour **append**, vous devez fournir les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="43841-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="43841-198">La valeur peut être une chaîne ou un objet au format JSON.</span><span class="sxs-lookup"><span data-stu-id="43841-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="43841-199">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-199">Aliases</span></span>

<span data-ttu-id="43841-200">Les alias de propriété permettent d’accéder aux propriétés spécifiques d’un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="43841-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="43841-201">Les alias permettent de restreindre les valeurs ou les conditions autorisées pour la propriété d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="43841-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="43841-202">Chaque alias correspond aux chemins des différentes versions d’API d’un type de ressource donné.</span><span class="sxs-lookup"><span data-stu-id="43841-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="43841-203">Lors de l’évaluation de la stratégie, le moteur de stratégie obtient le chemin de la propriété de cette version de l’API.</span><span class="sxs-lookup"><span data-stu-id="43841-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="43841-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="43841-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="43841-205">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-205">Alias</span></span> | <span data-ttu-id="43841-206">Description</span><span class="sxs-lookup"><span data-stu-id="43841-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="43841-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="43841-208">Définissez si le port du serveur Redis non-ssl (6379) est activé.</span><span class="sxs-lookup"><span data-stu-id="43841-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="43841-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="43841-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="43841-210">Définissez le nombre de partitions à créer sur un cache de cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="43841-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="43841-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="43841-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="43841-212">Définissez la taille du cache Redis à déployer.</span><span class="sxs-lookup"><span data-stu-id="43841-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="43841-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="43841-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="43841-214">Définissez la famille de références (SKU) à utiliser.</span><span class="sxs-lookup"><span data-stu-id="43841-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="43841-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="43841-216">Définissez le type de cache Redis à déployer.</span><span class="sxs-lookup"><span data-stu-id="43841-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="43841-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="43841-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="43841-218">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-218">Alias</span></span> | <span data-ttu-id="43841-219">Description</span><span class="sxs-lookup"><span data-stu-id="43841-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="43841-221">Définissez le nom du niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="43841-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="43841-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="43841-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="43841-223">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-223">Alias</span></span> | <span data-ttu-id="43841-224">Description</span><span class="sxs-lookup"><span data-stu-id="43841-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="43841-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="43841-226">Définissez l’offre de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="43841-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="43841-228">Définissez le serveur de publication de l’image de plateforme ou de l’image de Place de marché utilisé pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="43841-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="43841-230">Définissez la référence SKU de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="43841-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="43841-232">Définissez la version de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="43841-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="43841-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="43841-234">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-234">Alias</span></span> | <span data-ttu-id="43841-235">Description</span><span class="sxs-lookup"><span data-stu-id="43841-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="43841-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="43841-237">Définissez l’identificateur de l’image utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="43841-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="43841-239">Définissez l’offre de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="43841-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="43841-241">Définissez le serveur de publication de l’image de plateforme ou de l’image de Place de marché utilisé pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="43841-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="43841-243">Définissez la référence SKU de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="43841-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="43841-245">Définissez la version de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="43841-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="43841-247">Définissez si l’image ou le disque est sous licence en local.</span><span class="sxs-lookup"><span data-stu-id="43841-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="43841-248">Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="43841-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="43841-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="43841-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="43841-250">Définissez l’offre de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="43841-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="43841-252">Définissez le serveur de publication de l’image de plateforme ou de l’image de Place de marché utilisé pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="43841-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="43841-254">Définissez la référence SKU de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="43841-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="43841-256">Définissez la version de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="43841-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="43841-258">Définissez l’URI du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="43841-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="43841-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="43841-260">Définissez la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="43841-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="43841-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="43841-262">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-262">Alias</span></span> | <span data-ttu-id="43841-263">Description</span><span class="sxs-lookup"><span data-stu-id="43841-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="43841-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="43841-265">Définissez le nom du serveur de publication de l’extension.</span><span class="sxs-lookup"><span data-stu-id="43841-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="43841-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="43841-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="43841-267">Définissez le type d’extension.</span><span class="sxs-lookup"><span data-stu-id="43841-267">Set the type of extension.</span></span> |
| <span data-ttu-id="43841-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="43841-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="43841-269">Définissez la version de l’extension.</span><span class="sxs-lookup"><span data-stu-id="43841-269">Set the version of the extension.</span></span> |

<span data-ttu-id="43841-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="43841-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="43841-271">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-271">Alias</span></span> | <span data-ttu-id="43841-272">Description</span><span class="sxs-lookup"><span data-stu-id="43841-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="43841-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="43841-274">Définissez l’identificateur de l’image utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="43841-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="43841-276">Définissez l’offre de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="43841-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="43841-278">Définissez le serveur de publication de l’image de plateforme ou de l’image de Place de marché utilisé pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="43841-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="43841-280">Définissez la référence SKU de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="43841-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="43841-282">Définissez la version de l’image de plateforme ou de l’image de Place de marché utilisée pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43841-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="43841-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="43841-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="43841-284">Définissez si l’image ou le disque est sous licence en local.</span><span class="sxs-lookup"><span data-stu-id="43841-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="43841-285">Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="43841-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="43841-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="43841-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="43841-287">Définissez le préfixe du nom de l’ordinateur pour toutes les machines virtuelles dans le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="43841-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="43841-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="43841-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="43841-289">Définisez l’URI de blob pour l’image utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43841-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="43841-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="43841-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="43841-291">Définissez les URL de conteneur utilisées afin de stocker les disques du système d’exploitation pour le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="43841-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="43841-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="43841-293">Définissez la taille des machines virtuelles dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="43841-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="43841-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="43841-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="43841-295">Définissez le niveau des machines virtuelles dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="43841-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="43841-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="43841-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="43841-297">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-297">Alias</span></span> | <span data-ttu-id="43841-298">Description</span><span class="sxs-lookup"><span data-stu-id="43841-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="43841-300">Définissez la taille de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="43841-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="43841-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="43841-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="43841-302">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-302">Alias</span></span> | <span data-ttu-id="43841-303">Description</span><span class="sxs-lookup"><span data-stu-id="43841-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="43841-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="43841-305">Définissez le type de cette passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="43841-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="43841-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="43841-307">Définissez la référence SKU de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="43841-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="43841-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="43841-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="43841-309">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-309">Alias</span></span> | <span data-ttu-id="43841-310">Description</span><span class="sxs-lookup"><span data-stu-id="43841-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="43841-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="43841-312">Définissez la version du serveur.</span><span class="sxs-lookup"><span data-stu-id="43841-312">Set the version of the server.</span></span> |

<span data-ttu-id="43841-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="43841-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="43841-314">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-314">Alias</span></span> | <span data-ttu-id="43841-315">Description</span><span class="sxs-lookup"><span data-stu-id="43841-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="43841-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="43841-317">Définissez la modification de la base de données.</span><span class="sxs-lookup"><span data-stu-id="43841-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="43841-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="43841-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="43841-319">Définissez le nom du pool élastique dans lequel se trouve la base de données.</span><span class="sxs-lookup"><span data-stu-id="43841-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="43841-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="43841-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="43841-321">Définissez l’ID d’objectif de niveau de service configuré de la base de données.</span><span class="sxs-lookup"><span data-stu-id="43841-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="43841-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="43841-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="43841-323">Définissez le nom de l’objectif de niveau de service configuré de la base de données.</span><span class="sxs-lookup"><span data-stu-id="43841-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="43841-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="43841-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="43841-325">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-325">Alias</span></span> | <span data-ttu-id="43841-326">Description</span><span class="sxs-lookup"><span data-stu-id="43841-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="43841-327">servers/elasticpools</span></span> | <span data-ttu-id="43841-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="43841-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="43841-329">Définissez la valeur DTU partagée totale pour le pool élastique de la base de données.</span><span class="sxs-lookup"><span data-stu-id="43841-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="43841-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="43841-330">servers/elasticpools</span></span> | <span data-ttu-id="43841-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="43841-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="43841-332">Définissez la modification du pool élastique.</span><span class="sxs-lookup"><span data-stu-id="43841-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="43841-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="43841-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="43841-334">Alias</span><span class="sxs-lookup"><span data-stu-id="43841-334">Alias</span></span> | <span data-ttu-id="43841-335">Description</span><span class="sxs-lookup"><span data-stu-id="43841-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="43841-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="43841-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="43841-337">Définissez le niveau d’accès utilisé pour la facturation.</span><span class="sxs-lookup"><span data-stu-id="43841-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="43841-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="43841-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="43841-339">Définissez le nom de la référence SKU.</span><span class="sxs-lookup"><span data-stu-id="43841-339">Set the SKU name.</span></span> |
| <span data-ttu-id="43841-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="43841-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="43841-341">Définissez si le service chiffre les données lorsqu’elles sont stockées dans le service de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="43841-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="43841-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="43841-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="43841-343">Définissez si le service chiffre les données lorsqu’elles sont stockées dans le service de stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="43841-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="43841-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="43841-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="43841-345">Définissez le nom de la référence SKU.</span><span class="sxs-lookup"><span data-stu-id="43841-345">Set the SKU name.</span></span> |
| <span data-ttu-id="43841-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="43841-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="43841-347">Indiquez que seul le trafic https est autorisé vers le service de stockage.</span><span class="sxs-lookup"><span data-stu-id="43841-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="43841-348">Exemples de stratégies</span><span class="sxs-lookup"><span data-stu-id="43841-348">Policy examples</span></span>

<span data-ttu-id="43841-349">Les rubriques suivantes contiennent des exemples de stratégies :</span><span class="sxs-lookup"><span data-stu-id="43841-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="43841-350">Pour obtenir des exemples de stratégies de balises, consultez [Apply resource policies for tags](resource-manager-policy-tags.md) (Appliquer des stratégies de ressources pour les balises).</span><span class="sxs-lookup"><span data-stu-id="43841-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="43841-351">Pour obtenir des exemples de modèles d’affectation de noms et de texte, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="43841-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="43841-352">Pour obtenir des exemples de stratégies de balises, consultez [Apply resource policies to storage accounts](resource-manager-policy-storage.md) (Appliquer des stratégies de ressources aux comptes de stockage).</span><span class="sxs-lookup"><span data-stu-id="43841-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="43841-353">Pour obtenir des exemples de stratégies de machine virtuelle, consultez [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) (Appliquer des stratégies de ressources aux machines virtuelles Linux) et [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) (Appliquer des stratégies de ressources aux machines virtuelles Windows).</span><span class="sxs-lookup"><span data-stu-id="43841-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="43841-354">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43841-354">Next steps</span></span>
* <span data-ttu-id="43841-355">Après avoir défini une règle de stratégie, affectez-la à une étendue.</span><span class="sxs-lookup"><span data-stu-id="43841-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="43841-356">Pour affecter des stratégies via le portail, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43841-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="43841-357">Pour affecter des stratégies via l’API REST, PowerShell ou Azure CLI, consultez [Affecter et gérer des stratégies via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="43841-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="43841-358">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="43841-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="43841-359">Le schéma de stratégie est publié à l’adresse [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="43841-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

