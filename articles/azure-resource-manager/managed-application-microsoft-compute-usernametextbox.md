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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Élément d’interface utilisateur Microsoft.Compute.UserNameTextBox
Contrôle de zone de texte avec validation intégrée des noms d’utilisateur Windows et Linux. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Schéma
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

## <a name="remarks"></a>Remarques
- Si `constraints.required` est défini trop**true**, puis de la zone de texte hello doit contenir une valeur toovalidate avec succès. la valeur par défaut Hello est **true**.
- `osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.
- `constraints.regex` est un modèle d’expression régulière JavaScript. Si spécifié, puis la valeur de la zone de texte hello doit correspondre hello modèle toovalidate avec succès. La valeur par défaut est **null**.
- `constraints.validationMessage`est une chaîne de toodisplay lors de l’échec de la valeur de la zone de texte hello validation hello spécifiée par `constraints.regex`. Si ce n’est pas spécifié, puis hello de validation intégrées de la zone de texte les messages sont utilisés. la valeur par défaut Hello est **null**.
- Cet élément a une validation intégrées qui repose sur la valeur hello spécifiée pour `osPlatform`. validation intégrées de Hello peut être utilisée avec une expression régulière personnalisée.
Si une valeur pour `constraints.regex` est spécifié, les deux hello intégrées et validations personnalisées sont déclenchées.

## <a name="sample-output"></a>Exemple de sortie
```json
"tabrezm"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
