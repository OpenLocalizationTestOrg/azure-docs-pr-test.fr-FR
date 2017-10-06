---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - chaîne | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un toowork de modèle Azure Resource Manager avec des chaînes."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Fonctions de chaînes pour les modèles Azure Resource Manager

Gestionnaire de ressources fournit hello suivant des fonctions pour manipuler des chaînes :

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [length](#length)
* [padLeft](#padleft)
* [replace](#replace)
* [skip](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [découper](#trim)
* [uniqueString](#uniquestring)
* [URI](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>base64
`base64(inputString)`

Retourne hello représentation en base64 de la chaîne d’entrée de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_entrée |Oui |string |Bonjour tooreturn de valeur comme une représentation en base64. |

### <a name="return-value"></a>Valeur de retour

Chaîne contenant la représentation sous forme de hello en base64.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toouse hello base64 (fonction).

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Convertit un objet JSON de tooa de représentation en base64.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| base64Value |Oui |string |Hello base64 représentation tooconvert tooa objet JSON. |

### <a name="return-value"></a>Valeur de retour

Un objet JSON.

### <a name="examples"></a>Exemples

Hello exemple suivant utilise hello base64ToJson fonction tooconvert une valeur base64 :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Convertit une chaîne de tooa de représentation en base64.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| base64Value |Oui |string |Hello représentation tooconvert tooa la chaîne en base64. |

### <a name="return-value"></a>Valeur de retour

Une chaîne de hello convertie valeur base64.

### <a name="examples"></a>Exemples

Hello exemple suivant utilise hello base64ToString fonction tooconvert une valeur base64 :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| base64Output | String | b25lLCB0d28sIHRocmVl |
| toStringOutput | String | one, two, three |
| toJsonOutput | Object | {"one": "a", "two": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Combine plusieurs valeurs de chaîne et retourne la chaîne hello concaténée ou combine plusieurs tableaux et retourne hello concaténée tableau.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |chaîne ou tableau |valeur de la première Hello pour la concaténation. |
| arguments supplémentaires |Non |string |Valeurs supplémentaires en ordre séquentiel pour la concaténation. |

### <a name="return-value"></a>Valeur de retour
Chaîne ou tableau de valeurs concaténées.

### <a name="examples"></a>Exemples

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

<a id="contains" />

## <a name="contains"></a>contains
`contains (container, itemToFind)`

Vérifie si un tableau contient une valeur, un objet contient une clé ou une chaîne contient une sous-chaîne.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| conteneur |Oui |tableau, objet ou chaîne |valeur Hello contenant hello valeur toofind. |
| itemToFind |Oui |chaîne ou entier |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

**True** si l’élément de hello est trouvé ; sinon, **False**.

### <a name="examples"></a>Exemples

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Convertit des données tooa valeur URI.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToConvert |Oui |string |valeur tooconvert tooa les données de salutation URI. |

### <a name="return-value"></a>Valeur de retour

Une chaîne formatée en tant qu’URI de données.

### <a name="examples"></a>Exemples

Bonjour, l’exemple suivant convertit des données tooa valeur URI et convertit une chaîne d’URI tooa de données :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| dataUriOutput | String | data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | String | Hello, World! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Convertit un URI de données mise en forme de chaîne de valeur tooa.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Oui |string |données de salutation tooconvert de valeur d’URI. |

### <a name="return-value"></a>Valeur de retour

Chaîne contenant le hello de valeur convertie.

### <a name="examples"></a>Exemples

Bonjour, l’exemple suivant convertit des données tooa valeur URI et convertit une chaîne d’URI tooa de données :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| dataUriOutput | String | data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | String | Hello, World! |

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

### <a name="examples"></a>Exemples

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Détermine si une chaîne se termine par une valeur. comparaison de Hello respecte la casse.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToSearch |Oui |string |valeur Hello contenant hello élément toofind. |
| stringToFind |Oui |string |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

**True** si hello dernière ou les caractères de chaîne de hello correspond à hello ; sinon, **False**.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toouse hello startsWith et endsWith fonctions :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| startsTrue | Bool | true |
| startsCapTrue | Bool | true |
| startsFalse | Bool | False |
| endsTrue | Bool | true |
| endsCapTrue | Bool | true |
| endsFalse | Bool | False |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Retourne hello le premier caractère de la chaîne de hello ou le premier élément du tableau de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |premier élément Hello valeur tooretrieve hello ou caractère. |

### <a name="return-value"></a>Valeur de retour

Chaîne hello premier caractère, ou type hello (string, int, tableau ou objet) de hello premier élément dans un tableau.

### <a name="examples"></a>Exemples

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

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

Retourne hello première position d’une valeur dans une chaîne. comparaison de Hello respecte la casse.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToSearch |Oui |string |valeur Hello contenant hello élément toofind. |
| stringToFind |Oui |string |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

Entier qui représente la position de hello de hello élément toofind. valeur de Hello est de base zéro. Si l’élément de hello n’est pas trouvé, -1 est retourné.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toouse hello indexOf et lastIndexOf fonctions :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Retourne la dernière caractère de chaîne de hello ou hello dernier élément du tableau de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |dernier élément Hello valeur tooretrieve hello ou caractère. |

### <a name="return-value"></a>Valeur de retour

Une chaîne de caractères de dernière hello, ou type hello (string, int, tableau ou objet) de hello dernier élément d’un tableau.

### <a name="examples"></a>Exemples

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Retourne hello dernière position d’une valeur dans une chaîne. comparaison de Hello respecte la casse.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToSearch |Oui |string |valeur Hello contenant hello élément toofind. |
| stringToFind |Oui |string |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

Entier qui représente la dernière position de hello de hello élément toofind. valeur de Hello est de base zéro. Si l’élément de hello n’est pas trouvé, -1 est retourné.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toouse hello indexOf et lastIndexOf fonctions :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>length
`length(string)`

Retourne le nombre hello de caractères dans une chaîne ou les éléments dans un tableau.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| arg1 |Oui |tableau ou chaîne |Hello toouse de tableau pour l’obtention du nombre de hello d’éléments ou hello toouse de chaîne pour l’obtention du nombre de hello de caractères. |

### <a name="return-value"></a>Valeur de retour

Un entier. 

### <a name="examples"></a>Exemples

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

<a id="padleft" />

## <a name="padleft"></a>padLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Retourne une chaîne alignée à droite en ajoutant des caractères toohello gauche jusqu'à atteindre la longueur totale spécifiée hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| valeur_à_remplir |Oui |chaîne ou entier |Hello valeur tooright-aligner. |
| longueur_totale |Oui |int |Nombre total de Hello de caractères Bonjour a renvoyé la chaîne. |
| caractère_de_remplissage |Non |caractère unique |Bonjour toouse caractère de gauche-padding jusqu'à ce que la longueur totale hello est atteint. valeur par défaut de Hello est un espace. |

Si la chaîne d’origine de hello est plus longue que le nombre de hello de caractères toopad, aucuns caractères ne sont ajoutés.

### <a name="return-value"></a>Valeur de retour

Une chaîne avec hello au moins le nombre de caractères spécifiés.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toopad hello la valeur du paramètre fourni par l’utilisateur en ajoutant hello zéro caractère jusqu'à ce qu’il atteigne hello le nombre total de caractères. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| stringOutput | String | 0000000123 |

<a id="replace" />

## <a name="replace"></a>replace
`replace(originalString, oldString, newString)`

Renvoie une nouvelle chaîne dans laquelle toutes les instances d’une chaîne ont été remplacées par une autre.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_initiale |Oui |string |valeur de Hello qui a toutes les instances d’une chaîne remplacée par une autre chaîne. |
| oldString |Oui |string |Hello chaîne toobe est supprimé de la chaîne d’origine de hello. |
| newString |Oui |string |tooadd de chaîne Hello à la place de hello supprimé la chaîne. |

### <a name="return-value"></a>Valeur de retour

Une chaîne avec hello les caractères remplacés.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment tooremove tous les tirets à partir de la chaîne de hello fourni par l’utilisateur, et comment tooreplace partie hello chaîne par une autre chaîne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| firstOutput | String | 1231231234 |
| secodeOutput | String | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Retourne une chaîne contenant tous les caractères de hello après que hello spécifiée le nombre de caractères ou d’un tableau avec tous les éléments hello après hello nombre d’éléments.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| originalValue |Oui |tableau ou chaîne |Bonjour toouse tableau ou une chaîne pour l’ignorer. |
| numberToSkip |Oui |int |nombre de Hello d’éléments ou des caractères tooskip. Si cette valeur est inférieur ou égal à 0, tous les hello éléments ou dans la valeur de hello est renvoyé. Si elle est supérieure à la longueur du tableau de hello ou chaîne hello, un tableau vide ou une chaîne est retournée. |

### <a name="return-value"></a>Valeur de retour

Tableau ou chaîne.

### <a name="examples"></a>Exemples

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

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Retourne un tableau de chaînes qui contient les sous-chaînes hello Hello d’entrée de chaîne qui est délimitées par hello spécifié délimiteurs.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_entrée |Oui |string |toosplit de chaîne Hello. |
| delimiter |Oui |chaîne ou tableau de chaînes |Bonjour toouse délimiteur pour fractionner la chaîne de hello. |

### <a name="return-value"></a>Valeur de retour

Tableau de chaînes.

### <a name="examples"></a>Exemples

Hello exemple suivant fractionne hello la chaîne d’entrée avec une virgule et avec une virgule ou un point-virgule.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| firstOutput | Tableau | ["one", "two", "three"] |
| secondOutput | Tableau | ["one", "two", "three"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

Détermine si une chaîne commence par une valeur. comparaison de Hello respecte la casse.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToSearch |Oui |string |valeur Hello contenant hello élément toofind. |
| stringToFind |Oui |string |Hello toofind de valeur. |

### <a name="return-value"></a>Valeur de retour

**True** si hello premier caractère ou les caractères de chaîne de hello correspond à hello ; sinon, **False**.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment toouse hello startsWith et endsWith fonctions :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| startsTrue | Bool | true |
| startsCapTrue | Bool | true |
| startsFalse | Bool | False |
| endsTrue | Bool | true |
| endsCapTrue | Bool | true |
| endsFalse | Bool | False |

<a id="string" />

## <a name="string"></a>string
`string(valueToConvert)`

Convertit hello spécifié chaîne tooa de valeur.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| valueToConvert |Oui | Quelconque |Hello valeur tooconvert toostring. N’importe quel type de valeur peut être converti, y compris les objets et des tableaux. |

### <a name="return-value"></a>Valeur de retour

Une chaîne de valeur de hello converti.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment tooconvert différents types de valeurs toostrings :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| objectOutput | String | {"valueA":10,"valueB":"Example Text"} |
| arrayOutput | String | ["a","b","c"] |
| intOutput | String | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

Retourne une sous-chaîne qui commence à hello spécifié position de caractère que contient hello nombre spécifié de caractères.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_à_analyser |Oui |string |chaîne d’origine de Hello de quels hello sous-chaîne est extraite. |
| index_début |Non |int |Hello base zéro caractère position de départ de la sous-chaîne de hello. |
| length |Non |int |nombre de Hello de caractères pour la sous-chaîne de hello. Doit faire référence emplacement tooa au sein de la chaîne de hello. |

### <a name="return-value"></a>Valeur de retour

sous-chaîne de Hello.

### <a name="remarks"></a>Remarques

fonction Hello échoue lors de la sous-chaîne de hello s’étend au-delà de fin hello de chaîne de hello. Bonjour à l’exemple suivant échoue avec hello erreur « paramètres d’index et la longueur hello doivent faire référence emplacement tooa au sein de la chaîne de hello. Hello paramètre index : '0', hello paramètre de longueur : 11, hello longueur hello du paramètre de chaîne : « 10 ». ».

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant extrait une sous-chaîne à partir d’un paramètre.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| substringOutput | String | two |


<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Retourne une chaîne avec hello nombre spécifié de caractères à partir du début hello de hello chaîne ou un tableau avec hello spécifié le nombre d’éléments à partir du début hello du tableau de hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| originalValue |Oui |tableau ou chaîne |Bonjour les éléments de hello tootake tableau ou une chaîne à partir de. |
| numberToTake |Oui |int |nombre de Hello d’éléments ou des caractères tootake. Si cette valeur est inférieure ou égale à 0, une chaîne ou un tableau vide est renvoyé. Si elle est supérieure à la longueur de hello Hello donné de tableau ou une chaîne, tous les éléments hello hello tableau ou une chaîne sont retournés. |

### <a name="return-value"></a>Valeur de retour

Tableau ou chaîne.

### <a name="examples"></a>Exemples

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Convertit hello spécifié cas toolower de chaîne.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_à_modifier |Oui |string |cas de Hello valeur tooconvert toolower. |

### <a name="return-value"></a>Valeur de retour

chaîne de Hello converti toolower cas.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant convertit un cas de toolower de valeur de paramètre et les cas de tooupper.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| toLowerOutput | String | one two three |
| toUpperOutput | String | ONE TWO THREE |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Convertit hello spécifié cas tooupper de chaîne.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| chaîne_à_modifier |Oui |string |cas de Hello valeur tooconvert tooupper. |

### <a name="return-value"></a>Valeur de retour

chaîne de Hello converti tooupper cas.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant convertit un cas de toolower de valeur de paramètre et les cas de tooupper.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| toLowerOutput | String | one two three |
| toUpperOutput | String | ONE TWO THREE |

<a id="trim" />

## <a name="trim"></a>découper
`trim (stringToTrim)`

Supprime tous les premiers et derniers caractères d’espace blanc de hello de chaîne spécifiée.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToTrim |Oui |string |Hello tootrim de valeur. |

### <a name="return-value"></a>Valeur de retour

chaîne Hello sans les premiers et derniers caractères d’espace blanc.

### <a name="examples"></a>Exemples

Hello exemple suivant supprime les caractères d’espace blanc de hello de paramètre hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| return | String | one two three |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Crée une chaîne de hachage déterministe en fonction des valeurs hello fournies comme paramètres. 

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| baseString |Oui |string |valeur de Hello utilisé dans toocreate de fonction de hachage hello une chaîne unique. |
| paramètres supplémentaires le cas échéant |Non |string |Vous pouvez ajouter autant de chaînes en tant que valeur hello toocreate requis qui spécifie le niveau de hello d’unicité. |

### <a name="remarks"></a>Remarques

Cette fonction est utile lorsque vous avez besoin de toocreate un nom unique pour une ressource. Vous fournissez des valeurs des paramètres qui limitent la portée hello d’unicité pour résultat de hello. Vous pouvez spécifier si les nom de hello est unique vers le bas toosubscription, groupe de ressources ou le déploiement. 

Hello retourné la valeur n’est pas une chaîne aléatoire, mais plutôt hello résultat d’une fonction de hachage. Hello retourné la valeur est 13 caractères. Elle n’est pas globalement unique. Vous souhaiterez valeur hello de toocombine avec un préfixe à partir de votre toocreate de convention d’affectation de noms un nom significatif. Hello suivant montre format hello Hello retourné de valeur. valeur Hello varie selon le hello paramètres fourni.

    tcvhiyu5h2o5o

Hello suivant exemples montrent comment toocreate d’uniqueString toouse unique valeur couramment utilisés niveaux.

Toosubscription étendue unique

```json
"[uniqueString(subscription().subscriptionId)]"
```

Groupe de tooresource étendue unique

```json
"[uniqueString(resourceGroup().id)]"
```

Unique toodeployment étendue pour un groupe de ressources

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

Bonjour à l’exemple suivant montre comment toocreate un nom unique pour un compte de stockage en fonction de votre groupe de ressources. À l’intérieur du groupe de ressources hello, nom de hello n’est pas unique si construit hello identique.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Valeur de retour

Chaîne contenant 13 caractères.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant retourne les résultats d’uniquestring :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>URI
`uri (baseUri, relativeUri)`

Crée un URI absolu en combinant hello baseUri et la chaîne d’URI relatif hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| baseUri |Oui |string |chaîne d’uri de base Hello. |
| relativeUri |Oui |string |Hello uri relatif tooadd toohello uri de base chaîne. |

Hello valeur hello **baseUri** paramètre peut inclure un fichier spécifique, mais uniquement le chemin de base hello est utilisé lors de la construction hello URI. Par exemple, le passage `http://contoso.com/resources/azuredeploy.json` en tant que résultats de paramètre baseUri hello dans un URI de base `http://contoso.com/resources/`.

### <a name="return-value"></a>Valeur de retour

Chaîne représentant hello URI absolu pour les valeurs de base et relatifs hello.

### <a name="examples"></a>Exemples

Bonjour à l’exemple suivant montre comment tooconstruct un lien tooa imbriquée basées sur un modèle de valeur hello du modèle parent de hello.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Encode un URI.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| stringToEncode |Oui |string |Hello tooencode de valeur. |

### <a name="return-value"></a>Valeur de retour

Une chaîne de hello URI encodé de valeur.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Retourne une chaîne de la valeur encodée de l’URI.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Oui |string |Hello URI encodé de chaîne de valeur tooconvert tooa. |

### <a name="return-value"></a>Valeur de retour

Chaîne décodée de la valeur encodée de l’URI.

### <a name="examples"></a>Exemples

Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| uriOutput | String | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | String | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | String | http://contoso.com/resources/nested/azuredeploy.json |


## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

