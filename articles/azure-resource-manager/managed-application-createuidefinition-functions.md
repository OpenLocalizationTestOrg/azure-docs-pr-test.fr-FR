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
# <a name="createuidefinition-functions"></a><span data-ttu-id="7cc1b-103">Fonctions CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="7cc1b-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="7cc1b-104">Cette section contient des signatures hello pour toutes les fonctions prises en charge d’une CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="7cc1b-105">toouse une fonction de la déclaration de hello surround figurant entre crochets.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="7cc1b-106">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="7cc1b-107">Les chaînes et autres fonctions peuvent être référencées en tant que paramètres pour une fonction, mais les chaînes doivent être encadrées de guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="7cc1b-108">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="7cc1b-109">Le cas échéant, vous pouvez référencer des propriétés de sortie hello d’une fonction à l’aide de point hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="7cc1b-110">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="7cc1b-111">Fonctions de référencement</span><span class="sxs-lookup"><span data-stu-id="7cc1b-111">Referencing functions</span></span>
<span data-ttu-id="7cc1b-112">Ces fonctions peuvent être des sorties tooreference utilisés à partir des propriétés de hello ou contexte d’une CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="7cc1b-113">basics</span><span class="sxs-lookup"><span data-stu-id="7cc1b-113">basics</span></span>
<span data-ttu-id="7cc1b-114">Retourne les valeurs de sortie de hello d’un élément qui est défini à l’étape de principes de base hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="7cc1b-115">exemple Hello retourne sortie hello d’élément hello nommé `foo` à l’étape de principes de base hello :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="7cc1b-116">steps</span><span class="sxs-lookup"><span data-stu-id="7cc1b-116">steps</span></span>
<span data-ttu-id="7cc1b-117">Retourne les valeurs de sortie de hello d’un élément qui est défini à l’étape spécifiée de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="7cc1b-118">utiliser des valeurs de sortie hello tooget d’éléments à l’étape de principes de base hello, `basics()` à la place.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="7cc1b-119">exemple Hello retourne sortie hello d’élément hello nommé `bar` à l’étape hello nommé `foo`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="7cc1b-120">location</span><span class="sxs-lookup"><span data-stu-id="7cc1b-120">location</span></span>
<span data-ttu-id="7cc1b-121">Retourne l’emplacement hello sélectionné dans l’étape de principes de base hello ou le contexte actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="7cc1b-122">Hello suivant pourrait retourner `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="7cc1b-123">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-123">String functions</span></span>
<span data-ttu-id="7cc1b-124">Ces fonctions peuvent uniquement être utilisées avec des chaînes JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="7cc1b-125">concat</span><span class="sxs-lookup"><span data-stu-id="7cc1b-125">concat</span></span>
<span data-ttu-id="7cc1b-126">Concatène une ou plusieurs chaînes.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="7cc1b-127">Par exemple, si la valeur de la sortie hello `element1` si `"bar"`, cet exemple retourne la chaîne de hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="7cc1b-128">substring</span><span class="sxs-lookup"><span data-stu-id="7cc1b-128">substring</span></span>
<span data-ttu-id="7cc1b-129">Sous-chaîne de hello retourne Hello de chaîne spécifiée.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="7cc1b-130">Hello la sous-chaîne à l’index spécifié de hello et a hello la longueur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="7cc1b-131">Hello exemple suivant renvoie `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="7cc1b-132">replace</span><span class="sxs-lookup"><span data-stu-id="7cc1b-132">replace</span></span>
<span data-ttu-id="7cc1b-133">Retourne une chaîne dans laquelle toutes les occurrences de hello de chaîne spécifiée dans la chaîne actuelle de hello est remplacées par une autre chaîne.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="7cc1b-134">Hello exemple suivant renvoie `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="7cc1b-135">guid</span><span class="sxs-lookup"><span data-stu-id="7cc1b-135">guid</span></span>
<span data-ttu-id="7cc1b-136">Génère une chaîne globale unique (GUID).</span><span class="sxs-lookup"><span data-stu-id="7cc1b-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="7cc1b-137">Hello suivant pourrait retourner `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="7cc1b-138">toLower</span><span class="sxs-lookup"><span data-stu-id="7cc1b-138">toLower</span></span>
<span data-ttu-id="7cc1b-139">Retourne un toolowercase chaîne convertie.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="7cc1b-140">Hello exemple suivant renvoie `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="7cc1b-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="7cc1b-141">toUpper</span></span>
<span data-ttu-id="7cc1b-142">Retourne un toouppercase chaîne convertie.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="7cc1b-143">Hello exemple suivant renvoie `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="7cc1b-144">Fonctions de collection</span><span class="sxs-lookup"><span data-stu-id="7cc1b-144">Collection functions</span></span>
<span data-ttu-id="7cc1b-145">Ces fonctions peuvent être utilisées avec les collections, comme les chaînes JSON, les tableaux et les objets.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="7cc1b-146">contains</span><span class="sxs-lookup"><span data-stu-id="7cc1b-146">contains</span></span>
<span data-ttu-id="7cc1b-147">Retourne `true` si une chaîne contient hello sous-chaîne spécifiée, un tableau contient hello spécifié de valeur ou un objet contient la clé spécifiée de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-148">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-148">Example 1: string</span></span>
<span data-ttu-id="7cc1b-149">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-150">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-150">Example 2: array</span></span>
<span data-ttu-id="7cc1b-151">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-152">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-153">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-153">Example 3: object</span></span>
<span data-ttu-id="7cc1b-154">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7cc1b-155">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="7cc1b-156">length</span><span class="sxs-lookup"><span data-stu-id="7cc1b-156">length</span></span>
<span data-ttu-id="7cc1b-157">Retourne le nombre de hello de caractères dans une chaîne, hello nombre de valeurs dans un tableau ou hello nombre de clés dans un objet.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-158">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-158">Example 1: string</span></span>
<span data-ttu-id="7cc1b-159">Hello exemple suivant renvoie `6`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-160">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-160">Example 2: array</span></span>
<span data-ttu-id="7cc1b-161">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-162">Hello exemple suivant renvoie `3`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-163">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-163">Example 3: object</span></span>
<span data-ttu-id="7cc1b-164">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7cc1b-165">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="7cc1b-166">empty</span><span class="sxs-lookup"><span data-stu-id="7cc1b-166">empty</span></span>
<span data-ttu-id="7cc1b-167">Retourne `true` si la chaîne de hello, tableau ou un objet est null ou vide.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-168">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-168">Example 1: string</span></span>
<span data-ttu-id="7cc1b-169">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-170">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-170">Example 2: array</span></span>
<span data-ttu-id="7cc1b-171">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-172">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-173">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-173">Example 3: object</span></span>
<span data-ttu-id="7cc1b-174">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7cc1b-175">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="7cc1b-176">Exemple 4 : null et non défini</span><span class="sxs-lookup"><span data-stu-id="7cc1b-176">Example 4: null and undefined</span></span>
<span data-ttu-id="7cc1b-177">Supposons que `element1` est `null` ou n’est pas défini.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="7cc1b-178">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="7cc1b-179">first</span><span class="sxs-lookup"><span data-stu-id="7cc1b-179">first</span></span>
<span data-ttu-id="7cc1b-180">Retourne hello premier caractère de hello spécifié chaîne ; première valeur de tableau spécifié de hello ; ou hello première clé et la valeur de l’objet spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-181">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-181">Example 1: string</span></span>
<span data-ttu-id="7cc1b-182">Hello exemple suivant renvoie `"f"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-183">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-183">Example 2: array</span></span>
<span data-ttu-id="7cc1b-184">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-185">Hello exemple suivant renvoie `1`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-186">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-186">Example 3: object</span></span>
<span data-ttu-id="7cc1b-187">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="7cc1b-188">Hello exemple suivant renvoie `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="7cc1b-189">last</span><span class="sxs-lookup"><span data-stu-id="7cc1b-189">last</span></span>
<span data-ttu-id="7cc1b-190">Retourne hello dernier caractère de hello spécifié, hello dernière valeur de chaîne hello tableau spécifié, en ou hello dernière clé et la valeur de l’objet spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-191">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-191">Example 1: string</span></span>
<span data-ttu-id="7cc1b-192">Hello exemple suivant renvoie `"r"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-193">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-193">Example 2: array</span></span>
<span data-ttu-id="7cc1b-194">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-195">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-196">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-196">Example 3: object</span></span>
<span data-ttu-id="7cc1b-197">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7cc1b-198">Hello exemple suivant renvoie `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="7cc1b-199">take</span><span class="sxs-lookup"><span data-stu-id="7cc1b-199">take</span></span>
<span data-ttu-id="7cc1b-200">Retourne un nombre spécifié de caractères contigus à partir du début hello de chaîne de hello, un nombre spécifié de valeurs contiguës à partir du début hello du tableau de hello ou un nombre spécifié de clés contiguës et des valeurs de début hello d’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-201">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-201">Example 1: string</span></span>
<span data-ttu-id="7cc1b-202">Hello exemple suivant renvoie `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-203">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-203">Example 2: array</span></span>
<span data-ttu-id="7cc1b-204">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-205">Hello exemple suivant renvoie `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-206">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-206">Example 3: object</span></span>
<span data-ttu-id="7cc1b-207">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7cc1b-208">Hello exemple suivant renvoie `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="7cc1b-209">skip</span><span class="sxs-lookup"><span data-stu-id="7cc1b-209">skip</span></span>
<span data-ttu-id="7cc1b-210">Ignore un nombre spécifié d’éléments dans une collection et renvoie hello éléments restants.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7cc1b-211">Exemple 1 : chaîne</span><span class="sxs-lookup"><span data-stu-id="7cc1b-211">Example 1: string</span></span>
<span data-ttu-id="7cc1b-212">Hello exemple suivant renvoie `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7cc1b-213">Exemple 2 : tableau</span><span class="sxs-lookup"><span data-stu-id="7cc1b-213">Example 2: array</span></span>
<span data-ttu-id="7cc1b-214">Supposons que `element1` retourne `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7cc1b-215">Hello exemple suivant renvoie `[3]`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7cc1b-216">Example 3 : objet</span><span class="sxs-lookup"><span data-stu-id="7cc1b-216">Example 3: object</span></span>
<span data-ttu-id="7cc1b-217">Supposons que `element1` retourne :</span><span class="sxs-lookup"><span data-stu-id="7cc1b-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="7cc1b-218">Hello exemple suivant renvoie `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="7cc1b-219">Fonctions logiques</span><span class="sxs-lookup"><span data-stu-id="7cc1b-219">Logical functions</span></span>
<span data-ttu-id="7cc1b-220">Ces fonctions peuvent être utilisées dans des instructions conditionnelles.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="7cc1b-221">Certaines fonctions ne peuvent pas prendre en charge tous les types de données JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="7cc1b-222">equals</span><span class="sxs-lookup"><span data-stu-id="7cc1b-222">equals</span></span>
<span data-ttu-id="7cc1b-223">Retourne `true` si les deux paramètres ont hello même type et valeur.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="7cc1b-224">Cette fonction prend en charge tous les types de données JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="7cc1b-225">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="7cc1b-226">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="7cc1b-227">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="7cc1b-228">less</span><span class="sxs-lookup"><span data-stu-id="7cc1b-228">less</span></span>
<span data-ttu-id="7cc1b-229">Retourne `true` si hello premier paramètre est strictement inférieur au second paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="7cc1b-230">Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7cc1b-231">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="7cc1b-232">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="7cc1b-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="7cc1b-233">lessOrEquals</span></span>
<span data-ttu-id="7cc1b-234">Retourne `true` si hello premier paramètre est inférieur ou égal toohello deuxième paramètre.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="7cc1b-235">Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7cc1b-236">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="7cc1b-237">greater</span><span class="sxs-lookup"><span data-stu-id="7cc1b-237">greater</span></span>
<span data-ttu-id="7cc1b-238">Retourne `true` si hello premier paramètre est strictement supérieur au second paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="7cc1b-239">Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7cc1b-240">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="7cc1b-241">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="7cc1b-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="7cc1b-242">greaterOrEquals</span></span>
<span data-ttu-id="7cc1b-243">Retourne `true` si hello premier paramètre est supérieur ou égal toohello deuxième paramètre.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="7cc1b-244">Cette fonction prend en charge les paramètres de type nombre et chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7cc1b-245">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="7cc1b-246">and</span><span class="sxs-lookup"><span data-stu-id="7cc1b-246">and</span></span>
<span data-ttu-id="7cc1b-247">Retourne `true` si tous les paramètres de hello prennent trop`true`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="7cc1b-248">Cette fonction prend en charge plusieurs paramètres de type booléen uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="7cc1b-249">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="7cc1b-250">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="7cc1b-251">ou</span><span class="sxs-lookup"><span data-stu-id="7cc1b-251">or</span></span>
<span data-ttu-id="7cc1b-252">Retourne `true` si au moins un des paramètres de hello évalue trop`true`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="7cc1b-253">Cette fonction prend en charge plusieurs paramètres de type booléen uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="7cc1b-254">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="7cc1b-255">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="7cc1b-256">not</span><span class="sxs-lookup"><span data-stu-id="7cc1b-256">not</span></span>
<span data-ttu-id="7cc1b-257">Retourne `true` si le paramètre hello évalue trop`false`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="7cc1b-258">Cette fonction prend en charge les paramètres de type booléen uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="7cc1b-259">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="7cc1b-260">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="7cc1b-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="7cc1b-261">coalesce</span></span>
<span data-ttu-id="7cc1b-262">Retourne hello la valeur de paramètre non null de la première hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="7cc1b-263">Cette fonction prend en charge tous les types de données JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="7cc1b-264">Supposons que `element1` et `element2` ne soient pas définis.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="7cc1b-265">Hello exemple suivant renvoie `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="7cc1b-266">Fonctions de conversion</span><span class="sxs-lookup"><span data-stu-id="7cc1b-266">Conversion functions</span></span>
<span data-ttu-id="7cc1b-267">Ces fonctions peuvent être des valeurs de tooconvert utilisés entre les encodages et types de données JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="7cc1b-268">int</span><span class="sxs-lookup"><span data-stu-id="7cc1b-268">int</span></span>
<span data-ttu-id="7cc1b-269">Convertit l’entier de tooan paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="7cc1b-270">Cette fonction prend en charge les paramètres de type nombre et chaîne.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="7cc1b-271">Hello exemple suivant renvoie `1`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="7cc1b-272">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="7cc1b-273">float</span><span class="sxs-lookup"><span data-stu-id="7cc1b-273">float</span></span>
<span data-ttu-id="7cc1b-274">Convertit tooa de paramètre hello à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="7cc1b-275">Cette fonction prend en charge les paramètres de type nombre et chaîne.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="7cc1b-276">Hello exemple suivant renvoie `1.0`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="7cc1b-277">Hello exemple suivant renvoie `2.9`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="7cc1b-278">string</span><span class="sxs-lookup"><span data-stu-id="7cc1b-278">string</span></span>
<span data-ttu-id="7cc1b-279">Convertit la chaîne hello paramètres tooa.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="7cc1b-280">Cette fonction prend en charge les paramètres de tous les types de données JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="7cc1b-281">Hello exemple suivant renvoie `"1"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="7cc1b-282">Hello exemple suivant renvoie `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="7cc1b-283">Hello exemple suivant renvoie `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="7cc1b-284">Hello exemple suivant renvoie `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="7cc1b-285">bool</span><span class="sxs-lookup"><span data-stu-id="7cc1b-285">bool</span></span>
<span data-ttu-id="7cc1b-286">Convertit hello tooa de paramètre de type Boolean.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="7cc1b-287">Cette fonction prend en charge les paramètres de type nombre, chaîne et booléen.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="7cc1b-288">TooBooleans similaires dans JavaScript, toute valeur sauf `0` ou `'false'` retourne `true`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="7cc1b-289">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="7cc1b-290">Hello exemple suivant renvoie `false`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="7cc1b-291">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="7cc1b-292">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="7cc1b-293">parse</span><span class="sxs-lookup"><span data-stu-id="7cc1b-293">parse</span></span>
<span data-ttu-id="7cc1b-294">Convertit le type natif du paramètre tooa hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="7cc1b-295">En d’autres termes, cette fonction est inverse hello de `string()`.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="7cc1b-296">Cette fonction prend en charge les paramètres de type chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7cc1b-297">Hello exemple suivant renvoie `1`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="7cc1b-298">Hello exemple suivant renvoie `true`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="7cc1b-299">Hello exemple suivant renvoie `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="7cc1b-300">Hello exemple suivant renvoie `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="7cc1b-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="7cc1b-301">encodeBase64</span></span>
<span data-ttu-id="7cc1b-302">Encode la chaîne codée en base 64 tooa du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="7cc1b-303">Cette fonction prend en charge les paramètres de type chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7cc1b-304">Hello exemple suivant renvoie `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="7cc1b-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="7cc1b-305">decodeBase64</span></span>
<span data-ttu-id="7cc1b-306">Décode le paramètre hello à partir d’une chaîne codée en base 64.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="7cc1b-307">Cette fonction prend en charge les paramètres de type chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7cc1b-308">Hello exemple suivant renvoie `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="7cc1b-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="7cc1b-309">encodeUriComponent</span></span>
<span data-ttu-id="7cc1b-310">Encode la chaîne d’URL encodée hello paramètre tooa.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="7cc1b-311">Cette fonction prend en charge les paramètres de type chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7cc1b-312">Hello exemple suivant renvoie `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="7cc1b-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="7cc1b-313">decodeUriComponent</span></span>
<span data-ttu-id="7cc1b-314">Décode le paramètre hello à partir d’une chaîne d’URL encodée.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="7cc1b-315">Cette fonction prend en charge les paramètres de type chaîne uniquement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7cc1b-316">Hello exemple suivant renvoie `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="7cc1b-317">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="7cc1b-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="7cc1b-318">add</span><span class="sxs-lookup"><span data-stu-id="7cc1b-318">add</span></span>
<span data-ttu-id="7cc1b-319">Ajoute deux nombres et retourne le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="7cc1b-320">Hello exemple suivant renvoie `3`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="7cc1b-321">sub</span><span class="sxs-lookup"><span data-stu-id="7cc1b-321">sub</span></span>
<span data-ttu-id="7cc1b-322">Soustrait hello deuxième nombre hello premier et retourne le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="7cc1b-323">Hello exemple suivant renvoie `1`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="7cc1b-324">mul</span><span class="sxs-lookup"><span data-stu-id="7cc1b-324">mul</span></span>
<span data-ttu-id="7cc1b-325">Multiplie deux nombres et retourne le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="7cc1b-326">Hello exemple suivant renvoie `6`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="7cc1b-327">div</span><span class="sxs-lookup"><span data-stu-id="7cc1b-327">div</span></span>
<span data-ttu-id="7cc1b-328">Divise le premier nombre de hello par hello deuxième et retourne le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="7cc1b-329">Hello résultat est toujours un entier.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-329">hello result is always an integer.</span></span>

