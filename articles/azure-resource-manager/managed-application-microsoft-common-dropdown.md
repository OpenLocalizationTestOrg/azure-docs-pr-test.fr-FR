---
title: "Élément d’interface utilisateur DropDown des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.DropDown pour les applications gérées Azure"
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="0bba8-103">Élément d’interface utilisateur Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="0bba8-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="0bba8-104">Contrôle de sélection avec liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0bba8-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="0bba8-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0bba8-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0bba8-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="0bba8-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="0bba8-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="0bba8-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="0bba8-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="0bba8-109">Remarks</span></span>
- <span data-ttu-id="0bba8-110">L’étiquette de `constraints.allowedValues` est le texte qui s’affiche pour un élément, et sa valeur est la valeur de sortie de l’élément sélectionné lors de la sélection.</span><span class="sxs-lookup"><span data-stu-id="0bba8-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="0bba8-111">Si elle est spécifiée, la valeur par défaut doit être une étiquette présente dans `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="0bba8-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="0bba8-112">Dans le cas contraire, le premier élément de `constraints.allowedValues` est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0bba8-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="0bba8-113">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="0bba8-113">The default value is **null**.</span></span>
- <span data-ttu-id="0bba8-114">`constraints.allowedValues` doit contenir au moins un élément.</span><span class="sxs-lookup"><span data-stu-id="0bba8-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="0bba8-115">Cet élément ne prend pas en charge la propriété `constraints.required`.</span><span class="sxs-lookup"><span data-stu-id="0bba8-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="0bba8-116">Pour émuler ce comportement, ajoutez un élément avec une étiquette et la valeur de `""` (chaîne vide) à `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="0bba8-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0bba8-117">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="0bba8-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="0bba8-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bba8-118">Next steps</span></span>
* <span data-ttu-id="0bba8-119">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0bba8-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0bba8-120">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0bba8-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0bba8-121">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0bba8-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>