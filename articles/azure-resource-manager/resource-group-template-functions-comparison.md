---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - comparaison | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans des valeurs de toocompare modèles Azure Resource Manager."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9d645-103">Fonctions de comparaison pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9d645-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="9d645-104">Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.</span><span class="sxs-lookup"><span data-stu-id="9d645-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="9d645-105">equals</span><span class="sxs-lookup"><span data-stu-id="9d645-105">equals</span></span>](#equals)
* [<span data-ttu-id="9d645-106">greater</span><span class="sxs-lookup"><span data-stu-id="9d645-106">greater</span></span>](#greater)
* [<span data-ttu-id="9d645-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="9d645-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="9d645-108">less</span><span class="sxs-lookup"><span data-stu-id="9d645-108">less</span></span>](#less)
* [<span data-ttu-id="9d645-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="9d645-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="9d645-110">equals</span><span class="sxs-lookup"><span data-stu-id="9d645-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="9d645-111">Vérifie si deux valeurs sont égales.</span><span class="sxs-lookup"><span data-stu-id="9d645-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="9d645-112">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d645-112">Parameters</span></span>

| <span data-ttu-id="9d645-113">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9d645-113">Parameter</span></span> | <span data-ttu-id="9d645-114">Requis</span><span class="sxs-lookup"><span data-stu-id="9d645-114">Required</span></span> | <span data-ttu-id="9d645-115">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-115">Type</span></span> | <span data-ttu-id="9d645-116">Description</span><span class="sxs-lookup"><span data-stu-id="9d645-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d645-117">arg1</span><span class="sxs-lookup"><span data-stu-id="9d645-117">arg1</span></span> |<span data-ttu-id="9d645-118">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-118">Yes</span></span> |<span data-ttu-id="9d645-119">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="9d645-119">int, string, array, or object</span></span> |<span data-ttu-id="9d645-120">Hello première valeur toocheck pour l’égalité.</span><span class="sxs-lookup"><span data-stu-id="9d645-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="9d645-121">arg2</span><span class="sxs-lookup"><span data-stu-id="9d645-121">arg2</span></span> |<span data-ttu-id="9d645-122">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-122">Yes</span></span> |<span data-ttu-id="9d645-123">entier, chaîne, tableau ou objet</span><span class="sxs-lookup"><span data-stu-id="9d645-123">int, string, array, or object</span></span> |<span data-ttu-id="9d645-124">Bonjour deuxième toocheck de valeur pour l’égalité.</span><span class="sxs-lookup"><span data-stu-id="9d645-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9d645-125">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d645-125">Return value</span></span>

<span data-ttu-id="9d645-126">Retourne **True** si les valeurs hello sont égaux ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="9d645-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="9d645-127">Remarques</span><span class="sxs-lookup"><span data-stu-id="9d645-127">Remarks</span></span>

<span data-ttu-id="9d645-128">Hello fonction equals est souvent utilisée avec hello `condition` élément tootest indique si une ressource est déployée.</span><span class="sxs-lookup"><span data-stu-id="9d645-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="9d645-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d645-129">Example</span></span>

<span data-ttu-id="9d645-130">exemple de modèle de Hello vérifie les différents types de valeurs sont égales.</span><span class="sxs-lookup"><span data-stu-id="9d645-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="9d645-131">Toutes les valeurs par défaut de hello renvoient True.</span><span class="sxs-lookup"><span data-stu-id="9d645-131">All hello default values return True.</span></span>

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

<span data-ttu-id="9d645-132">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="9d645-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9d645-133">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-133">Name</span></span> | <span data-ttu-id="9d645-134">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-134">Type</span></span> | <span data-ttu-id="9d645-135">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="9d645-136">checkInts</span></span> | <span data-ttu-id="9d645-137">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-137">Bool</span></span> | <span data-ttu-id="9d645-138">True</span><span class="sxs-lookup"><span data-stu-id="9d645-138">True</span></span> |
| <span data-ttu-id="9d645-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="9d645-139">checkStrings</span></span> | <span data-ttu-id="9d645-140">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-140">Bool</span></span> | <span data-ttu-id="9d645-141">True</span><span class="sxs-lookup"><span data-stu-id="9d645-141">True</span></span> |
| <span data-ttu-id="9d645-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="9d645-142">checkArrays</span></span> | <span data-ttu-id="9d645-143">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-143">Bool</span></span> | <span data-ttu-id="9d645-144">True</span><span class="sxs-lookup"><span data-stu-id="9d645-144">True</span></span> |
| <span data-ttu-id="9d645-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="9d645-145">checkObjects</span></span> | <span data-ttu-id="9d645-146">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-146">Bool</span></span> | <span data-ttu-id="9d645-147">true</span><span class="sxs-lookup"><span data-stu-id="9d645-147">True</span></span> |


<span data-ttu-id="9d645-148">Hello exemple suivant utilise [pas](resource-group-template-functions-logical.md#not) avec **est égal à**.</span><span class="sxs-lookup"><span data-stu-id="9d645-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="9d645-149">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9d645-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9d645-150">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-150">Name</span></span> | <span data-ttu-id="9d645-151">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-151">Type</span></span> | <span data-ttu-id="9d645-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="9d645-153">checkNotEquals</span></span> | <span data-ttu-id="9d645-154">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-154">Bool</span></span> | <span data-ttu-id="9d645-155">true</span><span class="sxs-lookup"><span data-stu-id="9d645-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="9d645-156">greater</span><span class="sxs-lookup"><span data-stu-id="9d645-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="9d645-157">Vérifie si la première valeur de hello est supérieure à la valeur de seconde hello.</span><span class="sxs-lookup"><span data-stu-id="9d645-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9d645-158">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d645-158">Parameters</span></span>

| <span data-ttu-id="9d645-159">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9d645-159">Parameter</span></span> | <span data-ttu-id="9d645-160">Requis</span><span class="sxs-lookup"><span data-stu-id="9d645-160">Required</span></span> | <span data-ttu-id="9d645-161">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-161">Type</span></span> | <span data-ttu-id="9d645-162">Description</span><span class="sxs-lookup"><span data-stu-id="9d645-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d645-163">arg1</span><span class="sxs-lookup"><span data-stu-id="9d645-163">arg1</span></span> |<span data-ttu-id="9d645-164">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-164">Yes</span></span> |<span data-ttu-id="9d645-165">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-165">int or string</span></span> |<span data-ttu-id="9d645-166">Hello première valeur de comparaison supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="9d645-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="9d645-167">arg2</span><span class="sxs-lookup"><span data-stu-id="9d645-167">arg2</span></span> |<span data-ttu-id="9d645-168">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-168">Yes</span></span> |<span data-ttu-id="9d645-169">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-169">int or string</span></span> |<span data-ttu-id="9d645-170">Hello deuxième valeur de comparaison supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="9d645-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9d645-171">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d645-171">Return value</span></span>

<span data-ttu-id="9d645-172">Retourne **True** si hello première valeur est supérieure à hello deuxième ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="9d645-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9d645-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d645-173">Example</span></span>

<span data-ttu-id="9d645-174">exemple de modèle de Hello vérifie si une valeur de hello est supérieure à hello autres.</span><span class="sxs-lookup"><span data-stu-id="9d645-174">hello example template checks whether hello one value is greater than hello other.</span></span>

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

<span data-ttu-id="9d645-175">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="9d645-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9d645-176">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-176">Name</span></span> | <span data-ttu-id="9d645-177">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-177">Type</span></span> | <span data-ttu-id="9d645-178">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="9d645-179">checkInts</span></span> | <span data-ttu-id="9d645-180">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-180">Bool</span></span> | <span data-ttu-id="9d645-181">False</span><span class="sxs-lookup"><span data-stu-id="9d645-181">False</span></span> |
| <span data-ttu-id="9d645-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="9d645-182">checkStrings</span></span> | <span data-ttu-id="9d645-183">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-183">Bool</span></span> | <span data-ttu-id="9d645-184">True</span><span class="sxs-lookup"><span data-stu-id="9d645-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="9d645-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="9d645-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="9d645-186">Vérifie si hello première valeur est supérieure ou égale toohello seconde valeur.</span><span class="sxs-lookup"><span data-stu-id="9d645-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9d645-187">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d645-187">Parameters</span></span>

| <span data-ttu-id="9d645-188">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9d645-188">Parameter</span></span> | <span data-ttu-id="9d645-189">Requis</span><span class="sxs-lookup"><span data-stu-id="9d645-189">Required</span></span> | <span data-ttu-id="9d645-190">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-190">Type</span></span> | <span data-ttu-id="9d645-191">Description</span><span class="sxs-lookup"><span data-stu-id="9d645-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d645-192">arg1</span><span class="sxs-lookup"><span data-stu-id="9d645-192">arg1</span></span> |<span data-ttu-id="9d645-193">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-193">Yes</span></span> |<span data-ttu-id="9d645-194">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-194">int or string</span></span> |<span data-ttu-id="9d645-195">Hello première valeur de comparaison supérieure ou égal de hello.</span><span class="sxs-lookup"><span data-stu-id="9d645-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="9d645-196">arg2</span><span class="sxs-lookup"><span data-stu-id="9d645-196">arg2</span></span> |<span data-ttu-id="9d645-197">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-197">Yes</span></span> |<span data-ttu-id="9d645-198">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-198">int or string</span></span> |<span data-ttu-id="9d645-199">Hello deuxième valeur de comparaison supérieure ou égal de hello.</span><span class="sxs-lookup"><span data-stu-id="9d645-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9d645-200">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d645-200">Return value</span></span>

<span data-ttu-id="9d645-201">Retourne **True** si hello première valeur est supérieure ou égale toohello deuxième ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="9d645-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9d645-202">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d645-202">Example</span></span>

<span data-ttu-id="9d645-203">exemple de modèle de Hello vérifie si une valeur de hello est supérieure ou égal toohello autres.</span><span class="sxs-lookup"><span data-stu-id="9d645-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

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

<span data-ttu-id="9d645-204">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="9d645-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9d645-205">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-205">Name</span></span> | <span data-ttu-id="9d645-206">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-206">Type</span></span> | <span data-ttu-id="9d645-207">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="9d645-208">checkInts</span></span> | <span data-ttu-id="9d645-209">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-209">Bool</span></span> | <span data-ttu-id="9d645-210">False</span><span class="sxs-lookup"><span data-stu-id="9d645-210">False</span></span> |
| <span data-ttu-id="9d645-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="9d645-211">checkStrings</span></span> | <span data-ttu-id="9d645-212">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-212">Bool</span></span> | <span data-ttu-id="9d645-213">True</span><span class="sxs-lookup"><span data-stu-id="9d645-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="9d645-214">less</span><span class="sxs-lookup"><span data-stu-id="9d645-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="9d645-215">Vérifie si hello première valeur est inférieure hello deuxième valeur.</span><span class="sxs-lookup"><span data-stu-id="9d645-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9d645-216">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d645-216">Parameters</span></span>

| <span data-ttu-id="9d645-217">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9d645-217">Parameter</span></span> | <span data-ttu-id="9d645-218">Requis</span><span class="sxs-lookup"><span data-stu-id="9d645-218">Required</span></span> | <span data-ttu-id="9d645-219">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-219">Type</span></span> | <span data-ttu-id="9d645-220">Description</span><span class="sxs-lookup"><span data-stu-id="9d645-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d645-221">arg1</span><span class="sxs-lookup"><span data-stu-id="9d645-221">arg1</span></span> |<span data-ttu-id="9d645-222">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-222">Yes</span></span> |<span data-ttu-id="9d645-223">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-223">int or string</span></span> |<span data-ttu-id="9d645-224">Hello première valeur de hello moins de comparaison.</span><span class="sxs-lookup"><span data-stu-id="9d645-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="9d645-225">arg2</span><span class="sxs-lookup"><span data-stu-id="9d645-225">arg2</span></span> |<span data-ttu-id="9d645-226">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-226">Yes</span></span> |<span data-ttu-id="9d645-227">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-227">int or string</span></span> |<span data-ttu-id="9d645-228">Hello deuxième valeur de hello moins de comparaison.</span><span class="sxs-lookup"><span data-stu-id="9d645-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9d645-229">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d645-229">Return value</span></span>

<span data-ttu-id="9d645-230">Retourne **True** si hello première valeur est inférieure à hello deuxième valeur ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="9d645-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9d645-231">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d645-231">Example</span></span>

<span data-ttu-id="9d645-232">exemple de modèle de Hello vérifie si une valeur de hello est inférieure à hello autres.</span><span class="sxs-lookup"><span data-stu-id="9d645-232">hello example template checks whether hello one value is less than hello other.</span></span>

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

<span data-ttu-id="9d645-233">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="9d645-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9d645-234">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-234">Name</span></span> | <span data-ttu-id="9d645-235">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-235">Type</span></span> | <span data-ttu-id="9d645-236">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="9d645-237">checkInts</span></span> | <span data-ttu-id="9d645-238">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-238">Bool</span></span> | <span data-ttu-id="9d645-239">True</span><span class="sxs-lookup"><span data-stu-id="9d645-239">True</span></span> |
| <span data-ttu-id="9d645-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="9d645-240">checkStrings</span></span> | <span data-ttu-id="9d645-241">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-241">Bool</span></span> | <span data-ttu-id="9d645-242">False</span><span class="sxs-lookup"><span data-stu-id="9d645-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="9d645-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="9d645-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="9d645-244">Vérifie si la première valeur de hello est inférieur ou égal toohello seconde valeur.</span><span class="sxs-lookup"><span data-stu-id="9d645-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9d645-245">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d645-245">Parameters</span></span>

| <span data-ttu-id="9d645-246">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9d645-246">Parameter</span></span> | <span data-ttu-id="9d645-247">Requis</span><span class="sxs-lookup"><span data-stu-id="9d645-247">Required</span></span> | <span data-ttu-id="9d645-248">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-248">Type</span></span> | <span data-ttu-id="9d645-249">Description</span><span class="sxs-lookup"><span data-stu-id="9d645-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d645-250">arg1</span><span class="sxs-lookup"><span data-stu-id="9d645-250">arg1</span></span> |<span data-ttu-id="9d645-251">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-251">Yes</span></span> |<span data-ttu-id="9d645-252">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-252">int or string</span></span> |<span data-ttu-id="9d645-253">Hello première valeur de hello inférieur ou égal à la comparaison.</span><span class="sxs-lookup"><span data-stu-id="9d645-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="9d645-254">arg2</span><span class="sxs-lookup"><span data-stu-id="9d645-254">arg2</span></span> |<span data-ttu-id="9d645-255">Oui</span><span class="sxs-lookup"><span data-stu-id="9d645-255">Yes</span></span> |<span data-ttu-id="9d645-256">entier ou chaîne</span><span class="sxs-lookup"><span data-stu-id="9d645-256">int or string</span></span> |<span data-ttu-id="9d645-257">Hello deuxième valeur de hello inférieur ou égal à la comparaison.</span><span class="sxs-lookup"><span data-stu-id="9d645-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9d645-258">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d645-258">Return value</span></span>

<span data-ttu-id="9d645-259">Retourne **True** si hello première valeur est inférieure ou égale toohello deuxième valeur ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="9d645-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9d645-260">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d645-260">Example</span></span>

<span data-ttu-id="9d645-261">Hello exemple de modèle vérifie si une valeur de hello est inférieur ou égal toohello autres.</span><span class="sxs-lookup"><span data-stu-id="9d645-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

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

<span data-ttu-id="9d645-262">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="9d645-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9d645-263">Nom</span><span class="sxs-lookup"><span data-stu-id="9d645-263">Name</span></span> | <span data-ttu-id="9d645-264">Type</span><span class="sxs-lookup"><span data-stu-id="9d645-264">Type</span></span> | <span data-ttu-id="9d645-265">Valeur</span><span class="sxs-lookup"><span data-stu-id="9d645-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9d645-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="9d645-266">checkInts</span></span> | <span data-ttu-id="9d645-267">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-267">Bool</span></span> | <span data-ttu-id="9d645-268">True</span><span class="sxs-lookup"><span data-stu-id="9d645-268">True</span></span> |
| <span data-ttu-id="9d645-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="9d645-269">checkStrings</span></span> | <span data-ttu-id="9d645-270">Bool</span><span class="sxs-lookup"><span data-stu-id="9d645-270">Bool</span></span> | <span data-ttu-id="9d645-271">False</span><span class="sxs-lookup"><span data-stu-id="9d645-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="9d645-272">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d645-272">Next steps</span></span>
* <span data-ttu-id="9d645-273">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9d645-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9d645-274">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9d645-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9d645-275">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9d645-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9d645-276">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9d645-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

