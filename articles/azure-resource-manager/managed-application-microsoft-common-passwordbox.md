---
title: "élément de l’interface utilisateur de PasswordBox pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.PasswordBox pour des Applications managées Azure"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="17796-103">Élément d’interface utilisateur Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="17796-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="17796-104">Un contrôle qui peut être utilisé tooprovide et confirmez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="17796-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="17796-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="17796-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="17796-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="17796-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="17796-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="17796-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="17796-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="17796-109">Remarks</span></span>
- <span data-ttu-id="17796-110">Cet élément ne prend pas en charge hello `defaultValue` propriété.</span><span class="sxs-lookup"><span data-stu-id="17796-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="17796-111">Pour obtenir des détails relatifs à l’implémentation de `constraints`, consultez [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="17796-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="17796-112">Si `options.hideConfirmation` est défini trop**true**, deuxième zone de texte hello pour confirmer le mot de passe de l’utilisateur hello est masqué.</span><span class="sxs-lookup"><span data-stu-id="17796-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="17796-113">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="17796-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="17796-114">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="17796-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="17796-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17796-115">Next steps</span></span>
* <span data-ttu-id="17796-116">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17796-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="17796-117">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17796-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="17796-118">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="17796-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
