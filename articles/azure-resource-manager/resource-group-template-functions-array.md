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
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="7bfeb-103">Fonctions de tableau et d’objet pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7bfeb-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="7bfeb-104">Resource Manager fournit les fonctions ci-après pour travailler avec des tableaux et des objets.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="7bfeb-105">array</span><span class="sxs-lookup"><span data-stu-id="7bfeb-105">array</span></span>](#array)
* [<span data-ttu-id="7bfeb-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="7bfeb-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="7bfeb-107">concat</span><span class="sxs-lookup"><span data-stu-id="7bfeb-107">concat</span></span>](#concat)
* [<span data-ttu-id="7bfeb-108">contains</span><span class="sxs-lookup"><span data-stu-id="7bfeb-108">contains</span></span>](#contains)
* [<span data-ttu-id="7bfeb-109">createArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="7bfeb-110">empty</span><span class="sxs-lookup"><span data-stu-id="7bfeb-110">empty</span></span>](#empty)
* [<span data-ttu-id="7bfeb-111">first</span><span class="sxs-lookup"><span data-stu-id="7bfeb-111">first</span></span>](#first)
* [<span data-ttu-id="7bfeb-112">intersection</span><span class="sxs-lookup"><span data-stu-id="7bfeb-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="7bfeb-113">json</span><span class="sxs-lookup"><span data-stu-id="7bfeb-113">json</span></span>](#json)
* [<span data-ttu-id="7bfeb-114">last</span><span class="sxs-lookup"><span data-stu-id="7bfeb-114">last</span></span>](#last)
* [<span data-ttu-id="7bfeb-115">length</span><span class="sxs-lookup"><span data-stu-id="7bfeb-115">length</span></span>](#length)
* [<span data-ttu-id="7bfeb-116">min</span><span class="sxs-lookup"><span data-stu-id="7bfeb-116">min</span></span>](#min)
* [<span data-ttu-id="7bfeb-117">max</span><span class="sxs-lookup"><span data-stu-id="7bfeb-117">max</span></span>](#max)
* [<span data-ttu-id="7bfeb-118">range</span><span class="sxs-lookup"><span data-stu-id="7bfeb-118">range</span></span>](#range)
* [<span data-ttu-id="7bfeb-119">skip</span><span class="sxs-lookup"><span data-stu-id="7bfeb-119">skip</span></span>](#skip)
* [<span data-ttu-id="7bfeb-120">take</span><span class="sxs-lookup"><span data-stu-id="7bfeb-120">take</span></span>](#take)
* [<span data-ttu-id="7bfeb-121">union</span><span class="sxs-lookup"><span data-stu-id="7bfeb-121">union</span></span>](#union)

<span data-ttu-id="7bfeb-122">tooget un tableau de valeurs de chaîne délimitée par une valeur, consultez [fractionner](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="7bfeb-123">array</span><span class="sxs-lookup"><span data-stu-id="7bfeb-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="7bfeb-124">Convertit un tableau de tooan valeur hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-125">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-125">Parameters</span></span>

| <span data-ttu-id="7bfeb-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-126">Parameter</span></span> | <span data-ttu-id="7bfeb-127">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-127">Required</span></span> | <span data-ttu-id="7bfeb-128">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-128">Type</span></span> | <span data-ttu-id="7bfeb-129">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-130">convertToArray</span></span> |<span data-ttu-id="7bfeb-131">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-131">Yes</span></span> |<span data-ttu-id="7bfeb-132">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="7bfeb-132">int, string, array, or object</span></span> |<span data-ttu-id="7bfeb-133">tableau de tooan valeur tooconvert Hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-134">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-134">Return value</span></span>

<span data-ttu-id="7bfeb-135">Tableau.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-136">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-136">Example</span></span>

<span data-ttu-id="7bfeb-137">Hello suivant montre comment toouse hello fonction array avec des types différents.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="7bfeb-138">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-139">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-139">Name</span></span> | <span data-ttu-id="7bfeb-140">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-140">Type</span></span> | <span data-ttu-id="7bfeb-141">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-142">intOutput</span></span> | <span data-ttu-id="7bfeb-143">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-143">Array</span></span> | <span data-ttu-id="7bfeb-144">[1]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-144">[1]</span></span> |
| <span data-ttu-id="7bfeb-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-145">stringOutput</span></span> | <span data-ttu-id="7bfeb-146">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-146">Array</span></span> | <span data-ttu-id="7bfeb-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-147">["a"]</span></span> |
| <span data-ttu-id="7bfeb-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-148">objectOutput</span></span> | <span data-ttu-id="7bfeb-149">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-149">Array</span></span> | <span data-ttu-id="7bfeb-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="7bfeb-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="7bfeb-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="7bfeb-152">Retourne la première valeur non null à partir des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="7bfeb-153">Les chaînes vides, les tableaux vides et les objets vides ne sont pas null.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-154">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-154">Parameters</span></span>

| <span data-ttu-id="7bfeb-155">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-155">Parameter</span></span> | <span data-ttu-id="7bfeb-156">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-156">Required</span></span> | <span data-ttu-id="7bfeb-157">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-157">Type</span></span> | <span data-ttu-id="7bfeb-158">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-159">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-159">arg1</span></span> |<span data-ttu-id="7bfeb-160">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-160">Yes</span></span> |<span data-ttu-id="7bfeb-161">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="7bfeb-161">int, string, array, or object</span></span> |<span data-ttu-id="7bfeb-162">Bonjour premier tootest de valeur pour la valeur null.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="7bfeb-163">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bfeb-163">additional args</span></span> |<span data-ttu-id="7bfeb-164">Non</span><span class="sxs-lookup"><span data-stu-id="7bfeb-164">No</span></span> |<span data-ttu-id="7bfeb-165">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="7bfeb-165">int, string, array, or object</span></span> |<span data-ttu-id="7bfeb-166">Tootest des valeurs supplémentaires pour la valeur null.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-167">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-167">Return value</span></span>

<span data-ttu-id="7bfeb-168">valeur Hello de paramètres non null première hello, qui peut être une chaîne, un int, un tableau ou un objet.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="7bfeb-169">Null si tous les paramètres sont null.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="7bfeb-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-170">Example</span></span>

<span data-ttu-id="7bfeb-171">Hello suivant montre différentes utilisations de coalesce sortie hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="7bfeb-172">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-173">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-173">Name</span></span> | <span data-ttu-id="7bfeb-174">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-174">Type</span></span> | <span data-ttu-id="7bfeb-175">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-176">stringOutput</span></span> | <span data-ttu-id="7bfeb-177">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-177">String</span></span> | <span data-ttu-id="7bfeb-178">default</span><span class="sxs-lookup"><span data-stu-id="7bfeb-178">default</span></span> |
| <span data-ttu-id="7bfeb-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-179">intOutput</span></span> | <span data-ttu-id="7bfeb-180">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-180">Int</span></span> | <span data-ttu-id="7bfeb-181">1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-181">1</span></span> |
| <span data-ttu-id="7bfeb-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-182">objectOutput</span></span> | <span data-ttu-id="7bfeb-183">Object</span><span class="sxs-lookup"><span data-stu-id="7bfeb-183">Object</span></span> | <span data-ttu-id="7bfeb-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="7bfeb-184">{"first": "default"}</span></span> |
| <span data-ttu-id="7bfeb-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-185">arrayOutput</span></span> | <span data-ttu-id="7bfeb-186">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-186">Array</span></span> | <span data-ttu-id="7bfeb-187">[1]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-187">[1]</span></span> |
| <span data-ttu-id="7bfeb-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-188">emptyOutput</span></span> | <span data-ttu-id="7bfeb-189">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-189">Bool</span></span> | <span data-ttu-id="7bfeb-190">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="7bfeb-191">concat</span><span class="sxs-lookup"><span data-stu-id="7bfeb-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="7bfeb-192">Combine plusieurs tableaux et retourne un tableau hello concaténée, ou combine plusieurs valeurs de chaîne et retourne la chaîne de hello concaténé.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7bfeb-193">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-193">Parameters</span></span>

| <span data-ttu-id="7bfeb-194">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-194">Parameter</span></span> | <span data-ttu-id="7bfeb-195">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-195">Required</span></span> | <span data-ttu-id="7bfeb-196">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-196">Type</span></span> | <span data-ttu-id="7bfeb-197">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-198">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-198">arg1</span></span> |<span data-ttu-id="7bfeb-199">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-199">Yes</span></span> |<span data-ttu-id="7bfeb-200">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-200">array or string</span></span> |<span data-ttu-id="7bfeb-201">Bonjour premier tableau ou une chaîne pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="7bfeb-202">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bfeb-202">additional arguments</span></span> |<span data-ttu-id="7bfeb-203">Non</span><span class="sxs-lookup"><span data-stu-id="7bfeb-203">No</span></span> |<span data-ttu-id="7bfeb-204">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-204">array or string</span></span> |<span data-ttu-id="7bfeb-205">Tableaux ou chaînes supplémentaires en ordre séquentiel pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="7bfeb-206">Cette fonction peut prendre n’importe quel nombre d’arguments et peut accepter des chaînes ou des tableaux de paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="7bfeb-207">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-207">Return value</span></span>
<span data-ttu-id="7bfeb-208">Chaîne ou tableau de valeurs concaténées.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-209">Example</span></span>

<span data-ttu-id="7bfeb-210">Bonjour à l’exemple suivant montre comment toocombine deux tableaux.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="7bfeb-211">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-212">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-212">Name</span></span> | <span data-ttu-id="7bfeb-213">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-213">Type</span></span> | <span data-ttu-id="7bfeb-214">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-215">return</span><span class="sxs-lookup"><span data-stu-id="7bfeb-215">return</span></span> | <span data-ttu-id="7bfeb-216">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-216">Array</span></span> | <span data-ttu-id="7bfeb-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="7bfeb-218">Bonjour à l’exemple suivant montre comment toocombine deux valeurs de chaîne et retourne une chaîne concaténée.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="7bfeb-219">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-220">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-220">Name</span></span> | <span data-ttu-id="7bfeb-221">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-221">Type</span></span> | <span data-ttu-id="7bfeb-222">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-223">concatOutput</span></span> | <span data-ttu-id="7bfeb-224">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-224">String</span></span> | <span data-ttu-id="7bfeb-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="7bfeb-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="7bfeb-226">contains</span><span class="sxs-lookup"><span data-stu-id="7bfeb-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="7bfeb-227">Vérifie si un tableau contient une valeur, un objet contient une clé ou une chaîne contient une sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-228">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-228">Parameters</span></span>

| <span data-ttu-id="7bfeb-229">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-229">Parameter</span></span> | <span data-ttu-id="7bfeb-230">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-230">Required</span></span> | <span data-ttu-id="7bfeb-231">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-231">Type</span></span> | <span data-ttu-id="7bfeb-232">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-233">conteneur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-233">container</span></span> |<span data-ttu-id="7bfeb-234">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-234">Yes</span></span> |<span data-ttu-id="7bfeb-235">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-235">array, object, or string</span></span> |<span data-ttu-id="7bfeb-236">valeur Hello contenant hello valeur toofind.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="7bfeb-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="7bfeb-237">itemToFind</span></span> |<span data-ttu-id="7bfeb-238">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-238">Yes</span></span> |<span data-ttu-id="7bfeb-239">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="7bfeb-239">string or int</span></span> |<span data-ttu-id="7bfeb-240">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-241">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-241">Return value</span></span>

<span data-ttu-id="7bfeb-242">**True** si l’élément de hello est trouvé ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-243">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-243">Example</span></span>

<span data-ttu-id="7bfeb-244">Hello suivant montre comment toouse contient différents types :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="7bfeb-245">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-246">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-246">Name</span></span> | <span data-ttu-id="7bfeb-247">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-247">Type</span></span> | <span data-ttu-id="7bfeb-248">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="7bfeb-249">stringTrue</span></span> | <span data-ttu-id="7bfeb-250">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-250">Bool</span></span> | <span data-ttu-id="7bfeb-251">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-251">True</span></span> |
| <span data-ttu-id="7bfeb-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="7bfeb-252">stringFalse</span></span> | <span data-ttu-id="7bfeb-253">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-253">Bool</span></span> | <span data-ttu-id="7bfeb-254">False</span><span class="sxs-lookup"><span data-stu-id="7bfeb-254">False</span></span> |
| <span data-ttu-id="7bfeb-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="7bfeb-255">objectTrue</span></span> | <span data-ttu-id="7bfeb-256">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-256">Bool</span></span> | <span data-ttu-id="7bfeb-257">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-257">True</span></span> |
| <span data-ttu-id="7bfeb-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="7bfeb-258">objectFalse</span></span> | <span data-ttu-id="7bfeb-259">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-259">Bool</span></span> | <span data-ttu-id="7bfeb-260">False</span><span class="sxs-lookup"><span data-stu-id="7bfeb-260">False</span></span> |
| <span data-ttu-id="7bfeb-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="7bfeb-261">arrayTrue</span></span> | <span data-ttu-id="7bfeb-262">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-262">Bool</span></span> | <span data-ttu-id="7bfeb-263">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-263">True</span></span> |
| <span data-ttu-id="7bfeb-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="7bfeb-264">arrayFalse</span></span> | <span data-ttu-id="7bfeb-265">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-265">Bool</span></span> | <span data-ttu-id="7bfeb-266">False</span><span class="sxs-lookup"><span data-stu-id="7bfeb-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="7bfeb-267">createarray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="7bfeb-268">Crée un tableau à partir des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-269">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-269">Parameters</span></span>

| <span data-ttu-id="7bfeb-270">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-270">Parameter</span></span> | <span data-ttu-id="7bfeb-271">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-271">Required</span></span> | <span data-ttu-id="7bfeb-272">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-272">Type</span></span> | <span data-ttu-id="7bfeb-273">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-274">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-274">arg1</span></span> |<span data-ttu-id="7bfeb-275">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-275">Yes</span></span> |<span data-ttu-id="7bfeb-276">Chaîne, entier, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="7bfeb-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="7bfeb-277">Hello première valeur dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="7bfeb-278">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bfeb-278">additional arguments</span></span> |<span data-ttu-id="7bfeb-279">Non</span><span class="sxs-lookup"><span data-stu-id="7bfeb-279">No</span></span> |<span data-ttu-id="7bfeb-280">Chaîne, entier, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="7bfeb-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="7bfeb-281">Valeurs supplémentaires dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-282">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-282">Return value</span></span>

<span data-ttu-id="7bfeb-283">Tableau.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-284">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-284">Example</span></span>

<span data-ttu-id="7bfeb-285">Hello suivant montre l’exemple de comment createArray toouse avec des types différents :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="7bfeb-286">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-287">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-287">Name</span></span> | <span data-ttu-id="7bfeb-288">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-288">Type</span></span> | <span data-ttu-id="7bfeb-289">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-290">stringArray</span></span> | <span data-ttu-id="7bfeb-291">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-291">Array</span></span> | <span data-ttu-id="7bfeb-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="7bfeb-293">intArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-293">intArray</span></span> | <span data-ttu-id="7bfeb-294">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-294">Array</span></span> | <span data-ttu-id="7bfeb-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="7bfeb-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-296">objectArray</span></span> | <span data-ttu-id="7bfeb-297">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-297">Array</span></span> | <span data-ttu-id="7bfeb-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="7bfeb-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="7bfeb-299">arrayArray</span></span> | <span data-ttu-id="7bfeb-300">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-300">Array</span></span> | <span data-ttu-id="7bfeb-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="7bfeb-302">empty</span><span class="sxs-lookup"><span data-stu-id="7bfeb-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="7bfeb-303">Détermine si un tableau, un objet ou une chaîne est vide.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-304">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-304">Parameters</span></span>

| <span data-ttu-id="7bfeb-305">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-305">Parameter</span></span> | <span data-ttu-id="7bfeb-306">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-306">Required</span></span> | <span data-ttu-id="7bfeb-307">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-307">Type</span></span> | <span data-ttu-id="7bfeb-308">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="7bfeb-309">itemToTest</span></span> |<span data-ttu-id="7bfeb-310">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-310">Yes</span></span> |<span data-ttu-id="7bfeb-311">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-311">array, object, or string</span></span> |<span data-ttu-id="7bfeb-312">Bonjour toocheck de valeur s’il est vide.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-313">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-313">Return value</span></span>

<span data-ttu-id="7bfeb-314">Retourne **True** si la valeur de hello est vide ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-315">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-315">Example</span></span>

<span data-ttu-id="7bfeb-316">Bonjour à l’exemple suivant vérifie si un tableau, un objet et une chaîne sont vides.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="7bfeb-317">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-318">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-318">Name</span></span> | <span data-ttu-id="7bfeb-319">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-319">Type</span></span> | <span data-ttu-id="7bfeb-320">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="7bfeb-321">arrayEmpty</span></span> | <span data-ttu-id="7bfeb-322">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-322">Bool</span></span> | <span data-ttu-id="7bfeb-323">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-323">True</span></span> |
| <span data-ttu-id="7bfeb-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="7bfeb-324">objectEmpty</span></span> | <span data-ttu-id="7bfeb-325">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-325">Bool</span></span> | <span data-ttu-id="7bfeb-326">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-326">True</span></span> |
| <span data-ttu-id="7bfeb-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="7bfeb-327">stringEmpty</span></span> | <span data-ttu-id="7bfeb-328">Bool</span><span class="sxs-lookup"><span data-stu-id="7bfeb-328">Bool</span></span> | <span data-ttu-id="7bfeb-329">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="7bfeb-330">first</span><span class="sxs-lookup"><span data-stu-id="7bfeb-330">first</span></span>
`first(arg1)`

<span data-ttu-id="7bfeb-331">Retourne hello le premier élément du tableau de hello ou le premier caractère de la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-332">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-332">Parameters</span></span>

| <span data-ttu-id="7bfeb-333">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-333">Parameter</span></span> | <span data-ttu-id="7bfeb-334">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-334">Required</span></span> | <span data-ttu-id="7bfeb-335">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-335">Type</span></span> | <span data-ttu-id="7bfeb-336">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-337">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-337">arg1</span></span> |<span data-ttu-id="7bfeb-338">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-338">Yes</span></span> |<span data-ttu-id="7bfeb-339">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-339">array or string</span></span> |<span data-ttu-id="7bfeb-340">premier élément Hello valeur tooretrieve hello ou caractère.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-341">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-341">Return value</span></span>

<span data-ttu-id="7bfeb-342">type Hello (string, int, tableau ou objet) de hello premier élément dans un tableau, ou hello premier caractère d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-343">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-343">Example</span></span>

<span data-ttu-id="7bfeb-344">Hello suivant montre comment toouse hello première fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="7bfeb-345">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-346">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-346">Name</span></span> | <span data-ttu-id="7bfeb-347">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-347">Type</span></span> | <span data-ttu-id="7bfeb-348">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-349">arrayOutput</span></span> | <span data-ttu-id="7bfeb-350">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-350">String</span></span> | <span data-ttu-id="7bfeb-351">one</span><span class="sxs-lookup"><span data-stu-id="7bfeb-351">one</span></span> |
| <span data-ttu-id="7bfeb-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-352">stringOutput</span></span> | <span data-ttu-id="7bfeb-353">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-353">String</span></span> | <span data-ttu-id="7bfeb-354">O</span><span class="sxs-lookup"><span data-stu-id="7bfeb-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="7bfeb-355">intersection</span><span class="sxs-lookup"><span data-stu-id="7bfeb-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="7bfeb-356">Renvoie un tableau à une seule ou avec des éléments en commun hello à partir des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-357">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-357">Parameters</span></span>

| <span data-ttu-id="7bfeb-358">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-358">Parameter</span></span> | <span data-ttu-id="7bfeb-359">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-359">Required</span></span> | <span data-ttu-id="7bfeb-360">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-360">Type</span></span> | <span data-ttu-id="7bfeb-361">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-362">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-362">arg1</span></span> |<span data-ttu-id="7bfeb-363">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-363">Yes</span></span> |<span data-ttu-id="7bfeb-364">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-364">array or object</span></span> |<span data-ttu-id="7bfeb-365">Hello première valeur toouse pour la recherche d’éléments en commun.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="7bfeb-366">arg2</span><span class="sxs-lookup"><span data-stu-id="7bfeb-366">arg2</span></span> |<span data-ttu-id="7bfeb-367">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-367">Yes</span></span> |<span data-ttu-id="7bfeb-368">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-368">array or object</span></span> |<span data-ttu-id="7bfeb-369">Bonjour deuxième toouse de valeur pour la recherche d’éléments en commun.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="7bfeb-370">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bfeb-370">additional arguments</span></span> |<span data-ttu-id="7bfeb-371">Non</span><span class="sxs-lookup"><span data-stu-id="7bfeb-371">No</span></span> |<span data-ttu-id="7bfeb-372">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-372">array or object</span></span> |<span data-ttu-id="7bfeb-373">Toouse des valeurs supplémentaires pour la recherche d’éléments en commun.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-374">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-374">Return value</span></span>

<span data-ttu-id="7bfeb-375">Un tableau ou un objet avec des éléments en commun hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-376">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-376">Example</span></span>

<span data-ttu-id="7bfeb-377">Hello exemple montre comment l’intersection toouse avec les tableaux et les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="7bfeb-378">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-379">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-379">Name</span></span> | <span data-ttu-id="7bfeb-380">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-380">Type</span></span> | <span data-ttu-id="7bfeb-381">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-382">objectOutput</span></span> | <span data-ttu-id="7bfeb-383">Object</span><span class="sxs-lookup"><span data-stu-id="7bfeb-383">Object</span></span> | <span data-ttu-id="7bfeb-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="7bfeb-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="7bfeb-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-385">arrayOutput</span></span> | <span data-ttu-id="7bfeb-386">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-386">Array</span></span> | <span data-ttu-id="7bfeb-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="7bfeb-388">json</span><span class="sxs-lookup"><span data-stu-id="7bfeb-388">json</span></span>
`json(arg1)`

<span data-ttu-id="7bfeb-389">Renvoie un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-390">parameters</span><span class="sxs-lookup"><span data-stu-id="7bfeb-390">Parameters</span></span>

| <span data-ttu-id="7bfeb-391">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-391">Parameter</span></span> | <span data-ttu-id="7bfeb-392">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-392">Required</span></span> | <span data-ttu-id="7bfeb-393">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-393">Type</span></span> | <span data-ttu-id="7bfeb-394">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-395">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-395">arg1</span></span> |<span data-ttu-id="7bfeb-396">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-396">Yes</span></span> |<span data-ttu-id="7bfeb-397">string</span><span class="sxs-lookup"><span data-stu-id="7bfeb-397">string</span></span> |<span data-ttu-id="7bfeb-398">Hello valeur tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="7bfeb-399">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-399">Return value</span></span>

<span data-ttu-id="7bfeb-400">objet JSON Hello hello spécifié de chaîne ou un objet vide lorsque **null** est spécifié.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-401">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-401">Example</span></span>

<span data-ttu-id="7bfeb-402">Hello exemple montre comment l’intersection toouse avec les tableaux et les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="7bfeb-403">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-404">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-404">Name</span></span> | <span data-ttu-id="7bfeb-405">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-405">Type</span></span> | <span data-ttu-id="7bfeb-406">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-407">jsonOutput</span></span> | <span data-ttu-id="7bfeb-408">Object</span><span class="sxs-lookup"><span data-stu-id="7bfeb-408">Object</span></span> | <span data-ttu-id="7bfeb-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="7bfeb-409">{"a": "b"}</span></span> |
| <span data-ttu-id="7bfeb-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-410">nullOutput</span></span> | <span data-ttu-id="7bfeb-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="7bfeb-411">Boolean</span></span> | <span data-ttu-id="7bfeb-412">true</span><span class="sxs-lookup"><span data-stu-id="7bfeb-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="7bfeb-413">last</span><span class="sxs-lookup"><span data-stu-id="7bfeb-413">last</span></span>
`last (arg1)`

<span data-ttu-id="7bfeb-414">Retourne hello le dernier élément du tableau de hello ou dernier caractère de chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-415">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-415">Parameters</span></span>

| <span data-ttu-id="7bfeb-416">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-416">Parameter</span></span> | <span data-ttu-id="7bfeb-417">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-417">Required</span></span> | <span data-ttu-id="7bfeb-418">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-418">Type</span></span> | <span data-ttu-id="7bfeb-419">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-420">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-420">arg1</span></span> |<span data-ttu-id="7bfeb-421">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-421">Yes</span></span> |<span data-ttu-id="7bfeb-422">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-422">array or string</span></span> |<span data-ttu-id="7bfeb-423">dernier élément Hello valeur tooretrieve hello ou caractère.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-424">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-424">Return value</span></span>

<span data-ttu-id="7bfeb-425">Hello type (string, int, tableau ou objet) de hello dernier élément d’un tableau ou hello dernier caractère d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-426">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-426">Example</span></span>

<span data-ttu-id="7bfeb-427">Hello suivant montre comment toouse hello dernière fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="7bfeb-428">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-429">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-429">Name</span></span> | <span data-ttu-id="7bfeb-430">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-430">Type</span></span> | <span data-ttu-id="7bfeb-431">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-432">arrayOutput</span></span> | <span data-ttu-id="7bfeb-433">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-433">String</span></span> | <span data-ttu-id="7bfeb-434">three</span><span class="sxs-lookup"><span data-stu-id="7bfeb-434">three</span></span> |
| <span data-ttu-id="7bfeb-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-435">stringOutput</span></span> | <span data-ttu-id="7bfeb-436">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-436">String</span></span> | <span data-ttu-id="7bfeb-437">e</span><span class="sxs-lookup"><span data-stu-id="7bfeb-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="7bfeb-438">length</span><span class="sxs-lookup"><span data-stu-id="7bfeb-438">length</span></span>
`length(arg1)`

<span data-ttu-id="7bfeb-439">Retourne le nombre hello d’éléments dans un tableau ou d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-440">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-440">Parameters</span></span>

| <span data-ttu-id="7bfeb-441">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-441">Parameter</span></span> | <span data-ttu-id="7bfeb-442">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-442">Required</span></span> | <span data-ttu-id="7bfeb-443">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-443">Type</span></span> | <span data-ttu-id="7bfeb-444">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-445">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-445">arg1</span></span> |<span data-ttu-id="7bfeb-446">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-446">Yes</span></span> |<span data-ttu-id="7bfeb-447">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-447">array or string</span></span> |<span data-ttu-id="7bfeb-448">Hello toouse de tableau pour l’obtention du nombre de hello d’éléments ou hello toouse de chaîne pour l’obtention du nombre de hello de caractères.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-449">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-449">Return value</span></span>

<span data-ttu-id="7bfeb-450">Un entier.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="7bfeb-451">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-451">Example</span></span>

<span data-ttu-id="7bfeb-452">Hello suivant montre l’exemple de la longueur de toouse avec un tableau et une chaîne :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="7bfeb-453">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-454">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-454">Name</span></span> | <span data-ttu-id="7bfeb-455">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-455">Type</span></span> | <span data-ttu-id="7bfeb-456">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="7bfeb-457">arrayLength</span></span> | <span data-ttu-id="7bfeb-458">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-458">Int</span></span> | <span data-ttu-id="7bfeb-459">3</span><span class="sxs-lookup"><span data-stu-id="7bfeb-459">3</span></span> |
| <span data-ttu-id="7bfeb-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="7bfeb-460">stringLength</span></span> | <span data-ttu-id="7bfeb-461">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-461">Int</span></span> | <span data-ttu-id="7bfeb-462">13.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-462">13</span></span> |

<span data-ttu-id="7bfeb-463">Vous pouvez utiliser cette fonction avec un nombre de hello tableau toospecify d’itérations lors de la création de ressources.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="7bfeb-464">Dans l’exemple suivant de hello, hello paramètre **siteNames** rapporte tableau tooan de toouse de noms lors de la création de sites web de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="7bfeb-465">Pour plus d’informations sur l’utilisation de cette fonction avec un tableau, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="7bfeb-466">Min</span><span class="sxs-lookup"><span data-stu-id="7bfeb-466">min</span></span>
`min(arg1)`

<span data-ttu-id="7bfeb-467">Retourne hello valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-468">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-468">Parameters</span></span>

| <span data-ttu-id="7bfeb-469">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-469">Parameter</span></span> | <span data-ttu-id="7bfeb-470">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-470">Required</span></span> | <span data-ttu-id="7bfeb-471">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-471">Type</span></span> | <span data-ttu-id="7bfeb-472">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-473">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-473">arg1</span></span> |<span data-ttu-id="7bfeb-474">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-474">Yes</span></span> |<span data-ttu-id="7bfeb-475">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="7bfeb-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="7bfeb-476">Hello collection tooget hello valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-477">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-477">Return value</span></span>

<span data-ttu-id="7bfeb-478">Entier représentant la valeur minimale de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-479">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-479">Example</span></span>

<span data-ttu-id="7bfeb-480">Hello suivant montre l’exemple de comment min toouse avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="7bfeb-481">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-482">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-482">Name</span></span> | <span data-ttu-id="7bfeb-483">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-483">Type</span></span> | <span data-ttu-id="7bfeb-484">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-485">arrayOutput</span></span> | <span data-ttu-id="7bfeb-486">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-486">Int</span></span> | <span data-ttu-id="7bfeb-487">0</span><span class="sxs-lookup"><span data-stu-id="7bfeb-487">0</span></span> |
| <span data-ttu-id="7bfeb-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-488">intOutput</span></span> | <span data-ttu-id="7bfeb-489">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-489">Int</span></span> | <span data-ttu-id="7bfeb-490">0</span><span class="sxs-lookup"><span data-stu-id="7bfeb-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="7bfeb-491">max</span><span class="sxs-lookup"><span data-stu-id="7bfeb-491">max</span></span>
`max(arg1)`

<span data-ttu-id="7bfeb-492">Retourne hello valeur maximale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-493">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-493">Parameters</span></span>

| <span data-ttu-id="7bfeb-494">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-494">Parameter</span></span> | <span data-ttu-id="7bfeb-495">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-495">Required</span></span> | <span data-ttu-id="7bfeb-496">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-496">Type</span></span> | <span data-ttu-id="7bfeb-497">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-498">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-498">arg1</span></span> |<span data-ttu-id="7bfeb-499">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-499">Yes</span></span> |<span data-ttu-id="7bfeb-500">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="7bfeb-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="7bfeb-501">Hello collection tooget hello valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-502">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-502">Return value</span></span>

<span data-ttu-id="7bfeb-503">Entier représentant la valeur maximale de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-504">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-504">Example</span></span>

<span data-ttu-id="7bfeb-505">Hello suivant montre l’exemple de comment toouse max avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="7bfeb-506">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-507">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-507">Name</span></span> | <span data-ttu-id="7bfeb-508">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-508">Type</span></span> | <span data-ttu-id="7bfeb-509">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-510">arrayOutput</span></span> | <span data-ttu-id="7bfeb-511">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-511">Int</span></span> | <span data-ttu-id="7bfeb-512">5</span><span class="sxs-lookup"><span data-stu-id="7bfeb-512">5</span></span> |
| <span data-ttu-id="7bfeb-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-513">intOutput</span></span> | <span data-ttu-id="7bfeb-514">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-514">Int</span></span> | <span data-ttu-id="7bfeb-515">5</span><span class="sxs-lookup"><span data-stu-id="7bfeb-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="7bfeb-516">range</span><span class="sxs-lookup"><span data-stu-id="7bfeb-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="7bfeb-517">Crée un tableau d’entiers à partir d’un entier de départ et contenant un nombre d’éléments.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-518">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-518">Parameters</span></span>

| <span data-ttu-id="7bfeb-519">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-519">Parameter</span></span> | <span data-ttu-id="7bfeb-520">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-520">Required</span></span> | <span data-ttu-id="7bfeb-521">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-521">Type</span></span> | <span data-ttu-id="7bfeb-522">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="7bfeb-523">startingInteger</span></span> |<span data-ttu-id="7bfeb-524">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-524">Yes</span></span> |<span data-ttu-id="7bfeb-525">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-525">int</span></span> |<span data-ttu-id="7bfeb-526">Hello premier entier hello tableau.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="7bfeb-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="7bfeb-527">numberofElements</span></span> |<span data-ttu-id="7bfeb-528">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-528">Yes</span></span> |<span data-ttu-id="7bfeb-529">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-529">int</span></span> |<span data-ttu-id="7bfeb-530">nombre de Hello de nombres entiers dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-531">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-531">Return value</span></span>

<span data-ttu-id="7bfeb-532">Tableau d’entiers.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-533">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-533">Example</span></span>

<span data-ttu-id="7bfeb-534">Bonjour à l’exemple suivant montre comment toouse hello fonction plage :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="7bfeb-535">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-536">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-536">Name</span></span> | <span data-ttu-id="7bfeb-537">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-537">Type</span></span> | <span data-ttu-id="7bfeb-538">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-539">rangeOutput</span></span> | <span data-ttu-id="7bfeb-540">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-540">Array</span></span> | <span data-ttu-id="7bfeb-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="7bfeb-542">skip</span><span class="sxs-lookup"><span data-stu-id="7bfeb-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="7bfeb-543">Retourne un tableau avec tous les éléments hello après que le nombre spécifié dans le tableau de hello hello ou retourne une chaîne contenant tous les caractères de hello après que hello le nombre spécifié dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-544">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-544">Parameters</span></span>

| <span data-ttu-id="7bfeb-545">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-545">Parameter</span></span> | <span data-ttu-id="7bfeb-546">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-546">Required</span></span> | <span data-ttu-id="7bfeb-547">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-547">Type</span></span> | <span data-ttu-id="7bfeb-548">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="7bfeb-549">originalValue</span></span> |<span data-ttu-id="7bfeb-550">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-550">Yes</span></span> |<span data-ttu-id="7bfeb-551">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-551">array or string</span></span> |<span data-ttu-id="7bfeb-552">Bonjour toouse tableau ou une chaîne pour l’ignorer.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="7bfeb-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="7bfeb-553">numberToSkip</span></span> |<span data-ttu-id="7bfeb-554">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-554">Yes</span></span> |<span data-ttu-id="7bfeb-555">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-555">int</span></span> |<span data-ttu-id="7bfeb-556">nombre de Hello d’éléments ou des caractères tooskip.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="7bfeb-557">Si cette valeur est inférieur ou égal à 0, tous les hello éléments ou dans la valeur de hello est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="7bfeb-558">Si elle est supérieure à la longueur du tableau de hello ou chaîne hello, un tableau vide ou une chaîne est retournée.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-559">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-559">Return value</span></span>

<span data-ttu-id="7bfeb-560">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-561">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-561">Example</span></span>

<span data-ttu-id="7bfeb-562">Hello suivant exemple ignore hello le nombre d’éléments spécifié dans le tableau de hello et hello nombre spécifié de caractères dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="7bfeb-563">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-564">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-564">Name</span></span> | <span data-ttu-id="7bfeb-565">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-565">Type</span></span> | <span data-ttu-id="7bfeb-566">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-567">arrayOutput</span></span> | <span data-ttu-id="7bfeb-568">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-568">Array</span></span> | <span data-ttu-id="7bfeb-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-569">["three"]</span></span> |
| <span data-ttu-id="7bfeb-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-570">stringOutput</span></span> | <span data-ttu-id="7bfeb-571">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-571">String</span></span> | <span data-ttu-id="7bfeb-572">two three</span><span class="sxs-lookup"><span data-stu-id="7bfeb-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="7bfeb-573">take</span><span class="sxs-lookup"><span data-stu-id="7bfeb-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="7bfeb-574">Retourne un tableau avec hello spécifié le nombre d’éléments de hello début du tableau de hello, ou une chaîne avec hello nombre spécifié de caractères à partir du début hello de chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-575">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-575">Parameters</span></span>

| <span data-ttu-id="7bfeb-576">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-576">Parameter</span></span> | <span data-ttu-id="7bfeb-577">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-577">Required</span></span> | <span data-ttu-id="7bfeb-578">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-578">Type</span></span> | <span data-ttu-id="7bfeb-579">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="7bfeb-580">originalValue</span></span> |<span data-ttu-id="7bfeb-581">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-581">Yes</span></span> |<span data-ttu-id="7bfeb-582">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="7bfeb-582">array or string</span></span> |<span data-ttu-id="7bfeb-583">Bonjour les éléments de hello tootake tableau ou une chaîne à partir de.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="7bfeb-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="7bfeb-584">numberToTake</span></span> |<span data-ttu-id="7bfeb-585">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-585">Yes</span></span> |<span data-ttu-id="7bfeb-586">int</span><span class="sxs-lookup"><span data-stu-id="7bfeb-586">int</span></span> |<span data-ttu-id="7bfeb-587">nombre de Hello d’éléments ou des caractères tootake.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="7bfeb-588">Si cette valeur est inférieure ou égale à 0, une chaîne ou un tableau vide est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="7bfeb-589">Si elle est supérieure à la longueur de hello Hello donné de tableau ou une chaîne, tous les éléments hello hello tableau ou une chaîne sont retournés.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-590">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-590">Return value</span></span>

<span data-ttu-id="7bfeb-591">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-592">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-592">Example</span></span>

<span data-ttu-id="7bfeb-593">Hello suivant l’exemple prend hello spécifié le nombre d’éléments de tableau de hello et les caractères d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="7bfeb-594">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-595">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-595">Name</span></span> | <span data-ttu-id="7bfeb-596">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-596">Type</span></span> | <span data-ttu-id="7bfeb-597">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-598">arrayOutput</span></span> | <span data-ttu-id="7bfeb-599">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-599">Array</span></span> | <span data-ttu-id="7bfeb-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-600">["one", "two"]</span></span> |
| <span data-ttu-id="7bfeb-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-601">stringOutput</span></span> | <span data-ttu-id="7bfeb-602">String</span><span class="sxs-lookup"><span data-stu-id="7bfeb-602">String</span></span> | <span data-ttu-id="7bfeb-603">sur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="7bfeb-604">union</span><span class="sxs-lookup"><span data-stu-id="7bfeb-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="7bfeb-605">Renvoie un tableau à une seule ou avec tous les éléments à partir des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="7bfeb-606">Les valeurs ou les clés en double sont uniquement incluses une seule fois.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="7bfeb-607">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7bfeb-607">Parameters</span></span>

| <span data-ttu-id="7bfeb-608">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bfeb-608">Parameter</span></span> | <span data-ttu-id="7bfeb-609">Requis</span><span class="sxs-lookup"><span data-stu-id="7bfeb-609">Required</span></span> | <span data-ttu-id="7bfeb-610">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-610">Type</span></span> | <span data-ttu-id="7bfeb-611">Description</span><span class="sxs-lookup"><span data-stu-id="7bfeb-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7bfeb-612">arg1</span><span class="sxs-lookup"><span data-stu-id="7bfeb-612">arg1</span></span> |<span data-ttu-id="7bfeb-613">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-613">Yes</span></span> |<span data-ttu-id="7bfeb-614">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-614">array or object</span></span> |<span data-ttu-id="7bfeb-615">Hello première valeur toouse pour joindre des éléments.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="7bfeb-616">arg2</span><span class="sxs-lookup"><span data-stu-id="7bfeb-616">arg2</span></span> |<span data-ttu-id="7bfeb-617">Oui</span><span class="sxs-lookup"><span data-stu-id="7bfeb-617">Yes</span></span> |<span data-ttu-id="7bfeb-618">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-618">array or object</span></span> |<span data-ttu-id="7bfeb-619">Hello deuxième valeur toouse pour joindre des éléments.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="7bfeb-620">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bfeb-620">additional arguments</span></span> |<span data-ttu-id="7bfeb-621">Non</span><span class="sxs-lookup"><span data-stu-id="7bfeb-621">No</span></span> |<span data-ttu-id="7bfeb-622">objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-622">array or object</span></span> |<span data-ttu-id="7bfeb-623">Toouse des valeurs supplémentaires pour joindre des éléments.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7bfeb-624">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7bfeb-624">Return value</span></span>

<span data-ttu-id="7bfeb-625">Objet ou tableau.</span><span class="sxs-lookup"><span data-stu-id="7bfeb-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="7bfeb-626">Exemple</span><span class="sxs-lookup"><span data-stu-id="7bfeb-626">Example</span></span>

<span data-ttu-id="7bfeb-627">Hello exemple montre comment union toouse avec les tableaux et les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="7bfeb-628">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7bfeb-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7bfeb-629">Nom</span><span class="sxs-lookup"><span data-stu-id="7bfeb-629">Name</span></span> | <span data-ttu-id="7bfeb-630">Type</span><span class="sxs-lookup"><span data-stu-id="7bfeb-630">Type</span></span> | <span data-ttu-id="7bfeb-631">Valeur</span><span class="sxs-lookup"><span data-stu-id="7bfeb-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7bfeb-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-632">objectOutput</span></span> | <span data-ttu-id="7bfeb-633">Object</span><span class="sxs-lookup"><span data-stu-id="7bfeb-633">Object</span></span> | <span data-ttu-id="7bfeb-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="7bfeb-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="7bfeb-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="7bfeb-635">arrayOutput</span></span> | <span data-ttu-id="7bfeb-636">Tableau</span><span class="sxs-lookup"><span data-stu-id="7bfeb-636">Array</span></span> | <span data-ttu-id="7bfeb-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="7bfeb-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7bfeb-638">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bfeb-638">Next steps</span></span>
* <span data-ttu-id="7bfeb-639">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7bfeb-640">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7bfeb-641">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="7bfeb-642">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7bfeb-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

