---
title: "élément de l’interface utilisateur de StorageAccountSelector pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Storage.StorageAccountSelector pour des Applications managées Azure"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="6abc3-103">Élément d’interface utilisateur Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="6abc3-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="6abc3-104">Contrôle permettant de sélectionner un compte de stockage nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="6abc3-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="6abc3-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6abc3-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6abc3-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="6abc3-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="6abc3-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="6abc3-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="6abc3-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="6abc3-109">Remarks</span></span>
- <span data-ttu-id="6abc3-110">S’il est spécifié, le caractère unique de `defaultValue.name` est automatiquement validé.</span><span class="sxs-lookup"><span data-stu-id="6abc3-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="6abc3-111">Si le nom de compte de stockage hello n’est pas unique, utilisateur de hello doit spécifier un nom différent ou choisissez un compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="6abc3-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="6abc3-112">Hello la valeur par défaut de `defaultValue.type` est **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="6abc3-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="6abc3-113">Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6abc3-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="6abc3-114">`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="6abc3-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="6abc3-115">Si `options.hideExisting` est **true**, utilisateur de hello ne pouvez pas choisir un compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="6abc3-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="6abc3-116">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="6abc3-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="6abc3-117">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="6abc3-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="6abc3-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6abc3-118">Next steps</span></span>
* <span data-ttu-id="6abc3-119">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6abc3-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6abc3-120">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6abc3-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6abc3-121">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6abc3-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
