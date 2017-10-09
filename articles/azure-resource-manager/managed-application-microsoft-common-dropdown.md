---
title: "élément de l’interface utilisateur de liste déroulante pour les Application gérés aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.DropDown pour des Applications managées Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Élément d’interface utilisateur Microsoft.Common.DropDown
Contrôle de sélection avec liste déroulante. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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

## <a name="remarks"></a>Remarques
- étiquette Hello pour `constraints.allowedValues` hello texte à afficher pour un élément, et sa valeur est la valeur de sortie hello d’élément hello lorsqu’il est sélectionné.
- Si spécifié, valeur par défaut de hello doit être présent dans une étiquette de `constraints.allowedValues`. Si non spécifié, hello le premier élément de `constraints.allowedValues` est sélectionnée. la valeur par défaut Hello est **null**.
- `constraints.allowedValues` doit contenir au moins un élément.
- Cet élément ne prend pas en charge hello `constraints.required` propriété. tooemulate ce problème, ajoutez un élément avec une étiquette et la valeur de `""` (chaîne vide) trop`constraints.allowedValues`.

## <a name="sample-output"></a>Exemple de sortie
```json
"Bar"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
