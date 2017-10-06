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
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="d9df7-103">Fonctions de chaînes pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9df7-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="d9df7-104">Gestionnaire de ressources fournit hello suivant des fonctions pour manipuler des chaînes :</span><span class="sxs-lookup"><span data-stu-id="d9df7-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="d9df7-105">base64</span><span class="sxs-lookup"><span data-stu-id="d9df7-105">base64</span></span>](#base64)
* [<span data-ttu-id="d9df7-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="d9df7-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="d9df7-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="d9df7-108">concat</span><span class="sxs-lookup"><span data-stu-id="d9df7-108">concat</span></span>](#concat)
* [<span data-ttu-id="d9df7-109">contains</span><span class="sxs-lookup"><span data-stu-id="d9df7-109">contains</span></span>](#contains)
* [<span data-ttu-id="d9df7-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="d9df7-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="d9df7-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="d9df7-112">empty</span><span class="sxs-lookup"><span data-stu-id="d9df7-112">empty</span></span>](#empty)
* [<span data-ttu-id="d9df7-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="d9df7-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="d9df7-114">first</span><span class="sxs-lookup"><span data-stu-id="d9df7-114">first</span></span>](#first)
* [<span data-ttu-id="d9df7-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="d9df7-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="d9df7-116">last</span><span class="sxs-lookup"><span data-stu-id="d9df7-116">last</span></span>](#last)
* [<span data-ttu-id="d9df7-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="d9df7-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="d9df7-118">length</span><span class="sxs-lookup"><span data-stu-id="d9df7-118">length</span></span>](#length)
* [<span data-ttu-id="d9df7-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="d9df7-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="d9df7-120">replace</span><span class="sxs-lookup"><span data-stu-id="d9df7-120">replace</span></span>](#replace)
* [<span data-ttu-id="d9df7-121">skip</span><span class="sxs-lookup"><span data-stu-id="d9df7-121">skip</span></span>](#skip)
* [<span data-ttu-id="d9df7-122">split</span><span class="sxs-lookup"><span data-stu-id="d9df7-122">split</span></span>](#split)
* [<span data-ttu-id="d9df7-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="d9df7-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="d9df7-124">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-124">string</span></span>](#string)
* [<span data-ttu-id="d9df7-125">substring</span><span class="sxs-lookup"><span data-stu-id="d9df7-125">substring</span></span>](#substring)
* [<span data-ttu-id="d9df7-126">take</span><span class="sxs-lookup"><span data-stu-id="d9df7-126">take</span></span>](#take)
* [<span data-ttu-id="d9df7-127">toLower</span><span class="sxs-lookup"><span data-stu-id="d9df7-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="d9df7-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="d9df7-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="d9df7-129">découper</span><span class="sxs-lookup"><span data-stu-id="d9df7-129">trim</span></span>](#trim)
* [<span data-ttu-id="d9df7-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="d9df7-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="d9df7-131">URI</span><span class="sxs-lookup"><span data-stu-id="d9df7-131">uri</span></span>](#uri)
* [<span data-ttu-id="d9df7-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="d9df7-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="d9df7-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="d9df7-134">base64</span><span class="sxs-lookup"><span data-stu-id="d9df7-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="d9df7-135">Retourne hello représentation en base64 de la chaîne d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-136">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-136">Parameters</span></span>

| <span data-ttu-id="d9df7-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-137">Parameter</span></span> | <span data-ttu-id="d9df7-138">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-138">Required</span></span> | <span data-ttu-id="d9df7-139">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-139">Type</span></span> | <span data-ttu-id="d9df7-140">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-141">chaîne_entrée</span><span class="sxs-lookup"><span data-stu-id="d9df7-141">inputString</span></span> |<span data-ttu-id="d9df7-142">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-142">Yes</span></span> |<span data-ttu-id="d9df7-143">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-143">string</span></span> |<span data-ttu-id="d9df7-144">Bonjour tooreturn de valeur comme une représentation en base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-145">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-145">Return value</span></span>

<span data-ttu-id="d9df7-146">Chaîne contenant la représentation sous forme de hello en base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-147">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-147">Examples</span></span>

<span data-ttu-id="d9df7-148">Bonjour à l’exemple suivant montre comment toouse hello base64 (fonction).</span><span class="sxs-lookup"><span data-stu-id="d9df7-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="d9df7-149">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-150">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-150">Name</span></span> | <span data-ttu-id="d9df7-151">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-151">Type</span></span> | <span data-ttu-id="d9df7-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="d9df7-153">base64Output</span></span> | <span data-ttu-id="d9df7-154">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-154">String</span></span> | <span data-ttu-id="d9df7-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d9df7-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d9df7-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-156">toStringOutput</span></span> | <span data-ttu-id="d9df7-157">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-157">String</span></span> | <span data-ttu-id="d9df7-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d9df7-158">one, two, three</span></span> |
| <span data-ttu-id="d9df7-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-159">toJsonOutput</span></span> | <span data-ttu-id="d9df7-160">Object</span><span class="sxs-lookup"><span data-stu-id="d9df7-160">Object</span></span> | <span data-ttu-id="d9df7-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d9df7-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="d9df7-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="d9df7-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="d9df7-163">Convertit un objet JSON de tooa de représentation en base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-164">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-164">Parameters</span></span>

| <span data-ttu-id="d9df7-165">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-165">Parameter</span></span> | <span data-ttu-id="d9df7-166">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-166">Required</span></span> | <span data-ttu-id="d9df7-167">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-167">Type</span></span> | <span data-ttu-id="d9df7-168">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="d9df7-169">base64Value</span></span> |<span data-ttu-id="d9df7-170">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-170">Yes</span></span> |<span data-ttu-id="d9df7-171">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-171">string</span></span> |<span data-ttu-id="d9df7-172">Hello base64 représentation tooconvert tooa objet JSON.</span><span class="sxs-lookup"><span data-stu-id="d9df7-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-173">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-173">Return value</span></span>

<span data-ttu-id="d9df7-174">Un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="d9df7-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-175">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-175">Examples</span></span>

<span data-ttu-id="d9df7-176">Hello exemple suivant utilise hello base64ToJson fonction tooconvert une valeur base64 :</span><span class="sxs-lookup"><span data-stu-id="d9df7-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="d9df7-177">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-178">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-178">Name</span></span> | <span data-ttu-id="d9df7-179">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-179">Type</span></span> | <span data-ttu-id="d9df7-180">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="d9df7-181">base64Output</span></span> | <span data-ttu-id="d9df7-182">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-182">String</span></span> | <span data-ttu-id="d9df7-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d9df7-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d9df7-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-184">toStringOutput</span></span> | <span data-ttu-id="d9df7-185">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-185">String</span></span> | <span data-ttu-id="d9df7-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d9df7-186">one, two, three</span></span> |
| <span data-ttu-id="d9df7-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-187">toJsonOutput</span></span> | <span data-ttu-id="d9df7-188">Object</span><span class="sxs-lookup"><span data-stu-id="d9df7-188">Object</span></span> | <span data-ttu-id="d9df7-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d9df7-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="d9df7-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="d9df7-191">Convertit une chaîne de tooa de représentation en base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-192">Parameters</span></span>

| <span data-ttu-id="d9df7-193">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-193">Parameter</span></span> | <span data-ttu-id="d9df7-194">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-194">Required</span></span> | <span data-ttu-id="d9df7-195">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-195">Type</span></span> | <span data-ttu-id="d9df7-196">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="d9df7-197">base64Value</span></span> |<span data-ttu-id="d9df7-198">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-198">Yes</span></span> |<span data-ttu-id="d9df7-199">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-199">string</span></span> |<span data-ttu-id="d9df7-200">Hello représentation tooconvert tooa la chaîne en base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-201">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-201">Return value</span></span>

<span data-ttu-id="d9df7-202">Une chaîne de hello convertie valeur base64.</span><span class="sxs-lookup"><span data-stu-id="d9df7-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-203">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-203">Examples</span></span>

<span data-ttu-id="d9df7-204">Hello exemple suivant utilise hello base64ToString fonction tooconvert une valeur base64 :</span><span class="sxs-lookup"><span data-stu-id="d9df7-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="d9df7-205">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-206">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-206">Name</span></span> | <span data-ttu-id="d9df7-207">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-207">Type</span></span> | <span data-ttu-id="d9df7-208">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="d9df7-209">base64Output</span></span> | <span data-ttu-id="d9df7-210">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-210">String</span></span> | <span data-ttu-id="d9df7-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d9df7-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d9df7-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-212">toStringOutput</span></span> | <span data-ttu-id="d9df7-213">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-213">String</span></span> | <span data-ttu-id="d9df7-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d9df7-214">one, two, three</span></span> |
| <span data-ttu-id="d9df7-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-215">toJsonOutput</span></span> | <span data-ttu-id="d9df7-216">Object</span><span class="sxs-lookup"><span data-stu-id="d9df7-216">Object</span></span> | <span data-ttu-id="d9df7-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d9df7-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="d9df7-218">concat</span><span class="sxs-lookup"><span data-stu-id="d9df7-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="d9df7-219">Combine plusieurs valeurs de chaîne et retourne la chaîne hello concaténée ou combine plusieurs tableaux et retourne hello concaténée tableau.</span><span class="sxs-lookup"><span data-stu-id="d9df7-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-220">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-220">Parameters</span></span>

| <span data-ttu-id="d9df7-221">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-221">Parameter</span></span> | <span data-ttu-id="d9df7-222">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-222">Required</span></span> | <span data-ttu-id="d9df7-223">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-223">Type</span></span> | <span data-ttu-id="d9df7-224">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-225">arg1</span><span class="sxs-lookup"><span data-stu-id="d9df7-225">arg1</span></span> |<span data-ttu-id="d9df7-226">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-226">Yes</span></span> |<span data-ttu-id="d9df7-227">chaîne ou tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-227">string or array</span></span> |<span data-ttu-id="d9df7-228">valeur de la première Hello pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="d9df7-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="d9df7-229">arguments supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d9df7-229">additional arguments</span></span> |<span data-ttu-id="d9df7-230">Non</span><span class="sxs-lookup"><span data-stu-id="d9df7-230">No</span></span> |<span data-ttu-id="d9df7-231">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-231">string</span></span> |<span data-ttu-id="d9df7-232">Valeurs supplémentaires en ordre séquentiel pour la concaténation.</span><span class="sxs-lookup"><span data-stu-id="d9df7-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-233">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-233">Return value</span></span>
<span data-ttu-id="d9df7-234">Chaîne ou tableau de valeurs concaténées.</span><span class="sxs-lookup"><span data-stu-id="d9df7-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-235">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-235">Examples</span></span>

<span data-ttu-id="d9df7-236">Bonjour à l’exemple suivant montre comment toocombine deux valeurs de chaîne et retourne une chaîne concaténée.</span><span class="sxs-lookup"><span data-stu-id="d9df7-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="d9df7-237">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-238">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-238">Name</span></span> | <span data-ttu-id="d9df7-239">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-239">Type</span></span> | <span data-ttu-id="d9df7-240">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-241">concatOutput</span></span> | <span data-ttu-id="d9df7-242">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-242">String</span></span> | <span data-ttu-id="d9df7-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="d9df7-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="d9df7-244">Bonjour à l’exemple suivant montre comment toocombine deux tableaux.</span><span class="sxs-lookup"><span data-stu-id="d9df7-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="d9df7-245">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-246">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-246">Name</span></span> | <span data-ttu-id="d9df7-247">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-247">Type</span></span> | <span data-ttu-id="d9df7-248">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-249">return</span><span class="sxs-lookup"><span data-stu-id="d9df7-249">return</span></span> | <span data-ttu-id="d9df7-250">Tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-250">Array</span></span> | <span data-ttu-id="d9df7-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="d9df7-252">contains</span><span class="sxs-lookup"><span data-stu-id="d9df7-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="d9df7-253">Vérifie si un tableau contient une valeur, un objet contient une clé ou une chaîne contient une sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-254">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-254">Parameters</span></span>

| <span data-ttu-id="d9df7-255">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-255">Parameter</span></span> | <span data-ttu-id="d9df7-256">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-256">Required</span></span> | <span data-ttu-id="d9df7-257">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-257">Type</span></span> | <span data-ttu-id="d9df7-258">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-259">conteneur</span><span class="sxs-lookup"><span data-stu-id="d9df7-259">container</span></span> |<span data-ttu-id="d9df7-260">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-260">Yes</span></span> |<span data-ttu-id="d9df7-261">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-261">array, object, or string</span></span> |<span data-ttu-id="d9df7-262">valeur Hello contenant hello valeur toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="d9df7-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="d9df7-263">itemToFind</span></span> |<span data-ttu-id="d9df7-264">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-264">Yes</span></span> |<span data-ttu-id="d9df7-265">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="d9df7-265">string or int</span></span> |<span data-ttu-id="d9df7-266">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-267">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-267">Return value</span></span>

<span data-ttu-id="d9df7-268">**True** si l’élément de hello est trouvé ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="d9df7-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-269">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-269">Examples</span></span>

<span data-ttu-id="d9df7-270">Hello suivant montre comment toouse contient différents types :</span><span class="sxs-lookup"><span data-stu-id="d9df7-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="d9df7-271">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-272">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-272">Name</span></span> | <span data-ttu-id="d9df7-273">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-273">Type</span></span> | <span data-ttu-id="d9df7-274">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-275">stringTrue</span></span> | <span data-ttu-id="d9df7-276">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-276">Bool</span></span> | <span data-ttu-id="d9df7-277">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-277">True</span></span> |
| <span data-ttu-id="d9df7-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-278">stringFalse</span></span> | <span data-ttu-id="d9df7-279">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-279">Bool</span></span> | <span data-ttu-id="d9df7-280">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-280">False</span></span> |
| <span data-ttu-id="d9df7-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-281">objectTrue</span></span> | <span data-ttu-id="d9df7-282">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-282">Bool</span></span> | <span data-ttu-id="d9df7-283">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-283">True</span></span> |
| <span data-ttu-id="d9df7-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-284">objectFalse</span></span> | <span data-ttu-id="d9df7-285">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-285">Bool</span></span> | <span data-ttu-id="d9df7-286">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-286">False</span></span> |
| <span data-ttu-id="d9df7-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-287">arrayTrue</span></span> | <span data-ttu-id="d9df7-288">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-288">Bool</span></span> | <span data-ttu-id="d9df7-289">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-289">True</span></span> |
| <span data-ttu-id="d9df7-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-290">arrayFalse</span></span> | <span data-ttu-id="d9df7-291">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-291">Bool</span></span> | <span data-ttu-id="d9df7-292">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="d9df7-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="d9df7-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="d9df7-294">Convertit des données tooa valeur URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-295">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-295">Parameters</span></span>

| <span data-ttu-id="d9df7-296">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-296">Parameter</span></span> | <span data-ttu-id="d9df7-297">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-297">Required</span></span> | <span data-ttu-id="d9df7-298">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-298">Type</span></span> | <span data-ttu-id="d9df7-299">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="d9df7-300">stringToConvert</span></span> |<span data-ttu-id="d9df7-301">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-301">Yes</span></span> |<span data-ttu-id="d9df7-302">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-302">string</span></span> |<span data-ttu-id="d9df7-303">valeur tooconvert tooa les données de salutation URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-304">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-304">Return value</span></span>

<span data-ttu-id="d9df7-305">Une chaîne formatée en tant qu’URI de données.</span><span class="sxs-lookup"><span data-stu-id="d9df7-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-306">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-306">Examples</span></span>

<span data-ttu-id="d9df7-307">Bonjour, l’exemple suivant convertit des données tooa valeur URI et convertit une chaîne d’URI tooa de données :</span><span class="sxs-lookup"><span data-stu-id="d9df7-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="d9df7-308">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-309">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-309">Name</span></span> | <span data-ttu-id="d9df7-310">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-310">Type</span></span> | <span data-ttu-id="d9df7-311">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-312">dataUriOutput</span></span> | <span data-ttu-id="d9df7-313">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-313">String</span></span> | <span data-ttu-id="d9df7-314">data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="d9df7-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="d9df7-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-315">toStringOutput</span></span> | <span data-ttu-id="d9df7-316">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-316">String</span></span> | <span data-ttu-id="d9df7-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="d9df7-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="d9df7-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="d9df7-319">Convertit un URI de données mise en forme de chaîne de valeur tooa.</span><span class="sxs-lookup"><span data-stu-id="d9df7-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-320">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-320">Parameters</span></span>

| <span data-ttu-id="d9df7-321">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-321">Parameter</span></span> | <span data-ttu-id="d9df7-322">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-322">Required</span></span> | <span data-ttu-id="d9df7-323">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-323">Type</span></span> | <span data-ttu-id="d9df7-324">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="d9df7-325">dataUriToConvert</span></span> |<span data-ttu-id="d9df7-326">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-326">Yes</span></span> |<span data-ttu-id="d9df7-327">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-327">string</span></span> |<span data-ttu-id="d9df7-328">données de salutation tooconvert de valeur d’URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-329">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-329">Return value</span></span>

<span data-ttu-id="d9df7-330">Chaîne contenant le hello de valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="d9df7-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-331">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-331">Examples</span></span>

<span data-ttu-id="d9df7-332">Bonjour, l’exemple suivant convertit des données tooa valeur URI et convertit une chaîne d’URI tooa de données :</span><span class="sxs-lookup"><span data-stu-id="d9df7-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="d9df7-333">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-334">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-334">Name</span></span> | <span data-ttu-id="d9df7-335">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-335">Type</span></span> | <span data-ttu-id="d9df7-336">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-337">dataUriOutput</span></span> | <span data-ttu-id="d9df7-338">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-338">String</span></span> | <span data-ttu-id="d9df7-339">data: texte/brut;jeu de caractèresdata:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="d9df7-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="d9df7-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-340">toStringOutput</span></span> | <span data-ttu-id="d9df7-341">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-341">String</span></span> | <span data-ttu-id="d9df7-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="d9df7-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="d9df7-343">empty</span><span class="sxs-lookup"><span data-stu-id="d9df7-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="d9df7-344">Détermine si un tableau, un objet ou une chaîne est vide.</span><span class="sxs-lookup"><span data-stu-id="d9df7-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-345">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-345">Parameters</span></span>

| <span data-ttu-id="d9df7-346">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-346">Parameter</span></span> | <span data-ttu-id="d9df7-347">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-347">Required</span></span> | <span data-ttu-id="d9df7-348">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-348">Type</span></span> | <span data-ttu-id="d9df7-349">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="d9df7-350">itemToTest</span></span> |<span data-ttu-id="d9df7-351">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-351">Yes</span></span> |<span data-ttu-id="d9df7-352">tableau, objet ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-352">array, object, or string</span></span> |<span data-ttu-id="d9df7-353">Bonjour toocheck de valeur s’il est vide.</span><span class="sxs-lookup"><span data-stu-id="d9df7-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-354">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-354">Return value</span></span>

<span data-ttu-id="d9df7-355">Retourne **True** si la valeur de hello est vide ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="d9df7-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-356">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-356">Examples</span></span>

<span data-ttu-id="d9df7-357">Bonjour à l’exemple suivant vérifie si un tableau, un objet et une chaîne sont vides.</span><span class="sxs-lookup"><span data-stu-id="d9df7-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="d9df7-358">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-359">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-359">Name</span></span> | <span data-ttu-id="d9df7-360">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-360">Type</span></span> | <span data-ttu-id="d9df7-361">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="d9df7-362">arrayEmpty</span></span> | <span data-ttu-id="d9df7-363">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-363">Bool</span></span> | <span data-ttu-id="d9df7-364">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-364">True</span></span> |
| <span data-ttu-id="d9df7-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="d9df7-365">objectEmpty</span></span> | <span data-ttu-id="d9df7-366">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-366">Bool</span></span> | <span data-ttu-id="d9df7-367">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-367">True</span></span> |
| <span data-ttu-id="d9df7-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="d9df7-368">stringEmpty</span></span> | <span data-ttu-id="d9df7-369">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-369">Bool</span></span> | <span data-ttu-id="d9df7-370">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="d9df7-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="d9df7-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="d9df7-372">Détermine si une chaîne se termine par une valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="d9df7-373">comparaison de Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="d9df7-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-374">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-374">Parameters</span></span>

| <span data-ttu-id="d9df7-375">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-375">Parameter</span></span> | <span data-ttu-id="d9df7-376">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-376">Required</span></span> | <span data-ttu-id="d9df7-377">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-377">Type</span></span> | <span data-ttu-id="d9df7-378">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d9df7-379">stringToSearch</span></span> |<span data-ttu-id="d9df7-380">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-380">Yes</span></span> |<span data-ttu-id="d9df7-381">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-381">string</span></span> |<span data-ttu-id="d9df7-382">valeur Hello contenant hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d9df7-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d9df7-383">stringToFind</span></span> |<span data-ttu-id="d9df7-384">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-384">Yes</span></span> |<span data-ttu-id="d9df7-385">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-385">string</span></span> |<span data-ttu-id="d9df7-386">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-387">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-387">Return value</span></span>

<span data-ttu-id="d9df7-388">**True** si hello dernière ou les caractères de chaîne de hello correspond à hello ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="d9df7-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-389">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-389">Examples</span></span>

<span data-ttu-id="d9df7-390">Bonjour à l’exemple suivant montre comment toouse hello startsWith et endsWith fonctions :</span><span class="sxs-lookup"><span data-stu-id="d9df7-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="d9df7-391">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-392">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-392">Name</span></span> | <span data-ttu-id="d9df7-393">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-393">Type</span></span> | <span data-ttu-id="d9df7-394">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-395">startsTrue</span></span> | <span data-ttu-id="d9df7-396">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-396">Bool</span></span> | <span data-ttu-id="d9df7-397">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-397">True</span></span> |
| <span data-ttu-id="d9df7-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-398">startsCapTrue</span></span> | <span data-ttu-id="d9df7-399">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-399">Bool</span></span> | <span data-ttu-id="d9df7-400">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-400">True</span></span> |
| <span data-ttu-id="d9df7-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-401">startsFalse</span></span> | <span data-ttu-id="d9df7-402">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-402">Bool</span></span> | <span data-ttu-id="d9df7-403">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-403">False</span></span> |
| <span data-ttu-id="d9df7-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-404">endsTrue</span></span> | <span data-ttu-id="d9df7-405">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-405">Bool</span></span> | <span data-ttu-id="d9df7-406">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-406">True</span></span> |
| <span data-ttu-id="d9df7-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-407">endsCapTrue</span></span> | <span data-ttu-id="d9df7-408">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-408">Bool</span></span> | <span data-ttu-id="d9df7-409">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-409">True</span></span> |
| <span data-ttu-id="d9df7-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-410">endsFalse</span></span> | <span data-ttu-id="d9df7-411">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-411">Bool</span></span> | <span data-ttu-id="d9df7-412">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="d9df7-413">first</span><span class="sxs-lookup"><span data-stu-id="d9df7-413">first</span></span>
`first(arg1)`

<span data-ttu-id="d9df7-414">Retourne hello le premier caractère de la chaîne de hello ou le premier élément du tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-415">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-415">Parameters</span></span>

| <span data-ttu-id="d9df7-416">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-416">Parameter</span></span> | <span data-ttu-id="d9df7-417">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-417">Required</span></span> | <span data-ttu-id="d9df7-418">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-418">Type</span></span> | <span data-ttu-id="d9df7-419">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-420">arg1</span><span class="sxs-lookup"><span data-stu-id="d9df7-420">arg1</span></span> |<span data-ttu-id="d9df7-421">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-421">Yes</span></span> |<span data-ttu-id="d9df7-422">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-422">array or string</span></span> |<span data-ttu-id="d9df7-423">premier élément Hello valeur tooretrieve hello ou caractère.</span><span class="sxs-lookup"><span data-stu-id="d9df7-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-424">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-424">Return value</span></span>

<span data-ttu-id="d9df7-425">Chaîne hello premier caractère, ou type hello (string, int, tableau ou objet) de hello premier élément dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="d9df7-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-426">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-426">Examples</span></span>

<span data-ttu-id="d9df7-427">Hello suivant montre comment toouse hello première fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="d9df7-428">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-429">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-429">Name</span></span> | <span data-ttu-id="d9df7-430">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-430">Type</span></span> | <span data-ttu-id="d9df7-431">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-432">arrayOutput</span></span> | <span data-ttu-id="d9df7-433">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-433">String</span></span> | <span data-ttu-id="d9df7-434">one</span><span class="sxs-lookup"><span data-stu-id="d9df7-434">one</span></span> |
| <span data-ttu-id="d9df7-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-435">stringOutput</span></span> | <span data-ttu-id="d9df7-436">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-436">String</span></span> | <span data-ttu-id="d9df7-437">O</span><span class="sxs-lookup"><span data-stu-id="d9df7-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="d9df7-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="d9df7-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="d9df7-439">Retourne hello première position d’une valeur dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="d9df7-440">comparaison de Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="d9df7-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-441">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-441">Parameters</span></span>

| <span data-ttu-id="d9df7-442">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-442">Parameter</span></span> | <span data-ttu-id="d9df7-443">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-443">Required</span></span> | <span data-ttu-id="d9df7-444">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-444">Type</span></span> | <span data-ttu-id="d9df7-445">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d9df7-446">stringToSearch</span></span> |<span data-ttu-id="d9df7-447">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-447">Yes</span></span> |<span data-ttu-id="d9df7-448">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-448">string</span></span> |<span data-ttu-id="d9df7-449">valeur Hello contenant hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d9df7-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d9df7-450">stringToFind</span></span> |<span data-ttu-id="d9df7-451">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-451">Yes</span></span> |<span data-ttu-id="d9df7-452">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-452">string</span></span> |<span data-ttu-id="d9df7-453">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-454">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-454">Return value</span></span>

<span data-ttu-id="d9df7-455">Entier qui représente la position de hello de hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="d9df7-456">valeur de Hello est de base zéro.</span><span class="sxs-lookup"><span data-stu-id="d9df7-456">hello value is zero-based.</span></span> <span data-ttu-id="d9df7-457">Si l’élément de hello n’est pas trouvé, -1 est retourné.</span><span class="sxs-lookup"><span data-stu-id="d9df7-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-458">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-458">Examples</span></span>

<span data-ttu-id="d9df7-459">Bonjour à l’exemple suivant montre comment toouse hello indexOf et lastIndexOf fonctions :</span><span class="sxs-lookup"><span data-stu-id="d9df7-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="d9df7-460">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-461">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-461">Name</span></span> | <span data-ttu-id="d9df7-462">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-462">Type</span></span> | <span data-ttu-id="d9df7-463">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-464">firstT</span><span class="sxs-lookup"><span data-stu-id="d9df7-464">firstT</span></span> | <span data-ttu-id="d9df7-465">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-465">Int</span></span> | <span data-ttu-id="d9df7-466">0</span><span class="sxs-lookup"><span data-stu-id="d9df7-466">0</span></span> |
| <span data-ttu-id="d9df7-467">lastT</span><span class="sxs-lookup"><span data-stu-id="d9df7-467">lastT</span></span> | <span data-ttu-id="d9df7-468">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-468">Int</span></span> | <span data-ttu-id="d9df7-469">3</span><span class="sxs-lookup"><span data-stu-id="d9df7-469">3</span></span> |
| <span data-ttu-id="d9df7-470">firstString</span><span class="sxs-lookup"><span data-stu-id="d9df7-470">firstString</span></span> | <span data-ttu-id="d9df7-471">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-471">Int</span></span> | <span data-ttu-id="d9df7-472">2</span><span class="sxs-lookup"><span data-stu-id="d9df7-472">2</span></span> |
| <span data-ttu-id="d9df7-473">lastString</span><span class="sxs-lookup"><span data-stu-id="d9df7-473">lastString</span></span> | <span data-ttu-id="d9df7-474">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-474">Int</span></span> | <span data-ttu-id="d9df7-475">0</span><span class="sxs-lookup"><span data-stu-id="d9df7-475">0</span></span> |
| <span data-ttu-id="d9df7-476">notFound</span><span class="sxs-lookup"><span data-stu-id="d9df7-476">notFound</span></span> | <span data-ttu-id="d9df7-477">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-477">Int</span></span> | <span data-ttu-id="d9df7-478">-1</span><span class="sxs-lookup"><span data-stu-id="d9df7-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="d9df7-479">last</span><span class="sxs-lookup"><span data-stu-id="d9df7-479">last</span></span>
`last (arg1)`

<span data-ttu-id="d9df7-480">Retourne la dernière caractère de chaîne de hello ou hello dernier élément du tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-481">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-481">Parameters</span></span>

| <span data-ttu-id="d9df7-482">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-482">Parameter</span></span> | <span data-ttu-id="d9df7-483">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-483">Required</span></span> | <span data-ttu-id="d9df7-484">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-484">Type</span></span> | <span data-ttu-id="d9df7-485">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-486">arg1</span><span class="sxs-lookup"><span data-stu-id="d9df7-486">arg1</span></span> |<span data-ttu-id="d9df7-487">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-487">Yes</span></span> |<span data-ttu-id="d9df7-488">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-488">array or string</span></span> |<span data-ttu-id="d9df7-489">dernier élément Hello valeur tooretrieve hello ou caractère.</span><span class="sxs-lookup"><span data-stu-id="d9df7-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-490">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-490">Return value</span></span>

<span data-ttu-id="d9df7-491">Une chaîne de caractères de dernière hello, ou type hello (string, int, tableau ou objet) de hello dernier élément d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="d9df7-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-492">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-492">Examples</span></span>

<span data-ttu-id="d9df7-493">Hello suivant montre comment toouse hello dernière fonction avec un tableau et une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="d9df7-494">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-495">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-495">Name</span></span> | <span data-ttu-id="d9df7-496">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-496">Type</span></span> | <span data-ttu-id="d9df7-497">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-498">arrayOutput</span></span> | <span data-ttu-id="d9df7-499">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-499">String</span></span> | <span data-ttu-id="d9df7-500">three</span><span class="sxs-lookup"><span data-stu-id="d9df7-500">three</span></span> |
| <span data-ttu-id="d9df7-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-501">stringOutput</span></span> | <span data-ttu-id="d9df7-502">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-502">String</span></span> | <span data-ttu-id="d9df7-503">e</span><span class="sxs-lookup"><span data-stu-id="d9df7-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="d9df7-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="d9df7-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="d9df7-505">Retourne hello dernière position d’une valeur dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="d9df7-506">comparaison de Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="d9df7-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-507">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-507">Parameters</span></span>

| <span data-ttu-id="d9df7-508">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-508">Parameter</span></span> | <span data-ttu-id="d9df7-509">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-509">Required</span></span> | <span data-ttu-id="d9df7-510">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-510">Type</span></span> | <span data-ttu-id="d9df7-511">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d9df7-512">stringToSearch</span></span> |<span data-ttu-id="d9df7-513">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-513">Yes</span></span> |<span data-ttu-id="d9df7-514">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-514">string</span></span> |<span data-ttu-id="d9df7-515">valeur Hello contenant hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d9df7-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d9df7-516">stringToFind</span></span> |<span data-ttu-id="d9df7-517">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-517">Yes</span></span> |<span data-ttu-id="d9df7-518">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-518">string</span></span> |<span data-ttu-id="d9df7-519">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-520">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-520">Return value</span></span>

<span data-ttu-id="d9df7-521">Entier qui représente la dernière position de hello de hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="d9df7-522">valeur de Hello est de base zéro.</span><span class="sxs-lookup"><span data-stu-id="d9df7-522">hello value is zero-based.</span></span> <span data-ttu-id="d9df7-523">Si l’élément de hello n’est pas trouvé, -1 est retourné.</span><span class="sxs-lookup"><span data-stu-id="d9df7-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-524">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-524">Examples</span></span>

<span data-ttu-id="d9df7-525">Bonjour à l’exemple suivant montre comment toouse hello indexOf et lastIndexOf fonctions :</span><span class="sxs-lookup"><span data-stu-id="d9df7-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="d9df7-526">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-527">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-527">Name</span></span> | <span data-ttu-id="d9df7-528">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-528">Type</span></span> | <span data-ttu-id="d9df7-529">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-530">firstT</span><span class="sxs-lookup"><span data-stu-id="d9df7-530">firstT</span></span> | <span data-ttu-id="d9df7-531">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-531">Int</span></span> | <span data-ttu-id="d9df7-532">0</span><span class="sxs-lookup"><span data-stu-id="d9df7-532">0</span></span> |
| <span data-ttu-id="d9df7-533">lastT</span><span class="sxs-lookup"><span data-stu-id="d9df7-533">lastT</span></span> | <span data-ttu-id="d9df7-534">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-534">Int</span></span> | <span data-ttu-id="d9df7-535">3</span><span class="sxs-lookup"><span data-stu-id="d9df7-535">3</span></span> |
| <span data-ttu-id="d9df7-536">firstString</span><span class="sxs-lookup"><span data-stu-id="d9df7-536">firstString</span></span> | <span data-ttu-id="d9df7-537">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-537">Int</span></span> | <span data-ttu-id="d9df7-538">2</span><span class="sxs-lookup"><span data-stu-id="d9df7-538">2</span></span> |
| <span data-ttu-id="d9df7-539">lastString</span><span class="sxs-lookup"><span data-stu-id="d9df7-539">lastString</span></span> | <span data-ttu-id="d9df7-540">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-540">Int</span></span> | <span data-ttu-id="d9df7-541">0</span><span class="sxs-lookup"><span data-stu-id="d9df7-541">0</span></span> |
| <span data-ttu-id="d9df7-542">notFound</span><span class="sxs-lookup"><span data-stu-id="d9df7-542">notFound</span></span> | <span data-ttu-id="d9df7-543">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-543">Int</span></span> | <span data-ttu-id="d9df7-544">-1</span><span class="sxs-lookup"><span data-stu-id="d9df7-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="d9df7-545">length</span><span class="sxs-lookup"><span data-stu-id="d9df7-545">length</span></span>
`length(string)`

<span data-ttu-id="d9df7-546">Retourne le nombre hello de caractères dans une chaîne ou les éléments dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="d9df7-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-547">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-547">Parameters</span></span>

| <span data-ttu-id="d9df7-548">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-548">Parameter</span></span> | <span data-ttu-id="d9df7-549">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-549">Required</span></span> | <span data-ttu-id="d9df7-550">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-550">Type</span></span> | <span data-ttu-id="d9df7-551">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-552">arg1</span><span class="sxs-lookup"><span data-stu-id="d9df7-552">arg1</span></span> |<span data-ttu-id="d9df7-553">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-553">Yes</span></span> |<span data-ttu-id="d9df7-554">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-554">array or string</span></span> |<span data-ttu-id="d9df7-555">Hello toouse de tableau pour l’obtention du nombre de hello d’éléments ou hello toouse de chaîne pour l’obtention du nombre de hello de caractères.</span><span class="sxs-lookup"><span data-stu-id="d9df7-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-556">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-556">Return value</span></span>

<span data-ttu-id="d9df7-557">Un entier.</span><span class="sxs-lookup"><span data-stu-id="d9df7-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="d9df7-558">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-558">Examples</span></span>

<span data-ttu-id="d9df7-559">Hello suivant montre l’exemple de la longueur de toouse avec un tableau et une chaîne :</span><span class="sxs-lookup"><span data-stu-id="d9df7-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="d9df7-560">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-561">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-561">Name</span></span> | <span data-ttu-id="d9df7-562">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-562">Type</span></span> | <span data-ttu-id="d9df7-563">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="d9df7-564">arrayLength</span></span> | <span data-ttu-id="d9df7-565">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-565">Int</span></span> | <span data-ttu-id="d9df7-566">3</span><span class="sxs-lookup"><span data-stu-id="d9df7-566">3</span></span> |
| <span data-ttu-id="d9df7-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="d9df7-567">stringLength</span></span> | <span data-ttu-id="d9df7-568">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-568">Int</span></span> | <span data-ttu-id="d9df7-569">13.</span><span class="sxs-lookup"><span data-stu-id="d9df7-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="d9df7-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="d9df7-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="d9df7-571">Retourne une chaîne alignée à droite en ajoutant des caractères toohello gauche jusqu'à atteindre la longueur totale spécifiée hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-572">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-572">Parameters</span></span>

| <span data-ttu-id="d9df7-573">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-573">Parameter</span></span> | <span data-ttu-id="d9df7-574">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-574">Required</span></span> | <span data-ttu-id="d9df7-575">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-575">Type</span></span> | <span data-ttu-id="d9df7-576">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-577">valeur_à_remplir</span><span class="sxs-lookup"><span data-stu-id="d9df7-577">valueToPad</span></span> |<span data-ttu-id="d9df7-578">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-578">Yes</span></span> |<span data-ttu-id="d9df7-579">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="d9df7-579">string or int</span></span> |<span data-ttu-id="d9df7-580">Hello valeur tooright-aligner.</span><span class="sxs-lookup"><span data-stu-id="d9df7-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="d9df7-581">longueur_totale</span><span class="sxs-lookup"><span data-stu-id="d9df7-581">totalLength</span></span> |<span data-ttu-id="d9df7-582">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-582">Yes</span></span> |<span data-ttu-id="d9df7-583">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-583">int</span></span> |<span data-ttu-id="d9df7-584">Nombre total de Hello de caractères Bonjour a renvoyé la chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="d9df7-585">caractère_de_remplissage</span><span class="sxs-lookup"><span data-stu-id="d9df7-585">paddingCharacter</span></span> |<span data-ttu-id="d9df7-586">Non</span><span class="sxs-lookup"><span data-stu-id="d9df7-586">No</span></span> |<span data-ttu-id="d9df7-587">caractère unique</span><span class="sxs-lookup"><span data-stu-id="d9df7-587">single character</span></span> |<span data-ttu-id="d9df7-588">Bonjour toouse caractère de gauche-padding jusqu'à ce que la longueur totale hello est atteint.</span><span class="sxs-lookup"><span data-stu-id="d9df7-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="d9df7-589">valeur par défaut de Hello est un espace.</span><span class="sxs-lookup"><span data-stu-id="d9df7-589">hello default value is a space.</span></span> |

<span data-ttu-id="d9df7-590">Si la chaîne d’origine de hello est plus longue que le nombre de hello de caractères toopad, aucuns caractères ne sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="d9df7-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="d9df7-591">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-591">Return value</span></span>

<span data-ttu-id="d9df7-592">Une chaîne avec hello au moins le nombre de caractères spécifiés.</span><span class="sxs-lookup"><span data-stu-id="d9df7-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-593">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-593">Examples</span></span>

<span data-ttu-id="d9df7-594">Bonjour à l’exemple suivant montre comment toopad hello la valeur du paramètre fourni par l’utilisateur en ajoutant hello zéro caractère jusqu'à ce qu’il atteigne hello le nombre total de caractères.</span><span class="sxs-lookup"><span data-stu-id="d9df7-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="d9df7-595">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-596">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-596">Name</span></span> | <span data-ttu-id="d9df7-597">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-597">Type</span></span> | <span data-ttu-id="d9df7-598">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-599">stringOutput</span></span> | <span data-ttu-id="d9df7-600">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-600">String</span></span> | <span data-ttu-id="d9df7-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="d9df7-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="d9df7-602">replace</span><span class="sxs-lookup"><span data-stu-id="d9df7-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="d9df7-603">Renvoie une nouvelle chaîne dans laquelle toutes les instances d’une chaîne ont été remplacées par une autre.</span><span class="sxs-lookup"><span data-stu-id="d9df7-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-604">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-604">Parameters</span></span>

| <span data-ttu-id="d9df7-605">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-605">Parameter</span></span> | <span data-ttu-id="d9df7-606">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-606">Required</span></span> | <span data-ttu-id="d9df7-607">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-607">Type</span></span> | <span data-ttu-id="d9df7-608">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-609">chaîne_initiale</span><span class="sxs-lookup"><span data-stu-id="d9df7-609">originalString</span></span> |<span data-ttu-id="d9df7-610">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-610">Yes</span></span> |<span data-ttu-id="d9df7-611">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-611">string</span></span> |<span data-ttu-id="d9df7-612">valeur de Hello qui a toutes les instances d’une chaîne remplacée par une autre chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="d9df7-613">oldString</span><span class="sxs-lookup"><span data-stu-id="d9df7-613">oldString</span></span> |<span data-ttu-id="d9df7-614">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-614">Yes</span></span> |<span data-ttu-id="d9df7-615">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-615">string</span></span> |<span data-ttu-id="d9df7-616">Hello chaîne toobe est supprimé de la chaîne d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="d9df7-617">newString</span><span class="sxs-lookup"><span data-stu-id="d9df7-617">newString</span></span> |<span data-ttu-id="d9df7-618">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-618">Yes</span></span> |<span data-ttu-id="d9df7-619">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-619">string</span></span> |<span data-ttu-id="d9df7-620">tooadd de chaîne Hello à la place de hello supprimé la chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-621">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-621">Return value</span></span>

<span data-ttu-id="d9df7-622">Une chaîne avec hello les caractères remplacés.</span><span class="sxs-lookup"><span data-stu-id="d9df7-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-623">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-623">Examples</span></span>

<span data-ttu-id="d9df7-624">Bonjour à l’exemple suivant montre comment tooremove tous les tirets à partir de la chaîne de hello fourni par l’utilisateur, et comment tooreplace partie hello chaîne par une autre chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="d9df7-625">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-626">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-626">Name</span></span> | <span data-ttu-id="d9df7-627">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-627">Type</span></span> | <span data-ttu-id="d9df7-628">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-629">firstOutput</span></span> | <span data-ttu-id="d9df7-630">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-630">String</span></span> | <span data-ttu-id="d9df7-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="d9df7-631">1231231234</span></span> |
| <span data-ttu-id="d9df7-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-632">secodeOutput</span></span> | <span data-ttu-id="d9df7-633">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-633">String</span></span> | <span data-ttu-id="d9df7-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="d9df7-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="d9df7-635">skip</span><span class="sxs-lookup"><span data-stu-id="d9df7-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="d9df7-636">Retourne une chaîne contenant tous les caractères de hello après que hello spécifiée le nombre de caractères ou d’un tableau avec tous les éléments hello après hello nombre d’éléments.</span><span class="sxs-lookup"><span data-stu-id="d9df7-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-637">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-637">Parameters</span></span>

| <span data-ttu-id="d9df7-638">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-638">Parameter</span></span> | <span data-ttu-id="d9df7-639">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-639">Required</span></span> | <span data-ttu-id="d9df7-640">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-640">Type</span></span> | <span data-ttu-id="d9df7-641">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="d9df7-642">originalValue</span></span> |<span data-ttu-id="d9df7-643">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-643">Yes</span></span> |<span data-ttu-id="d9df7-644">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-644">array or string</span></span> |<span data-ttu-id="d9df7-645">Bonjour toouse tableau ou une chaîne pour l’ignorer.</span><span class="sxs-lookup"><span data-stu-id="d9df7-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="d9df7-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="d9df7-646">numberToSkip</span></span> |<span data-ttu-id="d9df7-647">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-647">Yes</span></span> |<span data-ttu-id="d9df7-648">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-648">int</span></span> |<span data-ttu-id="d9df7-649">nombre de Hello d’éléments ou des caractères tooskip.</span><span class="sxs-lookup"><span data-stu-id="d9df7-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="d9df7-650">Si cette valeur est inférieur ou égal à 0, tous les hello éléments ou dans la valeur de hello est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="d9df7-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="d9df7-651">Si elle est supérieure à la longueur du tableau de hello ou chaîne hello, un tableau vide ou une chaîne est retournée.</span><span class="sxs-lookup"><span data-stu-id="d9df7-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-652">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-652">Return value</span></span>

<span data-ttu-id="d9df7-653">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-654">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-654">Examples</span></span>

<span data-ttu-id="d9df7-655">Hello suivant exemple ignore hello le nombre d’éléments spécifié dans le tableau de hello et hello nombre spécifié de caractères dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="d9df7-656">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-657">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-657">Name</span></span> | <span data-ttu-id="d9df7-658">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-658">Type</span></span> | <span data-ttu-id="d9df7-659">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-660">arrayOutput</span></span> | <span data-ttu-id="d9df7-661">Tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-661">Array</span></span> | <span data-ttu-id="d9df7-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-662">["three"]</span></span> |
| <span data-ttu-id="d9df7-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-663">stringOutput</span></span> | <span data-ttu-id="d9df7-664">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-664">String</span></span> | <span data-ttu-id="d9df7-665">two three</span><span class="sxs-lookup"><span data-stu-id="d9df7-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="d9df7-666">split</span><span class="sxs-lookup"><span data-stu-id="d9df7-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="d9df7-667">Retourne un tableau de chaînes qui contient les sous-chaînes hello Hello d’entrée de chaîne qui est délimitées par hello spécifié délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="d9df7-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-668">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-668">Parameters</span></span>

| <span data-ttu-id="d9df7-669">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-669">Parameter</span></span> | <span data-ttu-id="d9df7-670">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-670">Required</span></span> | <span data-ttu-id="d9df7-671">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-671">Type</span></span> | <span data-ttu-id="d9df7-672">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-673">chaîne_entrée</span><span class="sxs-lookup"><span data-stu-id="d9df7-673">inputString</span></span> |<span data-ttu-id="d9df7-674">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-674">Yes</span></span> |<span data-ttu-id="d9df7-675">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-675">string</span></span> |<span data-ttu-id="d9df7-676">toosplit de chaîne Hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-676">hello string toosplit.</span></span> |
| <span data-ttu-id="d9df7-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="d9df7-677">delimiter</span></span> |<span data-ttu-id="d9df7-678">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-678">Yes</span></span> |<span data-ttu-id="d9df7-679">chaîne ou tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="d9df7-679">string or array of strings</span></span> |<span data-ttu-id="d9df7-680">Bonjour toouse délimiteur pour fractionner la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-681">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-681">Return value</span></span>

<span data-ttu-id="d9df7-682">Tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="d9df7-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-683">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-683">Examples</span></span>

<span data-ttu-id="d9df7-684">Hello exemple suivant fractionne hello la chaîne d’entrée avec une virgule et avec une virgule ou un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="d9df7-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="d9df7-685">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-686">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-686">Name</span></span> | <span data-ttu-id="d9df7-687">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-687">Type</span></span> | <span data-ttu-id="d9df7-688">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-689">firstOutput</span></span> | <span data-ttu-id="d9df7-690">Tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-690">Array</span></span> | <span data-ttu-id="d9df7-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="d9df7-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-692">secondOutput</span></span> | <span data-ttu-id="d9df7-693">Tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-693">Array</span></span> | <span data-ttu-id="d9df7-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="d9df7-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="d9df7-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="d9df7-696">Détermine si une chaîne commence par une valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="d9df7-697">comparaison de Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="d9df7-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-698">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-698">Parameters</span></span>

| <span data-ttu-id="d9df7-699">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-699">Parameter</span></span> | <span data-ttu-id="d9df7-700">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-700">Required</span></span> | <span data-ttu-id="d9df7-701">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-701">Type</span></span> | <span data-ttu-id="d9df7-702">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d9df7-703">stringToSearch</span></span> |<span data-ttu-id="d9df7-704">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-704">Yes</span></span> |<span data-ttu-id="d9df7-705">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-705">string</span></span> |<span data-ttu-id="d9df7-706">valeur Hello contenant hello élément toofind.</span><span class="sxs-lookup"><span data-stu-id="d9df7-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d9df7-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d9df7-707">stringToFind</span></span> |<span data-ttu-id="d9df7-708">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-708">Yes</span></span> |<span data-ttu-id="d9df7-709">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-709">string</span></span> |<span data-ttu-id="d9df7-710">Hello toofind de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-711">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-711">Return value</span></span>

<span data-ttu-id="d9df7-712">**True** si hello premier caractère ou les caractères de chaîne de hello correspond à hello ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="d9df7-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-713">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-713">Examples</span></span>

<span data-ttu-id="d9df7-714">Bonjour à l’exemple suivant montre comment toouse hello startsWith et endsWith fonctions :</span><span class="sxs-lookup"><span data-stu-id="d9df7-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="d9df7-715">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-716">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-716">Name</span></span> | <span data-ttu-id="d9df7-717">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-717">Type</span></span> | <span data-ttu-id="d9df7-718">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-719">startsTrue</span></span> | <span data-ttu-id="d9df7-720">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-720">Bool</span></span> | <span data-ttu-id="d9df7-721">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-721">True</span></span> |
| <span data-ttu-id="d9df7-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-722">startsCapTrue</span></span> | <span data-ttu-id="d9df7-723">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-723">Bool</span></span> | <span data-ttu-id="d9df7-724">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-724">True</span></span> |
| <span data-ttu-id="d9df7-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-725">startsFalse</span></span> | <span data-ttu-id="d9df7-726">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-726">Bool</span></span> | <span data-ttu-id="d9df7-727">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-727">False</span></span> |
| <span data-ttu-id="d9df7-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-728">endsTrue</span></span> | <span data-ttu-id="d9df7-729">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-729">Bool</span></span> | <span data-ttu-id="d9df7-730">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-730">True</span></span> |
| <span data-ttu-id="d9df7-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d9df7-731">endsCapTrue</span></span> | <span data-ttu-id="d9df7-732">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-732">Bool</span></span> | <span data-ttu-id="d9df7-733">true</span><span class="sxs-lookup"><span data-stu-id="d9df7-733">True</span></span> |
| <span data-ttu-id="d9df7-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="d9df7-734">endsFalse</span></span> | <span data-ttu-id="d9df7-735">Bool</span><span class="sxs-lookup"><span data-stu-id="d9df7-735">Bool</span></span> | <span data-ttu-id="d9df7-736">False</span><span class="sxs-lookup"><span data-stu-id="d9df7-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="d9df7-737">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="d9df7-738">Convertit hello spécifié chaîne tooa de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-739">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-739">Parameters</span></span>

| <span data-ttu-id="d9df7-740">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-740">Parameter</span></span> | <span data-ttu-id="d9df7-741">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-741">Required</span></span> | <span data-ttu-id="d9df7-742">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-742">Type</span></span> | <span data-ttu-id="d9df7-743">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="d9df7-744">valueToConvert</span></span> |<span data-ttu-id="d9df7-745">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-745">Yes</span></span> | <span data-ttu-id="d9df7-746">Quelconque</span><span class="sxs-lookup"><span data-stu-id="d9df7-746">Any</span></span> |<span data-ttu-id="d9df7-747">Hello valeur tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="d9df7-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="d9df7-748">N’importe quel type de valeur peut être converti, y compris les objets et des tableaux.</span><span class="sxs-lookup"><span data-stu-id="d9df7-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-749">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-749">Return value</span></span>

<span data-ttu-id="d9df7-750">Une chaîne de valeur de hello converti.</span><span class="sxs-lookup"><span data-stu-id="d9df7-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-751">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-751">Examples</span></span>

<span data-ttu-id="d9df7-752">Bonjour à l’exemple suivant montre comment tooconvert différents types de valeurs toostrings :</span><span class="sxs-lookup"><span data-stu-id="d9df7-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="d9df7-753">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-754">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-754">Name</span></span> | <span data-ttu-id="d9df7-755">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-755">Type</span></span> | <span data-ttu-id="d9df7-756">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-757">objectOutput</span></span> | <span data-ttu-id="d9df7-758">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-758">String</span></span> | <span data-ttu-id="d9df7-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="d9df7-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="d9df7-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-760">arrayOutput</span></span> | <span data-ttu-id="d9df7-761">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-761">String</span></span> | <span data-ttu-id="d9df7-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-762">["a","b","c"]</span></span> |
| <span data-ttu-id="d9df7-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-763">intOutput</span></span> | <span data-ttu-id="d9df7-764">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-764">String</span></span> | <span data-ttu-id="d9df7-765">5</span><span class="sxs-lookup"><span data-stu-id="d9df7-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="d9df7-766">substring</span><span class="sxs-lookup"><span data-stu-id="d9df7-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="d9df7-767">Retourne une sous-chaîne qui commence à hello spécifié position de caractère que contient hello nombre spécifié de caractères.</span><span class="sxs-lookup"><span data-stu-id="d9df7-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-768">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-768">Parameters</span></span>

| <span data-ttu-id="d9df7-769">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-769">Parameter</span></span> | <span data-ttu-id="d9df7-770">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-770">Required</span></span> | <span data-ttu-id="d9df7-771">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-771">Type</span></span> | <span data-ttu-id="d9df7-772">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-773">chaîne_à_analyser</span><span class="sxs-lookup"><span data-stu-id="d9df7-773">stringToParse</span></span> |<span data-ttu-id="d9df7-774">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-774">Yes</span></span> |<span data-ttu-id="d9df7-775">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-775">string</span></span> |<span data-ttu-id="d9df7-776">chaîne d’origine de Hello de quels hello sous-chaîne est extraite.</span><span class="sxs-lookup"><span data-stu-id="d9df7-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="d9df7-777">index_début</span><span class="sxs-lookup"><span data-stu-id="d9df7-777">startIndex</span></span> |<span data-ttu-id="d9df7-778">Non</span><span class="sxs-lookup"><span data-stu-id="d9df7-778">No</span></span> |<span data-ttu-id="d9df7-779">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-779">int</span></span> |<span data-ttu-id="d9df7-780">Hello base zéro caractère position de départ de la sous-chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="d9df7-781">length</span><span class="sxs-lookup"><span data-stu-id="d9df7-781">length</span></span> |<span data-ttu-id="d9df7-782">Non</span><span class="sxs-lookup"><span data-stu-id="d9df7-782">No</span></span> |<span data-ttu-id="d9df7-783">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-783">int</span></span> |<span data-ttu-id="d9df7-784">nombre de Hello de caractères pour la sous-chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="d9df7-785">Doit faire référence emplacement tooa au sein de la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-786">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-786">Return value</span></span>

<span data-ttu-id="d9df7-787">sous-chaîne de Hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="d9df7-788">Remarques</span><span class="sxs-lookup"><span data-stu-id="d9df7-788">Remarks</span></span>

<span data-ttu-id="d9df7-789">fonction Hello échoue lors de la sous-chaîne de hello s’étend au-delà de fin hello de chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="d9df7-790">Bonjour à l’exemple suivant échoue avec hello erreur « paramètres d’index et la longueur hello doivent faire référence emplacement tooa au sein de la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="d9df7-791">Hello paramètre index : '0', hello paramètre de longueur : 11, hello longueur hello du paramètre de chaîne : « 10 ». ».</span><span class="sxs-lookup"><span data-stu-id="d9df7-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="d9df7-792">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-792">Examples</span></span>

<span data-ttu-id="d9df7-793">Bonjour à l’exemple suivant extrait une sous-chaîne à partir d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="d9df7-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="d9df7-794">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-795">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-795">Name</span></span> | <span data-ttu-id="d9df7-796">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-796">Type</span></span> | <span data-ttu-id="d9df7-797">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-798">substringOutput</span></span> | <span data-ttu-id="d9df7-799">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-799">String</span></span> | <span data-ttu-id="d9df7-800">two</span><span class="sxs-lookup"><span data-stu-id="d9df7-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="d9df7-801">take</span><span class="sxs-lookup"><span data-stu-id="d9df7-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="d9df7-802">Retourne une chaîne avec hello nombre spécifié de caractères à partir du début hello de hello chaîne ou un tableau avec hello spécifié le nombre d’éléments à partir du début hello du tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-803">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-803">Parameters</span></span>

| <span data-ttu-id="d9df7-804">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-804">Parameter</span></span> | <span data-ttu-id="d9df7-805">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-805">Required</span></span> | <span data-ttu-id="d9df7-806">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-806">Type</span></span> | <span data-ttu-id="d9df7-807">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="d9df7-808">originalValue</span></span> |<span data-ttu-id="d9df7-809">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-809">Yes</span></span> |<span data-ttu-id="d9df7-810">tableau ou chaîne</span><span class="sxs-lookup"><span data-stu-id="d9df7-810">array or string</span></span> |<span data-ttu-id="d9df7-811">Bonjour les éléments de hello tootake tableau ou une chaîne à partir de.</span><span class="sxs-lookup"><span data-stu-id="d9df7-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="d9df7-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="d9df7-812">numberToTake</span></span> |<span data-ttu-id="d9df7-813">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-813">Yes</span></span> |<span data-ttu-id="d9df7-814">int</span><span class="sxs-lookup"><span data-stu-id="d9df7-814">int</span></span> |<span data-ttu-id="d9df7-815">nombre de Hello d’éléments ou des caractères tootake.</span><span class="sxs-lookup"><span data-stu-id="d9df7-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="d9df7-816">Si cette valeur est inférieure ou égale à 0, une chaîne ou un tableau vide est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="d9df7-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="d9df7-817">Si elle est supérieure à la longueur de hello Hello donné de tableau ou une chaîne, tous les éléments hello hello tableau ou une chaîne sont retournés.</span><span class="sxs-lookup"><span data-stu-id="d9df7-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-818">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-818">Return value</span></span>

<span data-ttu-id="d9df7-819">Tableau ou chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-820">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-820">Examples</span></span>

<span data-ttu-id="d9df7-821">Hello suivant l’exemple prend hello spécifié le nombre d’éléments de tableau de hello et les caractères d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="d9df7-822">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-823">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-823">Name</span></span> | <span data-ttu-id="d9df7-824">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-824">Type</span></span> | <span data-ttu-id="d9df7-825">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-826">arrayOutput</span></span> | <span data-ttu-id="d9df7-827">Tableau</span><span class="sxs-lookup"><span data-stu-id="d9df7-827">Array</span></span> | <span data-ttu-id="d9df7-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="d9df7-828">["one", "two"]</span></span> |
| <span data-ttu-id="d9df7-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-829">stringOutput</span></span> | <span data-ttu-id="d9df7-830">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-830">String</span></span> | <span data-ttu-id="d9df7-831">sur</span><span class="sxs-lookup"><span data-stu-id="d9df7-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="d9df7-832">toLower</span><span class="sxs-lookup"><span data-stu-id="d9df7-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="d9df7-833">Convertit hello spécifié cas toolower de chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-834">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-834">Parameters</span></span>

| <span data-ttu-id="d9df7-835">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-835">Parameter</span></span> | <span data-ttu-id="d9df7-836">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-836">Required</span></span> | <span data-ttu-id="d9df7-837">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-837">Type</span></span> | <span data-ttu-id="d9df7-838">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-839">chaîne_à_modifier</span><span class="sxs-lookup"><span data-stu-id="d9df7-839">stringToChange</span></span> |<span data-ttu-id="d9df7-840">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-840">Yes</span></span> |<span data-ttu-id="d9df7-841">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-841">string</span></span> |<span data-ttu-id="d9df7-842">cas de Hello valeur tooconvert toolower.</span><span class="sxs-lookup"><span data-stu-id="d9df7-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-843">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-843">Return value</span></span>

<span data-ttu-id="d9df7-844">chaîne de Hello converti toolower cas.</span><span class="sxs-lookup"><span data-stu-id="d9df7-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-845">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-845">Examples</span></span>

<span data-ttu-id="d9df7-846">Bonjour à l’exemple suivant convertit un cas de toolower de valeur de paramètre et les cas de tooupper.</span><span class="sxs-lookup"><span data-stu-id="d9df7-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="d9df7-847">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-848">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-848">Name</span></span> | <span data-ttu-id="d9df7-849">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-849">Type</span></span> | <span data-ttu-id="d9df7-850">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-851">toLowerOutput</span></span> | <span data-ttu-id="d9df7-852">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-852">String</span></span> | <span data-ttu-id="d9df7-853">one two three</span><span class="sxs-lookup"><span data-stu-id="d9df7-853">one two three</span></span> |
| <span data-ttu-id="d9df7-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-854">toUpperOutput</span></span> | <span data-ttu-id="d9df7-855">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-855">String</span></span> | <span data-ttu-id="d9df7-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="d9df7-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="d9df7-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="d9df7-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="d9df7-858">Convertit hello spécifié cas tooupper de chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-859">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-859">Parameters</span></span>

| <span data-ttu-id="d9df7-860">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-860">Parameter</span></span> | <span data-ttu-id="d9df7-861">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-861">Required</span></span> | <span data-ttu-id="d9df7-862">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-862">Type</span></span> | <span data-ttu-id="d9df7-863">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-864">chaîne_à_modifier</span><span class="sxs-lookup"><span data-stu-id="d9df7-864">stringToChange</span></span> |<span data-ttu-id="d9df7-865">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-865">Yes</span></span> |<span data-ttu-id="d9df7-866">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-866">string</span></span> |<span data-ttu-id="d9df7-867">cas de Hello valeur tooconvert tooupper.</span><span class="sxs-lookup"><span data-stu-id="d9df7-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-868">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-868">Return value</span></span>

<span data-ttu-id="d9df7-869">chaîne de Hello converti tooupper cas.</span><span class="sxs-lookup"><span data-stu-id="d9df7-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-870">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-870">Examples</span></span>

<span data-ttu-id="d9df7-871">Bonjour à l’exemple suivant convertit un cas de toolower de valeur de paramètre et les cas de tooupper.</span><span class="sxs-lookup"><span data-stu-id="d9df7-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="d9df7-872">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-873">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-873">Name</span></span> | <span data-ttu-id="d9df7-874">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-874">Type</span></span> | <span data-ttu-id="d9df7-875">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-876">toLowerOutput</span></span> | <span data-ttu-id="d9df7-877">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-877">String</span></span> | <span data-ttu-id="d9df7-878">one two three</span><span class="sxs-lookup"><span data-stu-id="d9df7-878">one two three</span></span> |
| <span data-ttu-id="d9df7-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-879">toUpperOutput</span></span> | <span data-ttu-id="d9df7-880">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-880">String</span></span> | <span data-ttu-id="d9df7-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="d9df7-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="d9df7-882">découper</span><span class="sxs-lookup"><span data-stu-id="d9df7-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="d9df7-883">Supprime tous les premiers et derniers caractères d’espace blanc de hello de chaîne spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d9df7-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-884">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-884">Parameters</span></span>

| <span data-ttu-id="d9df7-885">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-885">Parameter</span></span> | <span data-ttu-id="d9df7-886">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-886">Required</span></span> | <span data-ttu-id="d9df7-887">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-887">Type</span></span> | <span data-ttu-id="d9df7-888">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="d9df7-889">stringToTrim</span></span> |<span data-ttu-id="d9df7-890">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-890">Yes</span></span> |<span data-ttu-id="d9df7-891">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-891">string</span></span> |<span data-ttu-id="d9df7-892">Hello tootrim de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-893">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-893">Return value</span></span>

<span data-ttu-id="d9df7-894">chaîne Hello sans les premiers et derniers caractères d’espace blanc.</span><span class="sxs-lookup"><span data-stu-id="d9df7-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-895">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-895">Examples</span></span>

<span data-ttu-id="d9df7-896">Hello exemple suivant supprime les caractères d’espace blanc de hello de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="d9df7-897">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-898">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-898">Name</span></span> | <span data-ttu-id="d9df7-899">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-899">Type</span></span> | <span data-ttu-id="d9df7-900">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-901">return</span><span class="sxs-lookup"><span data-stu-id="d9df7-901">return</span></span> | <span data-ttu-id="d9df7-902">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-902">String</span></span> | <span data-ttu-id="d9df7-903">one two three</span><span class="sxs-lookup"><span data-stu-id="d9df7-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="d9df7-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="d9df7-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="d9df7-905">Crée une chaîne de hachage déterministe en fonction des valeurs hello fournies comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="d9df7-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="d9df7-906">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-906">Parameters</span></span>

| <span data-ttu-id="d9df7-907">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-907">Parameter</span></span> | <span data-ttu-id="d9df7-908">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-908">Required</span></span> | <span data-ttu-id="d9df7-909">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-909">Type</span></span> | <span data-ttu-id="d9df7-910">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-911">baseString</span><span class="sxs-lookup"><span data-stu-id="d9df7-911">baseString</span></span> |<span data-ttu-id="d9df7-912">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-912">Yes</span></span> |<span data-ttu-id="d9df7-913">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-913">string</span></span> |<span data-ttu-id="d9df7-914">valeur de Hello utilisé dans toocreate de fonction de hachage hello une chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="d9df7-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="d9df7-915">paramètres supplémentaires le cas échéant</span><span class="sxs-lookup"><span data-stu-id="d9df7-915">additional parameters as needed</span></span> |<span data-ttu-id="d9df7-916">Non</span><span class="sxs-lookup"><span data-stu-id="d9df7-916">No</span></span> |<span data-ttu-id="d9df7-917">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-917">string</span></span> |<span data-ttu-id="d9df7-918">Vous pouvez ajouter autant de chaînes en tant que valeur hello toocreate requis qui spécifie le niveau de hello d’unicité.</span><span class="sxs-lookup"><span data-stu-id="d9df7-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="d9df7-919">Remarques</span><span class="sxs-lookup"><span data-stu-id="d9df7-919">Remarks</span></span>

<span data-ttu-id="d9df7-920">Cette fonction est utile lorsque vous avez besoin de toocreate un nom unique pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="d9df7-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="d9df7-921">Vous fournissez des valeurs des paramètres qui limitent la portée hello d’unicité pour résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="d9df7-922">Vous pouvez spécifier si les nom de hello est unique vers le bas toosubscription, groupe de ressources ou le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d9df7-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="d9df7-923">Hello retourné la valeur n’est pas une chaîne aléatoire, mais plutôt hello résultat d’une fonction de hachage.</span><span class="sxs-lookup"><span data-stu-id="d9df7-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="d9df7-924">Hello retourné la valeur est 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="d9df7-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="d9df7-925">Elle n’est pas globalement unique.</span><span class="sxs-lookup"><span data-stu-id="d9df7-925">It is not globally unique.</span></span> <span data-ttu-id="d9df7-926">Vous souhaiterez valeur hello de toocombine avec un préfixe à partir de votre toocreate de convention d’affectation de noms un nom significatif.</span><span class="sxs-lookup"><span data-stu-id="d9df7-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="d9df7-927">Hello suivant montre format hello Hello retourné de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="d9df7-928">valeur Hello varie selon le hello paramètres fourni.</span><span class="sxs-lookup"><span data-stu-id="d9df7-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="d9df7-929">Hello suivant exemples montrent comment toocreate d’uniqueString toouse unique valeur couramment utilisés niveaux.</span><span class="sxs-lookup"><span data-stu-id="d9df7-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="d9df7-930">Toosubscription étendue unique</span><span class="sxs-lookup"><span data-stu-id="d9df7-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="d9df7-931">Groupe de tooresource étendue unique</span><span class="sxs-lookup"><span data-stu-id="d9df7-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="d9df7-932">Unique toodeployment étendue pour un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d9df7-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="d9df7-933">Bonjour à l’exemple suivant montre comment toocreate un nom unique pour un compte de stockage en fonction de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d9df7-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="d9df7-934">À l’intérieur du groupe de ressources hello, nom de hello n’est pas unique si construit hello identique.</span><span class="sxs-lookup"><span data-stu-id="d9df7-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="d9df7-935">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-935">Return value</span></span>

<span data-ttu-id="d9df7-936">Chaîne contenant 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="d9df7-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-937">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-937">Examples</span></span>

<span data-ttu-id="d9df7-938">Bonjour à l’exemple suivant retourne les résultats d’uniquestring :</span><span class="sxs-lookup"><span data-stu-id="d9df7-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="d9df7-939">URI</span><span class="sxs-lookup"><span data-stu-id="d9df7-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="d9df7-940">Crée un URI absolu en combinant hello baseUri et la chaîne d’URI relatif hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-941">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-941">Parameters</span></span>

| <span data-ttu-id="d9df7-942">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-942">Parameter</span></span> | <span data-ttu-id="d9df7-943">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-943">Required</span></span> | <span data-ttu-id="d9df7-944">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-944">Type</span></span> | <span data-ttu-id="d9df7-945">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="d9df7-946">baseUri</span></span> |<span data-ttu-id="d9df7-947">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-947">Yes</span></span> |<span data-ttu-id="d9df7-948">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-948">string</span></span> |<span data-ttu-id="d9df7-949">chaîne d’uri de base Hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-949">hello base uri string.</span></span> |
| <span data-ttu-id="d9df7-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="d9df7-950">relativeUri</span></span> |<span data-ttu-id="d9df7-951">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-951">Yes</span></span> |<span data-ttu-id="d9df7-952">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-952">string</span></span> |<span data-ttu-id="d9df7-953">Hello uri relatif tooadd toohello uri de base chaîne.</span><span class="sxs-lookup"><span data-stu-id="d9df7-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="d9df7-954">Hello valeur hello **baseUri** paramètre peut inclure un fichier spécifique, mais uniquement le chemin de base hello est utilisé lors de la construction hello URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="d9df7-955">Par exemple, le passage `http://contoso.com/resources/azuredeploy.json` en tant que résultats de paramètre baseUri hello dans un URI de base `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="d9df7-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="d9df7-956">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-956">Return value</span></span>

<span data-ttu-id="d9df7-957">Chaîne représentant hello URI absolu pour les valeurs de base et relatifs hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-958">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-958">Examples</span></span>

<span data-ttu-id="d9df7-959">Bonjour à l’exemple suivant montre comment tooconstruct un lien tooa imbriquée basées sur un modèle de valeur hello du modèle parent de hello.</span><span class="sxs-lookup"><span data-stu-id="d9df7-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="d9df7-960">Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="d9df7-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d9df7-961">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-962">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-962">Name</span></span> | <span data-ttu-id="d9df7-963">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-963">Type</span></span> | <span data-ttu-id="d9df7-964">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-965">uriOutput</span></span> | <span data-ttu-id="d9df7-966">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-966">String</span></span> | <span data-ttu-id="d9df7-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-968">componentOutput</span></span> | <span data-ttu-id="d9df7-969">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-969">String</span></span> | <span data-ttu-id="d9df7-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-971">toStringOutput</span></span> | <span data-ttu-id="d9df7-972">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-972">String</span></span> | <span data-ttu-id="d9df7-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="d9df7-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="d9df7-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="d9df7-975">Encode un URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-976">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-976">Parameters</span></span>

| <span data-ttu-id="d9df7-977">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-977">Parameter</span></span> | <span data-ttu-id="d9df7-978">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-978">Required</span></span> | <span data-ttu-id="d9df7-979">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-979">Type</span></span> | <span data-ttu-id="d9df7-980">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="d9df7-981">stringToEncode</span></span> |<span data-ttu-id="d9df7-982">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-982">Yes</span></span> |<span data-ttu-id="d9df7-983">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-983">string</span></span> |<span data-ttu-id="d9df7-984">Hello tooencode de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-985">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-985">Return value</span></span>

<span data-ttu-id="d9df7-986">Une chaîne de hello URI encodé de valeur.</span><span class="sxs-lookup"><span data-stu-id="d9df7-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-987">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-987">Examples</span></span>

<span data-ttu-id="d9df7-988">Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="d9df7-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d9df7-989">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-990">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-990">Name</span></span> | <span data-ttu-id="d9df7-991">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-991">Type</span></span> | <span data-ttu-id="d9df7-992">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-993">uriOutput</span></span> | <span data-ttu-id="d9df7-994">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-994">String</span></span> | <span data-ttu-id="d9df7-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-996">componentOutput</span></span> | <span data-ttu-id="d9df7-997">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-997">String</span></span> | <span data-ttu-id="d9df7-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-999">toStringOutput</span></span> | <span data-ttu-id="d9df7-1000">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-1000">String</span></span> | <span data-ttu-id="d9df7-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="d9df7-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="d9df7-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="d9df7-1003">Retourne une chaîne de la valeur encodée de l’URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d9df7-1004">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d9df7-1004">Parameters</span></span>

| <span data-ttu-id="d9df7-1005">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d9df7-1005">Parameter</span></span> | <span data-ttu-id="d9df7-1006">Requis</span><span class="sxs-lookup"><span data-stu-id="d9df7-1006">Required</span></span> | <span data-ttu-id="d9df7-1007">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-1007">Type</span></span> | <span data-ttu-id="d9df7-1008">Description</span><span class="sxs-lookup"><span data-stu-id="d9df7-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d9df7-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="d9df7-1009">uriEncodedString</span></span> |<span data-ttu-id="d9df7-1010">Oui</span><span class="sxs-lookup"><span data-stu-id="d9df7-1010">Yes</span></span> |<span data-ttu-id="d9df7-1011">string</span><span class="sxs-lookup"><span data-stu-id="d9df7-1011">string</span></span> |<span data-ttu-id="d9df7-1012">Hello URI encodé de chaîne de valeur tooconvert tooa.</span><span class="sxs-lookup"><span data-stu-id="d9df7-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d9df7-1013">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="d9df7-1013">Return value</span></span>

<span data-ttu-id="d9df7-1014">Chaîne décodée de la valeur encodée de l’URI.</span><span class="sxs-lookup"><span data-stu-id="d9df7-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="d9df7-1015">Exemples</span><span class="sxs-lookup"><span data-stu-id="d9df7-1015">Examples</span></span>

<span data-ttu-id="d9df7-1016">Hello suivant montre l’exemple de comment toouse uri, intégrante et uriComponentToString :</span><span class="sxs-lookup"><span data-stu-id="d9df7-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d9df7-1017">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="d9df7-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d9df7-1018">Nom</span><span class="sxs-lookup"><span data-stu-id="d9df7-1018">Name</span></span> | <span data-ttu-id="d9df7-1019">Type</span><span class="sxs-lookup"><span data-stu-id="d9df7-1019">Type</span></span> | <span data-ttu-id="d9df7-1020">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9df7-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d9df7-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-1021">uriOutput</span></span> | <span data-ttu-id="d9df7-1022">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-1022">String</span></span> | <span data-ttu-id="d9df7-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-1024">componentOutput</span></span> | <span data-ttu-id="d9df7-1025">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-1025">String</span></span> | <span data-ttu-id="d9df7-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d9df7-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d9df7-1027">toStringOutput</span></span> | <span data-ttu-id="d9df7-1028">String</span><span class="sxs-lookup"><span data-stu-id="d9df7-1028">String</span></span> | <span data-ttu-id="d9df7-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d9df7-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d9df7-1030">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9df7-1030">Next steps</span></span>
* <span data-ttu-id="d9df7-1031">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d9df7-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d9df7-1032">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d9df7-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d9df7-1033">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d9df7-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="d9df7-1034">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d9df7-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

