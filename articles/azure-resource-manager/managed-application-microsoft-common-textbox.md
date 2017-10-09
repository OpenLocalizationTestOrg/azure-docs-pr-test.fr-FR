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
# <a name="microsoftcommontextbox-ui-element"></a>Élément d’interface utilisateur Microsoft.Common.TextBox
Un contrôle qui peut être utilisé tooedit sans mise en forme de texte. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Schéma
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

## <a name="remarks"></a>Remarques
- Si `constraints.required` est défini trop**true**, puis de la zone de texte hello doit contenir une valeur toovalidate avec succès. la valeur par défaut Hello est **false**.
- `constraints.regex` est un modèle d’expression régulière JavaScript. Si spécifié, puis la valeur de la zone de texte hello doit correspondre hello modèle toovalidate avec succès. La valeur par défaut est **null**.
- `constraints.validationMessage`est une chaîne de toodisplay lorsque la valeur de la zone de texte hello de validation échoue. Si ce n’est pas spécifié, puis hello de validation intégrées de la zone de texte les messages sont utilisés. la valeur par défaut Hello est **null**.
- Il toospecify possible une valeur pour `constraints.regex` lorsque `constraints.required` est défini trop**false**. Dans ce scénario, une valeur n’est pas requise pour toovalidate de zone de texte hello avec succès. S’il est spécifié, il doit correspondre au modèle d’expression régulière hello.

## <a name="sample-output"></a>Exemple de sortie

```json
"foobar"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
