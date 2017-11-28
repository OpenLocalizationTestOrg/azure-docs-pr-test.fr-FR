---
title: "Stratégies de ressources Azure pour les balises | Microsoft Docs"
description: "Fournit des exemples de stratégies de ressources pour gérer les balises sur les ressources."
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="90f21-103">Appliquer des stratégies de ressources pour les balises</span><span class="sxs-lookup"><span data-stu-id="90f21-103">Apply resource policies for tags</span></span>

<span data-ttu-id="90f21-104">Cette rubrique fournit des règles de stratégie courantes que vous pouvez appliquer pour garantir une utilisation cohérente des balises sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="90f21-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="90f21-105">Le fait d’appliquer une stratégie de balise à un groupe de ressources ou à un abonnement contenant des ressources n’applique pas rétroactivement la stratégie à ces ressources.</span><span class="sxs-lookup"><span data-stu-id="90f21-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="90f21-106">Pour appliquer les stratégies à ces ressources, déclenchez une mise à jour des ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="90f21-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="90f21-107">Cet article comprend un exemple PowerShell de déclenchement d’une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="90f21-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="90f21-108">Vérifier que toutes les ressources d’un groupe de ressources ont une balise / valeur</span><span class="sxs-lookup"><span data-stu-id="90f21-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="90f21-109">Il est souvent exigé que toutes les ressources d’un groupe de ressources aient une valeur et une balise particulières.</span><span class="sxs-lookup"><span data-stu-id="90f21-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="90f21-110">Cette exigence est souvent nécessaire pour effectuer le suivi des coûts par département.</span><span class="sxs-lookup"><span data-stu-id="90f21-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="90f21-111">Les conditions suivantes doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="90f21-111">The following conditions must be met:</span></span>

* <span data-ttu-id="90f21-112">La balise et la valeur requises sont ajoutées à des ressources nouvelles et mises à jour qui ne possèdent pas de balises.</span><span class="sxs-lookup"><span data-stu-id="90f21-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="90f21-113">Il n’est pas possible de supprimer la balise et la valeur requises des ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="90f21-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="90f21-114">Pour respecter ces exigences, vous devez appliquer à un groupe de ressources deux stratégies intégrées.</span><span class="sxs-lookup"><span data-stu-id="90f21-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="90f21-115">ID</span><span class="sxs-lookup"><span data-stu-id="90f21-115">ID</span></span> | <span data-ttu-id="90f21-116">Description</span><span class="sxs-lookup"><span data-stu-id="90f21-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="90f21-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="90f21-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="90f21-118">Applique une balise requise et sa valeur par défaut lorsqu’elle n’est pas spécifiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90f21-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="90f21-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="90f21-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="90f21-120">Applique une balise requise et sa valeur.</span><span class="sxs-lookup"><span data-stu-id="90f21-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="90f21-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90f21-121">PowerShell</span></span>

<span data-ttu-id="90f21-122">Le script PowerShell suivant affecte les deux définitions de stratégies intégrées à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="90f21-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="90f21-123">Avant d’exécuter le script, affectez toutes les balises requises au groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="90f21-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="90f21-124">Chaque balise du groupe de ressources est requise pour les ressources contenues dans le groupe.</span><span class="sxs-lookup"><span data-stu-id="90f21-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="90f21-125">Pour les affecter à tous les groupes de ressources de votre abonnement, n’indiquez pas le paramètre `-Name` lorsque vous récupérez les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="90f21-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="90f21-126">Après avoir attribué les stratégies, vous pouvez déclencher une mise à jour sur toutes les ressources existantes pour appliquer les stratégies de balise que vous avez ajoutées.</span><span class="sxs-lookup"><span data-stu-id="90f21-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="90f21-127">Le script suivant conserve toutes les autres balises existant sur les ressources :</span><span class="sxs-lookup"><span data-stu-id="90f21-127">The following script retains any other tags that existed on the resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="90f21-128">Exiger des balises pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="90f21-128">Require tags for a resource type</span></span>
<span data-ttu-id="90f21-129">L’exemple suivant montre comment imbriquer des opérateurs logiques afin d’exiger une balise d’application pour un certain type de ressources seulement (dans ce cas, les comptes de stockage).</span><span class="sxs-lookup"><span data-stu-id="90f21-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
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
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="90f21-130">Exiger une balise</span><span class="sxs-lookup"><span data-stu-id="90f21-130">Require tag</span></span>
<span data-ttu-id="90f21-131">La stratégie suivante refuse les demandes dépourvues de balise contenant la clé « costCenter » (toutes les valeurs peuvent être appliquées) :</span><span class="sxs-lookup"><span data-stu-id="90f21-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="90f21-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90f21-132">Next steps</span></span>
* <span data-ttu-id="90f21-133">Après avoir défini une règle de stratégie (comme le montrent les exemples précédents), vous devez créer la définition de stratégie et l’attribuer à une étendue.</span><span class="sxs-lookup"><span data-stu-id="90f21-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="90f21-134">L’étendue peut être un abonnement, un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="90f21-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="90f21-135">Pour affecter des stratégies via le portail, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90f21-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="90f21-136">Pour affecter des stratégies via l’API REST, PowerShell ou Azure CLI, consultez [Affecter et gérer des stratégies via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="90f21-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="90f21-137">Pour une introduction aux stratégies de ressources, consultez la page [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="90f21-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="90f21-138">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="90f21-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

