---
title: "Fonctions de modèle Azure Resource Manager - numérique| Microsoft Docs"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour travailler avec des nombres."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="3f922-103">Fonctions numériques pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f922-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="3f922-104">Resource Manager fournit les expressions ci-après pour travailler avec des entiers :</span><span class="sxs-lookup"><span data-stu-id="3f922-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="3f922-105">ajouter</span><span class="sxs-lookup"><span data-stu-id="3f922-105">add</span></span>](#add)
* [<span data-ttu-id="3f922-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="3f922-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="3f922-107">div</span><span class="sxs-lookup"><span data-stu-id="3f922-107">div</span></span>](#div)
* [<span data-ttu-id="3f922-108">float</span><span class="sxs-lookup"><span data-stu-id="3f922-108">float</span></span>](#float)
* [<span data-ttu-id="3f922-109">int</span><span class="sxs-lookup"><span data-stu-id="3f922-109">int</span></span>](#int)
* [<span data-ttu-id="3f922-110">min</span><span class="sxs-lookup"><span data-stu-id="3f922-110">min</span></span>](#min)
* [<span data-ttu-id="3f922-111">max</span><span class="sxs-lookup"><span data-stu-id="3f922-111">max</span></span>](#max)
* [<span data-ttu-id="3f922-112">mod</span><span class="sxs-lookup"><span data-stu-id="3f922-112">mod</span></span>](#mod)
* [<span data-ttu-id="3f922-113">mul</span><span class="sxs-lookup"><span data-stu-id="3f922-113">mul</span></span>](#mul)
* [<span data-ttu-id="3f922-114">sub</span><span class="sxs-lookup"><span data-stu-id="3f922-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="3f922-115">ajouter</span><span class="sxs-lookup"><span data-stu-id="3f922-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="3f922-116">Retourne la somme des deux entiers fournis.</span><span class="sxs-lookup"><span data-stu-id="3f922-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-117">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-117">Parameters</span></span>

| <span data-ttu-id="3f922-118">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-118">Parameter</span></span> | <span data-ttu-id="3f922-119">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-119">Required</span></span> | <span data-ttu-id="3f922-120">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-120">Type</span></span> | <span data-ttu-id="3f922-121">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="3f922-122">operand1</span><span class="sxs-lookup"><span data-stu-id="3f922-122">operand1</span></span> |<span data-ttu-id="3f922-123">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-123">Yes</span></span> |<span data-ttu-id="3f922-124">int</span><span class="sxs-lookup"><span data-stu-id="3f922-124">int</span></span> |<span data-ttu-id="3f922-125">Premier nombre à ajouter.</span><span class="sxs-lookup"><span data-stu-id="3f922-125">First number to add.</span></span> |
|<span data-ttu-id="3f922-126">operand2</span><span class="sxs-lookup"><span data-stu-id="3f922-126">operand2</span></span> |<span data-ttu-id="3f922-127">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-127">Yes</span></span> |<span data-ttu-id="3f922-128">int</span><span class="sxs-lookup"><span data-stu-id="3f922-128">int</span></span> |<span data-ttu-id="3f922-129">Deuxième nombre à ajouter.</span><span class="sxs-lookup"><span data-stu-id="3f922-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-130">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-130">Return value</span></span>

<span data-ttu-id="3f922-131">Entier qui contient la somme des paramètres.</span><span class="sxs-lookup"><span data-stu-id="3f922-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-132">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-132">Example</span></span>

<span data-ttu-id="3f922-133">L’exemple suivant ajoute deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="3f922-133">The following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="3f922-134">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-135">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-135">Name</span></span> | <span data-ttu-id="3f922-136">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-136">Type</span></span> | <span data-ttu-id="3f922-137">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-138">addResult</span><span class="sxs-lookup"><span data-stu-id="3f922-138">addResult</span></span> | <span data-ttu-id="3f922-139">int</span><span class="sxs-lookup"><span data-stu-id="3f922-139">Int</span></span> | <span data-ttu-id="3f922-140">8</span><span class="sxs-lookup"><span data-stu-id="3f922-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="3f922-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="3f922-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="3f922-142">Retourne l’index d’une boucle d’itération.</span><span class="sxs-lookup"><span data-stu-id="3f922-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="3f922-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-143">Parameters</span></span>

| <span data-ttu-id="3f922-144">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-144">Parameter</span></span> | <span data-ttu-id="3f922-145">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-145">Required</span></span> | <span data-ttu-id="3f922-146">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-146">Type</span></span> | <span data-ttu-id="3f922-147">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-148">loopName</span><span class="sxs-lookup"><span data-stu-id="3f922-148">loopName</span></span> | <span data-ttu-id="3f922-149">Non</span><span class="sxs-lookup"><span data-stu-id="3f922-149">No</span></span> | <span data-ttu-id="3f922-150">string</span><span class="sxs-lookup"><span data-stu-id="3f922-150">string</span></span> | <span data-ttu-id="3f922-151">Nom de la boucle pour l’obtention de l’itération.</span><span class="sxs-lookup"><span data-stu-id="3f922-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="3f922-152">Offset</span><span class="sxs-lookup"><span data-stu-id="3f922-152">offset</span></span> |<span data-ttu-id="3f922-153">Non</span><span class="sxs-lookup"><span data-stu-id="3f922-153">No</span></span> |<span data-ttu-id="3f922-154">int</span><span class="sxs-lookup"><span data-stu-id="3f922-154">int</span></span> |<span data-ttu-id="3f922-155">Le nombre à ajouter à la valeur d’itération de base zéro.</span><span class="sxs-lookup"><span data-stu-id="3f922-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="3f922-156">Remarques</span><span class="sxs-lookup"><span data-stu-id="3f922-156">Remarks</span></span>

<span data-ttu-id="3f922-157">Cette fonction est toujours utilisée avec un objet **copy** .</span><span class="sxs-lookup"><span data-stu-id="3f922-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="3f922-158">Si aucune valeur n’est fournie pour **offset**, la valeur d’itération actuelle est retournée.</span><span class="sxs-lookup"><span data-stu-id="3f922-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="3f922-159">La valeur d’itération commence à zéro.</span><span class="sxs-lookup"><span data-stu-id="3f922-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="3f922-160">La propriété **loopName** permet d’indiquer si copyIndex fait référence à une itération de ressource ou de propriété.</span><span class="sxs-lookup"><span data-stu-id="3f922-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="3f922-161">Si aucune valeur n’est indiquée pour **loopName**, l’itération du type de ressource actuelle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="3f922-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="3f922-162">Indiquez une valeur pour **loopName** lors de l’itération sur une propriété.</span><span class="sxs-lookup"><span data-stu-id="3f922-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="3f922-163">Pour obtenir une description complète d’exemples d’utilisation de l’expression **copyIndex**, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3f922-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="3f922-164">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-164">Example</span></span>

<span data-ttu-id="3f922-165">L’exemple suivant montre une boucle de copie ainsi que la valeur d’index incluse dans le nom.</span><span class="sxs-lookup"><span data-stu-id="3f922-165">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="3f922-166">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-166">Return value</span></span>

<span data-ttu-id="3f922-167">Entier représentant l’index actuel de l’itération.</span><span class="sxs-lookup"><span data-stu-id="3f922-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="3f922-168">div</span><span class="sxs-lookup"><span data-stu-id="3f922-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="3f922-169">Retourne la division entière des deux entiers fournis.</span><span class="sxs-lookup"><span data-stu-id="3f922-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-170">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-170">Parameters</span></span>

| <span data-ttu-id="3f922-171">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-171">Parameter</span></span> | <span data-ttu-id="3f922-172">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-172">Required</span></span> | <span data-ttu-id="3f922-173">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-173">Type</span></span> | <span data-ttu-id="3f922-174">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-175">operand1</span><span class="sxs-lookup"><span data-stu-id="3f922-175">operand1</span></span> |<span data-ttu-id="3f922-176">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-176">Yes</span></span> |<span data-ttu-id="3f922-177">int</span><span class="sxs-lookup"><span data-stu-id="3f922-177">int</span></span> |<span data-ttu-id="3f922-178">Le nombre à diviser.</span><span class="sxs-lookup"><span data-stu-id="3f922-178">The number being divided.</span></span> |
| <span data-ttu-id="3f922-179">operand2</span><span class="sxs-lookup"><span data-stu-id="3f922-179">operand2</span></span> |<span data-ttu-id="3f922-180">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-180">Yes</span></span> |<span data-ttu-id="3f922-181">int</span><span class="sxs-lookup"><span data-stu-id="3f922-181">int</span></span> |<span data-ttu-id="3f922-182">Le nombre utilisé pour diviser.</span><span class="sxs-lookup"><span data-stu-id="3f922-182">The number that is used to divide.</span></span> <span data-ttu-id="3f922-183">Ne peut pas être 0.</span><span class="sxs-lookup"><span data-stu-id="3f922-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-184">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-184">Return value</span></span>

<span data-ttu-id="3f922-185">Entier représentant la division.</span><span class="sxs-lookup"><span data-stu-id="3f922-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-186">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-186">Example</span></span>

<span data-ttu-id="3f922-187">L’exemple suivant divise un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="3f922-187">The following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="3f922-188">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-189">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-189">Name</span></span> | <span data-ttu-id="3f922-190">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-190">Type</span></span> | <span data-ttu-id="3f922-191">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-192">divResult</span><span class="sxs-lookup"><span data-stu-id="3f922-192">divResult</span></span> | <span data-ttu-id="3f922-193">int</span><span class="sxs-lookup"><span data-stu-id="3f922-193">Int</span></span> | <span data-ttu-id="3f922-194">2</span><span class="sxs-lookup"><span data-stu-id="3f922-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="3f922-195">float</span><span class="sxs-lookup"><span data-stu-id="3f922-195">float</span></span>
`float(arg1)`

<span data-ttu-id="3f922-196">Convertit la valeur en nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="3f922-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="3f922-197">Vous utilisez uniquement cette fonction lors de la transmission de paramètres personnalisés à une application, telle qu’une application logique.</span><span class="sxs-lookup"><span data-stu-id="3f922-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-198">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-198">Parameters</span></span>

| <span data-ttu-id="3f922-199">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-199">Parameter</span></span> | <span data-ttu-id="3f922-200">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-200">Required</span></span> | <span data-ttu-id="3f922-201">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-201">Type</span></span> | <span data-ttu-id="3f922-202">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-203">arg1</span><span class="sxs-lookup"><span data-stu-id="3f922-203">arg1</span></span> |<span data-ttu-id="3f922-204">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-204">Yes</span></span> |<span data-ttu-id="3f922-205">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="3f922-205">string or int</span></span> |<span data-ttu-id="3f922-206">Valeur à convertir en nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="3f922-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-207">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-207">Return value</span></span>
<span data-ttu-id="3f922-208">Nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="3f922-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-209">Example</span></span>

<span data-ttu-id="3f922-210">L’exemple suivant montre comment utiliser float pour passer des paramètres à une application logique :</span><span class="sxs-lookup"><span data-stu-id="3f922-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="3f922-211">int</span><span class="sxs-lookup"><span data-stu-id="3f922-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="3f922-212">Convertit la valeur spécifiée en entier.</span><span class="sxs-lookup"><span data-stu-id="3f922-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-213">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-213">Parameters</span></span>

| <span data-ttu-id="3f922-214">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-214">Parameter</span></span> | <span data-ttu-id="3f922-215">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-215">Required</span></span> | <span data-ttu-id="3f922-216">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-216">Type</span></span> | <span data-ttu-id="3f922-217">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="3f922-218">valueToConvert</span></span> |<span data-ttu-id="3f922-219">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-219">Yes</span></span> |<span data-ttu-id="3f922-220">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="3f922-220">string or int</span></span> |<span data-ttu-id="3f922-221">La valeur à convertir en entier.</span><span class="sxs-lookup"><span data-stu-id="3f922-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-222">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-222">Return value</span></span>

<span data-ttu-id="3f922-223">Nombre entier de la valeur convertie.</span><span class="sxs-lookup"><span data-stu-id="3f922-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-224">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-224">Example</span></span>

<span data-ttu-id="3f922-225">L’exemple ci-après convertit la valeur de paramètre fournie par l’utilisateur en entier.</span><span class="sxs-lookup"><span data-stu-id="3f922-225">The following example converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="3f922-226">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-227">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-227">Name</span></span> | <span data-ttu-id="3f922-228">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-228">Type</span></span> | <span data-ttu-id="3f922-229">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-230">intResult</span><span class="sxs-lookup"><span data-stu-id="3f922-230">intResult</span></span> | <span data-ttu-id="3f922-231">int</span><span class="sxs-lookup"><span data-stu-id="3f922-231">Int</span></span> | <span data-ttu-id="3f922-232">4</span><span class="sxs-lookup"><span data-stu-id="3f922-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="3f922-233">min</span><span class="sxs-lookup"><span data-stu-id="3f922-233">min</span></span>
`min (arg1)`

<span data-ttu-id="3f922-234">Retourne la valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="3f922-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-235">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-235">Parameters</span></span>

| <span data-ttu-id="3f922-236">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-236">Parameter</span></span> | <span data-ttu-id="3f922-237">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-237">Required</span></span> | <span data-ttu-id="3f922-238">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-238">Type</span></span> | <span data-ttu-id="3f922-239">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-240">arg1</span><span class="sxs-lookup"><span data-stu-id="3f922-240">arg1</span></span> |<span data-ttu-id="3f922-241">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-241">Yes</span></span> |<span data-ttu-id="3f922-242">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="3f922-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="3f922-243">Collection permettant d’obtenir la valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="3f922-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-244">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-244">Return value</span></span>

<span data-ttu-id="3f922-245">Entier représentant la valeur minimale de la collection.</span><span class="sxs-lookup"><span data-stu-id="3f922-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-246">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-246">Example</span></span>

<span data-ttu-id="3f922-247">L’exemple suivant indique comment utiliser la fonction min avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="3f922-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="3f922-248">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-249">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-249">Name</span></span> | <span data-ttu-id="3f922-250">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-250">Type</span></span> | <span data-ttu-id="3f922-251">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="3f922-252">arrayOutput</span></span> | <span data-ttu-id="3f922-253">int</span><span class="sxs-lookup"><span data-stu-id="3f922-253">Int</span></span> | <span data-ttu-id="3f922-254">0</span><span class="sxs-lookup"><span data-stu-id="3f922-254">0</span></span> |
| <span data-ttu-id="3f922-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="3f922-255">intOutput</span></span> | <span data-ttu-id="3f922-256">int</span><span class="sxs-lookup"><span data-stu-id="3f922-256">Int</span></span> | <span data-ttu-id="3f922-257">0</span><span class="sxs-lookup"><span data-stu-id="3f922-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="3f922-258">max</span><span class="sxs-lookup"><span data-stu-id="3f922-258">max</span></span>
`max (arg1)`

<span data-ttu-id="3f922-259">Retourne la valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="3f922-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-260">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-260">Parameters</span></span>

| <span data-ttu-id="3f922-261">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-261">Parameter</span></span> | <span data-ttu-id="3f922-262">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-262">Required</span></span> | <span data-ttu-id="3f922-263">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-263">Type</span></span> | <span data-ttu-id="3f922-264">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-265">arg1</span><span class="sxs-lookup"><span data-stu-id="3f922-265">arg1</span></span> |<span data-ttu-id="3f922-266">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-266">Yes</span></span> |<span data-ttu-id="3f922-267">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="3f922-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="3f922-268">Collection permettant d’obtenir la valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="3f922-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-269">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-269">Return value</span></span>

<span data-ttu-id="3f922-270">Entier représentant la valeur maximale de la collection.</span><span class="sxs-lookup"><span data-stu-id="3f922-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-271">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-271">Example</span></span>

<span data-ttu-id="3f922-272">L’exemple suivant montre comment utiliser max avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="3f922-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="3f922-273">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-274">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-274">Name</span></span> | <span data-ttu-id="3f922-275">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-275">Type</span></span> | <span data-ttu-id="3f922-276">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="3f922-277">arrayOutput</span></span> | <span data-ttu-id="3f922-278">int</span><span class="sxs-lookup"><span data-stu-id="3f922-278">Int</span></span> | <span data-ttu-id="3f922-279">5</span><span class="sxs-lookup"><span data-stu-id="3f922-279">5</span></span> |
| <span data-ttu-id="3f922-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="3f922-280">intOutput</span></span> | <span data-ttu-id="3f922-281">int</span><span class="sxs-lookup"><span data-stu-id="3f922-281">Int</span></span> | <span data-ttu-id="3f922-282">5</span><span class="sxs-lookup"><span data-stu-id="3f922-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="3f922-283">mod</span><span class="sxs-lookup"><span data-stu-id="3f922-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="3f922-284">Retourne le reste de la division entière des deux entiers fournis.</span><span class="sxs-lookup"><span data-stu-id="3f922-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-285">Parameters</span></span>

| <span data-ttu-id="3f922-286">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-286">Parameter</span></span> | <span data-ttu-id="3f922-287">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-287">Required</span></span> | <span data-ttu-id="3f922-288">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-288">Type</span></span> | <span data-ttu-id="3f922-289">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-290">operand1</span><span class="sxs-lookup"><span data-stu-id="3f922-290">operand1</span></span> |<span data-ttu-id="3f922-291">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-291">Yes</span></span> |<span data-ttu-id="3f922-292">int</span><span class="sxs-lookup"><span data-stu-id="3f922-292">int</span></span> |<span data-ttu-id="3f922-293">Le nombre à diviser.</span><span class="sxs-lookup"><span data-stu-id="3f922-293">The number being divided.</span></span> |
| <span data-ttu-id="3f922-294">operand2</span><span class="sxs-lookup"><span data-stu-id="3f922-294">operand2</span></span> |<span data-ttu-id="3f922-295">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-295">Yes</span></span> |<span data-ttu-id="3f922-296">int</span><span class="sxs-lookup"><span data-stu-id="3f922-296">int</span></span> |<span data-ttu-id="3f922-297">Le nombre utilisé pour diviser, Ne peut pas être 0.</span><span class="sxs-lookup"><span data-stu-id="3f922-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-298">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-298">Return value</span></span>
<span data-ttu-id="3f922-299">Entier représentant le reste.</span><span class="sxs-lookup"><span data-stu-id="3f922-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-300">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-300">Example</span></span>

<span data-ttu-id="3f922-301">L’exemple suivant renvoie le reste de la division d’un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="3f922-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="3f922-302">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-303">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-303">Name</span></span> | <span data-ttu-id="3f922-304">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-304">Type</span></span> | <span data-ttu-id="3f922-305">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-306">modResult</span><span class="sxs-lookup"><span data-stu-id="3f922-306">modResult</span></span> | <span data-ttu-id="3f922-307">int</span><span class="sxs-lookup"><span data-stu-id="3f922-307">Int</span></span> | <span data-ttu-id="3f922-308">1</span><span class="sxs-lookup"><span data-stu-id="3f922-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="3f922-309">mul</span><span class="sxs-lookup"><span data-stu-id="3f922-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="3f922-310">Retourne la multiplication des deux entiers fournis.</span><span class="sxs-lookup"><span data-stu-id="3f922-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-311">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-311">Parameters</span></span>

| <span data-ttu-id="3f922-312">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-312">Parameter</span></span> | <span data-ttu-id="3f922-313">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-313">Required</span></span> | <span data-ttu-id="3f922-314">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-314">Type</span></span> | <span data-ttu-id="3f922-315">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-316">operand1</span><span class="sxs-lookup"><span data-stu-id="3f922-316">operand1</span></span> |<span data-ttu-id="3f922-317">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-317">Yes</span></span> |<span data-ttu-id="3f922-318">int</span><span class="sxs-lookup"><span data-stu-id="3f922-318">int</span></span> |<span data-ttu-id="3f922-319">Premier nombre à multiplier.</span><span class="sxs-lookup"><span data-stu-id="3f922-319">First number to multiply.</span></span> |
| <span data-ttu-id="3f922-320">operand2</span><span class="sxs-lookup"><span data-stu-id="3f922-320">operand2</span></span> |<span data-ttu-id="3f922-321">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-321">Yes</span></span> |<span data-ttu-id="3f922-322">int</span><span class="sxs-lookup"><span data-stu-id="3f922-322">int</span></span> |<span data-ttu-id="3f922-323">Deuxième nombre à multiplier.</span><span class="sxs-lookup"><span data-stu-id="3f922-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-324">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-324">Return value</span></span>

<span data-ttu-id="3f922-325">Entier représentant la multiplication.</span><span class="sxs-lookup"><span data-stu-id="3f922-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-326">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-326">Example</span></span>

<span data-ttu-id="3f922-327">L’exemple suivant multiplie un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="3f922-327">The following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="3f922-328">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-329">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-329">Name</span></span> | <span data-ttu-id="3f922-330">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-330">Type</span></span> | <span data-ttu-id="3f922-331">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="3f922-332">mulResult</span></span> | <span data-ttu-id="3f922-333">int</span><span class="sxs-lookup"><span data-stu-id="3f922-333">Int</span></span> | <span data-ttu-id="3f922-334">15</span><span class="sxs-lookup"><span data-stu-id="3f922-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="3f922-335">sub</span><span class="sxs-lookup"><span data-stu-id="3f922-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="3f922-336">Retourne la soustraction des deux entiers fournis.</span><span class="sxs-lookup"><span data-stu-id="3f922-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="3f922-337">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f922-337">Parameters</span></span>

| <span data-ttu-id="3f922-338">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3f922-338">Parameter</span></span> | <span data-ttu-id="3f922-339">Requis</span><span class="sxs-lookup"><span data-stu-id="3f922-339">Required</span></span> | <span data-ttu-id="3f922-340">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-340">Type</span></span> | <span data-ttu-id="3f922-341">Description</span><span class="sxs-lookup"><span data-stu-id="3f922-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3f922-342">operand1</span><span class="sxs-lookup"><span data-stu-id="3f922-342">operand1</span></span> |<span data-ttu-id="3f922-343">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-343">Yes</span></span> |<span data-ttu-id="3f922-344">int</span><span class="sxs-lookup"><span data-stu-id="3f922-344">int</span></span> |<span data-ttu-id="3f922-345">Le nombre auquel est appliquée la soustraction.</span><span class="sxs-lookup"><span data-stu-id="3f922-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="3f922-346">operand2</span><span class="sxs-lookup"><span data-stu-id="3f922-346">operand2</span></span> |<span data-ttu-id="3f922-347">Oui</span><span class="sxs-lookup"><span data-stu-id="3f922-347">Yes</span></span> |<span data-ttu-id="3f922-348">int</span><span class="sxs-lookup"><span data-stu-id="3f922-348">int</span></span> |<span data-ttu-id="3f922-349">Le nombre qui est soustrait.</span><span class="sxs-lookup"><span data-stu-id="3f922-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3f922-350">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="3f922-350">Return value</span></span>
<span data-ttu-id="3f922-351">Entier représentant la multiplication.</span><span class="sxs-lookup"><span data-stu-id="3f922-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="3f922-352">Exemple</span><span class="sxs-lookup"><span data-stu-id="3f922-352">Example</span></span>

<span data-ttu-id="3f922-353">L’exemple suivant soustrait un paramètre à un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="3f922-353">The following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="3f922-354">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f922-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="3f922-355">Nom</span><span class="sxs-lookup"><span data-stu-id="3f922-355">Name</span></span> | <span data-ttu-id="3f922-356">Type</span><span class="sxs-lookup"><span data-stu-id="3f922-356">Type</span></span> | <span data-ttu-id="3f922-357">Valeur</span><span class="sxs-lookup"><span data-stu-id="3f922-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3f922-358">subResult</span><span class="sxs-lookup"><span data-stu-id="3f922-358">subResult</span></span> | <span data-ttu-id="3f922-359">int</span><span class="sxs-lookup"><span data-stu-id="3f922-359">Int</span></span> | <span data-ttu-id="3f922-360">4</span><span class="sxs-lookup"><span data-stu-id="3f922-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f922-361">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f922-361">Next steps</span></span>
* <span data-ttu-id="3f922-362">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3f922-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3f922-363">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3f922-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="3f922-364">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3f922-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="3f922-365">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3f922-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

