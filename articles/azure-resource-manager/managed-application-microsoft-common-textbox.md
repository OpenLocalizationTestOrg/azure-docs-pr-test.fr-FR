---
title: "élément de l’interface utilisateur de zone de texte pour les Application gérés aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.TextBox pour des Applications managées Azure"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="12aea-103">Élément d’interface utilisateur Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="12aea-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="12aea-104">Un contrôle qui peut être utilisé tooedit sans mise en forme de texte.</span><span class="sxs-lookup"><span data-stu-id="12aea-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="12aea-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="12aea-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="12aea-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="12aea-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="12aea-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="12aea-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="12aea-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="12aea-109">Remarks</span></span>
- <span data-ttu-id="12aea-110">Si `constraints.required` est défini trop**true**, puis de la zone de texte hello doit contenir une valeur toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="12aea-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="12aea-111">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="12aea-111">hello default value is **false**.</span></span>
- <span data-ttu-id="12aea-112">`constraints.regex` est un modèle d’expression régulière JavaScript.</span><span class="sxs-lookup"><span data-stu-id="12aea-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="12aea-113">Si spécifié, puis la valeur de la zone de texte hello doit correspondre hello modèle toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="12aea-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="12aea-114">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="12aea-114">The default value is **null**.</span></span>
- <span data-ttu-id="12aea-115">`constraints.validationMessage`est une chaîne de toodisplay lorsque la valeur de la zone de texte hello de validation échoue.</span><span class="sxs-lookup"><span data-stu-id="12aea-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="12aea-116">Si ce n’est pas spécifié, puis hello de validation intégrées de la zone de texte les messages sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="12aea-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="12aea-117">la valeur par défaut Hello est **null**.</span><span class="sxs-lookup"><span data-stu-id="12aea-117">hello default value is **null**.</span></span>
- <span data-ttu-id="12aea-118">Il toospecify possible une valeur pour `constraints.regex` lorsque `constraints.required` est défini trop**false**.</span><span class="sxs-lookup"><span data-stu-id="12aea-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="12aea-119">Dans ce scénario, une valeur n’est pas requise pour toovalidate de zone de texte hello avec succès.</span><span class="sxs-lookup"><span data-stu-id="12aea-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="12aea-120">S’il est spécifié, il doit correspondre au modèle d’expression régulière hello.</span><span class="sxs-lookup"><span data-stu-id="12aea-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="12aea-121">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="12aea-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="12aea-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12aea-122">Next steps</span></span>
* <span data-ttu-id="12aea-123">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12aea-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="12aea-124">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12aea-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="12aea-125">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="12aea-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
