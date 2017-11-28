---
title: "Fonctions de modèle Azure Resource Manager - comparaison| Microsoft Docs"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour comparer des valeurs."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="64809-103">Fonctions de comparaison pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64809-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="64809-104">Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.</span><span class="sxs-lookup"><span data-stu-id="64809-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="64809-105">equals</span><span class="sxs-lookup"><span data-stu-id="64809-105">equals</span></span>](#equals)
* [<span data-ttu-id="64809-106">greater</span><span class="sxs-lookup"><span data-stu-id="64809-106">greater</span></span>](#greater)
* [<span data-ttu-id="64809-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="64809-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="64809-108">less</span><span class="sxs-lookup"><span data-stu-id="64809-108">less</span></span>](#less)
* [<span data-ttu-id="64809-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="64809-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="64809-110">equals</span><span class="sxs-lookup"><span data-stu-id="64809-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="64809-111">Vérifie si deux valeurs sont égales.</span><span class="sxs-lookup"><span data-stu-id="64809-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="64809-112">Paramètres</span><span class="sxs-lookup"><span data-stu-id="64809-112">Parameters</span></span>

| <span data-ttu-id="64809-113">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64809-113">Parameter</span></span> | <span data-ttu-id="64809-114">Requis</span><span class="sxs-lookup"><span data-stu-id="64809-114">Required</span></span> | <span data-ttu-id="64809-115">Type</span><span class="sxs-lookup"><span data-stu-id="64809-115">Type</span></span> | <span data-ttu-id="64809-116">Description</span><span class="sxs-lookup"><span data-stu-id="64809-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64809-117">arg1</span><span class="sxs-lookup"><span data-stu-id="64809-117">arg1</span></span> |<span data-ttu-id="64809-118">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-118">Yes</span></span> |<span data-ttu-id="64809-119">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="64809-119">int, string, array, or object</span></span> |<span data-ttu-id="64809-120">Première valeur dont l’égalité est à vérifier.</span><span class="sxs-lookup"><span data-stu-id="64809-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="64809-121">arg2</span><span class="sxs-lookup"><span data-stu-id="64809-121">arg2</span></span> |<span data-ttu-id="64809-122">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-122">Yes</span></span> |<span data-ttu-id="64809-123">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="64809-123">int, string, array, or object</span></span> |<span data-ttu-id="64809-124">Deuxième valeur dont l’égalité est à vérifier.</span><span class="sxs-lookup"><span data-stu-id="64809-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64809-125">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="64809-125">Return value</span></span>

<span data-ttu-id="64809-126">Retourne **True** si les valeurs sont égales ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="64809-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="64809-127">Remarques</span><span class="sxs-lookup"><span data-stu-id="64809-127">Remarks</span></span>

<span data-ttu-id="64809-128">La fonction equals est souvent utilisée avec l’élément `condition` pour tester si une ressource est déployée.</span><span class="sxs-lookup"><span data-stu-id="64809-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="64809-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="64809-129">Example</span></span>

<span data-ttu-id="64809-130">L’exemple de modèle vérifie que les différents types de valeurs sont égaux.</span><span class="sxs-lookup"><span data-stu-id="64809-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="64809-131">Toutes les valeurs par défaut retournent la valeur True.</span><span class="sxs-lookup"><span data-stu-id="64809-131">All the default values return True.</span></span>

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

<span data-ttu-id="64809-132">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="64809-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="64809-133">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-133">Name</span></span> | <span data-ttu-id="64809-134">Type</span><span class="sxs-lookup"><span data-stu-id="64809-134">Type</span></span> | <span data-ttu-id="64809-135">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="64809-136">checkInts</span></span> | <span data-ttu-id="64809-137">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-137">Bool</span></span> | <span data-ttu-id="64809-138">True</span><span class="sxs-lookup"><span data-stu-id="64809-138">True</span></span> |
| <span data-ttu-id="64809-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="64809-139">checkStrings</span></span> | <span data-ttu-id="64809-140">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-140">Bool</span></span> | <span data-ttu-id="64809-141">True</span><span class="sxs-lookup"><span data-stu-id="64809-141">True</span></span> |
| <span data-ttu-id="64809-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="64809-142">checkArrays</span></span> | <span data-ttu-id="64809-143">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-143">Bool</span></span> | <span data-ttu-id="64809-144">True</span><span class="sxs-lookup"><span data-stu-id="64809-144">True</span></span> |
| <span data-ttu-id="64809-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="64809-145">checkObjects</span></span> | <span data-ttu-id="64809-146">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-146">Bool</span></span> | <span data-ttu-id="64809-147">true</span><span class="sxs-lookup"><span data-stu-id="64809-147">True</span></span> |


<span data-ttu-id="64809-148">L’exemple suivant utilise [non](resource-group-template-functions-logical.md#not) avec**égal à**.</span><span class="sxs-lookup"><span data-stu-id="64809-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="64809-149">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="64809-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="64809-150">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-150">Name</span></span> | <span data-ttu-id="64809-151">Type</span><span class="sxs-lookup"><span data-stu-id="64809-151">Type</span></span> | <span data-ttu-id="64809-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="64809-153">checkNotEquals</span></span> | <span data-ttu-id="64809-154">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-154">Bool</span></span> | <span data-ttu-id="64809-155">true</span><span class="sxs-lookup"><span data-stu-id="64809-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="64809-156">greater</span><span class="sxs-lookup"><span data-stu-id="64809-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="64809-157">Vérifie si la première valeur est supérieure à la deuxième valeur.</span><span class="sxs-lookup"><span data-stu-id="64809-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="64809-158">Paramètres</span><span class="sxs-lookup"><span data-stu-id="64809-158">Parameters</span></span>

| <span data-ttu-id="64809-159">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64809-159">Parameter</span></span> | <span data-ttu-id="64809-160">Requis</span><span class="sxs-lookup"><span data-stu-id="64809-160">Required</span></span> | <span data-ttu-id="64809-161">Type</span><span class="sxs-lookup"><span data-stu-id="64809-161">Type</span></span> | <span data-ttu-id="64809-162">Description</span><span class="sxs-lookup"><span data-stu-id="64809-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64809-163">arg1</span><span class="sxs-lookup"><span data-stu-id="64809-163">arg1</span></span> |<span data-ttu-id="64809-164">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-164">Yes</span></span> |<span data-ttu-id="64809-165">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-165">int or string</span></span> |<span data-ttu-id="64809-166">Première valeur pour la comparaison « supérieur à ».</span><span class="sxs-lookup"><span data-stu-id="64809-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="64809-167">arg2</span><span class="sxs-lookup"><span data-stu-id="64809-167">arg2</span></span> |<span data-ttu-id="64809-168">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-168">Yes</span></span> |<span data-ttu-id="64809-169">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-169">int or string</span></span> |<span data-ttu-id="64809-170">Seconde valeur pour la comparaison « supérieur à ».</span><span class="sxs-lookup"><span data-stu-id="64809-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64809-171">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="64809-171">Return value</span></span>

<span data-ttu-id="64809-172">Retourne **True** si la première valeur est supérieure à la seconde ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="64809-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="64809-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="64809-173">Example</span></span>

<span data-ttu-id="64809-174">L’exemple de modèle vérifie si une valeur est supérieure à l’autre.</span><span class="sxs-lookup"><span data-stu-id="64809-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="64809-175">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="64809-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="64809-176">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-176">Name</span></span> | <span data-ttu-id="64809-177">Type</span><span class="sxs-lookup"><span data-stu-id="64809-177">Type</span></span> | <span data-ttu-id="64809-178">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="64809-179">checkInts</span></span> | <span data-ttu-id="64809-180">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-180">Bool</span></span> | <span data-ttu-id="64809-181">False</span><span class="sxs-lookup"><span data-stu-id="64809-181">False</span></span> |
| <span data-ttu-id="64809-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="64809-182">checkStrings</span></span> | <span data-ttu-id="64809-183">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-183">Bool</span></span> | <span data-ttu-id="64809-184">True</span><span class="sxs-lookup"><span data-stu-id="64809-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="64809-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="64809-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="64809-186">Vérifie si la première valeur est supérieure ou égale à la deuxième valeur.</span><span class="sxs-lookup"><span data-stu-id="64809-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="64809-187">Paramètres</span><span class="sxs-lookup"><span data-stu-id="64809-187">Parameters</span></span>

| <span data-ttu-id="64809-188">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64809-188">Parameter</span></span> | <span data-ttu-id="64809-189">Requis</span><span class="sxs-lookup"><span data-stu-id="64809-189">Required</span></span> | <span data-ttu-id="64809-190">Type</span><span class="sxs-lookup"><span data-stu-id="64809-190">Type</span></span> | <span data-ttu-id="64809-191">Description</span><span class="sxs-lookup"><span data-stu-id="64809-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64809-192">arg1</span><span class="sxs-lookup"><span data-stu-id="64809-192">arg1</span></span> |<span data-ttu-id="64809-193">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-193">Yes</span></span> |<span data-ttu-id="64809-194">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-194">int or string</span></span> |<span data-ttu-id="64809-195">Première valeur pour la comparaison « supérieur ou égal à ».</span><span class="sxs-lookup"><span data-stu-id="64809-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="64809-196">arg2</span><span class="sxs-lookup"><span data-stu-id="64809-196">arg2</span></span> |<span data-ttu-id="64809-197">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-197">Yes</span></span> |<span data-ttu-id="64809-198">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-198">int or string</span></span> |<span data-ttu-id="64809-199">Seconde valeur pour la comparaison « supérieur ou égal à ».</span><span class="sxs-lookup"><span data-stu-id="64809-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64809-200">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="64809-200">Return value</span></span>

<span data-ttu-id="64809-201">Retourne **True** si la première valeur est supérieure ou égale à la seconde ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="64809-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="64809-202">Exemple</span><span class="sxs-lookup"><span data-stu-id="64809-202">Example</span></span>

<span data-ttu-id="64809-203">L’exemple de modèle vérifie si une valeur est supérieure ou égale à l’autre.</span><span class="sxs-lookup"><span data-stu-id="64809-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="64809-204">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="64809-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="64809-205">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-205">Name</span></span> | <span data-ttu-id="64809-206">Type</span><span class="sxs-lookup"><span data-stu-id="64809-206">Type</span></span> | <span data-ttu-id="64809-207">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="64809-208">checkInts</span></span> | <span data-ttu-id="64809-209">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-209">Bool</span></span> | <span data-ttu-id="64809-210">False</span><span class="sxs-lookup"><span data-stu-id="64809-210">False</span></span> |
| <span data-ttu-id="64809-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="64809-211">checkStrings</span></span> | <span data-ttu-id="64809-212">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-212">Bool</span></span> | <span data-ttu-id="64809-213">True</span><span class="sxs-lookup"><span data-stu-id="64809-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="64809-214">less</span><span class="sxs-lookup"><span data-stu-id="64809-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="64809-215">Vérifie si la première valeur est inférieure à la deuxième valeur.</span><span class="sxs-lookup"><span data-stu-id="64809-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="64809-216">Paramètres</span><span class="sxs-lookup"><span data-stu-id="64809-216">Parameters</span></span>

| <span data-ttu-id="64809-217">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64809-217">Parameter</span></span> | <span data-ttu-id="64809-218">Requis</span><span class="sxs-lookup"><span data-stu-id="64809-218">Required</span></span> | <span data-ttu-id="64809-219">Type</span><span class="sxs-lookup"><span data-stu-id="64809-219">Type</span></span> | <span data-ttu-id="64809-220">Description</span><span class="sxs-lookup"><span data-stu-id="64809-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64809-221">arg1</span><span class="sxs-lookup"><span data-stu-id="64809-221">arg1</span></span> |<span data-ttu-id="64809-222">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-222">Yes</span></span> |<span data-ttu-id="64809-223">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-223">int or string</span></span> |<span data-ttu-id="64809-224">Première valeur pour la comparaison « inférieur à ».</span><span class="sxs-lookup"><span data-stu-id="64809-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="64809-225">arg2</span><span class="sxs-lookup"><span data-stu-id="64809-225">arg2</span></span> |<span data-ttu-id="64809-226">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-226">Yes</span></span> |<span data-ttu-id="64809-227">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-227">int or string</span></span> |<span data-ttu-id="64809-228">Deuxième valeur pour la comparaison « inférieur à ».</span><span class="sxs-lookup"><span data-stu-id="64809-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64809-229">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="64809-229">Return value</span></span>

<span data-ttu-id="64809-230">Retourne **True** si la première valeur est inférieure à la seconde ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="64809-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="64809-231">Exemple</span><span class="sxs-lookup"><span data-stu-id="64809-231">Example</span></span>

<span data-ttu-id="64809-232">L’exemple de modèle vérifie si une valeur est inférieure à l’autre.</span><span class="sxs-lookup"><span data-stu-id="64809-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="64809-233">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="64809-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="64809-234">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-234">Name</span></span> | <span data-ttu-id="64809-235">Type</span><span class="sxs-lookup"><span data-stu-id="64809-235">Type</span></span> | <span data-ttu-id="64809-236">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="64809-237">checkInts</span></span> | <span data-ttu-id="64809-238">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-238">Bool</span></span> | <span data-ttu-id="64809-239">True</span><span class="sxs-lookup"><span data-stu-id="64809-239">True</span></span> |
| <span data-ttu-id="64809-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="64809-240">checkStrings</span></span> | <span data-ttu-id="64809-241">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-241">Bool</span></span> | <span data-ttu-id="64809-242">False</span><span class="sxs-lookup"><span data-stu-id="64809-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="64809-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="64809-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="64809-244">Vérifie si la première valeur est inférieure ou égale à la deuxième valeur.</span><span class="sxs-lookup"><span data-stu-id="64809-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="64809-245">Paramètres</span><span class="sxs-lookup"><span data-stu-id="64809-245">Parameters</span></span>

| <span data-ttu-id="64809-246">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64809-246">Parameter</span></span> | <span data-ttu-id="64809-247">Requis</span><span class="sxs-lookup"><span data-stu-id="64809-247">Required</span></span> | <span data-ttu-id="64809-248">Type</span><span class="sxs-lookup"><span data-stu-id="64809-248">Type</span></span> | <span data-ttu-id="64809-249">Description</span><span class="sxs-lookup"><span data-stu-id="64809-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64809-250">arg1</span><span class="sxs-lookup"><span data-stu-id="64809-250">arg1</span></span> |<span data-ttu-id="64809-251">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-251">Yes</span></span> |<span data-ttu-id="64809-252">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-252">int or string</span></span> |<span data-ttu-id="64809-253">Première valeur pour la comparaison « inférieur à ».</span><span class="sxs-lookup"><span data-stu-id="64809-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="64809-254">arg2</span><span class="sxs-lookup"><span data-stu-id="64809-254">arg2</span></span> |<span data-ttu-id="64809-255">Oui</span><span class="sxs-lookup"><span data-stu-id="64809-255">Yes</span></span> |<span data-ttu-id="64809-256">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="64809-256">int or string</span></span> |<span data-ttu-id="64809-257">Première valeur pour la comparaison « inférieur ou égal à ».</span><span class="sxs-lookup"><span data-stu-id="64809-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64809-258">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="64809-258">Return value</span></span>

<span data-ttu-id="64809-259">Retourne **True** si la première valeur est inférieure ou égale à la seconde ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="64809-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="64809-260">Exemple</span><span class="sxs-lookup"><span data-stu-id="64809-260">Example</span></span>

<span data-ttu-id="64809-261">L’exemple de modèle vérifie si une valeur est inférieure ou égale à l’autre.</span><span class="sxs-lookup"><span data-stu-id="64809-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="64809-262">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="64809-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="64809-263">Nom</span><span class="sxs-lookup"><span data-stu-id="64809-263">Name</span></span> | <span data-ttu-id="64809-264">Type</span><span class="sxs-lookup"><span data-stu-id="64809-264">Type</span></span> | <span data-ttu-id="64809-265">Valeur</span><span class="sxs-lookup"><span data-stu-id="64809-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64809-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="64809-266">checkInts</span></span> | <span data-ttu-id="64809-267">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-267">Bool</span></span> | <span data-ttu-id="64809-268">True</span><span class="sxs-lookup"><span data-stu-id="64809-268">True</span></span> |
| <span data-ttu-id="64809-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="64809-269">checkStrings</span></span> | <span data-ttu-id="64809-270">Bool</span><span class="sxs-lookup"><span data-stu-id="64809-270">Bool</span></span> | <span data-ttu-id="64809-271">False</span><span class="sxs-lookup"><span data-stu-id="64809-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="64809-272">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64809-272">Next steps</span></span>
* <span data-ttu-id="64809-273">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64809-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="64809-274">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64809-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="64809-275">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="64809-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="64809-276">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="64809-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