<span data-ttu-id="7cc1b-330">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="7cc1b-331">mod</span><span class="sxs-lookup"><span data-stu-id="7cc1b-331">mod</span></span>
<span data-ttu-id="7cc1b-332">Divise le premier nombre de hello par hello deuxième et retourne le reste de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="7cc1b-333">Hello exemple suivant renvoie `0`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="7cc1b-334">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="7cc1b-335">Min</span><span class="sxs-lookup"><span data-stu-id="7cc1b-335">min</span></span>
<span data-ttu-id="7cc1b-336">Retourne hello petit des nombres de hello deux.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="7cc1b-337">Hello exemple suivant renvoie `1`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="7cc1b-338">max</span><span class="sxs-lookup"><span data-stu-id="7cc1b-338">max</span></span>
<span data-ttu-id="7cc1b-339">Hello de retourne plus grand de deux nombres de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="7cc1b-340">Hello exemple suivant renvoie `2`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="7cc1b-341">range</span><span class="sxs-lookup"><span data-stu-id="7cc1b-341">range</span></span>
<span data-ttu-id="7cc1b-342">Génère une séquence d’intégrale numéros dans hello spécifiés de plage.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="7cc1b-343">Hello exemple suivant renvoie `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="7cc1b-344">rand</span><span class="sxs-lookup"><span data-stu-id="7cc1b-344">rand</span></span>
<span data-ttu-id="7cc1b-345">Retourne un élément aléatoire un nombre intégral de hello spécifié de plage.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="7cc1b-346">Cette fonction ne génère pas de nombres aléatoires sécurisés par chiffrement.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="7cc1b-347">Hello suivant pourrait retourner `42`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="7cc1b-348">floor</span><span class="sxs-lookup"><span data-stu-id="7cc1b-348">floor</span></span>
<span data-ttu-id="7cc1b-349">Retourne des hello plus grand entier inférieur ou égal toohello de nombre spécifié.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="7cc1b-350">Hello exemple suivant renvoie `3`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="7cc1b-351">ceil</span><span class="sxs-lookup"><span data-stu-id="7cc1b-351">ceil</span></span>
<span data-ttu-id="7cc1b-352">Retourne hello plus grand entier supérieur ou égal toohello spécifié nombre.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="7cc1b-353">Hello exemple suivant renvoie `4`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="7cc1b-354">Fonctions de date</span><span class="sxs-lookup"><span data-stu-id="7cc1b-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="7cc1b-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="7cc1b-355">utcNow</span></span>
<span data-ttu-id="7cc1b-356">Retourne une chaîne au format ISO 8601 de hello date et l’heure sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="7cc1b-357">Hello suivant pourrait retourner `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="7cc1b-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="7cc1b-358">addSeconds</span></span>
<span data-ttu-id="7cc1b-359">Ajoute un nombre intégral de toohello de secondes spécifié timestamp.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="7cc1b-360">Hello exemple suivant renvoie `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="7cc1b-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="7cc1b-361">addMinutes</span></span>
<span data-ttu-id="7cc1b-362">Ajoute un nombre intégral de toohello de minutes spécifié timestamp.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="7cc1b-363">Hello exemple suivant renvoie `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="7cc1b-364">addHours</span><span class="sxs-lookup"><span data-stu-id="7cc1b-364">addHours</span></span>
<span data-ttu-id="7cc1b-365">Ajoute un nombre intégral de toohello d’heures spécifié timestamp.</span><span class="sxs-lookup"><span data-stu-id="7cc1b-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="7cc1b-366">Hello exemple suivant renvoie `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7cc1b-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="7cc1b-367">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7cc1b-367">Next steps</span></span>
* <span data-ttu-id="7cc1b-368">Pour une introduction tooAzure Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cc1b-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

