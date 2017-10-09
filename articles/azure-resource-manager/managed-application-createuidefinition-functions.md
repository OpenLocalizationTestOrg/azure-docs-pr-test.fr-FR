---
title: "aaaAzure Application managée créer des fonctions de définition de l’interface utilisateur | Documents Microsoft"
description: "Décrit les hello fonctions toouse lors de la construction des définitions d’interface utilisateur pour les Applications managées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a>Fonctions CreateUiDefinition
Cette section contient des signatures hello pour toutes les fonctions prises en charge d’une CreateUiDefinition.

toouse une fonction de la déclaration de hello surround figurant entre crochets. Par exemple :

```json
"[function()]"
```

Les chaînes et autres fonctions peuvent être référencées en tant que paramètres pour une fonction, mais les chaînes doivent être encadrées de guillemets simples. Par exemple :

```json
"[fn1(fn2(), 'foobar')]"
```

Le cas échéant, vous pouvez référencer des propriétés de sortie hello d’une fonction à l’aide de point hello. Par exemple :

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Fonctions de référencement
Ces fonctions peuvent être des sorties tooreference utilisés à partir des propriétés de hello ou contexte d’une CreateUiDefinition.

### <a name="basics"></a>basics
Retourne les valeurs de sortie de hello d’un élément qui est défini à l’étape de principes de base hello.

exemple Hello retourne sortie hello d’élément hello nommé `foo` à l’étape de principes de base hello :

```json
"[basics('foo')]"
```

### <a name="steps"></a>steps
Retourne les valeurs de sortie de hello d’un élément qui est défini à l’étape spécifiée de hello. utiliser des valeurs de sortie hello tooget d’éléments à l’étape de principes de base hello, `basics()` à la place.

exemple Hello retourne sortie hello d’élément hello nommé `bar` à l’étape hello nommé `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Retourne l’emplacement hello sélectionné dans l’étape de principes de base hello ou le contexte actuel de hello.

Hello suivant pourrait retourner `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Fonctions de chaîne
Ces fonctions peuvent uniquement être utilisées avec des chaînes JSON.

### <a name="concat"></a>concat
Concatène une ou plusieurs chaînes.

Par exemple, si la valeur de la sortie hello `element1` si `"bar"`, cet exemple retourne la chaîne de hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Sous-chaîne de hello retourne Hello de chaîne spécifiée. Hello la sous-chaîne à l’index spécifié de hello et a hello la longueur spécifiée.

Hello exemple suivant renvoie `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>replace
Retourne une chaîne dans laquelle toutes les occurrences de hello de chaîne spécifiée dans la chaîne actuelle de hello est remplacées par une autre chaîne.

Hello exemple suivant renvoie `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>guid
Génère une chaîne globale unique (GUID).

Hello suivant pourrait retourner `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Retourne un toolowercase chaîne convertie.

Hello exemple suivant renvoie `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Retourne un toouppercase chaîne convertie.

Hello exemple suivant renvoie `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Fonctions de collection
Ces fonctions peuvent être utilisées avec les collections, comme les chaînes JSON, les tableaux et les objets.

### <a name="contains"></a>contains
Retourne `true` si une chaîne contient hello sous-chaîne spécifiée, un tableau contient hello spécifié de valeur ou un objet contient la clé spécifiée de hello.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello exemple suivant renvoie `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
Retourne le nombre de hello de caractères dans une chaîne, hello nombre de valeurs dans un tableau ou hello nombre de clés dans un objet.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello exemple suivant renvoie `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
Retourne `true` si la chaîne de hello, tableau ou un objet est null ou vide.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello exemple suivant renvoie `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Exemple 4 : null et non défini
Supposons que `element1` est `null` ou n’est pas défini. Hello exemple suivant renvoie `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
Retourne hello premier caractère de hello spécifié chaîne ; première valeur de tableau spécifié de hello ; ou hello première clé et la valeur de l’objet spécifié de hello.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello exemple suivant renvoie `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
Retourne hello dernier caractère de hello spécifié, hello dernière valeur de chaîne hello tableau spécifié, en ou hello dernière clé et la valeur de l’objet spécifié de hello.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello exemple suivant renvoie `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
Retourne un nombre spécifié de caractères contigus à partir du début hello de chaîne de hello, un nombre spécifié de valeurs contiguës à partir du début hello du tableau de hello ou un nombre spécifié de clés contiguës et des valeurs de début hello d’objet de hello.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello exemple suivant renvoie `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
Ignore un nombre spécifié d’éléments dans une collection et renvoie hello éléments restants.

