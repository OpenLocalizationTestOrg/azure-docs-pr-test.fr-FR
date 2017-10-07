---
title: "élément de l’interface utilisateur de MultiStorageAccountCombo pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Storage.MultiStorageAccountCombo pour des Applications managées Azure"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Élément d’interface utilisateur Microsoft.Storage.MultiStorageAccountCombo
Groupe de contrôles pour la création de plusieurs comptes de stockage, avec des noms commençant par un préfixe commun. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

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
- Hello valeur pour `defaultValue.prefix` est concaténée avec une ou plusieurs entiers toogenerate hello séquence des noms de compte de stockage. Par exemple, si `defaultValue.prefix` est **foobar** et `count` est **2**, les noms de comptes de stockage **foobar1** et **foobar2** sont générés. Le caractère unique des noms de comptes de stockage générés est validé automatiquement.
- noms de compte de stockage Hello sont générés lexicographique en fonction `count`. Par exemple, si `count` est 10, puis les noms de compte de stockage hello se terminent par des entiers de 2 chiffres (01, 02, 03, etc..).
- Hello la valeur par défaut de `defaultValue.prefix` est **null**et pour `defaultValue.type` est **Premium_LRS**.
- Tout type non spécifié dans `constraints.allowedTypes` est masqué et tout type non spécifié dans `constraints.excludedTypes` s’affiche.
`constraints.allowedTypes`et `constraints.excludedTypes` sont tous deux facultatifs, mais ne peuvent pas être utilisés simultanément.
- Dans les noms de compte de stockage toogenerating de plus, `count` est tooset utilisé le multiplicateur approprié pour l’élément de hello. Il prend en charge une valeur statique, telle que **2**, ou une valeur dynamique issue d’un autre élément, comme `[steps('step1').storageAccountCount]`. la valeur par défaut Hello est **1**.

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
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
