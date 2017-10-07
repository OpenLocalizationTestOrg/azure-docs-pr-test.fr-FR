---
title: "élément de l’interface utilisateur de Section pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.Section pour des Applications managées Azure"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a>Élément d’interface utilisateur Microsoft.Common.Section
Contrôle qui regroupe un ou plusieurs éléments sous un titre. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- `elements`doit contenir au moins un élément et peut contenir tous les types d’éléments à l’exception de `Microsoft.Common.Section`.
- Cet élément ne prend pas en charge hello `toolTip` propriété.

## <a name="sample-output"></a>Exemple de sortie
les valeurs d’éléments de sortie de tooaccess hello `elements`, utilisez hello [basics()](managed-application-createuidefinition-functions.md#basics) ou [steps()](managed-application-createuidefinition-functions.md#steps) fonctions et la notation par points :

```json
basics('section1').element1
```

Les éléments de type `Microsoft.Common.Section` n’ont eux-mêmes aucune valeur de sortie.

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