#### <a name="example-1-string"></a>Exemple 1 : chaîne
Hello exemple suivant renvoie `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Exemple 2 : tableau
Supposons que `element1` retourne `[1, 2, 3]`. Hello exemple suivant renvoie `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Example 3 : objet
Supposons que `element1` retourne :

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello exemple suivant renvoie `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Fonctions logiques
Ces fonctions peuvent être utilisées dans des instructions conditionnelles. Certaines fonctions ne peuvent pas prendre en charge tous les types de données JSON.

### <a name="equals"></a>equals
Retourne `true` si les deux paramètres ont hello même type et valeur. Cette fonction prend en charge tous les types de données JSON.

Hello exemple suivant renvoie `true`:

```json
"[equals(0, 0)]"
```

Hello exemple suivant renvoie `true`:

```json
"[equals('foo', 'foo')]"
```

Hello exemple suivant renvoie `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
Retourne `true` si hello premier paramètre est strictement inférieur au second paramètre de hello. Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.

Hello exemple suivant renvoie `true`:

```json
"[less(1, 2)]"
```

Hello exemple suivant renvoie `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Retourne `true` si hello premier paramètre est inférieur ou égal toohello deuxième paramètre. Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.

Hello exemple suivant renvoie `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
Retourne `true` si hello premier paramètre est strictement supérieur au second paramètre de hello. Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.

Hello exemple suivant renvoie `false`:

```json
"[greater(1, 2)]"
```

Hello exemple suivant renvoie `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Retourne `true` si hello premier paramètre est supérieur ou égal toohello deuxième paramètre. Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.

Hello exemple suivant renvoie `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>and
Retourne `true` si tous les paramètres de hello prennent trop`true`. Cette fonction prend en charge plusieurs paramètres de type booléen uniquement.

Hello exemple suivant renvoie `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello exemple suivant renvoie `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>ou
Retourne `true` si au moins un des paramètres de hello évalue trop`true`. Cette fonction prend en charge plusieurs paramètres de type booléen uniquement.

Hello exemple suivant renvoie `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello exemple suivant renvoie `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>not
Retourne `true` si le paramètre hello évalue trop`false`. Cette fonction prend en charge les paramètres de type booléen uniquement.

Hello exemple suivant renvoie `true`:

```json
"[not(false)]"
```

Hello exemple suivant renvoie `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
Retourne hello la valeur de paramètre non null de la première hello. Cette fonction prend en charge tous les types de données JSON.

Supposons que `element1` et `element2` ne soient pas définis. Hello exemple suivant renvoie `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Fonctions de conversion
Ces fonctions peuvent être des valeurs de tooconvert utilisés entre les encodages et types de données JSON.

### <a name="int"></a>int
Convertit l’entier de tooan paramètre hello. Cette fonction prend en charge les paramètres de type nombre et chaîne.

Hello exemple suivant renvoie `1`:

```json
"[int('1')]"
```

Hello exemple suivant renvoie `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float
Convertit tooa de paramètre hello à virgule flottante. Cette fonction prend en charge les paramètres de type nombre et chaîne.

Hello exemple suivant renvoie `1.0`:

```json
"[float('1.0')]"
```

Hello exemple suivant renvoie `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>string
Convertit la chaîne hello paramètres tooa. Cette fonction prend en charge les paramètres de tous les types de données JSON.

