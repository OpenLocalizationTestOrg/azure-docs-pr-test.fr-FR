---
title: "Fonctions de modèle Azure Resource Manager - logiques | Documents Microsoft"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour déterminer les valeurs logiques."
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
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="df3b4-103">Fonctions logiques pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df3b4-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="df3b4-104">Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.</span><span class="sxs-lookup"><span data-stu-id="df3b4-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="df3b4-105">et</span><span class="sxs-lookup"><span data-stu-id="df3b4-105">and</span></span>](#and)
* [<span data-ttu-id="df3b4-106">bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-106">bool</span></span>](#bool)
* [<span data-ttu-id="df3b4-107">si</span><span class="sxs-lookup"><span data-stu-id="df3b4-107">if</span></span>](#if)
* [<span data-ttu-id="df3b4-108">non</span><span class="sxs-lookup"><span data-stu-id="df3b4-108">not</span></span>](#not)
* [<span data-ttu-id="df3b4-109">ou</span><span class="sxs-lookup"><span data-stu-id="df3b4-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="df3b4-110">and</span><span class="sxs-lookup"><span data-stu-id="df3b4-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="df3b4-111">Vérifie si les deux valeurs de paramètres sont true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="df3b4-112">parameters</span><span class="sxs-lookup"><span data-stu-id="df3b4-112">Parameters</span></span>

| <span data-ttu-id="df3b4-113">Paramètre</span><span class="sxs-lookup"><span data-stu-id="df3b4-113">Parameter</span></span> | <span data-ttu-id="df3b4-114">Requis</span><span class="sxs-lookup"><span data-stu-id="df3b4-114">Required</span></span> | <span data-ttu-id="df3b4-115">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-115">Type</span></span> | <span data-ttu-id="df3b4-116">Description</span><span class="sxs-lookup"><span data-stu-id="df3b4-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df3b4-117">arg1</span><span class="sxs-lookup"><span data-stu-id="df3b4-117">arg1</span></span> |<span data-ttu-id="df3b4-118">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-118">Yes</span></span> |<span data-ttu-id="df3b4-119">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-119">boolean</span></span> |<span data-ttu-id="df3b4-120">La première valeur pour vérifier si c’est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="df3b4-121">arg2</span><span class="sxs-lookup"><span data-stu-id="df3b4-121">arg2</span></span> |<span data-ttu-id="df3b4-122">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-122">Yes</span></span> |<span data-ttu-id="df3b4-123">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-123">boolean</span></span> |<span data-ttu-id="df3b4-124">La deuxième valeur pour vérifier si c’est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df3b4-125">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df3b4-125">Return value</span></span>

<span data-ttu-id="df3b4-126">Retourne **True** si les valeurs sont true ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="df3b4-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df3b4-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="df3b4-127">Examples</span></span>

<span data-ttu-id="df3b4-128">L’exemple suivant montre comment utiliser des fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="df3b4-128">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="df3b4-129">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="df3b4-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="df3b4-130">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-130">Name</span></span> | <span data-ttu-id="df3b4-131">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-131">Type</span></span> | <span data-ttu-id="df3b4-132">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-133">andExampleOutput</span></span> | <span data-ttu-id="df3b4-134">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-134">Bool</span></span> | <span data-ttu-id="df3b4-135">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-135">False</span></span> |
| <span data-ttu-id="df3b4-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-136">orExampleOutput</span></span> | <span data-ttu-id="df3b4-137">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-137">Bool</span></span> | <span data-ttu-id="df3b4-138">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-138">True</span></span> |
| <span data-ttu-id="df3b4-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-139">notExampleOutput</span></span> | <span data-ttu-id="df3b4-140">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-140">Bool</span></span> | <span data-ttu-id="df3b4-141">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="df3b4-142">bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="df3b4-143">Convertit le paramètre en valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="df3b4-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="df3b4-144">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df3b4-144">Parameters</span></span>

| <span data-ttu-id="df3b4-145">Paramètre</span><span class="sxs-lookup"><span data-stu-id="df3b4-145">Parameter</span></span> | <span data-ttu-id="df3b4-146">Requis</span><span class="sxs-lookup"><span data-stu-id="df3b4-146">Required</span></span> | <span data-ttu-id="df3b4-147">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-147">Type</span></span> | <span data-ttu-id="df3b4-148">Description</span><span class="sxs-lookup"><span data-stu-id="df3b4-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df3b4-149">arg1</span><span class="sxs-lookup"><span data-stu-id="df3b4-149">arg1</span></span> |<span data-ttu-id="df3b4-150">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-150">Yes</span></span> |<span data-ttu-id="df3b4-151">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="df3b4-151">string or int</span></span> |<span data-ttu-id="df3b4-152">La valeur à convertir en booléen.</span><span class="sxs-lookup"><span data-stu-id="df3b4-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df3b4-153">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df3b4-153">Return value</span></span>
<span data-ttu-id="df3b4-154">Valeur booléenne de la valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="df3b4-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="df3b4-155">Exemples</span><span class="sxs-lookup"><span data-stu-id="df3b4-155">Examples</span></span>

<span data-ttu-id="df3b4-156">L’exemple suivant montre comment utiliser le booléen avec une chaîne ou un entier.</span><span class="sxs-lookup"><span data-stu-id="df3b4-156">The following example shows how to use bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="df3b4-157">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="df3b4-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df3b4-158">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-158">Name</span></span> | <span data-ttu-id="df3b4-159">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-159">Type</span></span> | <span data-ttu-id="df3b4-160">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-161">trueString</span><span class="sxs-lookup"><span data-stu-id="df3b4-161">trueString</span></span> | <span data-ttu-id="df3b4-162">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-162">Bool</span></span> | <span data-ttu-id="df3b4-163">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-163">True</span></span> |
| <span data-ttu-id="df3b4-164">falseString</span><span class="sxs-lookup"><span data-stu-id="df3b4-164">falseString</span></span> | <span data-ttu-id="df3b4-165">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-165">Bool</span></span> | <span data-ttu-id="df3b4-166">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-166">False</span></span> |
| <span data-ttu-id="df3b4-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="df3b4-167">trueInt</span></span> | <span data-ttu-id="df3b4-168">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-168">Bool</span></span> | <span data-ttu-id="df3b4-169">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-169">True</span></span> |
| <span data-ttu-id="df3b4-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="df3b4-170">falseInt</span></span> | <span data-ttu-id="df3b4-171">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-171">Bool</span></span> | <span data-ttu-id="df3b4-172">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="df3b4-173">if</span><span class="sxs-lookup"><span data-stu-id="df3b4-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="df3b4-174">Retourne une valeur indiquant si une condition est true ou false.</span><span class="sxs-lookup"><span data-stu-id="df3b4-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="df3b4-175">parameters</span><span class="sxs-lookup"><span data-stu-id="df3b4-175">Parameters</span></span>

| <span data-ttu-id="df3b4-176">Paramètre</span><span class="sxs-lookup"><span data-stu-id="df3b4-176">Parameter</span></span> | <span data-ttu-id="df3b4-177">Requis</span><span class="sxs-lookup"><span data-stu-id="df3b4-177">Required</span></span> | <span data-ttu-id="df3b4-178">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-178">Type</span></span> | <span data-ttu-id="df3b4-179">Description</span><span class="sxs-lookup"><span data-stu-id="df3b4-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df3b4-180">condition</span><span class="sxs-lookup"><span data-stu-id="df3b4-180">condition</span></span> |<span data-ttu-id="df3b4-181">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-181">Yes</span></span> |<span data-ttu-id="df3b4-182">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-182">boolean</span></span> |<span data-ttu-id="df3b4-183">La valeur pour vérifier si c’est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="df3b4-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="df3b4-184">trueValue</span></span> |<span data-ttu-id="df3b4-185">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-185">Yes</span></span> | <span data-ttu-id="df3b4-186">chaîne, int, objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="df3b4-186">string, int, object, or array</span></span> |<span data-ttu-id="df3b4-187">La valeur à retourner lorsque la condition est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="df3b4-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="df3b4-188">falseValue</span></span> |<span data-ttu-id="df3b4-189">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-189">Yes</span></span> | <span data-ttu-id="df3b4-190">chaîne, int, objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="df3b4-190">string, int, object, or array</span></span> |<span data-ttu-id="df3b4-191">La valeur à retourner lorsque la condition est false.</span><span class="sxs-lookup"><span data-stu-id="df3b4-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df3b4-192">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df3b4-192">Return value</span></span>

<span data-ttu-id="df3b4-193">Retourne le deuxième paramètre lorsque le premier paramètre est **True** ; sinon, retourne le troisième paramètre.</span><span class="sxs-lookup"><span data-stu-id="df3b4-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="df3b4-194">Remarques</span><span class="sxs-lookup"><span data-stu-id="df3b4-194">Remarks</span></span>

<span data-ttu-id="df3b4-195">Vous pouvez utiliser cette fonction pour définir de manière conditionnelle une propriété de ressource.</span><span class="sxs-lookup"><span data-stu-id="df3b4-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="df3b4-196">L’exemple suivant n’est pas un modèle complet, mais il affiche les parties pertinentes pour la définition de manière conditionnelle du groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="df3b4-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="df3b4-197">Exemples</span><span class="sxs-lookup"><span data-stu-id="df3b4-197">Examples</span></span>

<span data-ttu-id="df3b4-198">L’exemple suivant explique comment utiliser la fonction `if`.</span><span class="sxs-lookup"><span data-stu-id="df3b4-198">The following example shows how to use the `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="df3b4-199">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="df3b4-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="df3b4-200">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-200">Name</span></span> | <span data-ttu-id="df3b4-201">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-201">Type</span></span> | <span data-ttu-id="df3b4-202">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-203">yesOutput</span></span> | <span data-ttu-id="df3b4-204">String</span><span class="sxs-lookup"><span data-stu-id="df3b4-204">String</span></span> | <span data-ttu-id="df3b4-205">yes</span><span class="sxs-lookup"><span data-stu-id="df3b4-205">yes</span></span> |
| <span data-ttu-id="df3b4-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-206">noOutput</span></span> | <span data-ttu-id="df3b4-207">String</span><span class="sxs-lookup"><span data-stu-id="df3b4-207">String</span></span> | <span data-ttu-id="df3b4-208">no</span><span class="sxs-lookup"><span data-stu-id="df3b4-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="df3b4-209">not</span><span class="sxs-lookup"><span data-stu-id="df3b4-209">not</span></span>
`not(arg1)`

<span data-ttu-id="df3b4-210">Convertit la valeur booléenne à sa valeur opposée.</span><span class="sxs-lookup"><span data-stu-id="df3b4-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="df3b4-211">parameters</span><span class="sxs-lookup"><span data-stu-id="df3b4-211">Parameters</span></span>

| <span data-ttu-id="df3b4-212">Paramètre</span><span class="sxs-lookup"><span data-stu-id="df3b4-212">Parameter</span></span> | <span data-ttu-id="df3b4-213">Requis</span><span class="sxs-lookup"><span data-stu-id="df3b4-213">Required</span></span> | <span data-ttu-id="df3b4-214">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-214">Type</span></span> | <span data-ttu-id="df3b4-215">Description</span><span class="sxs-lookup"><span data-stu-id="df3b4-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df3b4-216">arg1</span><span class="sxs-lookup"><span data-stu-id="df3b4-216">arg1</span></span> |<span data-ttu-id="df3b4-217">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-217">Yes</span></span> |<span data-ttu-id="df3b4-218">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-218">boolean</span></span> |<span data-ttu-id="df3b4-219">La valeur à convertir.</span><span class="sxs-lookup"><span data-stu-id="df3b4-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="df3b4-220">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df3b4-220">Return value</span></span>

<span data-ttu-id="df3b4-221">Retourne **True** lorsque le paramètre est **False**.</span><span class="sxs-lookup"><span data-stu-id="df3b4-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="df3b4-222">Retourne **False** lorsque le paramètre est **True**.</span><span class="sxs-lookup"><span data-stu-id="df3b4-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="df3b4-223">Exemples</span><span class="sxs-lookup"><span data-stu-id="df3b4-223">Examples</span></span>

<span data-ttu-id="df3b4-224">L’exemple suivant montre comment utiliser des fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="df3b4-224">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="df3b4-225">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="df3b4-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="df3b4-226">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-226">Name</span></span> | <span data-ttu-id="df3b4-227">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-227">Type</span></span> | <span data-ttu-id="df3b4-228">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-229">andExampleOutput</span></span> | <span data-ttu-id="df3b4-230">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-230">Bool</span></span> | <span data-ttu-id="df3b4-231">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-231">False</span></span> |
| <span data-ttu-id="df3b4-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-232">orExampleOutput</span></span> | <span data-ttu-id="df3b4-233">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-233">Bool</span></span> | <span data-ttu-id="df3b4-234">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-234">True</span></span> |
| <span data-ttu-id="df3b4-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-235">notExampleOutput</span></span> | <span data-ttu-id="df3b4-236">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-236">Bool</span></span> | <span data-ttu-id="df3b4-237">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-237">False</span></span> |

<span data-ttu-id="df3b4-238">L’exemple suivant utilise **non** avec[égal à](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="df3b4-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="df3b4-239">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="df3b4-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="df3b4-240">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-240">Name</span></span> | <span data-ttu-id="df3b4-241">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-241">Type</span></span> | <span data-ttu-id="df3b4-242">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="df3b4-243">checkNotEquals</span></span> | <span data-ttu-id="df3b4-244">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-244">Bool</span></span> | <span data-ttu-id="df3b4-245">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="df3b4-246">ou</span><span class="sxs-lookup"><span data-stu-id="df3b4-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="df3b4-247">Vérifie si l’une des valeurs du paramètre est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="df3b4-248">parameters</span><span class="sxs-lookup"><span data-stu-id="df3b4-248">Parameters</span></span>

| <span data-ttu-id="df3b4-249">Paramètre</span><span class="sxs-lookup"><span data-stu-id="df3b4-249">Parameter</span></span> | <span data-ttu-id="df3b4-250">Requis</span><span class="sxs-lookup"><span data-stu-id="df3b4-250">Required</span></span> | <span data-ttu-id="df3b4-251">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-251">Type</span></span> | <span data-ttu-id="df3b4-252">Description</span><span class="sxs-lookup"><span data-stu-id="df3b4-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df3b4-253">arg1</span><span class="sxs-lookup"><span data-stu-id="df3b4-253">arg1</span></span> |<span data-ttu-id="df3b4-254">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-254">Yes</span></span> |<span data-ttu-id="df3b4-255">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-255">boolean</span></span> |<span data-ttu-id="df3b4-256">La première valeur pour vérifier si c’est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="df3b4-257">arg2</span><span class="sxs-lookup"><span data-stu-id="df3b4-257">arg2</span></span> |<span data-ttu-id="df3b4-258">Oui</span><span class="sxs-lookup"><span data-stu-id="df3b4-258">Yes</span></span> |<span data-ttu-id="df3b4-259">booléenne</span><span class="sxs-lookup"><span data-stu-id="df3b4-259">boolean</span></span> |<span data-ttu-id="df3b4-260">La deuxième valeur pour vérifier si c’est true.</span><span class="sxs-lookup"><span data-stu-id="df3b4-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df3b4-261">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df3b4-261">Return value</span></span>

<span data-ttu-id="df3b4-262">Retourne **True** si la valeur est true ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="df3b4-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df3b4-263">Exemples</span><span class="sxs-lookup"><span data-stu-id="df3b4-263">Examples</span></span>

<span data-ttu-id="df3b4-264">L’exemple suivant montre comment utiliser des fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="df3b4-264">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="df3b4-265">La sortie de l’exemple précédent est :</span><span class="sxs-lookup"><span data-stu-id="df3b4-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="df3b4-266">Nom</span><span class="sxs-lookup"><span data-stu-id="df3b4-266">Name</span></span> | <span data-ttu-id="df3b4-267">Type</span><span class="sxs-lookup"><span data-stu-id="df3b4-267">Type</span></span> | <span data-ttu-id="df3b4-268">Valeur</span><span class="sxs-lookup"><span data-stu-id="df3b4-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df3b4-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-269">andExampleOutput</span></span> | <span data-ttu-id="df3b4-270">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-270">Bool</span></span> | <span data-ttu-id="df3b4-271">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-271">False</span></span> |
| <span data-ttu-id="df3b4-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-272">orExampleOutput</span></span> | <span data-ttu-id="df3b4-273">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-273">Bool</span></span> | <span data-ttu-id="df3b4-274">true</span><span class="sxs-lookup"><span data-stu-id="df3b4-274">True</span></span> |
| <span data-ttu-id="df3b4-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="df3b4-275">notExampleOutput</span></span> | <span data-ttu-id="df3b4-276">Bool</span><span class="sxs-lookup"><span data-stu-id="df3b4-276">Bool</span></span> | <span data-ttu-id="df3b4-277">False</span><span class="sxs-lookup"><span data-stu-id="df3b4-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="df3b4-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df3b4-278">Next steps</span></span>
* <span data-ttu-id="df3b4-279">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="df3b4-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="df3b4-280">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="df3b4-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="df3b4-281">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="df3b4-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="df3b4-282">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="df3b4-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

