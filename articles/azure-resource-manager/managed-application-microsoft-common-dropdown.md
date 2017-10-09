---
title: "élément de l’interface utilisateur de liste déroulante pour les Application gérés aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.DropDown pour des Applications managées Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="318f6-103">Élément d’interface utilisateur Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="318f6-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="318f6-104">Contrôle de sélection avec liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="318f6-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="318f6-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="318f6-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="318f6-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="318f6-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="318f6-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="318f6-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="318f6-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="318f6-109">Remarks</span></span>
- <span data-ttu-id="318f6-110">étiquette Hello pour `constraints.allowedValues` hello texte à afficher pour un élément, et sa valeur est la valeur de sortie hello d’élément hello lorsqu’il est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="318f6-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="318f6-111">Si spécifié, valeur par défaut de hello doit être présent dans une étiquette de `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="318f6-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="318f6-112">Si non spécifié, hello le premier élément de `constraints.allowedValues` est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="318f6-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="318f6-113">la valeur par défaut Hello est **null**.</span><span class="sxs-lookup"><span data-stu-id="318f6-113">hello default value is **null**.</span></span>
- <span data-ttu-id="318f6-114">`constraints.allowedValues` doit contenir au moins un élément.</span><span class="sxs-lookup"><span data-stu-id="318f6-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="318f6-115">Cet élément ne prend pas en charge hello `constraints.required` propriété.</span><span class="sxs-lookup"><span data-stu-id="318f6-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="318f6-116">tooemulate ce problème, ajoutez un élément avec une étiquette et la valeur de `""` (chaîne vide) trop`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="318f6-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="318f6-117">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="318f6-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="318f6-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="318f6-118">Next steps</span></span>
* <span data-ttu-id="318f6-119">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="318f6-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="318f6-120">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="318f6-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="318f6-121">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="318f6-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
