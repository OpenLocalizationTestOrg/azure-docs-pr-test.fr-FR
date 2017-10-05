---
title: "Fonctions de modèle Azure Resource Manager - chaîne | Microsoft Docs"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour travailler avec des chaînes."
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="30828-103">Fonctions de chaînes pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30828-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="30828-104">Resource Manager fournit les fonctions ci-après pour travailler avec des chaînes de caractères :</span><span class="sxs-lookup"><span data-stu-id="30828-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="30828-105">base64</span><span class="sxs-lookup"><span data-stu-id="30828-105">base64</span></span>](#base64)
* [<span data-ttu-id="30828-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="30828-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="30828-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="30828-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="30828-108">concat</span><span class="sxs-lookup"><span data-stu-id="30828-108">concat</span></span>](#concat)
* [<span data-ttu-id="30828-109">contains</span><span class="sxs-lookup"><span data-stu-id="30828-109">contains</span></span>](#contains)
* [<span data-ttu-id="30828-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="30828-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="30828-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="30828-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="30828-112">empty</span><span class="sxs-lookup"><span data-stu-id="30828-112">empty</span></span>](#empty)
* [<span data-ttu-id="30828-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="30828-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="30828-114">first</span><span class="sxs-lookup"><span data-stu-id="30828-114">first</span></span>](#first)
* [<span data-ttu-id="30828-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="30828-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="30828-116">last</span><span class="sxs-lookup"><span data-stu-id="30828-116">last</span></span>](#last)
* [<span data-ttu-id="30828-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="30828-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="30828-118">length</span><span class="sxs-lookup"><span data-stu-id="30828-118">length</span></span>](#length)
* [<span data-ttu-id="30828-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="30828-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="30828-120">replace</span><span class="sxs-lookup"><span data-stu-id="30828-120">replace</span></span>](#replace)
* [<span data-ttu-id="30828-121">skip</span><span class="sxs-lookup"><span data-stu-id="30828-121">skip</span></span>](#skip)
* [<span data-ttu-id="30828-122">split</span><span class="sxs-lookup"><span data-stu-id="30828-122">split</span></span>](#split)
* [<span data-ttu-id="30828-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="30828-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="30828-124">string</span><span class="sxs-lookup"><span data-stu-id="30828-124">string</span></span>](#string)
* [<span data-ttu-id="30828-125">substring</span><span class="sxs-lookup"><span data-stu-id="30828-125">substring</span></span>](#substring)
* [<span data-ttu-id="30828-126">take</span><span class="sxs-lookup"><span data-stu-id="30828-126">take</span></span>](#take)
* [<span data-ttu-id="30828-127">toLower</span><span class="sxs-lookup"><span data-stu-id="30828-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="30828-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="30828-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="30828-129">découper</span><span class="sxs-lookup"><span data-stu-id="30828-129">trim</span></span>](#trim)
* [<span data-ttu-id="30828-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="30828-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="30828-131">URI</span><span class="sxs-lookup"><span data-stu-id="30828-131">uri</span></span>](#uri)
* [<span data-ttu-id="30828-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="30828-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="30828-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="30828-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="30828-134">base64</span><span class="sxs-lookup"><span data-stu-id="30828-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="30828-135">Retourne la représentation en base 64 de la chaîne d'entrée.</span><span class="sxs-lookup"><span data-stu-id="30828-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-136">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-136">Parameters</span></span>

| <span data-ttu-id="30828-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-137">Parameter</span></span> | <span data-ttu-id="30828-138">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-138">Required</span></span> | <span data-ttu-id="30828-139">Type</span><span class="sxs-lookup"><span data-stu-id="30828-139">Type</span></span> | <span data-ttu-id="30828-140">Description</span><span class="sxs-lookup"><span data-stu-id="30828-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-141">chaîne_entrée</span><span class="sxs-lookup"><span data-stu-id="30828-141">inputString</span></span> |<span data-ttu-id="30828-142">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-142">Yes</span></span> |<span data-ttu-id="30828-143">string</span><span class="sxs-lookup"><span data-stu-id="30828-143">string</span></span> |<span data-ttu-id="30828-144">La valeur à retourner sous la forme d’une représentation en base64.</span><span class="sxs-lookup"><span data-stu-id="30828-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-145">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-145">Return value</span></span>

<span data-ttu-id="30828-146">Une chaîne contenant la représentation en base64.</span><span class="sxs-lookup"><span data-stu-id="30828-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-147">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-147">Examples</span></span>

<span data-ttu-id="30828-148">L’exemple suivant montre comment utiliser la fonction base64.</span><span class="sxs-lookup"><span data-stu-id="30828-148">The following example shows how to use the base64 function.</span></span>

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

<span data-ttu-id="30828-149">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-150">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-150">Name</span></span> | <span data-ttu-id="30828-151">Type</span><span class="sxs-lookup"><span data-stu-id="30828-151">Type</span></span> | <span data-ttu-id="30828-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="30828-153">base64Output</span></span> | <span data-ttu-id="30828-154">String</span><span class="sxs-lookup"><span data-stu-id="30828-154">String</span></span> | <span data-ttu-id="30828-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30828-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30828-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-156">toStringOutput</span></span> | <span data-ttu-id="30828-157">String</span><span class="sxs-lookup"><span data-stu-id="30828-157">String</span></span> | <span data-ttu-id="30828-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="30828-158">one, two, three</span></span> |
| <span data-ttu-id="30828-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30828-159">toJsonOutput</span></span> | <span data-ttu-id="30828-160">Object</span><span class="sxs-lookup"><span data-stu-id="30828-160">Object</span></span> | <span data-ttu-id="30828-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="30828-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="30828-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="30828-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="30828-163">Convertit une représentation en base64 en un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="30828-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-164">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-164">Parameters</span></span>

| <span data-ttu-id="30828-165">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-165">Parameter</span></span> | <span data-ttu-id="30828-166">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-166">Required</span></span> | <span data-ttu-id="30828-167">Type</span><span class="sxs-lookup"><span data-stu-id="30828-167">Type</span></span> | <span data-ttu-id="30828-168">Description</span><span class="sxs-lookup"><span data-stu-id="30828-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="30828-169">base64Value</span></span> |<span data-ttu-id="30828-170">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-170">Yes</span></span> |<span data-ttu-id="30828-171">string</span><span class="sxs-lookup"><span data-stu-id="30828-171">string</span></span> |<span data-ttu-id="30828-172">La représentation en base64 à convertir en un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="30828-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-173">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-173">Return value</span></span>

<span data-ttu-id="30828-174">Un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="30828-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-175">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-175">Examples</span></span>

<span data-ttu-id="30828-176">L’exemple suivant utilise la fonction base64ToJson pour convertir une valeur base64 :</span><span class="sxs-lookup"><span data-stu-id="30828-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

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

<span data-ttu-id="30828-177">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-178">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-178">Name</span></span> | <span data-ttu-id="30828-179">Type</span><span class="sxs-lookup"><span data-stu-id="30828-179">Type</span></span> | <span data-ttu-id="30828-180">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="30828-181">base64Output</span></span> | <span data-ttu-id="30828-182">String</span><span class="sxs-lookup"><span data-stu-id="30828-182">String</span></span> | <span data-ttu-id="30828-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30828-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30828-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-184">toStringOutput</span></span> | <span data-ttu-id="30828-185">String</span><span class="sxs-lookup"><span data-stu-id="30828-185">String</span></span> | <span data-ttu-id="30828-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="30828-186">one, two, three</span></span> |
| <span data-ttu-id="30828-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30828-187">toJsonOutput</span></span> | <span data-ttu-id="30828-188">Object</span><span class="sxs-lookup"><span data-stu-id="30828-188">Object</span></span> | <span data-ttu-id="30828-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="30828-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="30828-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="30828-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="30828-191">Convertit une représentation en base64 en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-192">Parameters</span></span>

| <span data-ttu-id="30828-193">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-193">Parameter</span></span> | <span data-ttu-id="30828-194">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-194">Required</span></span> | <span data-ttu-id="30828-195">Type</span><span class="sxs-lookup"><span data-stu-id="30828-195">Type</span></span> | <span data-ttu-id="30828-196">Description</span><span class="sxs-lookup"><span data-stu-id="30828-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="30828-197">base64Value</span></span> |<span data-ttu-id="30828-198">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-198">Yes</span></span> |<span data-ttu-id="30828-199">string</span><span class="sxs-lookup"><span data-stu-id="30828-199">string</span></span> |<span data-ttu-id="30828-200">La représentation en base64 à convertir en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-201">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-201">Return value</span></span>

<span data-ttu-id="30828-202">Une chaîne de la valeur base64 convertie.</span><span class="sxs-lookup"><span data-stu-id="30828-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-203">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-203">Examples</span></span>

<span data-ttu-id="30828-204">L’exemple suivant utilise la fonction base64ToString pour convertir une valeur base64 :</span><span class="sxs-lookup"><span data-stu-id="30828-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

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

<span data-ttu-id="30828-205">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-206">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-206">Name</span></span> | <span data-ttu-id="30828-207">Type</span><span class="sxs-lookup"><span data-stu-id="30828-207">Type</span></span> | <span data-ttu-id="30828-208">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="30828-209">base64Output</span></span> | <span data-ttu-id="30828-210">String</span><span class="sxs-lookup"><span data-stu-id="30828-210">String</span></span> | <span data-ttu-id="30828-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30828-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30828-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-212">toStringOutput</span></span> | <span data-ttu-id="30828-213">String</span><span class="sxs-lookup"><span data-stu-id="30828-213">String</span></span> | <span data-ttu-id="30828-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="30828-214">one, two, three</span></span> |
| <span data-ttu-id="30828-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30828-215">toJsonOutput</span></span> | <span data-ttu-id="30828-216">Object</span><span class="sxs-lookup"><span data-stu-id="30828-216">Object</span></span> | <span data-ttu-id="30828-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="30828-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="30828-218">concat</span><span class="sxs-lookup"><span data-stu-id="30828-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="30828-219">Combine plusieurs valeurs de chaîne et retourne la chaine concaténée, ou combine plusieurs tableaux et retourne le tableau concaténé.</span><span class="sxs-lookup"><span data-stu-id="30828-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-220">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-220">Parameters</span></span>

| <span data-ttu-id="30828-221">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-221">Parameter</span></span> | <span data-ttu-id="30828-222">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-222">Required</span></span> | <span data-ttu-id="30828-223">Type</span><span class="sxs-lookup"><span data-stu-id="30828-223">Type</span></span> | <span data-ttu-id="30828-224">Description</span><span class="sxs-lookup"><span data-stu-id="30828-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-225">arg1</span><span class="sxs-lookup"><span data-stu-id="30828-225">arg1</span></span> |<span data-ttu-id="30828-226">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-226">Yes</span></span> |<span data-ttu-id="30828-227">chaîne ou tableau</span><span class="sxs-lookup"><span data-stu-id="30828-227">string or array</span></span> |<span data-ttu-id="30828-228">La première valeur pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="30828-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="30828-229">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="30828-229">additional arguments</span></span> |<span data-ttu-id="30828-230">Non</span><span class="sxs-lookup"><span data-stu-id="30828-230">No</span></span> |<span data-ttu-id="30828-231">string</span><span class="sxs-lookup"><span data-stu-id="30828-231">string</span></span> |<span data-ttu-id="30828-232">Valeurs supplémentaires en ordre séquentiel pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="30828-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-233">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-233">Return value</span></span>
<span data-ttu-id="30828-234">Chaîne ou tableau de valeurs concaténées.</span><span class="sxs-lookup"><span data-stu-id="30828-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-235">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-235">Examples</span></span>

<span data-ttu-id="30828-236">L’exemple suivant montre comment combiner deux valeurs de chaîne et retourner une chaîne concaténée.</span><span class="sxs-lookup"><span data-stu-id="30828-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="30828-237">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-238">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-238">Name</span></span> | <span data-ttu-id="30828-239">Type</span><span class="sxs-lookup"><span data-stu-id="30828-239">Type</span></span> | <span data-ttu-id="30828-240">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="30828-241">concatOutput</span></span> | <span data-ttu-id="30828-242">String</span><span class="sxs-lookup"><span data-stu-id="30828-242">String</span></span> | <span data-ttu-id="30828-243">préfixe-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="30828-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="30828-244">L’exemple suivant montre comment combiner deux tableaux.</span><span class="sxs-lookup"><span data-stu-id="30828-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="30828-245">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-246">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-246">Name</span></span> | <span data-ttu-id="30828-247">Type</span><span class="sxs-lookup"><span data-stu-id="30828-247">Type</span></span> | <span data-ttu-id="30828-248">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-249">return</span><span class="sxs-lookup"><span data-stu-id="30828-249">return</span></span> | <span data-ttu-id="30828-250">Tableau</span><span class="sxs-lookup"><span data-stu-id="30828-250">Array</span></span> | <span data-ttu-id="30828-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="30828-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="30828-252">contains</span><span class="sxs-lookup"><span data-stu-id="30828-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="30828-253">Vérifie si un tableau contient une valeur, un objet contient une clé ou une chaîne contient une sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-254">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-254">Parameters</span></span>

| <span data-ttu-id="30828-255">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-255">Parameter</span></span> | <span data-ttu-id="30828-256">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-256">Required</span></span> | <span data-ttu-id="30828-257">Type</span><span class="sxs-lookup"><span data-stu-id="30828-257">Type</span></span> | <span data-ttu-id="30828-258">Description</span><span class="sxs-lookup"><span data-stu-id="30828-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-259">conteneur</span><span class="sxs-lookup"><span data-stu-id="30828-259">container</span></span> |<span data-ttu-id="30828-260">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-260">Yes</span></span> |<span data-ttu-id="30828-261">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-261">array, object, or string</span></span> |<span data-ttu-id="30828-262">La valeur qui contient la valeur à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="30828-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="30828-263">itemToFind</span></span> |<span data-ttu-id="30828-264">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-264">Yes</span></span> |<span data-ttu-id="30828-265">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="30828-265">string or int</span></span> |<span data-ttu-id="30828-266">La valeur à trouver.</span><span class="sxs-lookup"><span data-stu-id="30828-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-267">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-267">Return value</span></span>

<span data-ttu-id="30828-268">**True** si l’élément est trouvé ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="30828-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-269">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-269">Examples</span></span>

<span data-ttu-id="30828-270">L’exemple suivant montre comment utiliser contains avec différents types :</span><span class="sxs-lookup"><span data-stu-id="30828-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="30828-271">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-272">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-272">Name</span></span> | <span data-ttu-id="30828-273">Type</span><span class="sxs-lookup"><span data-stu-id="30828-273">Type</span></span> | <span data-ttu-id="30828-274">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="30828-275">stringTrue</span></span> | <span data-ttu-id="30828-276">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-276">Bool</span></span> | <span data-ttu-id="30828-277">true</span><span class="sxs-lookup"><span data-stu-id="30828-277">True</span></span> |
| <span data-ttu-id="30828-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="30828-278">stringFalse</span></span> | <span data-ttu-id="30828-279">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-279">Bool</span></span> | <span data-ttu-id="30828-280">False</span><span class="sxs-lookup"><span data-stu-id="30828-280">False</span></span> |
| <span data-ttu-id="30828-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="30828-281">objectTrue</span></span> | <span data-ttu-id="30828-282">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-282">Bool</span></span> | <span data-ttu-id="30828-283">true</span><span class="sxs-lookup"><span data-stu-id="30828-283">True</span></span> |
| <span data-ttu-id="30828-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="30828-284">objectFalse</span></span> | <span data-ttu-id="30828-285">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-285">Bool</span></span> | <span data-ttu-id="30828-286">False</span><span class="sxs-lookup"><span data-stu-id="30828-286">False</span></span> |
| <span data-ttu-id="30828-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="30828-287">arrayTrue</span></span> | <span data-ttu-id="30828-288">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-288">Bool</span></span> | <span data-ttu-id="30828-289">true</span><span class="sxs-lookup"><span data-stu-id="30828-289">True</span></span> |
| <span data-ttu-id="30828-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="30828-290">arrayFalse</span></span> | <span data-ttu-id="30828-291">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-291">Bool</span></span> | <span data-ttu-id="30828-292">False</span><span class="sxs-lookup"><span data-stu-id="30828-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="30828-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="30828-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="30828-294">Convertit une valeur en un URI de données.</span><span class="sxs-lookup"><span data-stu-id="30828-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-295">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-295">Parameters</span></span>

| <span data-ttu-id="30828-296">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-296">Parameter</span></span> | <span data-ttu-id="30828-297">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-297">Required</span></span> | <span data-ttu-id="30828-298">Type</span><span class="sxs-lookup"><span data-stu-id="30828-298">Type</span></span> | <span data-ttu-id="30828-299">Description</span><span class="sxs-lookup"><span data-stu-id="30828-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="30828-300">stringToConvert</span></span> |<span data-ttu-id="30828-301">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-301">Yes</span></span> |<span data-ttu-id="30828-302">string</span><span class="sxs-lookup"><span data-stu-id="30828-302">string</span></span> |<span data-ttu-id="30828-303">Valeur à convertir en URI de données.</span><span class="sxs-lookup"><span data-stu-id="30828-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-304">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-304">Return value</span></span>

<span data-ttu-id="30828-305">Une chaîne formatée en tant qu’URI de données.</span><span class="sxs-lookup"><span data-stu-id="30828-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-306">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-306">Examples</span></span>

<span data-ttu-id="30828-307">L’exemple suivant convertit une valeur en un URI de données et convertit un URI de données en chaîne :</span><span class="sxs-lookup"><span data-stu-id="30828-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="30828-308">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-309">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-309">Name</span></span> | <span data-ttu-id="30828-310">Type</span><span class="sxs-lookup"><span data-stu-id="30828-310">Type</span></span> | <span data-ttu-id="30828-311">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="30828-312">dataUriOutput</span></span> | <span data-ttu-id="30828-313">String</span><span class="sxs-lookup"><span data-stu-id="30828-313">String</span></span> | <span data-ttu-id="30828-314">data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="30828-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="30828-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-315">toStringOutput</span></span> | <span data-ttu-id="30828-316">String</span><span class="sxs-lookup"><span data-stu-id="30828-316">String</span></span> | <span data-ttu-id="30828-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="30828-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="30828-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="30828-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="30828-319">Convertit une valeur formatée en URI de données en chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-320">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-320">Parameters</span></span>

| <span data-ttu-id="30828-321">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-321">Parameter</span></span> | <span data-ttu-id="30828-322">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-322">Required</span></span> | <span data-ttu-id="30828-323">Type</span><span class="sxs-lookup"><span data-stu-id="30828-323">Type</span></span> | <span data-ttu-id="30828-324">Description</span><span class="sxs-lookup"><span data-stu-id="30828-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="30828-325">dataUriToConvert</span></span> |<span data-ttu-id="30828-326">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-326">Yes</span></span> |<span data-ttu-id="30828-327">string</span><span class="sxs-lookup"><span data-stu-id="30828-327">string</span></span> |<span data-ttu-id="30828-328">Valeur d’URI de données à convertir.</span><span class="sxs-lookup"><span data-stu-id="30828-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-329">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-329">Return value</span></span>

<span data-ttu-id="30828-330">Chaîne contenant la valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="30828-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-331">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-331">Examples</span></span>

<span data-ttu-id="30828-332">L’exemple suivant convertit une valeur en un URI de données et convertit un URI de données en chaîne :</span><span class="sxs-lookup"><span data-stu-id="30828-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="30828-333">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-334">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-334">Name</span></span> | <span data-ttu-id="30828-335">Type</span><span class="sxs-lookup"><span data-stu-id="30828-335">Type</span></span> | <span data-ttu-id="30828-336">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="30828-337">dataUriOutput</span></span> | <span data-ttu-id="30828-338">String</span><span class="sxs-lookup"><span data-stu-id="30828-338">String</span></span> | <span data-ttu-id="30828-339">data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="30828-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="30828-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-340">toStringOutput</span></span> | <span data-ttu-id="30828-341">String</span><span class="sxs-lookup"><span data-stu-id="30828-341">String</span></span> | <span data-ttu-id="30828-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="30828-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="30828-343">empty</span><span class="sxs-lookup"><span data-stu-id="30828-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="30828-344">Détermine si un tableau, un objet ou une chaîne est vide.</span><span class="sxs-lookup"><span data-stu-id="30828-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-345">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-345">Parameters</span></span>

| <span data-ttu-id="30828-346">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-346">Parameter</span></span> | <span data-ttu-id="30828-347">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-347">Required</span></span> | <span data-ttu-id="30828-348">Type</span><span class="sxs-lookup"><span data-stu-id="30828-348">Type</span></span> | <span data-ttu-id="30828-349">Description</span><span class="sxs-lookup"><span data-stu-id="30828-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="30828-350">itemToTest</span></span> |<span data-ttu-id="30828-351">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-351">Yes</span></span> |<span data-ttu-id="30828-352">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-352">array, object, or string</span></span> |<span data-ttu-id="30828-353">Valeur à vérifier pour voir si elle est vide.</span><span class="sxs-lookup"><span data-stu-id="30828-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-354">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-354">Return value</span></span>

<span data-ttu-id="30828-355">Retourne **True** si la valeur est vide ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="30828-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-356">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-356">Examples</span></span>

<span data-ttu-id="30828-357">L’exemple suivant vérifie si un tableau, un objet et une chaîne sont vides.</span><span class="sxs-lookup"><span data-stu-id="30828-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="30828-358">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-359">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-359">Name</span></span> | <span data-ttu-id="30828-360">Type</span><span class="sxs-lookup"><span data-stu-id="30828-360">Type</span></span> | <span data-ttu-id="30828-361">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="30828-362">arrayEmpty</span></span> | <span data-ttu-id="30828-363">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-363">Bool</span></span> | <span data-ttu-id="30828-364">true</span><span class="sxs-lookup"><span data-stu-id="30828-364">True</span></span> |
| <span data-ttu-id="30828-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="30828-365">objectEmpty</span></span> | <span data-ttu-id="30828-366">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-366">Bool</span></span> | <span data-ttu-id="30828-367">true</span><span class="sxs-lookup"><span data-stu-id="30828-367">True</span></span> |
| <span data-ttu-id="30828-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="30828-368">stringEmpty</span></span> | <span data-ttu-id="30828-369">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-369">Bool</span></span> | <span data-ttu-id="30828-370">true</span><span class="sxs-lookup"><span data-stu-id="30828-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="30828-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="30828-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="30828-372">Détermine si une chaîne se termine par une valeur.</span><span class="sxs-lookup"><span data-stu-id="30828-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="30828-373">La comparaison respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="30828-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-374">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-374">Parameters</span></span>

| <span data-ttu-id="30828-375">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-375">Parameter</span></span> | <span data-ttu-id="30828-376">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-376">Required</span></span> | <span data-ttu-id="30828-377">Type</span><span class="sxs-lookup"><span data-stu-id="30828-377">Type</span></span> | <span data-ttu-id="30828-378">Description</span><span class="sxs-lookup"><span data-stu-id="30828-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30828-379">stringToSearch</span></span> |<span data-ttu-id="30828-380">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-380">Yes</span></span> |<span data-ttu-id="30828-381">string</span><span class="sxs-lookup"><span data-stu-id="30828-381">string</span></span> |<span data-ttu-id="30828-382">La valeur qui contient l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30828-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30828-383">stringToFind</span></span> |<span data-ttu-id="30828-384">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-384">Yes</span></span> |<span data-ttu-id="30828-385">string</span><span class="sxs-lookup"><span data-stu-id="30828-385">string</span></span> |<span data-ttu-id="30828-386">La valeur à trouver.</span><span class="sxs-lookup"><span data-stu-id="30828-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-387">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-387">Return value</span></span>

<span data-ttu-id="30828-388">**True** si le ou les derniers caractères de la chaîne correspondent à la valeur ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="30828-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-389">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-389">Examples</span></span>

<span data-ttu-id="30828-390">L'exemple suivant montre comment utiliser les fonctions startsWith et endsWith :</span><span class="sxs-lookup"><span data-stu-id="30828-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="30828-391">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-392">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-392">Name</span></span> | <span data-ttu-id="30828-393">Type</span><span class="sxs-lookup"><span data-stu-id="30828-393">Type</span></span> | <span data-ttu-id="30828-394">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="30828-395">startsTrue</span></span> | <span data-ttu-id="30828-396">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-396">Bool</span></span> | <span data-ttu-id="30828-397">true</span><span class="sxs-lookup"><span data-stu-id="30828-397">True</span></span> |
| <span data-ttu-id="30828-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30828-398">startsCapTrue</span></span> | <span data-ttu-id="30828-399">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-399">Bool</span></span> | <span data-ttu-id="30828-400">true</span><span class="sxs-lookup"><span data-stu-id="30828-400">True</span></span> |
| <span data-ttu-id="30828-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="30828-401">startsFalse</span></span> | <span data-ttu-id="30828-402">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-402">Bool</span></span> | <span data-ttu-id="30828-403">False</span><span class="sxs-lookup"><span data-stu-id="30828-403">False</span></span> |
| <span data-ttu-id="30828-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="30828-404">endsTrue</span></span> | <span data-ttu-id="30828-405">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-405">Bool</span></span> | <span data-ttu-id="30828-406">true</span><span class="sxs-lookup"><span data-stu-id="30828-406">True</span></span> |
| <span data-ttu-id="30828-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30828-407">endsCapTrue</span></span> | <span data-ttu-id="30828-408">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-408">Bool</span></span> | <span data-ttu-id="30828-409">true</span><span class="sxs-lookup"><span data-stu-id="30828-409">True</span></span> |
| <span data-ttu-id="30828-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="30828-410">endsFalse</span></span> | <span data-ttu-id="30828-411">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-411">Bool</span></span> | <span data-ttu-id="30828-412">False</span><span class="sxs-lookup"><span data-stu-id="30828-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="30828-413">first</span><span class="sxs-lookup"><span data-stu-id="30828-413">first</span></span>
`first(arg1)`

<span data-ttu-id="30828-414">Retourne le premier caractère de la chaîne ou le premier élément du tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-415">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-415">Parameters</span></span>

| <span data-ttu-id="30828-416">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-416">Parameter</span></span> | <span data-ttu-id="30828-417">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-417">Required</span></span> | <span data-ttu-id="30828-418">Type</span><span class="sxs-lookup"><span data-stu-id="30828-418">Type</span></span> | <span data-ttu-id="30828-419">Description</span><span class="sxs-lookup"><span data-stu-id="30828-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-420">arg1</span><span class="sxs-lookup"><span data-stu-id="30828-420">arg1</span></span> |<span data-ttu-id="30828-421">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-421">Yes</span></span> |<span data-ttu-id="30828-422">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-422">array or string</span></span> |<span data-ttu-id="30828-423">La valeur permettant de récupérer le premier élément ou caractère.</span><span class="sxs-lookup"><span data-stu-id="30828-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-424">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-424">Return value</span></span>

<span data-ttu-id="30828-425">Chaîne du premier caractère ou type (chaîne, entier, tableau ou objet) du premier élément d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-426">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-426">Examples</span></span>

<span data-ttu-id="30828-427">L’exemple suivant montre comment utiliser la première fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="30828-428">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-429">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-429">Name</span></span> | <span data-ttu-id="30828-430">Type</span><span class="sxs-lookup"><span data-stu-id="30828-430">Type</span></span> | <span data-ttu-id="30828-431">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30828-432">arrayOutput</span></span> | <span data-ttu-id="30828-433">String</span><span class="sxs-lookup"><span data-stu-id="30828-433">String</span></span> | <span data-ttu-id="30828-434">one</span><span class="sxs-lookup"><span data-stu-id="30828-434">one</span></span> |
| <span data-ttu-id="30828-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-435">stringOutput</span></span> | <span data-ttu-id="30828-436">String</span><span class="sxs-lookup"><span data-stu-id="30828-436">String</span></span> | <span data-ttu-id="30828-437">O</span><span class="sxs-lookup"><span data-stu-id="30828-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="30828-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="30828-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="30828-439">Retourne la première position d’une valeur dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="30828-440">La comparaison respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="30828-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-441">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-441">Parameters</span></span>

| <span data-ttu-id="30828-442">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-442">Parameter</span></span> | <span data-ttu-id="30828-443">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-443">Required</span></span> | <span data-ttu-id="30828-444">Type</span><span class="sxs-lookup"><span data-stu-id="30828-444">Type</span></span> | <span data-ttu-id="30828-445">Description</span><span class="sxs-lookup"><span data-stu-id="30828-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30828-446">stringToSearch</span></span> |<span data-ttu-id="30828-447">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-447">Yes</span></span> |<span data-ttu-id="30828-448">string</span><span class="sxs-lookup"><span data-stu-id="30828-448">string</span></span> |<span data-ttu-id="30828-449">La valeur qui contient l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30828-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30828-450">stringToFind</span></span> |<span data-ttu-id="30828-451">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-451">Yes</span></span> |<span data-ttu-id="30828-452">string</span><span class="sxs-lookup"><span data-stu-id="30828-452">string</span></span> |<span data-ttu-id="30828-453">La valeur à trouver.</span><span class="sxs-lookup"><span data-stu-id="30828-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-454">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-454">Return value</span></span>

<span data-ttu-id="30828-455">Entier qui représente la position de l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="30828-456">La valeur est basée sur zéro.</span><span class="sxs-lookup"><span data-stu-id="30828-456">The value is zero-based.</span></span> <span data-ttu-id="30828-457">Si l’élément est introuvable, la valeur -1 est retournée.</span><span class="sxs-lookup"><span data-stu-id="30828-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-458">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-458">Examples</span></span>

<span data-ttu-id="30828-459">L'exemple suivant montre comment utiliser les fonctions indexOf et lastIndexOf :</span><span class="sxs-lookup"><span data-stu-id="30828-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="30828-460">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-461">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-461">Name</span></span> | <span data-ttu-id="30828-462">Type</span><span class="sxs-lookup"><span data-stu-id="30828-462">Type</span></span> | <span data-ttu-id="30828-463">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-464">firstT</span><span class="sxs-lookup"><span data-stu-id="30828-464">firstT</span></span> | <span data-ttu-id="30828-465">int</span><span class="sxs-lookup"><span data-stu-id="30828-465">Int</span></span> | <span data-ttu-id="30828-466">0</span><span class="sxs-lookup"><span data-stu-id="30828-466">0</span></span> |
| <span data-ttu-id="30828-467">lastT</span><span class="sxs-lookup"><span data-stu-id="30828-467">lastT</span></span> | <span data-ttu-id="30828-468">int</span><span class="sxs-lookup"><span data-stu-id="30828-468">Int</span></span> | <span data-ttu-id="30828-469">3</span><span class="sxs-lookup"><span data-stu-id="30828-469">3</span></span> |
| <span data-ttu-id="30828-470">firstString</span><span class="sxs-lookup"><span data-stu-id="30828-470">firstString</span></span> | <span data-ttu-id="30828-471">int</span><span class="sxs-lookup"><span data-stu-id="30828-471">Int</span></span> | <span data-ttu-id="30828-472">2</span><span class="sxs-lookup"><span data-stu-id="30828-472">2</span></span> |
| <span data-ttu-id="30828-473">lastString</span><span class="sxs-lookup"><span data-stu-id="30828-473">lastString</span></span> | <span data-ttu-id="30828-474">int</span><span class="sxs-lookup"><span data-stu-id="30828-474">Int</span></span> | <span data-ttu-id="30828-475">0</span><span class="sxs-lookup"><span data-stu-id="30828-475">0</span></span> |
| <span data-ttu-id="30828-476">notFound</span><span class="sxs-lookup"><span data-stu-id="30828-476">notFound</span></span> | <span data-ttu-id="30828-477">int</span><span class="sxs-lookup"><span data-stu-id="30828-477">Int</span></span> | <span data-ttu-id="30828-478">-1</span><span class="sxs-lookup"><span data-stu-id="30828-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="30828-479">last</span><span class="sxs-lookup"><span data-stu-id="30828-479">last</span></span>
`last (arg1)`

<span data-ttu-id="30828-480">Retourne le dernier caractère de la chaîne ou le dernier élément du tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-481">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-481">Parameters</span></span>

| <span data-ttu-id="30828-482">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-482">Parameter</span></span> | <span data-ttu-id="30828-483">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-483">Required</span></span> | <span data-ttu-id="30828-484">Type</span><span class="sxs-lookup"><span data-stu-id="30828-484">Type</span></span> | <span data-ttu-id="30828-485">Description</span><span class="sxs-lookup"><span data-stu-id="30828-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-486">arg1</span><span class="sxs-lookup"><span data-stu-id="30828-486">arg1</span></span> |<span data-ttu-id="30828-487">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-487">Yes</span></span> |<span data-ttu-id="30828-488">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-488">array or string</span></span> |<span data-ttu-id="30828-489">La valeur permettant de récupérer le dernier élément ou caractère.</span><span class="sxs-lookup"><span data-stu-id="30828-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-490">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-490">Return value</span></span>

<span data-ttu-id="30828-491">Chaîne du dernier caractère ou type (chaîne, entier, tableau ou objet) du dernier élément d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-492">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-492">Examples</span></span>

<span data-ttu-id="30828-493">L’exemple suivant indique comment utiliser la dernière fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="30828-494">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-495">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-495">Name</span></span> | <span data-ttu-id="30828-496">Type</span><span class="sxs-lookup"><span data-stu-id="30828-496">Type</span></span> | <span data-ttu-id="30828-497">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30828-498">arrayOutput</span></span> | <span data-ttu-id="30828-499">String</span><span class="sxs-lookup"><span data-stu-id="30828-499">String</span></span> | <span data-ttu-id="30828-500">three</span><span class="sxs-lookup"><span data-stu-id="30828-500">three</span></span> |
| <span data-ttu-id="30828-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-501">stringOutput</span></span> | <span data-ttu-id="30828-502">String</span><span class="sxs-lookup"><span data-stu-id="30828-502">String</span></span> | <span data-ttu-id="30828-503">e</span><span class="sxs-lookup"><span data-stu-id="30828-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="30828-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="30828-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="30828-505">Retourne la dernière position d’une valeur dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="30828-506">La comparaison respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="30828-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-507">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-507">Parameters</span></span>

| <span data-ttu-id="30828-508">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-508">Parameter</span></span> | <span data-ttu-id="30828-509">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-509">Required</span></span> | <span data-ttu-id="30828-510">Type</span><span class="sxs-lookup"><span data-stu-id="30828-510">Type</span></span> | <span data-ttu-id="30828-511">Description</span><span class="sxs-lookup"><span data-stu-id="30828-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30828-512">stringToSearch</span></span> |<span data-ttu-id="30828-513">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-513">Yes</span></span> |<span data-ttu-id="30828-514">string</span><span class="sxs-lookup"><span data-stu-id="30828-514">string</span></span> |<span data-ttu-id="30828-515">La valeur qui contient l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30828-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30828-516">stringToFind</span></span> |<span data-ttu-id="30828-517">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-517">Yes</span></span> |<span data-ttu-id="30828-518">string</span><span class="sxs-lookup"><span data-stu-id="30828-518">string</span></span> |<span data-ttu-id="30828-519">La valeur à trouver.</span><span class="sxs-lookup"><span data-stu-id="30828-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-520">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-520">Return value</span></span>

<span data-ttu-id="30828-521">Entier qui représente la dernière position de l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="30828-522">La valeur est basée sur zéro.</span><span class="sxs-lookup"><span data-stu-id="30828-522">The value is zero-based.</span></span> <span data-ttu-id="30828-523">Si l’élément est introuvable, la valeur -1 est retournée.</span><span class="sxs-lookup"><span data-stu-id="30828-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-524">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-524">Examples</span></span>

<span data-ttu-id="30828-525">L'exemple suivant montre comment utiliser les fonctions indexOf et lastIndexOf :</span><span class="sxs-lookup"><span data-stu-id="30828-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="30828-526">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-527">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-527">Name</span></span> | <span data-ttu-id="30828-528">Type</span><span class="sxs-lookup"><span data-stu-id="30828-528">Type</span></span> | <span data-ttu-id="30828-529">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-530">firstT</span><span class="sxs-lookup"><span data-stu-id="30828-530">firstT</span></span> | <span data-ttu-id="30828-531">int</span><span class="sxs-lookup"><span data-stu-id="30828-531">Int</span></span> | <span data-ttu-id="30828-532">0</span><span class="sxs-lookup"><span data-stu-id="30828-532">0</span></span> |
| <span data-ttu-id="30828-533">lastT</span><span class="sxs-lookup"><span data-stu-id="30828-533">lastT</span></span> | <span data-ttu-id="30828-534">int</span><span class="sxs-lookup"><span data-stu-id="30828-534">Int</span></span> | <span data-ttu-id="30828-535">3</span><span class="sxs-lookup"><span data-stu-id="30828-535">3</span></span> |
| <span data-ttu-id="30828-536">firstString</span><span class="sxs-lookup"><span data-stu-id="30828-536">firstString</span></span> | <span data-ttu-id="30828-537">int</span><span class="sxs-lookup"><span data-stu-id="30828-537">Int</span></span> | <span data-ttu-id="30828-538">2</span><span class="sxs-lookup"><span data-stu-id="30828-538">2</span></span> |
| <span data-ttu-id="30828-539">lastString</span><span class="sxs-lookup"><span data-stu-id="30828-539">lastString</span></span> | <span data-ttu-id="30828-540">int</span><span class="sxs-lookup"><span data-stu-id="30828-540">Int</span></span> | <span data-ttu-id="30828-541">0</span><span class="sxs-lookup"><span data-stu-id="30828-541">0</span></span> |
| <span data-ttu-id="30828-542">notFound</span><span class="sxs-lookup"><span data-stu-id="30828-542">notFound</span></span> | <span data-ttu-id="30828-543">int</span><span class="sxs-lookup"><span data-stu-id="30828-543">Int</span></span> | <span data-ttu-id="30828-544">-1</span><span class="sxs-lookup"><span data-stu-id="30828-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="30828-545">length</span><span class="sxs-lookup"><span data-stu-id="30828-545">length</span></span>
`length(string)`

<span data-ttu-id="30828-546">Retourne le nombre de caractères dans une chaîne ou le nombre d’éléments dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-547">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-547">Parameters</span></span>

| <span data-ttu-id="30828-548">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-548">Parameter</span></span> | <span data-ttu-id="30828-549">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-549">Required</span></span> | <span data-ttu-id="30828-550">Type</span><span class="sxs-lookup"><span data-stu-id="30828-550">Type</span></span> | <span data-ttu-id="30828-551">Description</span><span class="sxs-lookup"><span data-stu-id="30828-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-552">arg1</span><span class="sxs-lookup"><span data-stu-id="30828-552">arg1</span></span> |<span data-ttu-id="30828-553">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-553">Yes</span></span> |<span data-ttu-id="30828-554">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-554">array or string</span></span> |<span data-ttu-id="30828-555">Tableau à utiliser pour l’obtention du nombre d’éléments, ou chaîne à utiliser pour l’obtention du nombre de caractères.</span><span class="sxs-lookup"><span data-stu-id="30828-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-556">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-556">Return value</span></span>

<span data-ttu-id="30828-557">Un entier.</span><span class="sxs-lookup"><span data-stu-id="30828-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="30828-558">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-558">Examples</span></span>

<span data-ttu-id="30828-559">L’exemple suivant montre comment utiliser la longueur avec un tableau et une chaîne :</span><span class="sxs-lookup"><span data-stu-id="30828-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="30828-560">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-561">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-561">Name</span></span> | <span data-ttu-id="30828-562">Type</span><span class="sxs-lookup"><span data-stu-id="30828-562">Type</span></span> | <span data-ttu-id="30828-563">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="30828-564">arrayLength</span></span> | <span data-ttu-id="30828-565">int</span><span class="sxs-lookup"><span data-stu-id="30828-565">Int</span></span> | <span data-ttu-id="30828-566">3</span><span class="sxs-lookup"><span data-stu-id="30828-566">3</span></span> |
| <span data-ttu-id="30828-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="30828-567">stringLength</span></span> | <span data-ttu-id="30828-568">int</span><span class="sxs-lookup"><span data-stu-id="30828-568">Int</span></span> | <span data-ttu-id="30828-569">13.</span><span class="sxs-lookup"><span data-stu-id="30828-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="30828-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="30828-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="30828-571">Renvoie une chaîne alignée à droite en lui ajoutant des caractères sur la gauche jusqu’à ce que la longueur totale spécifiée ait été atteinte.</span><span class="sxs-lookup"><span data-stu-id="30828-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-572">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-572">Parameters</span></span>

| <span data-ttu-id="30828-573">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-573">Parameter</span></span> | <span data-ttu-id="30828-574">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-574">Required</span></span> | <span data-ttu-id="30828-575">Type</span><span class="sxs-lookup"><span data-stu-id="30828-575">Type</span></span> | <span data-ttu-id="30828-576">Description</span><span class="sxs-lookup"><span data-stu-id="30828-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-577">valeur_à_remplir</span><span class="sxs-lookup"><span data-stu-id="30828-577">valueToPad</span></span> |<span data-ttu-id="30828-578">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-578">Yes</span></span> |<span data-ttu-id="30828-579">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="30828-579">string or int</span></span> |<span data-ttu-id="30828-580">Valeur à aligner à droite.</span><span class="sxs-lookup"><span data-stu-id="30828-580">The value to right-align.</span></span> |
| <span data-ttu-id="30828-581">longueur_totale</span><span class="sxs-lookup"><span data-stu-id="30828-581">totalLength</span></span> |<span data-ttu-id="30828-582">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-582">Yes</span></span> |<span data-ttu-id="30828-583">int</span><span class="sxs-lookup"><span data-stu-id="30828-583">int</span></span> |<span data-ttu-id="30828-584">Nombre total de caractères de la chaîne renvoyée.</span><span class="sxs-lookup"><span data-stu-id="30828-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="30828-585">caractère_de_remplissage</span><span class="sxs-lookup"><span data-stu-id="30828-585">paddingCharacter</span></span> |<span data-ttu-id="30828-586">Non</span><span class="sxs-lookup"><span data-stu-id="30828-586">No</span></span> |<span data-ttu-id="30828-587">caractère unique</span><span class="sxs-lookup"><span data-stu-id="30828-587">single character</span></span> |<span data-ttu-id="30828-588">Caractère de remplissage à insérer sur la gauche jusqu’à ce que la longueur totale soit atteinte.</span><span class="sxs-lookup"><span data-stu-id="30828-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="30828-589">La valeur par défaut est un espace.</span><span class="sxs-lookup"><span data-stu-id="30828-589">The default value is a space.</span></span> |

<span data-ttu-id="30828-590">Si la chaîne d’origine est plus longue que le nombre de caractères de remplissage, aucun caractère n’est ajouté.</span><span class="sxs-lookup"><span data-stu-id="30828-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="30828-591">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-591">Return value</span></span>

<span data-ttu-id="30828-592">Chaîne avec au moins le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="30828-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-593">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-593">Examples</span></span>

<span data-ttu-id="30828-594">L’exemple ci-après indique comment remplir la valeur de paramètre fournie par l’utilisateur avec le caractère zéro jusqu’à atteindre le nombre total de caractères.</span><span class="sxs-lookup"><span data-stu-id="30828-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

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

<span data-ttu-id="30828-595">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-596">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-596">Name</span></span> | <span data-ttu-id="30828-597">Type</span><span class="sxs-lookup"><span data-stu-id="30828-597">Type</span></span> | <span data-ttu-id="30828-598">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-599">stringOutput</span></span> | <span data-ttu-id="30828-600">String</span><span class="sxs-lookup"><span data-stu-id="30828-600">String</span></span> | <span data-ttu-id="30828-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="30828-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="30828-602">replace</span><span class="sxs-lookup"><span data-stu-id="30828-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="30828-603">Renvoie une nouvelle chaîne dans laquelle toutes les instances d’une chaîne ont été remplacées par une autre.</span><span class="sxs-lookup"><span data-stu-id="30828-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-604">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-604">Parameters</span></span>

| <span data-ttu-id="30828-605">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-605">Parameter</span></span> | <span data-ttu-id="30828-606">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-606">Required</span></span> | <span data-ttu-id="30828-607">Type</span><span class="sxs-lookup"><span data-stu-id="30828-607">Type</span></span> | <span data-ttu-id="30828-608">Description</span><span class="sxs-lookup"><span data-stu-id="30828-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-609">chaîne_initiale</span><span class="sxs-lookup"><span data-stu-id="30828-609">originalString</span></span> |<span data-ttu-id="30828-610">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-610">Yes</span></span> |<span data-ttu-id="30828-611">string</span><span class="sxs-lookup"><span data-stu-id="30828-611">string</span></span> |<span data-ttu-id="30828-612">La valeur qu’ont toutes les instances d’une chaîne ont été remplacées par une autre.</span><span class="sxs-lookup"><span data-stu-id="30828-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="30828-613">oldString</span><span class="sxs-lookup"><span data-stu-id="30828-613">oldString</span></span> |<span data-ttu-id="30828-614">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-614">Yes</span></span> |<span data-ttu-id="30828-615">string</span><span class="sxs-lookup"><span data-stu-id="30828-615">string</span></span> |<span data-ttu-id="30828-616">Chaîne à supprimer de la chaîne initiale.</span><span class="sxs-lookup"><span data-stu-id="30828-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="30828-617">newString</span><span class="sxs-lookup"><span data-stu-id="30828-617">newString</span></span> |<span data-ttu-id="30828-618">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-618">Yes</span></span> |<span data-ttu-id="30828-619">string</span><span class="sxs-lookup"><span data-stu-id="30828-619">string</span></span> |<span data-ttu-id="30828-620">Chaîne à ajouter à la place de la chaîne supprimée.</span><span class="sxs-lookup"><span data-stu-id="30828-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-621">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-621">Return value</span></span>

<span data-ttu-id="30828-622">Chaîne contenant les caractères remplacés.</span><span class="sxs-lookup"><span data-stu-id="30828-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-623">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-623">Examples</span></span>

<span data-ttu-id="30828-624">L’exemple suivant illustre comment supprimer tous les tirets de la chaîne fournie par l’utilisateur et comment remplacer une partie de la chaîne par une autre chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

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

<span data-ttu-id="30828-625">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-626">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-626">Name</span></span> | <span data-ttu-id="30828-627">Type</span><span class="sxs-lookup"><span data-stu-id="30828-627">Type</span></span> | <span data-ttu-id="30828-628">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="30828-629">firstOutput</span></span> | <span data-ttu-id="30828-630">String</span><span class="sxs-lookup"><span data-stu-id="30828-630">String</span></span> | <span data-ttu-id="30828-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="30828-631">1231231234</span></span> |
| <span data-ttu-id="30828-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="30828-632">secodeOutput</span></span> | <span data-ttu-id="30828-633">String</span><span class="sxs-lookup"><span data-stu-id="30828-633">String</span></span> | <span data-ttu-id="30828-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="30828-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="30828-635">skip</span><span class="sxs-lookup"><span data-stu-id="30828-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="30828-636">Retourne une chaîne avec tous les caractères après le nombre spécifié de caractères, ou un tableau avec tous les éléments après le nombre spécifié d’éléments.</span><span class="sxs-lookup"><span data-stu-id="30828-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-637">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-637">Parameters</span></span>

| <span data-ttu-id="30828-638">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-638">Parameter</span></span> | <span data-ttu-id="30828-639">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-639">Required</span></span> | <span data-ttu-id="30828-640">Type</span><span class="sxs-lookup"><span data-stu-id="30828-640">Type</span></span> | <span data-ttu-id="30828-641">Description</span><span class="sxs-lookup"><span data-stu-id="30828-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="30828-642">originalValue</span></span> |<span data-ttu-id="30828-643">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-643">Yes</span></span> |<span data-ttu-id="30828-644">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-644">array or string</span></span> |<span data-ttu-id="30828-645">Tableau ou chaîne à utiliser pour ignorer les caractères.</span><span class="sxs-lookup"><span data-stu-id="30828-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="30828-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="30828-646">numberToSkip</span></span> |<span data-ttu-id="30828-647">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-647">Yes</span></span> |<span data-ttu-id="30828-648">int</span><span class="sxs-lookup"><span data-stu-id="30828-648">int</span></span> |<span data-ttu-id="30828-649">Nombre d’éléments ou de caractères à ignorer.</span><span class="sxs-lookup"><span data-stu-id="30828-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="30828-650">Si cette valeur est inférieure ou égale à 0, tous les éléments ou caractères de la valeur sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="30828-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="30828-651">Si elle est supérieure à la longueur du tableau ou de la chaîne, un tableau ou une chaîne vide est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="30828-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-652">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-652">Return value</span></span>

<span data-ttu-id="30828-653">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-654">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-654">Examples</span></span>

<span data-ttu-id="30828-655">L’exemple suivant ignore le nombre spécifié d’éléments dans le tableau et le nombre spécifié de caractères dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="30828-656">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-657">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-657">Name</span></span> | <span data-ttu-id="30828-658">Type</span><span class="sxs-lookup"><span data-stu-id="30828-658">Type</span></span> | <span data-ttu-id="30828-659">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30828-660">arrayOutput</span></span> | <span data-ttu-id="30828-661">Tableau</span><span class="sxs-lookup"><span data-stu-id="30828-661">Array</span></span> | <span data-ttu-id="30828-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="30828-662">["three"]</span></span> |
| <span data-ttu-id="30828-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-663">stringOutput</span></span> | <span data-ttu-id="30828-664">String</span><span class="sxs-lookup"><span data-stu-id="30828-664">String</span></span> | <span data-ttu-id="30828-665">two three</span><span class="sxs-lookup"><span data-stu-id="30828-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="30828-666">split</span><span class="sxs-lookup"><span data-stu-id="30828-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="30828-667">Renvoie un tableau de chaînes qui contient les sous-chaînes de la chaîne d’entrée séparées par les délimiteurs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="30828-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-668">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-668">Parameters</span></span>

| <span data-ttu-id="30828-669">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-669">Parameter</span></span> | <span data-ttu-id="30828-670">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-670">Required</span></span> | <span data-ttu-id="30828-671">Type</span><span class="sxs-lookup"><span data-stu-id="30828-671">Type</span></span> | <span data-ttu-id="30828-672">Description</span><span class="sxs-lookup"><span data-stu-id="30828-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-673">chaîne_entrée</span><span class="sxs-lookup"><span data-stu-id="30828-673">inputString</span></span> |<span data-ttu-id="30828-674">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-674">Yes</span></span> |<span data-ttu-id="30828-675">string</span><span class="sxs-lookup"><span data-stu-id="30828-675">string</span></span> |<span data-ttu-id="30828-676">Chaîne à fractionner.</span><span class="sxs-lookup"><span data-stu-id="30828-676">The string to split.</span></span> |
| <span data-ttu-id="30828-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="30828-677">delimiter</span></span> |<span data-ttu-id="30828-678">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-678">Yes</span></span> |<span data-ttu-id="30828-679">chaîne ou tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="30828-679">string or array of strings</span></span> |<span data-ttu-id="30828-680">Le séparateur à utiliser pour fractionner la chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-681">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-681">Return value</span></span>

<span data-ttu-id="30828-682">Tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="30828-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-683">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-683">Examples</span></span>

<span data-ttu-id="30828-684">L’exemple suivant fractionne la chaîne d’entrée par une virgule et par une virgule ou un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="30828-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="30828-685">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-686">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-686">Name</span></span> | <span data-ttu-id="30828-687">Type</span><span class="sxs-lookup"><span data-stu-id="30828-687">Type</span></span> | <span data-ttu-id="30828-688">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="30828-689">firstOutput</span></span> | <span data-ttu-id="30828-690">Tableau</span><span class="sxs-lookup"><span data-stu-id="30828-690">Array</span></span> | <span data-ttu-id="30828-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="30828-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="30828-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="30828-692">secondOutput</span></span> | <span data-ttu-id="30828-693">Tableau</span><span class="sxs-lookup"><span data-stu-id="30828-693">Array</span></span> | <span data-ttu-id="30828-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="30828-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="30828-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="30828-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="30828-696">Détermine si une chaîne commence par une valeur.</span><span class="sxs-lookup"><span data-stu-id="30828-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="30828-697">La comparaison respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="30828-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-698">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-698">Parameters</span></span>

| <span data-ttu-id="30828-699">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-699">Parameter</span></span> | <span data-ttu-id="30828-700">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-700">Required</span></span> | <span data-ttu-id="30828-701">Type</span><span class="sxs-lookup"><span data-stu-id="30828-701">Type</span></span> | <span data-ttu-id="30828-702">Description</span><span class="sxs-lookup"><span data-stu-id="30828-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30828-703">stringToSearch</span></span> |<span data-ttu-id="30828-704">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-704">Yes</span></span> |<span data-ttu-id="30828-705">string</span><span class="sxs-lookup"><span data-stu-id="30828-705">string</span></span> |<span data-ttu-id="30828-706">La valeur qui contient l’élément à rechercher.</span><span class="sxs-lookup"><span data-stu-id="30828-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30828-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30828-707">stringToFind</span></span> |<span data-ttu-id="30828-708">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-708">Yes</span></span> |<span data-ttu-id="30828-709">string</span><span class="sxs-lookup"><span data-stu-id="30828-709">string</span></span> |<span data-ttu-id="30828-710">La valeur à trouver.</span><span class="sxs-lookup"><span data-stu-id="30828-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-711">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-711">Return value</span></span>

<span data-ttu-id="30828-712">**True** si le ou les premiers caractères de la chaîne correspondent à la valeur ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="30828-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-713">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-713">Examples</span></span>

<span data-ttu-id="30828-714">L'exemple suivant montre comment utiliser les fonctions startsWith et endsWith :</span><span class="sxs-lookup"><span data-stu-id="30828-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="30828-715">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-716">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-716">Name</span></span> | <span data-ttu-id="30828-717">Type</span><span class="sxs-lookup"><span data-stu-id="30828-717">Type</span></span> | <span data-ttu-id="30828-718">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="30828-719">startsTrue</span></span> | <span data-ttu-id="30828-720">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-720">Bool</span></span> | <span data-ttu-id="30828-721">true</span><span class="sxs-lookup"><span data-stu-id="30828-721">True</span></span> |
| <span data-ttu-id="30828-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30828-722">startsCapTrue</span></span> | <span data-ttu-id="30828-723">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-723">Bool</span></span> | <span data-ttu-id="30828-724">true</span><span class="sxs-lookup"><span data-stu-id="30828-724">True</span></span> |
| <span data-ttu-id="30828-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="30828-725">startsFalse</span></span> | <span data-ttu-id="30828-726">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-726">Bool</span></span> | <span data-ttu-id="30828-727">False</span><span class="sxs-lookup"><span data-stu-id="30828-727">False</span></span> |
| <span data-ttu-id="30828-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="30828-728">endsTrue</span></span> | <span data-ttu-id="30828-729">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-729">Bool</span></span> | <span data-ttu-id="30828-730">true</span><span class="sxs-lookup"><span data-stu-id="30828-730">True</span></span> |
| <span data-ttu-id="30828-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30828-731">endsCapTrue</span></span> | <span data-ttu-id="30828-732">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-732">Bool</span></span> | <span data-ttu-id="30828-733">true</span><span class="sxs-lookup"><span data-stu-id="30828-733">True</span></span> |
| <span data-ttu-id="30828-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="30828-734">endsFalse</span></span> | <span data-ttu-id="30828-735">Bool</span><span class="sxs-lookup"><span data-stu-id="30828-735">Bool</span></span> | <span data-ttu-id="30828-736">False</span><span class="sxs-lookup"><span data-stu-id="30828-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="30828-737">string</span><span class="sxs-lookup"><span data-stu-id="30828-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="30828-738">Convertit la valeur spécifiée en chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-739">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-739">Parameters</span></span>

| <span data-ttu-id="30828-740">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-740">Parameter</span></span> | <span data-ttu-id="30828-741">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-741">Required</span></span> | <span data-ttu-id="30828-742">Type</span><span class="sxs-lookup"><span data-stu-id="30828-742">Type</span></span> | <span data-ttu-id="30828-743">Description</span><span class="sxs-lookup"><span data-stu-id="30828-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="30828-744">valueToConvert</span></span> |<span data-ttu-id="30828-745">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-745">Yes</span></span> | <span data-ttu-id="30828-746">Quelconque</span><span class="sxs-lookup"><span data-stu-id="30828-746">Any</span></span> |<span data-ttu-id="30828-747">Valeur à convertir en chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-747">The value to convert to string.</span></span> <span data-ttu-id="30828-748">N’importe quel type de valeur peut être converti, y compris les objets et des tableaux.</span><span class="sxs-lookup"><span data-stu-id="30828-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-749">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-749">Return value</span></span>

<span data-ttu-id="30828-750">Chaîne de la valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="30828-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-751">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-751">Examples</span></span>

<span data-ttu-id="30828-752">L’exemple suivant montre comment convertir différents types de valeurs de chaînes :</span><span class="sxs-lookup"><span data-stu-id="30828-752">The following example shows how to convert different types of values to strings:</span></span>

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

<span data-ttu-id="30828-753">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-754">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-754">Name</span></span> | <span data-ttu-id="30828-755">Type</span><span class="sxs-lookup"><span data-stu-id="30828-755">Type</span></span> | <span data-ttu-id="30828-756">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="30828-757">objectOutput</span></span> | <span data-ttu-id="30828-758">String</span><span class="sxs-lookup"><span data-stu-id="30828-758">String</span></span> | <span data-ttu-id="30828-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="30828-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="30828-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30828-760">arrayOutput</span></span> | <span data-ttu-id="30828-761">String</span><span class="sxs-lookup"><span data-stu-id="30828-761">String</span></span> | <span data-ttu-id="30828-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="30828-762">["a","b","c"]</span></span> |
| <span data-ttu-id="30828-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="30828-763">intOutput</span></span> | <span data-ttu-id="30828-764">String</span><span class="sxs-lookup"><span data-stu-id="30828-764">String</span></span> | <span data-ttu-id="30828-765">5</span><span class="sxs-lookup"><span data-stu-id="30828-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="30828-766">substring</span><span class="sxs-lookup"><span data-stu-id="30828-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="30828-767">Retourne une sous-chaîne qui commence à la position de caractère spécifiée et qui contient le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="30828-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-768">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-768">Parameters</span></span>

| <span data-ttu-id="30828-769">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-769">Parameter</span></span> | <span data-ttu-id="30828-770">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-770">Required</span></span> | <span data-ttu-id="30828-771">Type</span><span class="sxs-lookup"><span data-stu-id="30828-771">Type</span></span> | <span data-ttu-id="30828-772">Description</span><span class="sxs-lookup"><span data-stu-id="30828-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-773">chaîne_à_analyser</span><span class="sxs-lookup"><span data-stu-id="30828-773">stringToParse</span></span> |<span data-ttu-id="30828-774">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-774">Yes</span></span> |<span data-ttu-id="30828-775">string</span><span class="sxs-lookup"><span data-stu-id="30828-775">string</span></span> |<span data-ttu-id="30828-776">La chaîne d’origine de laquelle la sous-chaîne est extraite.</span><span class="sxs-lookup"><span data-stu-id="30828-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="30828-777">index_début</span><span class="sxs-lookup"><span data-stu-id="30828-777">startIndex</span></span> |<span data-ttu-id="30828-778">Non</span><span class="sxs-lookup"><span data-stu-id="30828-778">No</span></span> |<span data-ttu-id="30828-779">int</span><span class="sxs-lookup"><span data-stu-id="30828-779">int</span></span> |<span data-ttu-id="30828-780">La position de caractère (commençant à zéro) de la sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="30828-781">length</span><span class="sxs-lookup"><span data-stu-id="30828-781">length</span></span> |<span data-ttu-id="30828-782">Non</span><span class="sxs-lookup"><span data-stu-id="30828-782">No</span></span> |<span data-ttu-id="30828-783">int</span><span class="sxs-lookup"><span data-stu-id="30828-783">int</span></span> |<span data-ttu-id="30828-784">Le nombre de caractères de la sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-784">The number of characters for the substring.</span></span> <span data-ttu-id="30828-785">Doit faire référence à un emplacement au sein de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-786">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-786">Return value</span></span>

<span data-ttu-id="30828-787">Sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="30828-788">Remarques</span><span class="sxs-lookup"><span data-stu-id="30828-788">Remarks</span></span>

<span data-ttu-id="30828-789">La fonction échoue lorsque la sous-chaîne s’étend au-delà de la fin de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="30828-790">L’exemple suivant échoue avec l’erreur « Les paramètres d’index et de longueur doivent correspondre à un emplacement au sein de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="30828-791">Paramètre d’index : « 0 », paramètre de longueur : « 11 », paramètre de longueur de la chaîne : « 10 ».</span><span class="sxs-lookup"><span data-stu-id="30828-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="30828-792">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-792">Examples</span></span>

<span data-ttu-id="30828-793">L’exemple suivant extrait une sous-chaîne à partir d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="30828-793">The following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="30828-794">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-795">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-795">Name</span></span> | <span data-ttu-id="30828-796">Type</span><span class="sxs-lookup"><span data-stu-id="30828-796">Type</span></span> | <span data-ttu-id="30828-797">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-798">substringOutput</span></span> | <span data-ttu-id="30828-799">String</span><span class="sxs-lookup"><span data-stu-id="30828-799">String</span></span> | <span data-ttu-id="30828-800">two</span><span class="sxs-lookup"><span data-stu-id="30828-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="30828-801">take</span><span class="sxs-lookup"><span data-stu-id="30828-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="30828-802">Retourne une chaîne avec le nombre spécifié de caractères à partir du début de la chaîne, ou un tableau avec le nombre spécifié d’éléments à partir du début du tableau.</span><span class="sxs-lookup"><span data-stu-id="30828-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-803">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-803">Parameters</span></span>

| <span data-ttu-id="30828-804">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-804">Parameter</span></span> | <span data-ttu-id="30828-805">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-805">Required</span></span> | <span data-ttu-id="30828-806">Type</span><span class="sxs-lookup"><span data-stu-id="30828-806">Type</span></span> | <span data-ttu-id="30828-807">Description</span><span class="sxs-lookup"><span data-stu-id="30828-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="30828-808">originalValue</span></span> |<span data-ttu-id="30828-809">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-809">Yes</span></span> |<span data-ttu-id="30828-810">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="30828-810">array or string</span></span> |<span data-ttu-id="30828-811">Tableau ou chaîne à partir duquel les éléments sont tirés.</span><span class="sxs-lookup"><span data-stu-id="30828-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="30828-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="30828-812">numberToTake</span></span> |<span data-ttu-id="30828-813">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-813">Yes</span></span> |<span data-ttu-id="30828-814">int</span><span class="sxs-lookup"><span data-stu-id="30828-814">int</span></span> |<span data-ttu-id="30828-815">Nombre d’éléments ou de caractères à prendre.</span><span class="sxs-lookup"><span data-stu-id="30828-815">The number of elements or characters to take.</span></span> <span data-ttu-id="30828-816">Si cette valeur est inférieure ou égale à 0, une chaîne ou un tableau vide est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="30828-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="30828-817">Si elle est supérieure à la longueur du tableau ou de la chaîne donné(e), tous les éléments du tableau ou de chaîne sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="30828-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-818">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-818">Return value</span></span>

<span data-ttu-id="30828-819">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-820">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-820">Examples</span></span>

<span data-ttu-id="30828-821">L’exemple suivant prend le nombre spécifié d’éléments du tableau, et les caractères d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="30828-822">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-823">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-823">Name</span></span> | <span data-ttu-id="30828-824">Type</span><span class="sxs-lookup"><span data-stu-id="30828-824">Type</span></span> | <span data-ttu-id="30828-825">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30828-826">arrayOutput</span></span> | <span data-ttu-id="30828-827">Tableau</span><span class="sxs-lookup"><span data-stu-id="30828-827">Array</span></span> | <span data-ttu-id="30828-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="30828-828">["one", "two"]</span></span> |
| <span data-ttu-id="30828-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-829">stringOutput</span></span> | <span data-ttu-id="30828-830">String</span><span class="sxs-lookup"><span data-stu-id="30828-830">String</span></span> | <span data-ttu-id="30828-831">sur</span><span class="sxs-lookup"><span data-stu-id="30828-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="30828-832">toLower</span><span class="sxs-lookup"><span data-stu-id="30828-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="30828-833">Convertit la chaîne spécifiée en minuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-834">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-834">Parameters</span></span>

| <span data-ttu-id="30828-835">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-835">Parameter</span></span> | <span data-ttu-id="30828-836">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-836">Required</span></span> | <span data-ttu-id="30828-837">Type</span><span class="sxs-lookup"><span data-stu-id="30828-837">Type</span></span> | <span data-ttu-id="30828-838">Description</span><span class="sxs-lookup"><span data-stu-id="30828-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-839">chaîne_à_modifier</span><span class="sxs-lookup"><span data-stu-id="30828-839">stringToChange</span></span> |<span data-ttu-id="30828-840">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-840">Yes</span></span> |<span data-ttu-id="30828-841">string</span><span class="sxs-lookup"><span data-stu-id="30828-841">string</span></span> |<span data-ttu-id="30828-842">La valeur à convertir en minuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-843">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-843">Return value</span></span>

<span data-ttu-id="30828-844">Chaîne convertie en minuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-845">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-845">Examples</span></span>

<span data-ttu-id="30828-846">L’exemple ci-après convertit une valeur de paramètre en minuscules et en majuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-846">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="30828-847">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-848">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-848">Name</span></span> | <span data-ttu-id="30828-849">Type</span><span class="sxs-lookup"><span data-stu-id="30828-849">Type</span></span> | <span data-ttu-id="30828-850">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="30828-851">toLowerOutput</span></span> | <span data-ttu-id="30828-852">String</span><span class="sxs-lookup"><span data-stu-id="30828-852">String</span></span> | <span data-ttu-id="30828-853">one two three</span><span class="sxs-lookup"><span data-stu-id="30828-853">one two three</span></span> |
| <span data-ttu-id="30828-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="30828-854">toUpperOutput</span></span> | <span data-ttu-id="30828-855">String</span><span class="sxs-lookup"><span data-stu-id="30828-855">String</span></span> | <span data-ttu-id="30828-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="30828-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="30828-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="30828-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="30828-858">Convertit la chaîne spécifiée en majuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-859">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-859">Parameters</span></span>

| <span data-ttu-id="30828-860">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-860">Parameter</span></span> | <span data-ttu-id="30828-861">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-861">Required</span></span> | <span data-ttu-id="30828-862">Type</span><span class="sxs-lookup"><span data-stu-id="30828-862">Type</span></span> | <span data-ttu-id="30828-863">Description</span><span class="sxs-lookup"><span data-stu-id="30828-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-864">chaîne_à_modifier</span><span class="sxs-lookup"><span data-stu-id="30828-864">stringToChange</span></span> |<span data-ttu-id="30828-865">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-865">Yes</span></span> |<span data-ttu-id="30828-866">string</span><span class="sxs-lookup"><span data-stu-id="30828-866">string</span></span> |<span data-ttu-id="30828-867">La valeur à convertir en majuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-868">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-868">Return value</span></span>

<span data-ttu-id="30828-869">Chaîne convertie en majuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-870">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-870">Examples</span></span>

<span data-ttu-id="30828-871">L’exemple ci-après convertit une valeur de paramètre en minuscules et en majuscules.</span><span class="sxs-lookup"><span data-stu-id="30828-871">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="30828-872">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-873">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-873">Name</span></span> | <span data-ttu-id="30828-874">Type</span><span class="sxs-lookup"><span data-stu-id="30828-874">Type</span></span> | <span data-ttu-id="30828-875">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="30828-876">toLowerOutput</span></span> | <span data-ttu-id="30828-877">String</span><span class="sxs-lookup"><span data-stu-id="30828-877">String</span></span> | <span data-ttu-id="30828-878">one two three</span><span class="sxs-lookup"><span data-stu-id="30828-878">one two three</span></span> |
| <span data-ttu-id="30828-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="30828-879">toUpperOutput</span></span> | <span data-ttu-id="30828-880">String</span><span class="sxs-lookup"><span data-stu-id="30828-880">String</span></span> | <span data-ttu-id="30828-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="30828-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="30828-882">découper</span><span class="sxs-lookup"><span data-stu-id="30828-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="30828-883">Supprime tous les espaces de début et de fin de la chaîne indiquée.</span><span class="sxs-lookup"><span data-stu-id="30828-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-884">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-884">Parameters</span></span>

| <span data-ttu-id="30828-885">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-885">Parameter</span></span> | <span data-ttu-id="30828-886">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-886">Required</span></span> | <span data-ttu-id="30828-887">Type</span><span class="sxs-lookup"><span data-stu-id="30828-887">Type</span></span> | <span data-ttu-id="30828-888">Description</span><span class="sxs-lookup"><span data-stu-id="30828-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="30828-889">stringToTrim</span></span> |<span data-ttu-id="30828-890">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-890">Yes</span></span> |<span data-ttu-id="30828-891">string</span><span class="sxs-lookup"><span data-stu-id="30828-891">string</span></span> |<span data-ttu-id="30828-892">La valeur à supprimer.</span><span class="sxs-lookup"><span data-stu-id="30828-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-893">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-893">Return value</span></span>

<span data-ttu-id="30828-894">Chaîne sans les premiers et derniers caractères d’espace.</span><span class="sxs-lookup"><span data-stu-id="30828-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-895">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-895">Examples</span></span>

<span data-ttu-id="30828-896">L’exemple suivant supprime les espaces à partir du paramètre.</span><span class="sxs-lookup"><span data-stu-id="30828-896">The following example trims the white-space characters from the parameter.</span></span>

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

<span data-ttu-id="30828-897">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-898">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-898">Name</span></span> | <span data-ttu-id="30828-899">Type</span><span class="sxs-lookup"><span data-stu-id="30828-899">Type</span></span> | <span data-ttu-id="30828-900">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-901">return</span><span class="sxs-lookup"><span data-stu-id="30828-901">return</span></span> | <span data-ttu-id="30828-902">String</span><span class="sxs-lookup"><span data-stu-id="30828-902">String</span></span> | <span data-ttu-id="30828-903">one two three</span><span class="sxs-lookup"><span data-stu-id="30828-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="30828-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="30828-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="30828-905">Crée une chaîne de hachage déterministe basée sur les valeurs fournies en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="30828-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="30828-906">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-906">Parameters</span></span>

| <span data-ttu-id="30828-907">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-907">Parameter</span></span> | <span data-ttu-id="30828-908">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-908">Required</span></span> | <span data-ttu-id="30828-909">Type</span><span class="sxs-lookup"><span data-stu-id="30828-909">Type</span></span> | <span data-ttu-id="30828-910">Description</span><span class="sxs-lookup"><span data-stu-id="30828-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-911">baseString</span><span class="sxs-lookup"><span data-stu-id="30828-911">baseString</span></span> |<span data-ttu-id="30828-912">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-912">Yes</span></span> |<span data-ttu-id="30828-913">string</span><span class="sxs-lookup"><span data-stu-id="30828-913">string</span></span> |<span data-ttu-id="30828-914">La valeur utilisée dans la fonction de hachage pour créer une chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="30828-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="30828-915">paramètres supplémentaires le cas échéant</span><span class="sxs-lookup"><span data-stu-id="30828-915">additional parameters as needed</span></span> |<span data-ttu-id="30828-916">Non</span><span class="sxs-lookup"><span data-stu-id="30828-916">No</span></span> |<span data-ttu-id="30828-917">string</span><span class="sxs-lookup"><span data-stu-id="30828-917">string</span></span> |<span data-ttu-id="30828-918">Vous pouvez ajouter autant de chaînes que nécessaire pour créer la valeur qui spécifie le niveau d’unicité.</span><span class="sxs-lookup"><span data-stu-id="30828-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="30828-919">Remarques</span><span class="sxs-lookup"><span data-stu-id="30828-919">Remarks</span></span>

<span data-ttu-id="30828-920">Cette fonction est utile lorsque vous avez besoin de créer un nom unique pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="30828-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="30828-921">Vous fournissez des valeurs de paramètre qui limitent l’étendue d’unicité pour le résultat.</span><span class="sxs-lookup"><span data-stu-id="30828-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="30828-922">Vous pouvez spécifier si le nom est unique pour l’abonnement, le groupe de ressources ou le déploiement.</span><span class="sxs-lookup"><span data-stu-id="30828-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="30828-923">La valeur renvoyée n’est pas une chaîne aléatoire, mais plutôt le résultat d’une fonction de hachage.</span><span class="sxs-lookup"><span data-stu-id="30828-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="30828-924">La valeur renvoyée comprend 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="30828-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="30828-925">Elle n’est pas globalement unique.</span><span class="sxs-lookup"><span data-stu-id="30828-925">It is not globally unique.</span></span> <span data-ttu-id="30828-926">Il se peut que vous souhaitiez associer un préfixe de votre convention d’affectation de noms à la valeur pour créer un nom explicite.</span><span class="sxs-lookup"><span data-stu-id="30828-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="30828-927">L’exemple suivant montre le format de la valeur renvoyée.</span><span class="sxs-lookup"><span data-stu-id="30828-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="30828-928">La valeur réelle varie en fonction des paramètres fournis.</span><span class="sxs-lookup"><span data-stu-id="30828-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="30828-929">Les exemples suivants montrent comment utiliser uniqueString afin de créer une valeur unique pour des niveaux couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="30828-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="30828-930">Unique limité à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="30828-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="30828-931">Unique limité au groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="30828-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="30828-932">Unique limité au déploiement pour un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="30828-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="30828-933">L'exemple suivant montre comment créer un nom unique pour un compte de stockage basé sur votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="30828-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="30828-934">Dans le groupe de ressources, le nom n’est pas unique s’il est construit de la même façon.</span><span class="sxs-lookup"><span data-stu-id="30828-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="30828-935">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-935">Return value</span></span>

<span data-ttu-id="30828-936">Chaîne contenant 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="30828-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-937">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-937">Examples</span></span>

<span data-ttu-id="30828-938">L’exemple suivant renvoie les résultats à partir d’uniquestring :</span><span class="sxs-lookup"><span data-stu-id="30828-938">The following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="30828-939">URI</span><span class="sxs-lookup"><span data-stu-id="30828-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="30828-940">Crée un URI absolu en combinant le baseUri et la chaîne relativeUri.</span><span class="sxs-lookup"><span data-stu-id="30828-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-941">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-941">Parameters</span></span>

| <span data-ttu-id="30828-942">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-942">Parameter</span></span> | <span data-ttu-id="30828-943">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-943">Required</span></span> | <span data-ttu-id="30828-944">Type</span><span class="sxs-lookup"><span data-stu-id="30828-944">Type</span></span> | <span data-ttu-id="30828-945">Description</span><span class="sxs-lookup"><span data-stu-id="30828-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="30828-946">baseUri</span></span> |<span data-ttu-id="30828-947">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-947">Yes</span></span> |<span data-ttu-id="30828-948">string</span><span class="sxs-lookup"><span data-stu-id="30828-948">string</span></span> |<span data-ttu-id="30828-949">La chaîne d’URI de base.</span><span class="sxs-lookup"><span data-stu-id="30828-949">The base uri string.</span></span> |
| <span data-ttu-id="30828-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="30828-950">relativeUri</span></span> |<span data-ttu-id="30828-951">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-951">Yes</span></span> |<span data-ttu-id="30828-952">string</span><span class="sxs-lookup"><span data-stu-id="30828-952">string</span></span> |<span data-ttu-id="30828-953">La chaîne d’URI relatif à ajouter à la chaîne d’URI de base.</span><span class="sxs-lookup"><span data-stu-id="30828-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="30828-954">La valeur du paramètre **baseUri** peut inclure un fichier spécifique, mais seul le chemin de base est utilisé lors de la construction de l’URI.</span><span class="sxs-lookup"><span data-stu-id="30828-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="30828-955">Par exemple, si vous passez `http://contoso.com/resources/azuredeploy.json` comme paramètre baseUri, l’URI de base résultant est `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="30828-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="30828-956">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-956">Return value</span></span>

<span data-ttu-id="30828-957">Chaîne représentant l’URI absolu pour les valeurs de base et relative.</span><span class="sxs-lookup"><span data-stu-id="30828-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-958">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-958">Examples</span></span>

<span data-ttu-id="30828-959">L’exemple suivant montre comment créer un lien vers un modèle imbriqué en fonction de la valeur du modèle parent.</span><span class="sxs-lookup"><span data-stu-id="30828-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="30828-960">L’exemple suivant montre comment utiliser les paramètres uri, uriComponent et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="30828-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30828-961">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-962">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-962">Name</span></span> | <span data-ttu-id="30828-963">Type</span><span class="sxs-lookup"><span data-stu-id="30828-963">Type</span></span> | <span data-ttu-id="30828-964">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30828-965">uriOutput</span></span> | <span data-ttu-id="30828-966">String</span><span class="sxs-lookup"><span data-stu-id="30828-966">String</span></span> | <span data-ttu-id="30828-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30828-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30828-968">componentOutput</span></span> | <span data-ttu-id="30828-969">String</span><span class="sxs-lookup"><span data-stu-id="30828-969">String</span></span> | <span data-ttu-id="30828-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30828-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-971">toStringOutput</span></span> | <span data-ttu-id="30828-972">String</span><span class="sxs-lookup"><span data-stu-id="30828-972">String</span></span> | <span data-ttu-id="30828-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="30828-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="30828-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="30828-975">Encode un URI.</span><span class="sxs-lookup"><span data-stu-id="30828-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-976">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-976">Parameters</span></span>

| <span data-ttu-id="30828-977">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-977">Parameter</span></span> | <span data-ttu-id="30828-978">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-978">Required</span></span> | <span data-ttu-id="30828-979">Type</span><span class="sxs-lookup"><span data-stu-id="30828-979">Type</span></span> | <span data-ttu-id="30828-980">Description</span><span class="sxs-lookup"><span data-stu-id="30828-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="30828-981">stringToEncode</span></span> |<span data-ttu-id="30828-982">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-982">Yes</span></span> |<span data-ttu-id="30828-983">string</span><span class="sxs-lookup"><span data-stu-id="30828-983">string</span></span> |<span data-ttu-id="30828-984">Valeur à encoder.</span><span class="sxs-lookup"><span data-stu-id="30828-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-985">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-985">Return value</span></span>

<span data-ttu-id="30828-986">Chaîne de la valeur encodée de l’URI.</span><span class="sxs-lookup"><span data-stu-id="30828-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-987">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-987">Examples</span></span>

<span data-ttu-id="30828-988">L’exemple suivant montre comment utiliser les paramètres uri, uriComponent et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="30828-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30828-989">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-990">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-990">Name</span></span> | <span data-ttu-id="30828-991">Type</span><span class="sxs-lookup"><span data-stu-id="30828-991">Type</span></span> | <span data-ttu-id="30828-992">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30828-993">uriOutput</span></span> | <span data-ttu-id="30828-994">String</span><span class="sxs-lookup"><span data-stu-id="30828-994">String</span></span> | <span data-ttu-id="30828-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30828-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30828-996">componentOutput</span></span> | <span data-ttu-id="30828-997">String</span><span class="sxs-lookup"><span data-stu-id="30828-997">String</span></span> | <span data-ttu-id="30828-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30828-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-999">toStringOutput</span></span> | <span data-ttu-id="30828-1000">String</span><span class="sxs-lookup"><span data-stu-id="30828-1000">String</span></span> | <span data-ttu-id="30828-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="30828-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="30828-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="30828-1003">Retourne une chaîne de la valeur encodée de l’URI.</span><span class="sxs-lookup"><span data-stu-id="30828-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="30828-1004">Paramètres</span><span class="sxs-lookup"><span data-stu-id="30828-1004">Parameters</span></span>

| <span data-ttu-id="30828-1005">Paramètre</span><span class="sxs-lookup"><span data-stu-id="30828-1005">Parameter</span></span> | <span data-ttu-id="30828-1006">Requis</span><span class="sxs-lookup"><span data-stu-id="30828-1006">Required</span></span> | <span data-ttu-id="30828-1007">Type</span><span class="sxs-lookup"><span data-stu-id="30828-1007">Type</span></span> | <span data-ttu-id="30828-1008">Description</span><span class="sxs-lookup"><span data-stu-id="30828-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30828-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="30828-1009">uriEncodedString</span></span> |<span data-ttu-id="30828-1010">Oui</span><span class="sxs-lookup"><span data-stu-id="30828-1010">Yes</span></span> |<span data-ttu-id="30828-1011">string</span><span class="sxs-lookup"><span data-stu-id="30828-1011">string</span></span> |<span data-ttu-id="30828-1012">Valeur encodée de l’URI à convertir en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="30828-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30828-1013">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="30828-1013">Return value</span></span>

<span data-ttu-id="30828-1014">Chaîne décodée de la valeur encodée de l’URI.</span><span class="sxs-lookup"><span data-stu-id="30828-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="30828-1015">Exemples</span><span class="sxs-lookup"><span data-stu-id="30828-1015">Examples</span></span>

<span data-ttu-id="30828-1016">L’exemple suivant montre comment utiliser les paramètres uri, uriComponent et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="30828-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30828-1017">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="30828-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30828-1018">Nom</span><span class="sxs-lookup"><span data-stu-id="30828-1018">Name</span></span> | <span data-ttu-id="30828-1019">Type</span><span class="sxs-lookup"><span data-stu-id="30828-1019">Type</span></span> | <span data-ttu-id="30828-1020">Valeur</span><span class="sxs-lookup"><span data-stu-id="30828-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30828-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30828-1021">uriOutput</span></span> | <span data-ttu-id="30828-1022">String</span><span class="sxs-lookup"><span data-stu-id="30828-1022">String</span></span> | <span data-ttu-id="30828-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30828-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30828-1024">componentOutput</span></span> | <span data-ttu-id="30828-1025">String</span><span class="sxs-lookup"><span data-stu-id="30828-1025">String</span></span> | <span data-ttu-id="30828-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30828-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30828-1027">toStringOutput</span></span> | <span data-ttu-id="30828-1028">String</span><span class="sxs-lookup"><span data-stu-id="30828-1028">String</span></span> | <span data-ttu-id="30828-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="30828-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="30828-1030">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30828-1030">Next steps</span></span>
* <span data-ttu-id="30828-1031">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30828-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="30828-1032">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30828-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="30828-1033">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="30828-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="30828-1034">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="30828-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

