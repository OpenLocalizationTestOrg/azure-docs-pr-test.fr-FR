---
title: "Élément d’interface utilisateur PasswordBox des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.PasswordBox pour les applications gérées Azure"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="f15c0-103">Élément d’interface utilisateur Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="f15c0-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="f15c0-104">Contrôle qui peut être utilisé pour indiquer et confirmer un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f15c0-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="f15c0-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f15c0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f15c0-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f15c0-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="f15c0-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="f15c0-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="f15c0-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="f15c0-109">Remarks</span></span>
- <span data-ttu-id="f15c0-110">Cet élément ne prend pas en charge la propriété `defaultValue`.</span><span class="sxs-lookup"><span data-stu-id="f15c0-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="f15c0-111">Pour obtenir des détails relatifs à l’implémentation de `constraints`, consultez [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="f15c0-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="f15c0-112">Si `options.hideConfirmation` est défini sur **true**, la deuxième zone de texte de confirmation du mot de passe utilisateur est masquée.</span><span class="sxs-lookup"><span data-stu-id="f15c0-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="f15c0-113">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="f15c0-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f15c0-114">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="f15c0-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="f15c0-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f15c0-115">Next steps</span></span>
* <span data-ttu-id="f15c0-116">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f15c0-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f15c0-117">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f15c0-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f15c0-118">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f15c0-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
