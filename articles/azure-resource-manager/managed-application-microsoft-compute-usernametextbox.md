---
title: "Élément d’interface utilisateur UserNameTextBox des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Compute.UserNameTextBox pour les applications gérées Azure"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="2207f-103">Élément d’interface utilisateur Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="2207f-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="2207f-104">Contrôle de zone de texte avec validation intégrée des noms d’utilisateur Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="2207f-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="2207f-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2207f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2207f-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="2207f-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="2207f-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="2207f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="2207f-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="2207f-109">Remarks</span></span>
- <span data-ttu-id="2207f-110">Si `constraints.required` est défini sur **true**, la zone de texte doit contenir une valeur permettant de réussir la validation.</span><span class="sxs-lookup"><span data-stu-id="2207f-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="2207f-111">La valeur par défaut est **true**.</span><span class="sxs-lookup"><span data-stu-id="2207f-111">The default value is **true**.</span></span>
- <span data-ttu-id="2207f-112">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="2207f-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="2207f-113">`constraints.regex` est un modèle d’expression régulière JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2207f-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="2207f-114">S’il est spécifié, la valeur de la zone de texte doit correspondre au modèle pour permettre la réussite de la validation.</span><span class="sxs-lookup"><span data-stu-id="2207f-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="2207f-115">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="2207f-115">The default value is **null**.</span></span>
- <span data-ttu-id="2207f-116">`constraints.validationMessage` est une chaîne à afficher en cas d’échec de la validation de la valeur de la zone de texte spécifiée par `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="2207f-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="2207f-117">Si elle n’est pas spécifiée, les messages de validation intégrés de la zone de texte sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="2207f-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="2207f-118">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="2207f-118">The default value is **null**.</span></span>
- <span data-ttu-id="2207f-119">Cet élément dispose d’une validation intégrée basée sur la valeur spécifiée pour `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="2207f-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="2207f-120">La validation intégrée est utilisable avec une expression régulière personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2207f-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="2207f-121">Si une valeur est spécifiée pour `constraints.regex`, les validations intégrées et personnalisées sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="2207f-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2207f-122">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="2207f-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="2207f-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2207f-123">Next steps</span></span>
* <span data-ttu-id="2207f-124">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2207f-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2207f-125">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2207f-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2207f-126">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2207f-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
