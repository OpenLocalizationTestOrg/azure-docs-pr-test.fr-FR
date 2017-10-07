---
title: "élément de l’interface utilisateur de MultiStorageAccountCombo pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Storage.MultiStorageAccountCombo pour des Applications managées Azure"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="ecd71-103">Élément d’interface utilisateur Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="ecd71-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="ecd71-104">Groupe de contrôles pour la création de plusieurs comptes de stockage, avec des noms commençant par un préfixe commun.</span><span class="sxs-lookup"><span data-stu-id="ecd71-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="ecd71-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ecd71-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ecd71-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ecd71-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="ecd71-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="ecd71-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="ecd71-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="ecd71-109">Remarks</span></span>
- <span data-ttu-id="ecd71-110">Hello valeur pour `defaultValue.prefix` est concaténée avec une ou plusieurs entiers toogenerate hello séquence des noms de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ecd71-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="ecd71-111">Par exemple, si `defaultValue.prefix` est **foobar** et `count` est **2**, les noms de comptes de stockage **foobar1** et **foobar2** sont générés.</span><span class="sxs-lookup"><span data-stu-id="ecd71-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="ecd71-112">Le caractère unique des noms de comptes de stockage générés est validé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ecd71-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="ecd71-113">noms de compte de stockage Hello sont générés lexicographique en fonction `count`.</span><span class="sxs-lookup"><span data-stu-id="ecd71-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="ecd71-114">Par exemple, si `count` est 10, puis les noms de compte de stockage hello se terminent par des entiers de 2 chiffres (01, 02, 03, etc..).</span><span class="sxs-lookup"><span data-stu-id="ecd71-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="ecd71-115">Hello la valeur par défaut de `defaultValue.prefix` est **null**et pour `defaultValue.type` est **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="ecd71-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="ecd71-116">Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ecd71-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="ecd71-117">`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="ecd71-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="ecd71-118">Dans les noms de compte de stockage toogenerating de plus, `count` est tooset utilisé le multiplicateur approprié pour l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd71-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="ecd71-119">Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="ecd71-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="ecd71-120">la valeur par défaut Hello est **1**.</span><span class="sxs-lookup"><span data-stu-id="ecd71-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ecd71-121">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="ecd71-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="ecd71-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecd71-122">Next steps</span></span>
* <span data-ttu-id="ecd71-123">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecd71-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ecd71-124">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecd71-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ecd71-125">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ecd71-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
