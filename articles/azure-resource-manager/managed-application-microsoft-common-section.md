---
title: "élément de l’interface utilisateur de Section pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.Section pour des Applications managées Azure"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="d457d-103">Élément d’interface utilisateur Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="d457d-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="d457d-104">Contrôle qui regroupe un ou plusieurs éléments sous un titre.</span><span class="sxs-lookup"><span data-stu-id="d457d-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="d457d-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d457d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d457d-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="d457d-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="d457d-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="d457d-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="d457d-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="d457d-109">Remarks</span></span>
- <span data-ttu-id="d457d-110">`elements`doit contenir au moins un élément et peut contenir tous les types d’éléments à l’exception de `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="d457d-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="d457d-111">Cet élément ne prend pas en charge hello `toolTip` propriété.</span><span class="sxs-lookup"><span data-stu-id="d457d-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d457d-112">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="d457d-112">Sample output</span></span>
<span data-ttu-id="d457d-113">les valeurs d’éléments de sortie de tooaccess hello `elements`, utilisez hello [basics()](managed-application-createuidefinition-functions.md#basics) ou [steps()](managed-application-createuidefinition-functions.md#steps) fonctions et la notation par points :</span><span class="sxs-lookup"><span data-stu-id="d457d-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="d457d-114">Les éléments de type `Microsoft.Common.Section` n’ont eux-mêmes aucune valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="d457d-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d457d-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d457d-115">Next steps</span></span>
* <span data-ttu-id="d457d-116">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d457d-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d457d-117">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d457d-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d457d-118">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d457d-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
