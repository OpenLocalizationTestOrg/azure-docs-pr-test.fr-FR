---
title: "modèle de gestionnaire de ressources aaaAzure fonctions : les tableaux et les objets | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un modèle Azure Resource Manager pour l’utilisation des tableaux et les objets."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Fonctions de tableau et d’objet pour les modèles Azure Resource Manager 

Resource Manager fournit les fonctions ci-après pour travailler avec des tableaux et des objets.

* [array](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget un tableau de valeurs de chaîne délimitée par une valeur, consultez [fractionner](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Convertit un tableau de tooan valeur hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| convertToArray |Oui |entier, chaîne, tableau ou objet |tableau de tooan valeur tooconvert Hello. |

### <a name="return-value"></a>Valeur de retour

Tableau.

### <a name="example"></a>Exemple

Hello suivant montre comment toouse hello fonction array avec des types différents.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| intOutput | Tableau | [1] |
| stringOutput | Tableau | ["a"] |
| objectOutput | Tableau | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Retourne la première valeur non null à partir des paramètres de hello. Les chaînes vides, les tableaux vides et les objets vides ne sont pas null.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |entier, chaîne, tableau ou objet |Bonjour premier tootest de valeur pour la valeur null. |
| arguments supplémentaires |Non |entier, chaîne, tableau ou objet |Tootest des valeurs supplémentaires pour la valeur null. |

### <a name="return-value"></a>Valeur de retour

valeur Hello de paramètres non null première hello, qui peut être une chaîne, un int, un tableau ou un objet. Null si tous les paramètres sont null. 

### <a name="example"></a>Exemple

Hello suivant montre différentes utilisations de coalesce sortie hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| stringOutput | String | default |
| intOutput | int | 1 |
| objectOutput | Object | {"first": "default"} |
| arrayOutput | Tableau | [1] |
| emptyOutput | Bool | true |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Combine plusieurs tableaux et retourne un tableau hello concaténée, ou combine plusieurs valeurs de chaîne et retourne la chaîne de hello concaténé. 

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |Bonjour premier tableau ou une chaîne pour la concaténation. |
| arguments supplémentaires |Non |tableau ou chaîne |Tableaux ou chaînes supplémentaires en ordre séquentiel pour la concaténation. |

Cette fonction peut prendre n’importe quel nombre d’arguments et peut accepter des chaînes ou des tableaux de paramètres de hello.

### <a name="return-value"></a>Valeur de retour
Chaîne ou tableau de valeurs concaténées.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant montre comment toocombine deux tableaux.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| return | Tableau | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Bonjour à l’exemple suivant montre comment toocombine deux valeurs de chaîne et retourne une chaîne concaténée.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| concatOutput | String | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

Vérifie si un tableau contient une valeur, un objet contient une clé ou une chaîne contient une sous-chaîne.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| conteneur |Oui |tableau, objet ou chaîne |valeur Hello contenant hello valeur toofind. |
| itemToFind |Oui |chaîne ou entier |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

**True** si l’élément de hello est trouvé ; sinon, **False**.

### <a name="example"></a>Exemple

Hello suivant montre comment toouse contient différents types :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| stringTrue | Bool | true |
| stringFalse | Bool | False |
| objectTrue | Bool | true |
| objectFalse | Bool | False |
| arrayTrue | Bool | true |
| arrayFalse | Bool | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Crée un tableau à partir des paramètres de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |Chaîne, entier, tableau ou objet |Hello première valeur dans le tableau de hello. |
| arguments supplémentaires |Non |Chaîne, entier, tableau ou objet |Valeurs supplémentaires dans le tableau de hello. |

### <a name="return-value"></a>Valeur de retour

Tableau.

### <a name="example"></a>Exemple

Hello suivant montre l’exemple de comment createArray toouse avec des types différents :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| stringArray | Tableau | ["a", "b", "c"] |
| intArray | Tableau | [1, 2, 3] |
| objectArray | Tableau | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | Tableau | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

Détermine si un tableau, un objet ou une chaîne est vide.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| itemToTest |Oui |tableau, objet ou chaîne |Bonjour toocheck de valeur s’il est vide. |

### <a name="return-value"></a>Valeur de retour

Retourne **True** si la valeur de hello est vide ; sinon, **False**.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant vérifie si un tableau, un objet et une chaîne sont vides.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayEmpty | Bool | true |
| objectEmpty | Bool | true |
| stringEmpty | Bool | true |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Retourne hello le premier élément du tableau de hello ou le premier caractère de la chaîne de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |premier élément Hello valeur tooretrieve hello ou caractère. |

### <a name="return-value"></a>Valeur de retour

type Hello (string, int, tableau ou objet) de hello premier élément dans un tableau, ou hello premier caractère d’une chaîne.

### <a name="example"></a>Exemple

Hello suivant montre comment toouse hello première fonction avec un tableau et une chaîne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | String | one |
| stringOutput | String | O |

<a id="intersection" />

## <a name="intersection"></a>intersection
`intersection(arg1, arg2, arg3, ...)`

Renvoie un tableau à une seule ou avec des éléments en commun hello à partir des paramètres de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |objet ou tableau |Hello première valeur toouse pour la recherche d’éléments en commun. |
| arg2 |Oui |objet ou tableau |Bonjour deuxième toouse de valeur pour la recherche d’éléments en commun. |
| arguments supplémentaires |Non |objet ou tableau |Toouse des valeurs supplémentaires pour la recherche d’éléments en commun. |

### <a name="return-value"></a>Valeur de retour

Un tableau ou un objet avec des éléments en commun hello.

### <a name="example"></a>Exemple

Hello exemple montre comment l’intersection toouse avec les tableaux et les objets suivants :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "three": "c"} |
| arrayOutput | Tableau | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

Renvoie un objet JSON.

### <a name="parameters"></a>parameters

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |string |Hello valeur tooconvert tooJSON. |


### <a name="return-value"></a>Valeur de retour

objet JSON Hello hello spécifié de chaîne ou un objet vide lorsque **null** est spécifié.

### <a name="example"></a>Exemple

Hello exemple montre comment l’intersection toouse avec les tableaux et les objets suivants :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| jsonOutput | Object | {"a": "b"} |
| nullOutput | Boolean | true |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Retourne hello le dernier élément du tableau de hello ou dernier caractère de chaîne de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |dernier élément Hello valeur tooretrieve hello ou caractère. |

### <a name="return-value"></a>Valeur de retour

Hello type (string, int, tableau ou objet) de hello dernier élément d’un tableau ou hello dernier caractère d’une chaîne.

### <a name="example"></a>Exemple

Hello suivant montre comment toouse hello dernière fonction avec un tableau et une chaîne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | String | three |
| stringOutput | String | e |

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

Retourne le nombre hello d’éléments dans un tableau ou d’une chaîne.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |Hello toouse de tableau pour l’obtention du nombre de hello d’éléments ou hello toouse de chaîne pour l’obtention du nombre de hello de caractères. |

### <a name="return-value"></a>Valeur de retour

Un entier. 

### <a name="example"></a>Exemple

Hello suivant montre l’exemple de la longueur de toouse avec un tableau et une chaîne :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13. |

Vous pouvez utiliser cette fonction avec un nombre de hello tableau toospecify d’itérations lors de la création de ressources. Dans l’exemple suivant de hello, hello paramètre **siteNames** rapporte tableau tooan de toouse de noms lors de la création de sites web de hello.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Pour plus d’informations sur l’utilisation de cette fonction avec un tableau, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

Retourne hello valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau d’entiers ou liste séparée par des virgules d’entiers |Hello collection tooget hello valeur minimale. |

### <a name="return-value"></a>Valeur de retour

Entier représentant la valeur minimale de hello.

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
`max(arg1)`

Retourne hello valeur maximale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau d’entiers ou liste séparée par des virgules d’entiers |Hello collection tooget hello valeur maximale. |

### <a name="return-value"></a>Valeur de retour

Entier représentant la valeur maximale de hello.

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

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

Crée un tableau d’entiers à partir d’un entier de départ et contenant un nombre d’éléments.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| startingInteger |Oui |int |Hello premier entier hello tableau. |
| numberofElements |Oui |int |nombre de Hello de nombres entiers dans le tableau de hello. |

### <a name="return-value"></a>Valeur de retour

Tableau d’entiers.

### <a name="example"></a>Exemple

Bonjour à l’exemple suivant montre comment toouse hello fonction plage :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| rangeOutput | Tableau | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Retourne un tableau avec tous les éléments hello après que le nombre spécifié dans le tableau de hello hello ou retourne une chaîne contenant tous les caractères de hello après que hello le nombre spécifié dans la chaîne de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| originalValue |Oui |tableau ou chaîne |Bonjour toouse tableau ou une chaîne pour l’ignorer. |
| numberToSkip |Oui |int |nombre de Hello d’éléments ou des caractères tooskip. Si cette valeur est inférieur ou égal à 0, tous les hello éléments ou dans la valeur de hello est renvoyé. Si elle est supérieure à la longueur du tableau de hello ou chaîne hello, un tableau vide ou une chaîne est retournée. |

### <a name="return-value"></a>Valeur de retour

Tableau ou chaîne.

### <a name="example"></a>Exemple

Hello suivant exemple ignore hello le nombre d’éléments spécifié dans le tableau de hello et hello nombre spécifié de caractères dans une chaîne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | Tableau | ["three"] |
| stringOutput | String | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Retourne un tableau avec hello spécifié le nombre d’éléments de hello début du tableau de hello, ou une chaîne avec hello nombre spécifié de caractères à partir du début hello de chaîne de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| originalValue |Oui |tableau ou chaîne |Bonjour les éléments de hello tootake tableau ou une chaîne à partir de. |
| numberToTake |Oui |int |nombre de Hello d’éléments ou des caractères tootake. Si cette valeur est inférieure ou égale à 0, une chaîne ou un tableau vide est renvoyé. Si elle est supérieure à la longueur de hello Hello donné de tableau ou une chaîne, tous les éléments hello hello tableau ou une chaîne sont retournés. |

### <a name="return-value"></a>Valeur de retour

Tableau ou chaîne.

### <a name="example"></a>Exemple

Hello suivant l’exemple prend hello spécifié le nombre d’éléments de tableau de hello et les caractères d’une chaîne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| arrayOutput | Tableau | ["one", "two"] |
| stringOutput | String | sur |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Renvoie un tableau à une seule ou avec tous les éléments à partir des paramètres de hello. Les valeurs ou les clés en double sont uniquement incluses une seule fois.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |objet ou tableau |Hello première valeur toouse pour joindre des éléments. |
| arg2 |Oui |objet ou tableau |Hello deuxième valeur toouse pour joindre des éléments. |
| arguments supplémentaires |Non |objet ou tableau |Toouse des valeurs supplémentaires pour joindre des éléments. |

### <a name="return-value"></a>Valeur de retour

Objet ou tableau.

### <a name="example"></a>Exemple

Hello exemple montre comment union toouse avec les tableaux et les objets suivants :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| objectOutput | Object | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | Tableau | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

