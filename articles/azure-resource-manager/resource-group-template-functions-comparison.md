---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - comparaison | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans des valeurs de toocompare modèles Azure Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Fonctions de comparaison pour les modèles Azure Resource Manager

Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.

* [equals](#equals)
* [greater](#greater)
* [greaterOrEquals](#greaterorequals)
* [less](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>equals
`equals(arg1, arg2)`

Vérifie si deux valeurs sont égales.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier, chaîne, tableau ou objet |Hello première valeur toocheck pour l’égalité. |
| arg2 |Oui |entier, chaîne, tableau ou objet |Bonjour deuxième toocheck de valeur pour l’égalité. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si les valeurs hello sont égaux ; sinon, **False**.

### <a name="remarks"></a>Remarques

Hello fonction equals est souvent utilisée avec hello `condition` élément tootest indique si une ressource est déployée.

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a>Exemple

exemple de modèle de Hello vérifie les différents types de valeurs sont égales. Toutes les valeurs par défaut de hello renvoient True.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | True |
| checkArrays | Bool | True |
| checkObjects | Bool | true |


Hello exemple suivant utilise [pas](resource-group-template-functions-logical.md#not) avec **est égal à**.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

est résultat Hello hello précédant l’exemple suivant :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkNotEquals | Bool | true |


## <a name="greater"></a>greater
`greater(arg1, arg2)`

Vérifie si la première valeur de hello est supérieure à la valeur de seconde hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier ou chaîne |Hello première valeur de comparaison supérieur de hello. |
| arg2 |Oui |entier ou chaîne |Hello deuxième valeur de comparaison supérieur de hello. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si hello première valeur est supérieure à hello deuxième ; sinon, **False**.

### <a name="example"></a>Exemple

exemple de modèle de Hello vérifie si une valeur de hello est supérieure à hello autres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Vérifie si hello première valeur est supérieure ou égale toohello seconde valeur.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier ou chaîne |Hello première valeur de comparaison supérieure ou égal de hello. |
| arg2 |Oui |entier ou chaîne |Hello deuxième valeur de comparaison supérieure ou égal de hello. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si hello première valeur est supérieure ou égale toohello deuxième ; sinon, **False**.

### <a name="example"></a>Exemple

exemple de modèle de Hello vérifie si une valeur de hello est supérieure ou égal toohello autres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkInts | Bool | False |
| checkStrings | Bool | True |



## <a name="less"></a>less
`less(arg1, arg2)`

Vérifie si hello première valeur est inférieure hello deuxième valeur.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier ou chaîne |Hello première valeur de hello moins de comparaison. |
| arg2 |Oui |entier ou chaîne |Hello deuxième valeur de hello moins de comparaison. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si hello première valeur est inférieure à hello deuxième valeur ; sinon, **False**.

### <a name="example"></a>Exemple

exemple de modèle de Hello vérifie si une valeur de hello est inférieure à hello autres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Vérifie si la première valeur de hello est inférieur ou égal toohello seconde valeur.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier ou chaîne |Hello première valeur de hello inférieur ou égal à la comparaison. |
| arg2 |Oui |entier ou chaîne |Hello deuxième valeur de hello inférieur ou égal à la comparaison. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si hello première valeur est inférieure ou égale toohello deuxième valeur ; sinon, **False**.

### <a name="example"></a>Exemple

Hello exemple de modèle vérifie si une valeur de hello est inférieur ou égal toohello autres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| checkInts | Bool | True |
| checkStrings | Bool | False |



## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

