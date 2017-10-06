---
title: "stratégies de ressources aaaAzure | Documents Microsoft"
description: "Décrit comment les propriétés de ressource cohérent tooensure toouse Azure Resource Manager stratégies sont définies au cours du déploiement. Les stratégies peuvent être appliquées à des groupes d’abonnement ou une ressource hello."
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="c1fb8-104">Vue d’ensemble des stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="c1fb8-104">Resource policy overview</span></span>
<span data-ttu-id="c1fb8-105">Stratégies de ressources permettent de conventions tooestablish pour les ressources de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="c1fb8-106">En définissant des conventions, vous pouvez contrôler les coûts et gérer plus facilement vos ressources.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="c1fb8-107">Par exemple, vous pouvez spécifier que seuls certains types de machines virtuelles sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="c1fb8-108">Vous pouvez aussi exiger que toutes les ressources soient marquées.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="c1fb8-109">Toutes les ressources enfants héritent des stratégies.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="c1fb8-110">Donc, si une stratégie est un groupe de ressources appliquée tooa, ressources de hello tooall applicable dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="c1fb8-111">Il existe deux concepts toounderstand, sur les stratégies :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="c1fb8-112">définition de stratégie - décrivent lorsque hello appliquée et le tootake d’action</span><span class="sxs-lookup"><span data-stu-id="c1fb8-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="c1fb8-113">attribution de stratégie - que vous appliquez étendue tooa définition hello de stratégie (abonnement ou groupe de ressources)</span><span class="sxs-lookup"><span data-stu-id="c1fb8-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="c1fb8-114">Cette rubrique porte sur la définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="c1fb8-115">Pour plus d’informations sur l’attribution de stratégie, consultez [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md) ou [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="c1fb8-116">Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="c1fb8-117">Actuellement, la stratégie n’évalue pas les types de ressources qui ne prennent pas en charge les balises, type et emplacement, par exemple, type de ressource Microsoft.Resources/deployments hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="c1fb8-118">Cette prise en charge sera ajoutée prochainement.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-118">This support will be added at a future time.</span></span> <span data-ttu-id="c1fb8-119">tooavoid des problèmes de compatibilité descendante, vous devez spécifier explicitement le type lors de la création de stratégies.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="c1fb8-120">Par exemple, une stratégie de balises sans spécification des types est appliquée à tous les types.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="c1fb8-121">Dans ce cas, un déploiement de modèle peut échouer s’il existe une ressource imbriquée qui ne prennent pas en charge les balises, et type de ressource de déploiement hello a été ajouté à l’évaluation toopolicy.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="c1fb8-122">Quelle est la différence avec RBAC ?</span><span class="sxs-lookup"><span data-stu-id="c1fb8-122">How is it different from RBAC?</span></span>
<span data-ttu-id="c1fb8-123">Il existe quelques différences importantes entre la stratégie et le contrôle d’accès en fonction du rôle (RBAC).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="c1fb8-124">RBAC porte sur les actions des **utilisateurs** dans différentes étendues.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="c1fb8-125">Par exemple, vous sont ajoutés toohello rôle de collaborateur pour un groupe de ressources de la portée de hello souhaité pour vous permettre de groupe de ressources toothat de modifications.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="c1fb8-126">La stratégie se focalise sur les propriétés des **ressources** pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="c1fb8-127">Par exemple, via des stratégies, vous pouvez contrôler les types de hello des ressources qui peuvent être configurées.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="c1fb8-128">Ou bien, vous pouvez restreindre les emplacements de hello dans lequel les ressources hello peuvent être configurés.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="c1fb8-129">Contrairement à RBAC, la stratégie est, par défaut, un système explicite d'autorisation et de refus.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="c1fb8-130">stratégies de toouse, vous devez être authentifié au moyen de RBAC.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="c1fb8-131">Plus précisément, votre compte a besoin de :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="c1fb8-132">`Microsoft.Authorization/policydefinitions/write`autorisation toodefine une stratégie</span><span class="sxs-lookup"><span data-stu-id="c1fb8-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="c1fb8-133">`Microsoft.Authorization/policyassignments/write`autorisation tooassign une stratégie</span><span class="sxs-lookup"><span data-stu-id="c1fb8-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="c1fb8-134">Ces autorisations ne sont pas incluses dans hello **collaborateur** rôle.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="c1fb8-135">Stratégies prédéfinies</span><span class="sxs-lookup"><span data-stu-id="c1fb8-135">Built-in policies</span></span>

<span data-ttu-id="c1fb8-136">Azure fournit des définitions de stratégie intégrée qui peuvent réduire hello nombre de stratégies, vous avez toodefine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="c1fb8-137">Avant de procéder à des définitions de stratégie, vous devez envisager si une stratégie intégrée fournit déjà définition hello que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="c1fb8-138">les définitions de stratégie intégrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="c1fb8-139">Emplacements autorisés</span><span class="sxs-lookup"><span data-stu-id="c1fb8-139">Allowed locations</span></span>
* <span data-ttu-id="c1fb8-140">Types de ressources autorisés</span><span class="sxs-lookup"><span data-stu-id="c1fb8-140">Allowed resource types</span></span>
* <span data-ttu-id="c1fb8-141">Références SKU de compte de stockage autorisées</span><span class="sxs-lookup"><span data-stu-id="c1fb8-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="c1fb8-142">Références SKU de machine virtuelle autorisées</span><span class="sxs-lookup"><span data-stu-id="c1fb8-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="c1fb8-143">Appliquer la valeur par défaut et la balise</span><span class="sxs-lookup"><span data-stu-id="c1fb8-143">Apply tag and default value</span></span>
* <span data-ttu-id="c1fb8-144">Appliquer une balise et une valeur</span><span class="sxs-lookup"><span data-stu-id="c1fb8-144">Enforce tag and value</span></span>
* <span data-ttu-id="c1fb8-145">Types de ressources non autorisés</span><span class="sxs-lookup"><span data-stu-id="c1fb8-145">Not allowed resource types</span></span>
* <span data-ttu-id="c1fb8-146">Nécessitent SQL Server version 12.0</span><span class="sxs-lookup"><span data-stu-id="c1fb8-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="c1fb8-147">Nécessitent le chiffrement du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="c1fb8-147">Require storage account encryption</span></span>

<span data-ttu-id="c1fb8-148">Vous pouvez affecter une de ces stratégies via hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), ou [CLI d’Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="c1fb8-149">Structure de la définition de stratégie</span><span class="sxs-lookup"><span data-stu-id="c1fb8-149">Policy definition structure</span></span>
<span data-ttu-id="c1fb8-150">Vous utilisez JSON toocreate une définition de stratégie.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="c1fb8-151">définition de stratégie Hello contient les éléments de :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="c1fb8-152">parameters</span><span class="sxs-lookup"><span data-stu-id="c1fb8-152">parameters</span></span>
* <span data-ttu-id="c1fb8-153">le nom d’affichage</span><span class="sxs-lookup"><span data-stu-id="c1fb8-153">display name</span></span>
* <span data-ttu-id="c1fb8-154">description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-154">description</span></span>
* <span data-ttu-id="c1fb8-155">la règle de stratégie</span><span class="sxs-lookup"><span data-stu-id="c1fb8-155">policy rule</span></span>
  * <span data-ttu-id="c1fb8-156">évaluation logique</span><span class="sxs-lookup"><span data-stu-id="c1fb8-156">logical evaluation</span></span>
  * <span data-ttu-id="c1fb8-157">effet</span><span class="sxs-lookup"><span data-stu-id="c1fb8-157">effect</span></span>

<span data-ttu-id="c1fb8-158">Hello, l’exemple suivant illustre une stratégie qui limite où vous déployez des ressources :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="c1fb8-159">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c1fb8-159">Parameters</span></span>
<span data-ttu-id="c1fb8-160">À l’aide des paramètres permet de simplifier la gestion de stratégie en réduisant le nombre de hello de définitions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="c1fb8-161">Vous définissez une stratégie pour une propriété de ressource (par exemple, la limitation des emplacements de hello où les ressources peuvent être déployés) et incluez des paramètres dans la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="c1fb8-162">Ensuite, vous réutilisez cette définition de stratégie pour différents scénarios en passant des valeurs différentes (par exemple, la spécification d’un ensemble d’emplacements pour un abonnement) lorsque attribution de stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="c1fb8-163">Vous déclarez des paramètres lorsque vous créez des définitions de stratégies.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="c1fb8-164">type Hello d’un paramètre peut être une chaîne ou le tableau.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="c1fb8-165">propriété de métadonnées Hello est utilisée pour les outils, tels que les informations conviviales toodisplay portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="c1fb8-166">Dans la règle de stratégie hello, vous faites référence aux paramètres hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="c1fb8-167">Nom d’affichage et description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-167">Display name and description</span></span>

<span data-ttu-id="c1fb8-168">Vous utilisez hello **displayName** et **description** tooidentify hello de définition de la stratégie et fournissent un contexte pour lorsqu’il est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="c1fb8-169">Règle de stratégie</span><span class="sxs-lookup"><span data-stu-id="c1fb8-169">Policy rule</span></span>

<span data-ttu-id="c1fb8-170">règle de stratégie Hello se compose de **si** et **puis** blocs.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="c1fb8-171">Bonjour **si** bloc, vous définissez une ou plusieurs conditions qui spécifient quand la stratégie de hello est appliquée.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="c1fb8-172">Vous pouvez appliquer des conditions de toothese d’opérateurs logiques tooprecisely définir scénario hello pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="c1fb8-173">Bonjour **puis** bloc, vous définissez effet hello lorsque hello **si** conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="c1fb8-174">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="c1fb8-174">Logical operators</span></span>
<span data-ttu-id="c1fb8-175">les opérateurs logiques Hello pris en charge sont :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="c1fb8-176">Hello **pas** syntaxe inverse le résultat de hello de condition de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="c1fb8-177">Hello **tous** syntaxe (toohello similaire logique **et** opération) nécessite le vrai de toobe toutes les conditions.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="c1fb8-178">Hello **anyOf** syntaxe (toohello similaire logique **ou** opération) nécessite un ou plusieurs conditions toobe la valeur true.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="c1fb8-179">Vous pouvez imbriquer des opérateurs logiques.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-179">You can nest logical operators.</span></span> <span data-ttu-id="c1fb8-180">Hello suivant montre l’exemple un **pas** opération qui est imbriquée dans une **tous** opération.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="c1fb8-181">Conditions</span><span class="sxs-lookup"><span data-stu-id="c1fb8-181">Conditions</span></span>
<span data-ttu-id="c1fb8-182">condition de Hello évalue si un **champ** répond à certains critères.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="c1fb8-183">conditions de Hello pris en charge sont :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="c1fb8-184">Lorsque vous utilisez hello **comme** condition, vous pouvez fournir un caractère générique (*) dans la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="c1fb8-185">Lorsque vous utilisez hello **correspond à** de condition, fournir `#` toorepresent un chiffre, `?` pour une lettre, ainsi que tout autre caractère toorepresent ce caractère réel.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="c1fb8-186">Pour obtenir des exemples, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="c1fb8-187">Champs</span><span class="sxs-lookup"><span data-stu-id="c1fb8-187">Fields</span></span>
<span data-ttu-id="c1fb8-188">Les conditions sont formées à partir de champs.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="c1fb8-189">Un champ représente des propriétés dans la charge utile de demande hello ressource qui est utilisé toodescribe hello état de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="c1fb8-190">Hello champs qui suivent est pris en charge :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="c1fb8-191">alias de propriété : pour en obtenir la liste, consultez [Alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="c1fb8-192">Résultat</span><span class="sxs-lookup"><span data-stu-id="c1fb8-192">Effect</span></span>
<span data-ttu-id="c1fb8-193">La stratégie prend en charge trois types d’effet : `deny`, `audit` et `append`.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="c1fb8-194">**Refuser** génère un événement dans le journal d’audit de hello et faire échouer hello demande</span><span class="sxs-lookup"><span data-stu-id="c1fb8-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="c1fb8-195">**Audit** génère un événement d’avertissement dans le journal d’audit, mais n’échoue pas de demande de hello</span><span class="sxs-lookup"><span data-stu-id="c1fb8-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="c1fb8-196">**Ajouter** ajoute ensemble hello défini de champs toohello demande</span><span class="sxs-lookup"><span data-stu-id="c1fb8-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="c1fb8-197">Pour **ajouter**, vous devez fournir hello les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="c1fb8-198">valeur de Hello peut être une chaîne ou un objet du format JSON.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="c1fb8-199">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-199">Aliases</span></span>

<span data-ttu-id="c1fb8-200">Vous utilisez des alias tooaccess spécifique de propriétés pour un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="c1fb8-201">Les alias autorisent toorestrict les conditions ou les valeurs autorisées pour une propriété sur une ressource.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="c1fb8-202">Chaque alias mappe toopaths dans les différentes versions d’API pour un type de ressource donné.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="c1fb8-203">Lors de l’évaluation de stratégie, moteur de stratégie hello Obtient le chemin d’accès de propriété hello pour cette version de l’API.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="c1fb8-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="c1fb8-205">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-205">Alias</span></span> | <span data-ttu-id="c1fb8-206">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="c1fb8-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="c1fb8-208">La valeur indique si de port du serveur de Redis de non-ssl hello (6379) est activée.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="c1fb8-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="c1fb8-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="c1fb8-210">Définir nombre hello de toobe de partitions créée sur un Cache de Cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="c1fb8-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="c1fb8-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="c1fb8-212">Définir la taille hello de hello Redis cache toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="c1fb8-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="c1fb8-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="c1fb8-214">Valeur toouse de famille hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="c1fb8-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="c1fb8-216">Définir le type hello du Cache Redis toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="c1fb8-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="c1fb8-218">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-218">Alias</span></span> | <span data-ttu-id="c1fb8-219">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="c1fb8-221">Hello le nom du niveau tarifaire de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="c1fb8-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="c1fb8-223">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-223">Alias</span></span> | <span data-ttu-id="c1fb8-224">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="c1fb8-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="c1fb8-226">Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="c1fb8-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="c1fb8-228">Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="c1fb8-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="c1fb8-230">Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="c1fb8-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="c1fb8-232">Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="c1fb8-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="c1fb8-234">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-234">Alias</span></span> | <span data-ttu-id="c1fb8-235">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="c1fb8-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="c1fb8-237">Définir l’identificateur hello de machine virtuelle de hello image utilisée toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="c1fb8-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="c1fb8-239">Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="c1fb8-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="c1fb8-241">Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="c1fb8-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="c1fb8-243">Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="c1fb8-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="c1fb8-245">Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="c1fb8-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="c1fb8-247">Définir cette image hello ou disque local sous licence.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="c1fb8-248">Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation de serveur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="c1fb8-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="c1fb8-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="c1fb8-250">Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="c1fb8-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="c1fb8-252">Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="c1fb8-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="c1fb8-254">Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="c1fb8-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="c1fb8-256">Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="c1fb8-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="c1fb8-258">Définir le disque dur virtuel hello URI.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="c1fb8-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="c1fb8-260">Définir la taille hello de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="c1fb8-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="c1fb8-262">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-262">Alias</span></span> | <span data-ttu-id="c1fb8-263">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="c1fb8-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="c1fb8-265">Hello le nom du serveur de publication de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="c1fb8-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="c1fb8-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="c1fb8-267">Définir le type hello d’extension.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="c1fb8-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="c1fb8-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="c1fb8-269">Définissez la version hello d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="c1fb8-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="c1fb8-271">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-271">Alias</span></span> | <span data-ttu-id="c1fb8-272">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="c1fb8-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="c1fb8-274">Définir l’identificateur hello de machine virtuelle de hello image utilisée toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="c1fb8-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="c1fb8-276">Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="c1fb8-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="c1fb8-278">Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="c1fb8-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="c1fb8-280">Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="c1fb8-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="c1fb8-282">Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="c1fb8-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="c1fb8-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="c1fb8-284">Définir cette image hello ou disque local sous licence.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="c1fb8-285">Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation de serveur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="c1fb8-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="c1fb8-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="c1fb8-287">Définir le préfixe du nom d’ordinateur hello pour tous les ordinateurs virtuels hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="c1fb8-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="c1fb8-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="c1fb8-289">Ensemble hello URI d’objet blob d’image de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="c1fb8-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="c1fb8-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="c1fb8-291">Définir les URL du conteneur hello qui sont des disques de système d’exploitation toostore utilisé pour l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="c1fb8-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="c1fb8-293">Définir la taille hello des machines virtuelles dans un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="c1fb8-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="c1fb8-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="c1fb8-295">Définir le niveau hello des ordinateurs virtuels dans un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="c1fb8-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="c1fb8-297">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-297">Alias</span></span> | <span data-ttu-id="c1fb8-298">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="c1fb8-300">Définir la taille hello de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="c1fb8-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="c1fb8-302">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-302">Alias</span></span> | <span data-ttu-id="c1fb8-303">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="c1fb8-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="c1fb8-305">Valeur de type hello de cette passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="c1fb8-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="c1fb8-307">Définir le nom de référence (SKU) de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="c1fb8-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="c1fb8-309">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-309">Alias</span></span> | <span data-ttu-id="c1fb8-310">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="c1fb8-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="c1fb8-312">Définissez la version hello du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="c1fb8-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="c1fb8-314">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-314">Alias</span></span> | <span data-ttu-id="c1fb8-315">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="c1fb8-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="c1fb8-317">Définir edition hello de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="c1fb8-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="c1fb8-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="c1fb8-319">Nom de base de données hello pool élastique hello hello est dans.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="c1fb8-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="c1fb8-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="c1fb8-321">Ensemble hello configuré ID objectif de niveau de service de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="c1fb8-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="c1fb8-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="c1fb8-323">Nom du jeu hello Hello configuré objectif de niveau de service de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="c1fb8-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="c1fb8-325">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-325">Alias</span></span> | <span data-ttu-id="c1fb8-326">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="c1fb8-327">servers/elasticpools</span></span> | <span data-ttu-id="c1fb8-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="c1fb8-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="c1fb8-329">Nombre total de SET hello partagé DTU pour le pool élastique de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="c1fb8-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="c1fb8-330">servers/elasticpools</span></span> | <span data-ttu-id="c1fb8-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="c1fb8-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="c1fb8-332">Définir edition hello du pool élastique de hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="c1fb8-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="c1fb8-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="c1fb8-334">Alias</span><span class="sxs-lookup"><span data-stu-id="c1fb8-334">Alias</span></span> | <span data-ttu-id="c1fb8-335">Description</span><span class="sxs-lookup"><span data-stu-id="c1fb8-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="c1fb8-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="c1fb8-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="c1fb8-337">Niveau d’accès hello jeu utilisé pour la facturation.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="c1fb8-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="c1fb8-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="c1fb8-339">Définir le nom de référence (SKU) hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="c1fb8-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="c1fb8-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="c1fb8-341">Définir si le service de hello chiffre les données de hello tel qu’il est stocké dans le service de stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="c1fb8-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="c1fb8-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="c1fb8-343">Définir si le service de hello chiffre les données de hello tel qu’il est stocké dans le service de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="c1fb8-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="c1fb8-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="c1fb8-345">Définir le nom de référence (SKU) hello.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="c1fb8-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="c1fb8-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="c1fb8-347">Définir les https uniquement tooallow service toostorage du trafic.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="c1fb8-348">Exemples de stratégies</span><span class="sxs-lookup"><span data-stu-id="c1fb8-348">Policy examples</span></span>

<span data-ttu-id="c1fb8-349">Hello rubriques suivantes contiennent des exemples de stratégie :</span><span class="sxs-lookup"><span data-stu-id="c1fb8-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="c1fb8-350">Pour obtenir des exemples de stratégies de balises, consultez [Apply resource policies for tags](resource-manager-policy-tags.md) (Appliquer des stratégies de ressources pour les balises).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="c1fb8-351">Pour obtenir des exemples de modèles d’affectation de noms et de texte, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="c1fb8-352">Pour obtenir des exemples de stratégies de stockage, consultez [appliquer les comptes de ressources stratégies toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="c1fb8-353">Pour obtenir des exemples de stratégies de l’ordinateur virtuel, consultez [appliquer des stratégies de ressources tooLinux machines virtuelles](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) et [appliquer des stratégies de ressources tooWindows machines virtuelles](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c1fb8-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1fb8-354">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1fb8-354">Next steps</span></span>
* <span data-ttu-id="c1fb8-355">Après avoir défini une règle de stratégie, attribuez-lui tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="c1fb8-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="c1fb8-356">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c1fb8-357">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="c1fb8-358">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="c1fb8-359">schéma de stratégie Hello est publiée à [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="c1fb8-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

