---
title: "aaaAzure Gestionnaire de ressources fonctions de modèle - logiques | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un gestionnaire de ressources Azure modèle toodetermine les valeurs logiques."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="915ec-103">Fonctions logiques pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="915ec-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="915ec-104">Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.</span><span class="sxs-lookup"><span data-stu-id="915ec-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="915ec-105">et</span><span class="sxs-lookup"><span data-stu-id="915ec-105">and</span></span>](#and)
* [<span data-ttu-id="915ec-106">bool</span><span class="sxs-lookup"><span data-stu-id="915ec-106">bool</span></span>](#bool)
* [<span data-ttu-id="915ec-107">si</span><span class="sxs-lookup"><span data-stu-id="915ec-107">if</span></span>](#if)
* [<span data-ttu-id="915ec-108">non</span><span class="sxs-lookup"><span data-stu-id="915ec-108">not</span></span>](#not)
* [<span data-ttu-id="915ec-109">ou</span><span class="sxs-lookup"><span data-stu-id="915ec-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="915ec-110">and</span><span class="sxs-lookup"><span data-stu-id="915ec-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="915ec-111">Vérifie si les deux valeurs de paramètres sont true.</span><span class="sxs-lookup"><span data-stu-id="915ec-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="915ec-112">parameters</span><span class="sxs-lookup"><span data-stu-id="915ec-112">Parameters</span></span>

| <span data-ttu-id="915ec-113">Paramètre</span><span class="sxs-lookup"><span data-stu-id="915ec-113">Parameter</span></span> | <span data-ttu-id="915ec-114">Requis</span><span class="sxs-lookup"><span data-stu-id="915ec-114">Required</span></span> | <span data-ttu-id="915ec-115">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-115">Type</span></span> | <span data-ttu-id="915ec-116">Description</span><span class="sxs-lookup"><span data-stu-id="915ec-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="915ec-117">arg1</span><span class="sxs-lookup"><span data-stu-id="915ec-117">arg1</span></span> |<span data-ttu-id="915ec-118">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-118">Yes</span></span> |<span data-ttu-id="915ec-119">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-119">boolean</span></span> |<span data-ttu-id="915ec-120">Hello première valeur toocheck si a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="915ec-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="915ec-121">arg2</span><span class="sxs-lookup"><span data-stu-id="915ec-121">arg2</span></span> |<span data-ttu-id="915ec-122">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-122">Yes</span></span> |<span data-ttu-id="915ec-123">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-123">boolean</span></span> |<span data-ttu-id="915ec-124">Hello deuxième valeur toocheck si a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="915ec-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="915ec-125">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="915ec-125">Return value</span></span>

<span data-ttu-id="915ec-126">Retourne **True** si les valeurs sont true ; sinon, renvoie **False**.</span><span class="sxs-lookup"><span data-stu-id="915ec-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="915ec-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="915ec-127">Examples</span></span>

<span data-ttu-id="915ec-128">Hello suivant montre l’exemple de comment toouse les fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="915ec-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="915ec-129">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915ec-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="915ec-130">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-130">Name</span></span> | <span data-ttu-id="915ec-131">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-131">Type</span></span> | <span data-ttu-id="915ec-132">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-133">andExampleOutput</span></span> | <span data-ttu-id="915ec-134">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-134">Bool</span></span> | <span data-ttu-id="915ec-135">False</span><span class="sxs-lookup"><span data-stu-id="915ec-135">False</span></span> |
| <span data-ttu-id="915ec-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-136">orExampleOutput</span></span> | <span data-ttu-id="915ec-137">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-137">Bool</span></span> | <span data-ttu-id="915ec-138">true</span><span class="sxs-lookup"><span data-stu-id="915ec-138">True</span></span> |
| <span data-ttu-id="915ec-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-139">notExampleOutput</span></span> | <span data-ttu-id="915ec-140">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-140">Bool</span></span> | <span data-ttu-id="915ec-141">False</span><span class="sxs-lookup"><span data-stu-id="915ec-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="915ec-142">bool</span><span class="sxs-lookup"><span data-stu-id="915ec-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="915ec-143">Convertit hello tooa de paramètre boolean.</span><span class="sxs-lookup"><span data-stu-id="915ec-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="915ec-144">Paramètres</span><span class="sxs-lookup"><span data-stu-id="915ec-144">Parameters</span></span>

| <span data-ttu-id="915ec-145">Paramètre</span><span class="sxs-lookup"><span data-stu-id="915ec-145">Parameter</span></span> | <span data-ttu-id="915ec-146">Requis</span><span class="sxs-lookup"><span data-stu-id="915ec-146">Required</span></span> | <span data-ttu-id="915ec-147">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-147">Type</span></span> | <span data-ttu-id="915ec-148">Description</span><span class="sxs-lookup"><span data-stu-id="915ec-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="915ec-149">arg1</span><span class="sxs-lookup"><span data-stu-id="915ec-149">arg1</span></span> |<span data-ttu-id="915ec-150">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-150">Yes</span></span> |<span data-ttu-id="915ec-151">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="915ec-151">string or int</span></span> |<span data-ttu-id="915ec-152">Hello tooa tooconvert de valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="915ec-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="915ec-153">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="915ec-153">Return value</span></span>
<span data-ttu-id="915ec-154">Une valeur booléenne de hello de valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="915ec-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="915ec-155">Exemples</span><span class="sxs-lookup"><span data-stu-id="915ec-155">Examples</span></span>

<span data-ttu-id="915ec-156">Hello suivant montre l’exemple de comment bool toouse par une chaîne ou un entier.</span><span class="sxs-lookup"><span data-stu-id="915ec-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="915ec-157">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="915ec-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="915ec-158">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-158">Name</span></span> | <span data-ttu-id="915ec-159">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-159">Type</span></span> | <span data-ttu-id="915ec-160">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-161">trueString</span><span class="sxs-lookup"><span data-stu-id="915ec-161">trueString</span></span> | <span data-ttu-id="915ec-162">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-162">Bool</span></span> | <span data-ttu-id="915ec-163">true</span><span class="sxs-lookup"><span data-stu-id="915ec-163">True</span></span> |
| <span data-ttu-id="915ec-164">falseString</span><span class="sxs-lookup"><span data-stu-id="915ec-164">falseString</span></span> | <span data-ttu-id="915ec-165">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-165">Bool</span></span> | <span data-ttu-id="915ec-166">False</span><span class="sxs-lookup"><span data-stu-id="915ec-166">False</span></span> |
| <span data-ttu-id="915ec-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="915ec-167">trueInt</span></span> | <span data-ttu-id="915ec-168">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-168">Bool</span></span> | <span data-ttu-id="915ec-169">true</span><span class="sxs-lookup"><span data-stu-id="915ec-169">True</span></span> |
| <span data-ttu-id="915ec-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="915ec-170">falseInt</span></span> | <span data-ttu-id="915ec-171">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-171">Bool</span></span> | <span data-ttu-id="915ec-172">False</span><span class="sxs-lookup"><span data-stu-id="915ec-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="915ec-173">if</span><span class="sxs-lookup"><span data-stu-id="915ec-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="915ec-174">Retourne une valeur indiquant si une condition est true ou false.</span><span class="sxs-lookup"><span data-stu-id="915ec-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="915ec-175">parameters</span><span class="sxs-lookup"><span data-stu-id="915ec-175">Parameters</span></span>

| <span data-ttu-id="915ec-176">Paramètre</span><span class="sxs-lookup"><span data-stu-id="915ec-176">Parameter</span></span> | <span data-ttu-id="915ec-177">Requis</span><span class="sxs-lookup"><span data-stu-id="915ec-177">Required</span></span> | <span data-ttu-id="915ec-178">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-178">Type</span></span> | <span data-ttu-id="915ec-179">Description</span><span class="sxs-lookup"><span data-stu-id="915ec-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="915ec-180">condition</span><span class="sxs-lookup"><span data-stu-id="915ec-180">condition</span></span> |<span data-ttu-id="915ec-181">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-181">Yes</span></span> |<span data-ttu-id="915ec-182">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-182">boolean</span></span> |<span data-ttu-id="915ec-183">Bonjour valeur toocheck si elle a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="915ec-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="915ec-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="915ec-184">trueValue</span></span> |<span data-ttu-id="915ec-185">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-185">Yes</span></span> | <span data-ttu-id="915ec-186">chaîne, int, objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="915ec-186">string, int, object, or array</span></span> |<span data-ttu-id="915ec-187">valeur de Hello tooreturn quand hello condition est vraie.</span><span class="sxs-lookup"><span data-stu-id="915ec-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="915ec-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="915ec-188">falseValue</span></span> |<span data-ttu-id="915ec-189">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-189">Yes</span></span> | <span data-ttu-id="915ec-190">chaîne, int, objet ou tableau</span><span class="sxs-lookup"><span data-stu-id="915ec-190">string, int, object, or array</span></span> |<span data-ttu-id="915ec-191">valeur de Hello tooreturn lorsque hello condition est false.</span><span class="sxs-lookup"><span data-stu-id="915ec-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="915ec-192">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="915ec-192">Return value</span></span>

<span data-ttu-id="915ec-193">Retourne le deuxième paramètre lorsque le premier paramètre est **True** ; sinon, retourne le troisième paramètre.</span><span class="sxs-lookup"><span data-stu-id="915ec-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="915ec-194">Remarques</span><span class="sxs-lookup"><span data-stu-id="915ec-194">Remarks</span></span>

<span data-ttu-id="915ec-195">Vous pouvez utiliser cet ensemble de tooconditionally de fonction à une propriété de ressource.</span><span class="sxs-lookup"><span data-stu-id="915ec-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="915ec-196">Hello suivant n’est pas un modèle complet, mais il montre les parties pertinentes d’hello pour la définition de manière conditionnelle hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="915ec-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="915ec-197">Exemples</span><span class="sxs-lookup"><span data-stu-id="915ec-197">Examples</span></span>

<span data-ttu-id="915ec-198">Hello suivant montre l’exemple de comment toouse hello `if` (fonction).</span><span class="sxs-lookup"><span data-stu-id="915ec-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="915ec-199">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915ec-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="915ec-200">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-200">Name</span></span> | <span data-ttu-id="915ec-201">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-201">Type</span></span> | <span data-ttu-id="915ec-202">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-203">yesOutput</span></span> | <span data-ttu-id="915ec-204">String</span><span class="sxs-lookup"><span data-stu-id="915ec-204">String</span></span> | <span data-ttu-id="915ec-205">yes</span><span class="sxs-lookup"><span data-stu-id="915ec-205">yes</span></span> |
| <span data-ttu-id="915ec-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-206">noOutput</span></span> | <span data-ttu-id="915ec-207">String</span><span class="sxs-lookup"><span data-stu-id="915ec-207">String</span></span> | <span data-ttu-id="915ec-208">no</span><span class="sxs-lookup"><span data-stu-id="915ec-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="915ec-209">not</span><span class="sxs-lookup"><span data-stu-id="915ec-209">not</span></span>
`not(arg1)`

<span data-ttu-id="915ec-210">Convertit la valeur booléenne tooits inverse la valeur.</span><span class="sxs-lookup"><span data-stu-id="915ec-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="915ec-211">Paramètres</span><span class="sxs-lookup"><span data-stu-id="915ec-211">Parameters</span></span>

| <span data-ttu-id="915ec-212">Paramètre</span><span class="sxs-lookup"><span data-stu-id="915ec-212">Parameter</span></span> | <span data-ttu-id="915ec-213">Requis</span><span class="sxs-lookup"><span data-stu-id="915ec-213">Required</span></span> | <span data-ttu-id="915ec-214">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-214">Type</span></span> | <span data-ttu-id="915ec-215">Description</span><span class="sxs-lookup"><span data-stu-id="915ec-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="915ec-216">arg1</span><span class="sxs-lookup"><span data-stu-id="915ec-216">arg1</span></span> |<span data-ttu-id="915ec-217">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-217">Yes</span></span> |<span data-ttu-id="915ec-218">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-218">boolean</span></span> |<span data-ttu-id="915ec-219">Hello tooconvert de valeur.</span><span class="sxs-lookup"><span data-stu-id="915ec-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="915ec-220">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="915ec-220">Return value</span></span>

<span data-ttu-id="915ec-221">Retourne **True** lorsque le paramètre est **False**.</span><span class="sxs-lookup"><span data-stu-id="915ec-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="915ec-222">Retourne **False** lorsque le paramètre est **True**.</span><span class="sxs-lookup"><span data-stu-id="915ec-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="915ec-223">Exemples</span><span class="sxs-lookup"><span data-stu-id="915ec-223">Examples</span></span>

<span data-ttu-id="915ec-224">Hello suivant montre l’exemple de comment toouse les fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="915ec-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="915ec-225">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915ec-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="915ec-226">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-226">Name</span></span> | <span data-ttu-id="915ec-227">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-227">Type</span></span> | <span data-ttu-id="915ec-228">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-229">andExampleOutput</span></span> | <span data-ttu-id="915ec-230">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-230">Bool</span></span> | <span data-ttu-id="915ec-231">False</span><span class="sxs-lookup"><span data-stu-id="915ec-231">False</span></span> |
| <span data-ttu-id="915ec-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-232">orExampleOutput</span></span> | <span data-ttu-id="915ec-233">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-233">Bool</span></span> | <span data-ttu-id="915ec-234">true</span><span class="sxs-lookup"><span data-stu-id="915ec-234">True</span></span> |
| <span data-ttu-id="915ec-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-235">notExampleOutput</span></span> | <span data-ttu-id="915ec-236">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-236">Bool</span></span> | <span data-ttu-id="915ec-237">False</span><span class="sxs-lookup"><span data-stu-id="915ec-237">False</span></span> |

<span data-ttu-id="915ec-238">Hello exemple suivant utilise **pas** avec [est égal à](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="915ec-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="915ec-239">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915ec-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="915ec-240">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-240">Name</span></span> | <span data-ttu-id="915ec-241">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-241">Type</span></span> | <span data-ttu-id="915ec-242">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="915ec-243">checkNotEquals</span></span> | <span data-ttu-id="915ec-244">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-244">Bool</span></span> | <span data-ttu-id="915ec-245">true</span><span class="sxs-lookup"><span data-stu-id="915ec-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="915ec-246">ou</span><span class="sxs-lookup"><span data-stu-id="915ec-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="915ec-247">Vérifie si l’une des valeurs du paramètre est true.</span><span class="sxs-lookup"><span data-stu-id="915ec-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="915ec-248">parameters</span><span class="sxs-lookup"><span data-stu-id="915ec-248">Parameters</span></span>

| <span data-ttu-id="915ec-249">Paramètre</span><span class="sxs-lookup"><span data-stu-id="915ec-249">Parameter</span></span> | <span data-ttu-id="915ec-250">Requis</span><span class="sxs-lookup"><span data-stu-id="915ec-250">Required</span></span> | <span data-ttu-id="915ec-251">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-251">Type</span></span> | <span data-ttu-id="915ec-252">Description</span><span class="sxs-lookup"><span data-stu-id="915ec-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="915ec-253">arg1</span><span class="sxs-lookup"><span data-stu-id="915ec-253">arg1</span></span> |<span data-ttu-id="915ec-254">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-254">Yes</span></span> |<span data-ttu-id="915ec-255">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-255">boolean</span></span> |<span data-ttu-id="915ec-256">Hello première valeur toocheck si a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="915ec-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="915ec-257">arg2</span><span class="sxs-lookup"><span data-stu-id="915ec-257">arg2</span></span> |<span data-ttu-id="915ec-258">Oui</span><span class="sxs-lookup"><span data-stu-id="915ec-258">Yes</span></span> |<span data-ttu-id="915ec-259">booléenne</span><span class="sxs-lookup"><span data-stu-id="915ec-259">boolean</span></span> |<span data-ttu-id="915ec-260">Hello deuxième valeur toocheck si a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="915ec-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="915ec-261">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="915ec-261">Return value</span></span>

<span data-ttu-id="915ec-262">Retourne **True** si la valeur est true ; sinon, **False**.</span><span class="sxs-lookup"><span data-stu-id="915ec-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="915ec-263">Exemples</span><span class="sxs-lookup"><span data-stu-id="915ec-263">Examples</span></span>

<span data-ttu-id="915ec-264">Hello suivant montre l’exemple de comment toouse les fonctions logiques.</span><span class="sxs-lookup"><span data-stu-id="915ec-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="915ec-265">est résultat Hello hello précédant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915ec-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="915ec-266">Nom</span><span class="sxs-lookup"><span data-stu-id="915ec-266">Name</span></span> | <span data-ttu-id="915ec-267">Type</span><span class="sxs-lookup"><span data-stu-id="915ec-267">Type</span></span> | <span data-ttu-id="915ec-268">Valeur</span><span class="sxs-lookup"><span data-stu-id="915ec-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="915ec-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-269">andExampleOutput</span></span> | <span data-ttu-id="915ec-270">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-270">Bool</span></span> | <span data-ttu-id="915ec-271">False</span><span class="sxs-lookup"><span data-stu-id="915ec-271">False</span></span> |
| <span data-ttu-id="915ec-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-272">orExampleOutput</span></span> | <span data-ttu-id="915ec-273">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-273">Bool</span></span> | <span data-ttu-id="915ec-274">true</span><span class="sxs-lookup"><span data-stu-id="915ec-274">True</span></span> |
| <span data-ttu-id="915ec-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="915ec-275">notExampleOutput</span></span> | <span data-ttu-id="915ec-276">Bool</span><span class="sxs-lookup"><span data-stu-id="915ec-276">Bool</span></span> | <span data-ttu-id="915ec-277">False</span><span class="sxs-lookup"><span data-stu-id="915ec-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="915ec-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="915ec-278">Next steps</span></span>
* <span data-ttu-id="915ec-279">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="915ec-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="915ec-280">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="915ec-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="915ec-281">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="915ec-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="915ec-282">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="915ec-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

