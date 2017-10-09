---
title: "aaaAzure Gestionnaire de ressources fonctions de modèle - logiques | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un gestionnaire de ressources Azure modèle toodetermine les valeurs logiques."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Fonctions logiques pour les modèles Azure Resource Manager

Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.

* [et](#and)
* [bool](#bool)
* [si](#if)
* [non](#not)
* [ou](#or)

## <a name="and"></a>and
`and(arg1, arg2)`

Vérifie si les deux valeurs de paramètres sont true.

### <a name="parameters"></a>parameters

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |booléenne |Hello première valeur toocheck si a la valeur true. |
| arg2 |Oui |booléenne |Hello deuxième valeur toocheck si a la valeur true. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si les valeurs sont true ; sinon, renvoie **False**.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse les fonctions logiques.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

est résultat Hello hello précédant l’exemple suivant :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | true |
| notExampleOutput | Bool | False |


## <a name="bool"></a>bool
`bool(arg1)`

Convertit hello tooa de paramètre boolean.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |chaîne ou entier |Hello tooa tooconvert de valeur booléenne. |

### <a name="return-value"></a>Valeur de retour
Une valeur booléenne de hello de valeur convertie.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment bool toouse par une chaîne ou un entier.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| trueString | Bool | true |
| falseString | Bool | False |
| trueInt | Bool | true |
| falseInt | Bool | False |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Retourne une valeur indiquant si une condition est true ou false.

### <a name="parameters"></a>parameters

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| condition |Oui |booléenne |Bonjour valeur toocheck si elle a la valeur true. |
| trueValue |Oui | chaîne, int, objet ou tableau |valeur de Hello tooreturn quand hello condition est vraie. |
| falseValue |Oui | chaîne, int, objet ou tableau |valeur de Hello tooreturn lorsque hello condition est false. |

### <a name="return-value"></a>Valeur de retour

Retourne le deuxième paramètre lorsque le premier paramètre est **True** ; sinon, retourne le troisième paramètre.

### <a name="remarks"></a>Remarques

Vous pouvez utiliser cet ensemble de tooconditionally de fonction à une propriété de ressource. Hello suivant n’est pas un modèle complet, mais il montre les parties pertinentes d’hello pour la définition de manière conditionnelle hello à haute disponibilité.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse hello `if` (fonction).

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

est résultat Hello hello précédant l’exemple suivant :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| yesOutput | String | yes |
| noOutput | String | no |


## <a name="not"></a>not
`not(arg1)`

Convertit la valeur booléenne tooits inverse la valeur.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |booléenne |Hello tooconvert de valeur. |


### <a name="return-value"></a>Valeur de retour

Retourne **True** lorsque le paramètre est **False**. Retourne **False** lorsque le paramètre est **True**.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse les fonctions logiques.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

est résultat Hello hello précédant l’exemple suivant :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | true |
| notExampleOutput | Bool | False |

Hello exemple suivant utilise **pas** avec [est égal à](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>ou
`or(arg1, arg2)`

Vérifie si l’une des valeurs du paramètre est true.

### <a name="parameters"></a>parameters

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |booléenne |Hello première valeur toocheck si a la valeur true. |
| arg2 |Oui |booléenne |Hello deuxième valeur toocheck si a la valeur true. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si la valeur est true ; sinon, **False**.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse les fonctions logiques.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

est résultat Hello hello précédant l’exemple suivant :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| andExampleOutput | Bool | False |
| orExampleOutput | Bool | true |
| notExampleOutput | Bool | False |


## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

