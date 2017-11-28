---
title: "Stratégies de ressources Azure pour les conventions d’affectation de noms | Microsoft Docs"
description: "Décrit les stratégies Azure Resource Manager pour les conventions d’affectation de noms des ressources."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="a24f4-103">Appliquer des stratégies de ressources pour les noms et le texte</span><span class="sxs-lookup"><span data-stu-id="a24f4-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="a24f4-104">Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) que vous pouvez appliquer pour établir des conventions d’affectation de noms et de texte.</span><span class="sxs-lookup"><span data-stu-id="a24f4-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="a24f4-105">Ces stratégies garantissent la cohérence des noms de ressources et des valeurs de balise.</span><span class="sxs-lookup"><span data-stu-id="a24f4-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="a24f4-106">Définir une convention d’affectation de noms avec un caractère générique</span><span class="sxs-lookup"><span data-stu-id="a24f4-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="a24f4-107">L’exemple suivant illustre l’utilisation de caractères génériques, grâce à la condition **like**.</span><span class="sxs-lookup"><span data-stu-id="a24f4-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="a24f4-108">La condition stipule que la demande est refusée si le nom ne correspond pas au modèle indiqué (namePrefix\*nameSuffix) :</span><span class="sxs-lookup"><span data-stu-id="a24f4-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="a24f4-109">Définir une convention d’affectation de noms avec un modèle</span><span class="sxs-lookup"><span data-stu-id="a24f4-109">Set naming convention with pattern</span></span>

<span data-ttu-id="a24f4-110">Utilisez la condition de correspondance pour indiquer que des noms de ressources correspondent à un modèle.</span><span class="sxs-lookup"><span data-stu-id="a24f4-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="a24f4-111">L’exemple suivant requiert que les noms commencent par `contoso` et contiennent six lettres supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="a24f4-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="a24f4-112">Définir le modèle de date pour la valeur de balise</span><span class="sxs-lookup"><span data-stu-id="a24f4-112">Set date pattern for tag value</span></span>

<span data-ttu-id="a24f4-113">Pour exiger l’utilisation d’un modèle de date à deux chiffres, tiret, trois lettres, tiret et quatre chiffres, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a24f4-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="a24f4-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a24f4-114">Next steps</span></span>
* <span data-ttu-id="a24f4-115">Après avoir défini une règle de stratégie (comme le montrent les exemples précédents), vous devez créer la définition de stratégie et l’attribuer à une étendue.</span><span class="sxs-lookup"><span data-stu-id="a24f4-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="a24f4-116">L’étendue peut être un abonnement, un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="a24f4-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="a24f4-117">Pour affecter des stratégies via le portail, consultez [Utiliser le portail Azure pour affecter et gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a24f4-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="a24f4-118">Pour affecter des stratégies via l’API REST, PowerShell ou Azure CLI, consultez [Affecter et gérer des stratégies via un script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="a24f4-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="a24f4-119">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a24f4-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

