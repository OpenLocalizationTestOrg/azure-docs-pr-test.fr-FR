---
title: "Élément d’interface utilisateur MultiStorageAccountCombo des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur MultiStorageAccountCombo pour les applications gérées Azure"
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
ms.openlocfilehash: e1dda7917988146807ca6cfab10a3a4eac0b7bb2
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Élément d’interface utilisateur Microsoft.Storage.MultiStorageAccountCombo
Groupe de contrôles pour la création de plusieurs comptes de stockage, avec des noms commençant par un préfixe commun. Vous utilisez cet élément lors de la [création d’une application gérée Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- La valeur de `defaultValue.prefix` est concaténée avec un ou plusieurs entiers pour générer la séquence de noms de comptes de stockage. Par exemple, si `defaultValue.prefix` est **foobar** et `count` est **2**, les noms de comptes de stockage **foobar1** et **foobar2** sont générés. Le caractère unique des noms de comptes de stockage générés est validé automatiquement.
- Les noms de comptes de stockage sont générés lexicographiquement en se basant sur `count`. Par exemple, si `count` est égal à 10, les noms de comptes de stockage se terminent par des entiers à 2 chiffres (01, 02, 03, etc..).
- La valeur par défaut pour `defaultValue.prefix` est égale à **null** et pour `defaultValue.type` équivaut à **Premium_LRS**.
- Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.
`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.
- En plus de générer des noms de comptes de stockage, `count` est utilisé pour définir le multiplicateur approprié pour l’élément. Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').storageAccountCount]`. La valeur par défaut est **1**.

## <a name="sample-output"></a>Exemple de sortie
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](overview.md).
* Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](create-uidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](create-uidefinition-elements.md).
