---
title: "Élément d’interface utilisateur UserNameTextBox des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Compute.UserNameTextBox pour les applications gérées Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 6a395915af274750eb57a085ee51b55fdd392615
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Élément d’interface utilisateur Microsoft.Compute.UserNameTextBox
Contrôle de zone de texte avec validation intégrée des noms d’utilisateur Windows et Linux. Vous utilisez cet élément lors de la [création d’une application gérée Azure](publish-service-catalog-app.md).

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
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- Si `constraints.required` est défini sur **true**, la zone de texte doit contenir une valeur permettant de réussir la validation. La valeur par défaut est **true**.
- `osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.
- `constraints.regex` est un modèle d’expression régulière JavaScript. S’il est spécifié, la valeur de la zone de texte doit correspondre au modèle pour permettre la réussite de la validation. La valeur par défaut est **null**.
- `constraints.validationMessage` est une chaîne à afficher en cas d’échec de la validation de la valeur de la zone de texte spécifiée par `constraints.regex`. Si elle n’est pas spécifiée, les messages de validation intégrés de la zone de texte sont utilisés. La valeur par défaut est **null**.
- Cet élément dispose d’une validation intégrée basée sur la valeur spécifiée pour `osPlatform`. La validation intégrée est utilisable avec une expression régulière personnalisée.
Si une valeur est spécifiée pour `constraints.regex`, les validations intégrées et personnalisées sont déclenchées.

## <a name="sample-output"></a>Exemple de sortie
```json
"tabrezm"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](overview.md).
* Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](create-uidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](create-uidefinition-elements.md).
