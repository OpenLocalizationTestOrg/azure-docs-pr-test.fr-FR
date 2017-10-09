---
title: "stratégies de ressources aaaAzure pour les balises | Documents Microsoft"
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
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="24fb2-103">Appliquer des stratégies de ressources pour les balises</span><span class="sxs-lookup"><span data-stu-id="24fb2-103">Apply resource policies for tags</span></span>

<span data-ttu-id="24fb2-104">Cette rubrique fournit une stratégie commune de règles que vous pouvez appliquer tooensure une utilisation cohérente de balises de ressources.</span><span class="sxs-lookup"><span data-stu-id="24fb2-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="24fb2-105">Application d’un abonnement à des ressources existantes ou groupe de ressources de balise stratégie tooa ne s’appliquent pas rétroactivement toothose ressources de la stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="24fb2-106">stratégies de hello tooenforce sur ces ressources, déclencher un toohello de mise à jour de ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="24fb2-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="24fb2-107">Cet article comprend un exemple PowerShell de déclenchement d’une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="24fb2-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="24fb2-108">Vérifier que toutes les ressources d’un groupe de ressources ont une balise / valeur</span><span class="sxs-lookup"><span data-stu-id="24fb2-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="24fb2-109">Il est souvent exigé que toutes les ressources d’un groupe de ressources aient une valeur et une balise particulières.</span><span class="sxs-lookup"><span data-stu-id="24fb2-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="24fb2-110">Cette exigence est souvent nécessaire tootrack les coûts par département.</span><span class="sxs-lookup"><span data-stu-id="24fb2-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="24fb2-111">Hello conditions suivantes doit être remplie :</span><span class="sxs-lookup"><span data-stu-id="24fb2-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="24fb2-112">Hello requis balise valeur toonew ajouté et sont mis à jour des ressources qui n’ont pas de balise de hello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="24fb2-113">balise obligatoire de Hello et valeur ne peut pas être supprimée à partir de toutes les ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="24fb2-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="24fb2-114">Vous satisfaire cette exigence en appliquant le groupe de ressources de deux stratégies intégrées tooa.</span><span class="sxs-lookup"><span data-stu-id="24fb2-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="24fb2-115">ID</span><span class="sxs-lookup"><span data-stu-id="24fb2-115">ID</span></span> | <span data-ttu-id="24fb2-116">Description</span><span class="sxs-lookup"><span data-stu-id="24fb2-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="24fb2-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="24fb2-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="24fb2-118">Applique une balise requise et sa valeur par défaut lorsqu’il n’est pas spécifié par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="24fb2-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="24fb2-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="24fb2-120">Applique une balise requise et sa valeur.</span><span class="sxs-lookup"><span data-stu-id="24fb2-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="24fb2-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24fb2-121">PowerShell</span></span>

<span data-ttu-id="24fb2-122">Hello PowerShell script suivant affecte le groupe de ressources tooa hello stratégie intégrée deux définitions.</span><span class="sxs-lookup"><span data-stu-id="24fb2-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="24fb2-123">Avant d’exécuter le script de hello, affecter le groupe de ressources de toutes les balises nécessaires toohello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="24fb2-124">Chaque balise de groupe de ressources hello est requis pour les ressources hello dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="24fb2-125">groupes de ressources tooassign tooall dans votre abonnement, ne fournissent pas hello `-Name` paramètre lors de l’obtention des groupes de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="24fb2-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

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

<span data-ttu-id="24fb2-126">Après avoir affecté les stratégies hello, vous pouvez déclencher un tooall de mise à jour existant ressources tooenforce hello balise des stratégies que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="24fb2-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="24fb2-127">Hello script suivant conserve toutes les autres balises qui existaient sur les ressources hello :</span><span class="sxs-lookup"><span data-stu-id="24fb2-127">hello following script retains any other tags that existed on hello resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="24fb2-128">Exiger des balises pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="24fb2-128">Require tags for a resource type</span></span>
<span data-ttu-id="24fb2-129">Hello, l’exemple suivant montre comment la balise toonest opérateurs logiques toorequire une application pour un type de ressource spécifié (dans ce cas, comptes de stockage).</span><span class="sxs-lookup"><span data-stu-id="24fb2-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="24fb2-130">Exiger une balise</span><span class="sxs-lookup"><span data-stu-id="24fb2-130">Require tag</span></span>
<span data-ttu-id="24fb2-131">Hello stratégie suivant refuse les demandes qui n’ont pas une balise qui contient la clé « Centre de coût » (n’importe quelle valeur peut être appliquée) :</span><span class="sxs-lookup"><span data-stu-id="24fb2-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="24fb2-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24fb2-132">Next steps</span></span>
* <span data-ttu-id="24fb2-133">Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="24fb2-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="24fb2-134">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="24fb2-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="24fb2-135">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24fb2-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="24fb2-136">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="24fb2-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="24fb2-137">Pour un tooresource des stratégies de présentation, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="24fb2-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="24fb2-138">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="24fb2-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

