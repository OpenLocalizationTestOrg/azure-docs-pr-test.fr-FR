---
title: "élément de l’interface utilisateur de UserNameTextBox pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Compute.UserNameTextBox pour des Applications managées Azure"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="ea1b1-103">Élément d’interface utilisateur Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="ea1b1-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="ea1b1-104">Contrôle de zone de texte avec validation intégrée des noms d’utilisateur Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="ea1b1-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b1-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ea1b1-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ea1b1-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="ea1b1-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="ea1b1-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="ea1b1-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="ea1b1-109">Remarks</span></span>
- <span data-ttu-id="ea1b1-110">Si `constraints.required` est défini trop**true**, puis de la zone de texte hello doit contenir une valeur toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="ea1b1-111">la valeur par défaut Hello est **true**.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-111">hello default value is **true**.</span></span>
- <span data-ttu-id="ea1b1-112">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="ea1b1-113">`constraints.regex` est un modèle d’expression régulière JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="ea1b1-114">Si spécifié, puis la valeur de la zone de texte hello doit correspondre hello modèle toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="ea1b1-115">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-115">The default value is **null**.</span></span>
- <span data-ttu-id="ea1b1-116">`constraints.validationMessage`est une chaîne de toodisplay lors de l’échec de la valeur de la zone de texte hello validation hello spécifiée par `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="ea1b1-117">Si ce n’est pas spécifié, puis hello de validation intégrées de la zone de texte les messages sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="ea1b1-118">la valeur par défaut Hello est **null**.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-118">hello default value is **null**.</span></span>
- <span data-ttu-id="ea1b1-119">Cet élément a une validation intégrées qui repose sur la valeur hello spécifiée pour `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="ea1b1-120">validation intégrées de Hello peut être utilisée avec une expression régulière personnalisée.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="ea1b1-121">Si une valeur pour `constraints.regex` est spécifié, les deux hello intégrées et validations personnalisées sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="ea1b1-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ea1b1-122">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="ea1b1-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="ea1b1-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea1b1-123">Next steps</span></span>
* <span data-ttu-id="ea1b1-124">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b1-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ea1b1-125">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b1-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ea1b1-126">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ea1b1-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