Hello exemple suivant renvoie `"1"`:

```json
"[string(1)]"
```

Hello exemple suivant renvoie `"2.9"`:

```json
"[string(2.9)]"
```

Hello exemple suivant renvoie `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Hello exemple suivant renvoie `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Convertit hello tooa de paramètre de type Boolean. Cette fonction prend en charge les paramètres de type nombre, chaîne et booléen. TooBooleans similaires dans JavaScript, toute valeur sauf `0` ou `'false'` retourne `true`.

Hello exemple suivant renvoie `true`:

```json
"[bool(1)]"
```

Hello exemple suivant renvoie `false`:

```json
"[bool(0)]"
```

Hello exemple suivant renvoie `true`:

```json
"[bool(true)]"
```

Hello exemple suivant renvoie `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
Convertit le type natif du paramètre tooa hello. En d’autres termes, cette fonction est inverse hello de `string()`. Cette fonction prend en charge les paramètres de type chaîne uniquement.

Hello exemple suivant renvoie `1`:

```json
"[parse('1')]"
```

Hello exemple suivant renvoie `true`:

```json
"[parse('true')]"
```

Hello exemple suivant renvoie `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Hello exemple suivant renvoie `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Encode la chaîne codée en base 64 tooa du paramètre hello. Cette fonction prend en charge les paramètres de type chaîne uniquement.

Hello exemple suivant renvoie `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Décode le paramètre hello à partir d’une chaîne codée en base 64. Cette fonction prend en charge les paramètres de type chaîne uniquement.

Hello exemple suivant renvoie `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Encode la chaîne d’URL encodée hello paramètre tooa. Cette fonction prend en charge les paramètres de type chaîne uniquement.

Hello exemple suivant renvoie `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Décode le paramètre hello à partir d’une chaîne d’URL encodée. Cette fonction prend en charge les paramètres de type chaîne uniquement.

Hello exemple suivant renvoie `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Fonctions mathématiques
### <a name="add"></a>add
Ajoute deux nombres et retourne le résultat de hello.

Hello exemple suivant renvoie `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Soustrait hello deuxième nombre hello premier et retourne le résultat de hello.

Hello exemple suivant renvoie `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Multiplie deux nombres et retourne le résultat de hello.

Hello exemple suivant renvoie `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Divise le premier nombre de hello par hello deuxième et retourne le résultat de hello. Hello résultat est toujours un entier.

Hello exemple suivant renvoie `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Divise le premier nombre de hello par hello deuxième et retourne le reste de hello.

Hello exemple suivant renvoie `0`:

```json
"[mod(6, 3)]"
```

Hello exemple suivant renvoie `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
Retourne hello petit des nombres de hello deux.

Hello exemple suivant renvoie `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Hello de retourne plus grand de deux nombres de hello.

Hello exemple suivant renvoie `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
Génère une séquence d’intégrale numéros dans hello spécifiés de plage.

Hello exemple suivant renvoie `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Retourne un élément aléatoire un nombre intégral de hello spécifié de plage. Cette fonction ne génère pas de nombres aléatoires sécurisés par chiffrement.

Hello suivant pourrait retourner `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
Retourne des hello plus grand entier inférieur ou égal toohello de nombre spécifié.

Hello exemple suivant renvoie `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Retourne hello plus grand entier supérieur ou égal toohello spécifié nombre.

Hello exemple suivant renvoie `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Fonctions de date
### <a name="utcnow"></a>utcNow
Retourne une chaîne au format ISO 8601 de hello date et l’heure sur l’ordinateur local de hello.

Hello suivant pourrait retourner `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Ajoute un nombre intégral de toohello de secondes spécifié timestamp.

Hello exemple suivant renvoie `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Ajoute un nombre intégral de toohello de minutes spécifié timestamp.

Hello exemple suivant renvoie `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Ajoute un nombre intégral de toohello d’heures spécifié timestamp.

Hello exemple suivant renvoie `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction tooAzure Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

