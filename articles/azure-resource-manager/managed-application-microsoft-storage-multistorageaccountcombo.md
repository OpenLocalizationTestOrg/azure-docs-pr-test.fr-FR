---
title: "Élément d’interface utilisateur MultiStorageAccountCombo des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur MultiStorageAccountCombo pour les applications gérées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="78a17-103">Élément d’interface utilisateur Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="78a17-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="78a17-104">Groupe de contrôles pour la création de plusieurs comptes de stockage, avec des noms commençant par un préfixe commun.</span><span class="sxs-lookup"><span data-stu-id="78a17-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="78a17-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="78a17-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="78a17-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="78a17-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="78a17-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="78a17-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="78a17-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="78a17-109">Remarks</span></span>
- <span data-ttu-id="78a17-110">La valeur de `defaultValue.prefix` est concaténée avec un ou plusieurs entiers pour générer la séquence de noms de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="78a17-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="78a17-111">Par exemple, si `defaultValue.prefix` est **foobar** et `count` est **2**, les noms de comptes de stockage **foobar1** et **foobar2** sont générés.</span><span class="sxs-lookup"><span data-stu-id="78a17-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="78a17-112">Le caractère unique des noms de comptes de stockage générés est validé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="78a17-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="78a17-113">Les noms de comptes de stockage sont générés lexicographiquement en se basant sur `count`.</span><span class="sxs-lookup"><span data-stu-id="78a17-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="78a17-114">Par exemple, si `count` est égal à 10, les noms de comptes de stockage se terminent par des entiers à 2 chiffres (01, 02, 03, etc..).</span><span class="sxs-lookup"><span data-stu-id="78a17-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="78a17-115">La valeur par défaut pour `defaultValue.prefix` est égale à **null** et pour `defaultValue.type` équivaut à **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="78a17-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="78a17-116">Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="78a17-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="78a17-117">`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="78a17-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="78a17-118">En plus de générer des noms de comptes de stockage, `count` est utilisé pour définir le multiplicateur approprié pour l’élément.</span><span class="sxs-lookup"><span data-stu-id="78a17-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="78a17-119">Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="78a17-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="78a17-120">La valeur par défaut est **1**.</span><span class="sxs-lookup"><span data-stu-id="78a17-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="78a17-121">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="78a17-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="78a17-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78a17-122">Next steps</span></span>
* <span data-ttu-id="78a17-123">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78a17-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="78a17-124">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78a17-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="78a17-125">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="78a17-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
