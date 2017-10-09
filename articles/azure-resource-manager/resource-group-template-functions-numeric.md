---
title: "aaaAzure Gestionnaire de ressources fonctions de modèle - numériques | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un toowork de modèle Azure Resource Manager avec les nombres."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Fonctions numériques pour les modèles Azure Resource Manager

Gestionnaire de ressources fournit hello suivant des fonctions permettant de travailler avec des entiers :

* [ajouter](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [sub](#sub)

<a id="add" />

## <a name="add"></a>add
`add(operand1, operand2)`

Retourne hello somme de deux entiers de fourni hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- | 
|operand1 |Oui |int |Nombre tooadd. |
|operand2 |Oui |int |Deuxième nombre tooadd. |

### <a name="return-value"></a>Valeur de retour

Entier qui contient la somme de hello des paramètres de hello.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant ajoute deux paramètres.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Retourne hello index d’une boucle d’itération. 

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| loopName | Non | string | nom de Hello de boucle de hello pour l’obtention d’itération de hello. |
| Offset |Non |int |Hello tooadd toohello itération de base zéro valeur numérique. |

### <a name="remarks"></a>Remarques

Cette fonction est toujours utilisée avec un objet **copy** . Si aucune valeur n’est fournie pour **offset**, valeur de l’itération actuelle hello est retourné. valeur de l’itération Hello commence à zéro.

Hello **loopName** propriété vous permet de toospecify si copyIndex fait référence tooa ressource itération ou une itération de la propriété. Si aucune valeur n’est fournie pour **loopName**, hello itération du type ressource actuelle est utilisée. Indiquez une valeur pour **loopName** lors de l’itération sur une propriété. 
 
Pour obtenir une description complète d’exemples d’utilisation de l’expression **copyIndex**, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Exemple

Hello suivant montre une boucle et hello index valeur copie incluse dans le nom de hello. 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a>Valeur de retour

Entier représentant l’index en cours de hello d’itération de hello.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Retourne hello division d’entier de deux entiers de fourni hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| operand1 |Oui |int |nombre de Hello est divisée. |
| operand2 |Oui |int |nombre Hello toodivide utilisé. Ne peut pas être 0. |

### <a name="return-value"></a>Valeur de retour

Une division hello représentant d’entier.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant divise un paramètre par un autre paramètre.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>float
`float(arg1)`

Convertit tooa de valeur hello nombre à virgule flottante. Vous utilisez uniquement cette fonction lors du passage d’application tooan, par exemple une application de la logique des paramètres personnalisés.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |chaîne ou entier |Bonjour tooa tooconvert de valeur nombre à virgule flottante. |

### <a name="return-value"></a>Valeur de retour
Nombre à virgule flottante.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant montre comment toouse float toopass paramètres tooa application logique :

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a>int
`int(valueToConvert)`

Convertit l’entier de tooan hello valeur spécifiée.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| valueToConvert |Oui |chaîne ou entier |nombre entier tooan tooconvert valeur Hello. |

### <a name="return-value"></a>Valeur de retour

Nombre entier de valeur de hello converti.

### <a name="example"></a>Exemple

Hello suivant convertit toointeger de valeur de paramètre fourni par l’utilisateur hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>Min
`min (arg1)`

Retourne hello valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau d’entiers ou liste séparée par des virgules d’entiers |Hello collection tooget hello valeur minimale. |

### <a name="return-value"></a>Valeur de retour

Entier représentant la valeur minimale à partir de la collection de hello.

### <a name="example"></a>Exemple

Hello suivant montre l’exemple de comment min toouse avec un tableau et une liste d’entiers :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max (arg1)`

Retourne hello valeur maximale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau d’entiers ou liste séparée par des virgules d’entiers |Hello collection tooget hello valeur maximale. |

### <a name="return-value"></a>Valeur de retour

Entier représentant la valeur maximale de hello à partir de la collection de hello.

### <a name="example"></a>Exemple

Hello suivant montre l’exemple de comment toouse max avec un tableau et une liste d’entiers :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Retourne le reste hello de division d’entier hello hello sur deux entiers fourni.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| operand1 |Oui |int |nombre de Hello est divisée. |
| operand2 |Oui |int |numéro de Hello toodivide utilisé, ne peut pas être 0. |

### <a name="return-value"></a>Valeur de retour
Un modulo entier représentant hello.

### <a name="example"></a>Exemple

Hello exemple ci-dessous retourne reste hello de la division d’un paramètre par un autre paramètre.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Retourne hello multiplication de deux entiers de fourni hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| operand1 |Oui |int |Nombre toomultiply. |
| operand2 |Oui |int |Deuxième nombre toomultiply. |

### <a name="return-value"></a>Valeur de retour

Une entier représentant hello la multiplication.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant multiplie un paramètre par un autre paramètre.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>sub
`sub(operand1, operand2)`

Retourne hello soustraction de deux entiers de fourni hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| operand1 |Oui |int |nombre de Hello est soustraite. |
| operand2 |Oui |int |nombre de Hello est soustrait. |

### <a name="return-value"></a>Valeur de retour
Une soustraction entier représentant hello.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant soustrait un paramètre à partir d’un autre paramètre.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

