---
title: "Élément d’interface utilisateur OptionsGroup des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.OptionsGroup pour les applications gérées Azure"
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="b1918-103">Élément d’interface utilisateur Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="b1918-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="b1918-104">Contrôle de sélection avec une ligne d’options disponibles.</span><span class="sxs-lookup"><span data-stu-id="b1918-104">A selection control with a row of available options.</span></span> <span data-ttu-id="b1918-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b1918-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="b1918-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="b1918-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="b1918-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="b1918-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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

## <a name="remarks"></a><span data-ttu-id="b1918-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="b1918-109">Remarks</span></span>
- <span data-ttu-id="b1918-110">L’étiquette de `constraints.allowedValues` est le texte qui s’affiche pour un élément, et sa valeur est la valeur de sortie de l’élément sélectionné lors de la sélection.</span><span class="sxs-lookup"><span data-stu-id="b1918-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="b1918-111">Si elle est spécifiée, la valeur par défaut doit être une étiquette présente dans `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="b1918-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="b1918-112">Dans le cas contraire, le premier élément de `constraints.allowedValues` est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="b1918-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="b1918-113">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="b1918-113">The default value is **null**.</span></span>
- <span data-ttu-id="b1918-114">`constraints.allowedValues` doit contenir au moins un élément.</span><span class="sxs-lookup"><span data-stu-id="b1918-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="b1918-115">Cet élément ne prend pas en charge la propriété `constraints.required` ; un élément doit être sélectionné pour réussir la validation.</span><span class="sxs-lookup"><span data-stu-id="b1918-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="b1918-116">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="b1918-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="b1918-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1918-117">Next steps</span></span>
* <span data-ttu-id="b1918-118">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1918-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b1918-119">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1918-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="b1918-120">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="b1918-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
