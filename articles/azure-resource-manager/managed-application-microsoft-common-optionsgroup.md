---
title: "élément de l’interface utilisateur de groupe Options pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.OptionsGroup pour des Applications managées Azure"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="ae34c-103">Élément d’interface utilisateur Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="ae34c-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="ae34c-104">Contrôle de sélection avec une ligne d’options disponibles.</span><span class="sxs-lookup"><span data-stu-id="ae34c-104">A selection control with a row of available options.</span></span> <span data-ttu-id="ae34c-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ae34c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ae34c-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ae34c-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="ae34c-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="ae34c-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="ae34c-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="ae34c-109">Remarks</span></span>
- <span data-ttu-id="ae34c-110">étiquette Hello pour `constraints.allowedValues` hello texte à afficher pour un élément, et sa valeur est la valeur de sortie hello d’élément hello lorsqu’il est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ae34c-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="ae34c-111">Si spécifié, valeur par défaut de hello doit être présent dans une étiquette de `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="ae34c-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="ae34c-112">Si non spécifié, hello le premier élément de `constraints.allowedValues` est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ae34c-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="ae34c-113">la valeur par défaut Hello est **null**.</span><span class="sxs-lookup"><span data-stu-id="ae34c-113">hello default value is **null**.</span></span>
- <span data-ttu-id="ae34c-114">`constraints.allowedValues` doit contenir au moins un élément.</span><span class="sxs-lookup"><span data-stu-id="ae34c-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="ae34c-115">Cet élément ne prend pas en charge hello `constraints.required` propriété ; un élément doit être sélectionné toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="ae34c-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ae34c-116">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="ae34c-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="ae34c-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae34c-117">Next steps</span></span>
* <span data-ttu-id="ae34c-118">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae34c-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ae34c-119">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae34c-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ae34c-120">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ae34c-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
