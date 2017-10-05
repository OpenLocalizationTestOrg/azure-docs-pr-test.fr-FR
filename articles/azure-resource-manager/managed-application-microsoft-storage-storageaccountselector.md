---
title: "Élément d’interface utilisateur StorageAccountSelector des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Storage.StorageAccountSelector pour les applications gérées Azure"
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="9cae1-103">Élément d’interface utilisateur Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="9cae1-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="9cae1-104">Contrôle permettant de sélectionner un compte de stockage nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="9cae1-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="9cae1-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9cae1-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9cae1-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="9cae1-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="9cae1-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="9cae1-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9cae1-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="9cae1-109">Remarks</span></span>
- <span data-ttu-id="9cae1-110">S’il est spécifié, le caractère unique de `defaultValue.name` est automatiquement validé.</span><span class="sxs-lookup"><span data-stu-id="9cae1-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="9cae1-111">Si le nom de compte de stockage n’est pas unique, l’utilisateur doit indiquer un autre nom ou choisir un compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="9cae1-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="9cae1-112">La valeur par défaut pour `defaultValue.type` est **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="9cae1-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="9cae1-113">Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9cae1-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="9cae1-114">`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="9cae1-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="9cae1-115">Si `options.hideExisting` est défini sur **true**, l’utilisateur ne peut pas choisir de compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="9cae1-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="9cae1-116">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="9cae1-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="9cae1-117">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="9cae1-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="9cae1-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9cae1-118">Next steps</span></span>
* <span data-ttu-id="9cae1-119">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cae1-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9cae1-120">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cae1-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9cae1-121">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9cae1-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
