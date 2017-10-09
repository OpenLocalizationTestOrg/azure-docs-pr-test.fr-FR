---
title: "stratégies de ressources aaaAzure pour les conventions d’affectation de noms | Documents Microsoft"
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="3a590-103">Appliquer des stratégies de ressources pour les noms et le texte</span><span class="sxs-lookup"><span data-stu-id="3a590-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="3a590-104">Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) vous pouvez appliquer des conventions d’affectation de noms et le texte de tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3a590-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="3a590-105">Ces stratégies garantissent la cohérence des noms de ressources et des valeurs de balise.</span><span class="sxs-lookup"><span data-stu-id="3a590-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="3a590-106">Définir une convention d’affectation de noms avec un caractère générique</span><span class="sxs-lookup"><span data-stu-id="3a590-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="3a590-107">exemple Hello présente utilisez hello de caractère générique, ce qui est pris en charge par hello **comme** condition.</span><span class="sxs-lookup"><span data-stu-id="3a590-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="3a590-108">Hello condition stipule que si hello nom correspond au modèle mentionné de hello (namePrefix\*nameSuffix) puis refuser la demande de hello :</span><span class="sxs-lookup"><span data-stu-id="3a590-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="3a590-109">Définir une convention d’affectation de noms avec un modèle</span><span class="sxs-lookup"><span data-stu-id="3a590-109">Set naming convention with pattern</span></span>

<span data-ttu-id="3a590-110">toospecify que les noms des ressources correspondent à un modèle, utilisez hello correspondent à la condition.</span><span class="sxs-lookup"><span data-stu-id="3a590-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="3a590-111">exemple Hello nécessite toostart de noms avec `contoso` et contenir des six lettres supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="3a590-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="3a590-112">Définir le modèle de date pour la valeur de balise</span><span class="sxs-lookup"><span data-stu-id="3a590-112">Set date pattern for tag value</span></span>

<span data-ttu-id="3a590-113">toorequire un modèle de date de deux chiffres, tiret, trois lettres, tiret et quatre chiffres, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3a590-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3a590-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a590-114">Next steps</span></span>
* <span data-ttu-id="3a590-115">Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue.</span><span class="sxs-lookup"><span data-stu-id="3a590-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="3a590-116">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="3a590-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="3a590-117">stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3a590-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="3a590-118">stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="3a590-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="3a590-119">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3a590-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

