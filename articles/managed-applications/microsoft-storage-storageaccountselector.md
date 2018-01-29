---
title: "Élément d’interface utilisateur StorageAccountSelector des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Storage.StorageAccountSelector pour les applications gérées Azure"
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
ms.openlocfilehash: 366a862acc15decf6a8e19f875d5d052695f373c
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a>Élément d’interface utilisateur Microsoft.Storage.StorageAccountSelector
Contrôle permettant de sélectionner un compte de stockage nouveau ou existant. Vous utilisez cet élément lors de la [création d’une application gérée Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- S’il est spécifié, le caractère unique de `defaultValue.name` est automatiquement validé. Si le nom de compte de stockage n’est pas unique, l’utilisateur doit indiquer un autre nom ou choisir un compte de stockage existant.
- La valeur par défaut pour `defaultValue.type` est **Premium_LRS**.
- Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.
`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.
- Si `options.hideExisting` est défini sur **true**, l’utilisateur ne peut pas choisir de compte de stockage existant. La valeur par défaut est **false**.


## <a name="sample-output"></a>Exemple de sortie
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](overview.md).
* Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](create-uidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](create-uidefinition-elements.md).
