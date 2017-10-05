---
title: "Élément d’interface utilisateur Section des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.Section pour les applications gérées Azure"
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="0b1b4-103">Élément d’interface utilisateur Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="0b1b4-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="0b1b4-104">Contrôle qui regroupe un ou plusieurs éléments sous un titre.</span><span class="sxs-lookup"><span data-stu-id="0b1b4-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="0b1b4-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0b1b4-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0b1b4-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="0b1b4-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="0b1b4-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="0b1b4-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0b1b4-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="0b1b4-109">Remarks</span></span>
- <span data-ttu-id="0b1b4-110">`elements`doit contenir au moins un élément et peut contenir tous les types d’éléments à l’exception de `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="0b1b4-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="0b1b4-111">Cet élément ne prend pas en charge la propriété `toolTip`.</span><span class="sxs-lookup"><span data-stu-id="0b1b4-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0b1b4-112">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="0b1b4-112">Sample output</span></span>
<span data-ttu-id="0b1b4-113">Pour accéder aux valeurs de sortie des éléments de `elements`, utilisez les fonctions [basics()](managed-application-createuidefinition-functions.md#basics) ou [steps()](managed-application-createuidefinition-functions.md#steps) et la notation sous forme de points :</span><span class="sxs-lookup"><span data-stu-id="0b1b4-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="0b1b4-114">Les éléments de type `Microsoft.Common.Section` n’ont eux-mêmes aucune valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="0b1b4-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b1b4-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b1b4-115">Next steps</span></span>
* <span data-ttu-id="0b1b4-116">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b1b4-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0b1b4-117">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b1b4-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0b1b4-118">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0b1b4-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
