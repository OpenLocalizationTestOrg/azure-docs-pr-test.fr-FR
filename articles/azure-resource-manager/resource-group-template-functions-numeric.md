---
title: "aaaAzure Gestionnaire de ressources fonctions de modèle - numériques | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans un toowork de modèle Azure Resource Manager avec les nombres."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="cec4a-103">Fonctions numériques pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cec4a-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="cec4a-104">Gestionnaire de ressources fournit hello suivant des fonctions permettant de travailler avec des entiers :</span><span class="sxs-lookup"><span data-stu-id="cec4a-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="cec4a-105">ajouter</span><span class="sxs-lookup"><span data-stu-id="cec4a-105">add</span></span>](#add)
* [<span data-ttu-id="cec4a-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="cec4a-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="cec4a-107">div</span><span class="sxs-lookup"><span data-stu-id="cec4a-107">div</span></span>](#div)
* [<span data-ttu-id="cec4a-108">float</span><span class="sxs-lookup"><span data-stu-id="cec4a-108">float</span></span>](#float)
* [<span data-ttu-id="cec4a-109">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-109">int</span></span>](#int)
* [<span data-ttu-id="cec4a-110">min</span><span class="sxs-lookup"><span data-stu-id="cec4a-110">min</span></span>](#min)
* [<span data-ttu-id="cec4a-111">max</span><span class="sxs-lookup"><span data-stu-id="cec4a-111">max</span></span>](#max)
* [<span data-ttu-id="cec4a-112">mod</span><span class="sxs-lookup"><span data-stu-id="cec4a-112">mod</span></span>](#mod)
* [<span data-ttu-id="cec4a-113">mul</span><span class="sxs-lookup"><span data-stu-id="cec4a-113">mul</span></span>](#mul)
* [<span data-ttu-id="cec4a-114">sub</span><span class="sxs-lookup"><span data-stu-id="cec4a-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="cec4a-115">add</span><span class="sxs-lookup"><span data-stu-id="cec4a-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="cec4a-116">Retourne hello somme de deux entiers de fourni hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-117">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-117">Parameters</span></span>

| <span data-ttu-id="cec4a-118">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-118">Parameter</span></span> | <span data-ttu-id="cec4a-119">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-119">Required</span></span> | <span data-ttu-id="cec4a-120">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-120">Type</span></span> | <span data-ttu-id="cec4a-121">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="cec4a-122">operand1</span><span class="sxs-lookup"><span data-stu-id="cec4a-122">operand1</span></span> |<span data-ttu-id="cec4a-123">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-123">Yes</span></span> |<span data-ttu-id="cec4a-124">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-124">int</span></span> |<span data-ttu-id="cec4a-125">Nombre tooadd.</span><span class="sxs-lookup"><span data-stu-id="cec4a-125">First number tooadd.</span></span> |
|<span data-ttu-id="cec4a-126">operand2</span><span class="sxs-lookup"><span data-stu-id="cec4a-126">operand2</span></span> |<span data-ttu-id="cec4a-127">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-127">Yes</span></span> |<span data-ttu-id="cec4a-128">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-128">int</span></span> |<span data-ttu-id="cec4a-129">Deuxième nombre tooadd.</span><span class="sxs-lookup"><span data-stu-id="cec4a-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-130">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-130">Return value</span></span>

<span data-ttu-id="cec4a-131">Entier qui contient la somme de hello des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-132">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-132">Example</span></span>

<span data-ttu-id="cec4a-133">Bonjour à l’exemple suivant ajoute deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="cec4a-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

<span data-ttu-id="cec4a-134">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-135">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-135">Name</span></span> | <span data-ttu-id="cec4a-136">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-136">Type</span></span> | <span data-ttu-id="cec4a-137">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-138">addResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-138">addResult</span></span> | <span data-ttu-id="cec4a-139">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-139">Int</span></span> | <span data-ttu-id="cec4a-140">8</span><span class="sxs-lookup"><span data-stu-id="cec4a-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="cec4a-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="cec4a-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="cec4a-142">Retourne hello index d’une boucle d’itération.</span><span class="sxs-lookup"><span data-stu-id="cec4a-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="cec4a-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-143">Parameters</span></span>

| <span data-ttu-id="cec4a-144">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-144">Parameter</span></span> | <span data-ttu-id="cec4a-145">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-145">Required</span></span> | <span data-ttu-id="cec4a-146">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-146">Type</span></span> | <span data-ttu-id="cec4a-147">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-148">loopName</span><span class="sxs-lookup"><span data-stu-id="cec4a-148">loopName</span></span> | <span data-ttu-id="cec4a-149">Non</span><span class="sxs-lookup"><span data-stu-id="cec4a-149">No</span></span> | <span data-ttu-id="cec4a-150">string</span><span class="sxs-lookup"><span data-stu-id="cec4a-150">string</span></span> | <span data-ttu-id="cec4a-151">nom de Hello de boucle de hello pour l’obtention d’itération de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="cec4a-152">Offset</span><span class="sxs-lookup"><span data-stu-id="cec4a-152">offset</span></span> |<span data-ttu-id="cec4a-153">Non</span><span class="sxs-lookup"><span data-stu-id="cec4a-153">No</span></span> |<span data-ttu-id="cec4a-154">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-154">int</span></span> |<span data-ttu-id="cec4a-155">Hello tooadd toohello itération de base zéro valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="cec4a-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="cec4a-156">Remarques</span><span class="sxs-lookup"><span data-stu-id="cec4a-156">Remarks</span></span>

<span data-ttu-id="cec4a-157">Cette fonction est toujours utilisée avec un objet **copy** .</span><span class="sxs-lookup"><span data-stu-id="cec4a-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="cec4a-158">Si aucune valeur n’est fournie pour **offset**, valeur de l’itération actuelle hello est retourné.</span><span class="sxs-lookup"><span data-stu-id="cec4a-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="cec4a-159">valeur de l’itération Hello commence à zéro.</span><span class="sxs-lookup"><span data-stu-id="cec4a-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="cec4a-160">Hello **loopName** propriété vous permet de toospecify si copyIndex fait référence tooa ressource itération ou une itération de la propriété.</span><span class="sxs-lookup"><span data-stu-id="cec4a-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="cec4a-161">Si aucune valeur n’est fournie pour **loopName**, hello itération du type ressource actuelle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="cec4a-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="cec4a-162">Indiquez une valeur pour **loopName** lors de l’itération sur une propriété.</span><span class="sxs-lookup"><span data-stu-id="cec4a-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="cec4a-163">Pour obtenir une description complète d’exemples d’utilisation de l’expression **copyIndex**, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cec4a-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-164">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-164">Example</span></span>

<span data-ttu-id="cec4a-165">Hello suivant montre une boucle et hello index valeur copie incluse dans le nom de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="cec4a-166">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-166">Return value</span></span>

<span data-ttu-id="cec4a-167">Entier représentant l’index en cours de hello d’itération de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="cec4a-168">div</span><span class="sxs-lookup"><span data-stu-id="cec4a-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="cec4a-169">Retourne hello division d’entier de deux entiers de fourni hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-170">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-170">Parameters</span></span>

| <span data-ttu-id="cec4a-171">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-171">Parameter</span></span> | <span data-ttu-id="cec4a-172">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-172">Required</span></span> | <span data-ttu-id="cec4a-173">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-173">Type</span></span> | <span data-ttu-id="cec4a-174">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-175">operand1</span><span class="sxs-lookup"><span data-stu-id="cec4a-175">operand1</span></span> |<span data-ttu-id="cec4a-176">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-176">Yes</span></span> |<span data-ttu-id="cec4a-177">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-177">int</span></span> |<span data-ttu-id="cec4a-178">nombre de Hello est divisée.</span><span class="sxs-lookup"><span data-stu-id="cec4a-178">hello number being divided.</span></span> |
| <span data-ttu-id="cec4a-179">operand2</span><span class="sxs-lookup"><span data-stu-id="cec4a-179">operand2</span></span> |<span data-ttu-id="cec4a-180">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-180">Yes</span></span> |<span data-ttu-id="cec4a-181">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-181">int</span></span> |<span data-ttu-id="cec4a-182">nombre Hello toodivide utilisé.</span><span class="sxs-lookup"><span data-stu-id="cec4a-182">hello number that is used toodivide.</span></span> <span data-ttu-id="cec4a-183">Ne peut pas être 0.</span><span class="sxs-lookup"><span data-stu-id="cec4a-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-184">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-184">Return value</span></span>

<span data-ttu-id="cec4a-185">Une division hello représentant d’entier.</span><span class="sxs-lookup"><span data-stu-id="cec4a-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-186">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-186">Example</span></span>

<span data-ttu-id="cec4a-187">Bonjour à l’exemple suivant divise un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="cec4a-187">hello following example divides one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="cec4a-188">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-189">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-189">Name</span></span> | <span data-ttu-id="cec4a-190">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-190">Type</span></span> | <span data-ttu-id="cec4a-191">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-192">divResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-192">divResult</span></span> | <span data-ttu-id="cec4a-193">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-193">Int</span></span> | <span data-ttu-id="cec4a-194">2</span><span class="sxs-lookup"><span data-stu-id="cec4a-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="cec4a-195">float</span><span class="sxs-lookup"><span data-stu-id="cec4a-195">float</span></span>
`float(arg1)`

<span data-ttu-id="cec4a-196">Convertit tooa de valeur hello nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="cec4a-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="cec4a-197">Vous utilisez uniquement cette fonction lors du passage d’application tooan, par exemple une application de la logique des paramètres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cec4a-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-198">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-198">Parameters</span></span>

| <span data-ttu-id="cec4a-199">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-199">Parameter</span></span> | <span data-ttu-id="cec4a-200">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-200">Required</span></span> | <span data-ttu-id="cec4a-201">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-201">Type</span></span> | <span data-ttu-id="cec4a-202">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-203">arg1</span><span class="sxs-lookup"><span data-stu-id="cec4a-203">arg1</span></span> |<span data-ttu-id="cec4a-204">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-204">Yes</span></span> |<span data-ttu-id="cec4a-205">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="cec4a-205">string or int</span></span> |<span data-ttu-id="cec4a-206">Bonjour tooa tooconvert de valeur nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="cec4a-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-207">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-207">Return value</span></span>
<span data-ttu-id="cec4a-208">Nombre à virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="cec4a-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-209">Example</span></span>

<span data-ttu-id="cec4a-210">Bonjour à l’exemple suivant montre comment toouse float toopass paramètres tooa application logique :</span><span class="sxs-lookup"><span data-stu-id="cec4a-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="cec4a-211">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="cec4a-212">Convertit l’entier de tooan hello valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cec4a-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-213">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-213">Parameters</span></span>

| <span data-ttu-id="cec4a-214">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-214">Parameter</span></span> | <span data-ttu-id="cec4a-215">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-215">Required</span></span> | <span data-ttu-id="cec4a-216">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-216">Type</span></span> | <span data-ttu-id="cec4a-217">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="cec4a-218">valueToConvert</span></span> |<span data-ttu-id="cec4a-219">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-219">Yes</span></span> |<span data-ttu-id="cec4a-220">chaîne ou entier</span><span class="sxs-lookup"><span data-stu-id="cec4a-220">string or int</span></span> |<span data-ttu-id="cec4a-221">nombre entier tooan tooconvert valeur Hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-222">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-222">Return value</span></span>

<span data-ttu-id="cec4a-223">Nombre entier de valeur de hello converti.</span><span class="sxs-lookup"><span data-stu-id="cec4a-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-224">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-224">Example</span></span>

<span data-ttu-id="cec4a-225">Hello suivant convertit toointeger de valeur de paramètre fourni par l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="cec4a-226">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-227">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-227">Name</span></span> | <span data-ttu-id="cec4a-228">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-228">Type</span></span> | <span data-ttu-id="cec4a-229">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-230">intResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-230">intResult</span></span> | <span data-ttu-id="cec4a-231">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-231">Int</span></span> | <span data-ttu-id="cec4a-232">4</span><span class="sxs-lookup"><span data-stu-id="cec4a-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="cec4a-233">Min</span><span class="sxs-lookup"><span data-stu-id="cec4a-233">min</span></span>
`min (arg1)`

<span data-ttu-id="cec4a-234">Retourne hello valeur minimale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="cec4a-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-235">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-235">Parameters</span></span>

| <span data-ttu-id="cec4a-236">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-236">Parameter</span></span> | <span data-ttu-id="cec4a-237">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-237">Required</span></span> | <span data-ttu-id="cec4a-238">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-238">Type</span></span> | <span data-ttu-id="cec4a-239">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-240">arg1</span><span class="sxs-lookup"><span data-stu-id="cec4a-240">arg1</span></span> |<span data-ttu-id="cec4a-241">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-241">Yes</span></span> |<span data-ttu-id="cec4a-242">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="cec4a-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="cec4a-243">Hello collection tooget hello valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="cec4a-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-244">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-244">Return value</span></span>

<span data-ttu-id="cec4a-245">Entier représentant la valeur minimale à partir de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-246">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-246">Example</span></span>

<span data-ttu-id="cec4a-247">Hello suivant montre l’exemple de comment min toouse avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="cec4a-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="cec4a-248">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-249">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-249">Name</span></span> | <span data-ttu-id="cec4a-250">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-250">Type</span></span> | <span data-ttu-id="cec4a-251">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cec4a-252">arrayOutput</span></span> | <span data-ttu-id="cec4a-253">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-253">Int</span></span> | <span data-ttu-id="cec4a-254">0</span><span class="sxs-lookup"><span data-stu-id="cec4a-254">0</span></span> |
| <span data-ttu-id="cec4a-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="cec4a-255">intOutput</span></span> | <span data-ttu-id="cec4a-256">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-256">Int</span></span> | <span data-ttu-id="cec4a-257">0</span><span class="sxs-lookup"><span data-stu-id="cec4a-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="cec4a-258">max</span><span class="sxs-lookup"><span data-stu-id="cec4a-258">max</span></span>
`max (arg1)`

<span data-ttu-id="cec4a-259">Retourne hello valeur maximale à partir d’un tableau d’entiers ou une liste séparée par des virgules d’entiers.</span><span class="sxs-lookup"><span data-stu-id="cec4a-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-260">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-260">Parameters</span></span>

| <span data-ttu-id="cec4a-261">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-261">Parameter</span></span> | <span data-ttu-id="cec4a-262">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-262">Required</span></span> | <span data-ttu-id="cec4a-263">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-263">Type</span></span> | <span data-ttu-id="cec4a-264">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-265">arg1</span><span class="sxs-lookup"><span data-stu-id="cec4a-265">arg1</span></span> |<span data-ttu-id="cec4a-266">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-266">Yes</span></span> |<span data-ttu-id="cec4a-267">tableau d’entiers ou liste séparée par des virgules d’entiers</span><span class="sxs-lookup"><span data-stu-id="cec4a-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="cec4a-268">Hello collection tooget hello valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="cec4a-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-269">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-269">Return value</span></span>

<span data-ttu-id="cec4a-270">Entier représentant la valeur maximale de hello à partir de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-271">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-271">Example</span></span>

<span data-ttu-id="cec4a-272">Hello suivant montre l’exemple de comment toouse max avec un tableau et une liste d’entiers :</span><span class="sxs-lookup"><span data-stu-id="cec4a-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="cec4a-273">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-274">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-274">Name</span></span> | <span data-ttu-id="cec4a-275">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-275">Type</span></span> | <span data-ttu-id="cec4a-276">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cec4a-277">arrayOutput</span></span> | <span data-ttu-id="cec4a-278">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-278">Int</span></span> | <span data-ttu-id="cec4a-279">5</span><span class="sxs-lookup"><span data-stu-id="cec4a-279">5</span></span> |
| <span data-ttu-id="cec4a-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="cec4a-280">intOutput</span></span> | <span data-ttu-id="cec4a-281">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-281">Int</span></span> | <span data-ttu-id="cec4a-282">5</span><span class="sxs-lookup"><span data-stu-id="cec4a-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="cec4a-283">mod</span><span class="sxs-lookup"><span data-stu-id="cec4a-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="cec4a-284">Retourne le reste hello de division d’entier hello hello sur deux entiers fourni.</span><span class="sxs-lookup"><span data-stu-id="cec4a-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-285">Parameters</span></span>

| <span data-ttu-id="cec4a-286">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-286">Parameter</span></span> | <span data-ttu-id="cec4a-287">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-287">Required</span></span> | <span data-ttu-id="cec4a-288">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-288">Type</span></span> | <span data-ttu-id="cec4a-289">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-290">operand1</span><span class="sxs-lookup"><span data-stu-id="cec4a-290">operand1</span></span> |<span data-ttu-id="cec4a-291">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-291">Yes</span></span> |<span data-ttu-id="cec4a-292">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-292">int</span></span> |<span data-ttu-id="cec4a-293">nombre de Hello est divisée.</span><span class="sxs-lookup"><span data-stu-id="cec4a-293">hello number being divided.</span></span> |
| <span data-ttu-id="cec4a-294">operand2</span><span class="sxs-lookup"><span data-stu-id="cec4a-294">operand2</span></span> |<span data-ttu-id="cec4a-295">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-295">Yes</span></span> |<span data-ttu-id="cec4a-296">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-296">int</span></span> |<span data-ttu-id="cec4a-297">numéro de Hello toodivide utilisé, ne peut pas être 0.</span><span class="sxs-lookup"><span data-stu-id="cec4a-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-298">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-298">Return value</span></span>
<span data-ttu-id="cec4a-299">Un modulo entier représentant hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-300">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-300">Example</span></span>

<span data-ttu-id="cec4a-301">Hello exemple ci-dessous retourne reste hello de la division d’un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="cec4a-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="cec4a-302">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-303">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-303">Name</span></span> | <span data-ttu-id="cec4a-304">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-304">Type</span></span> | <span data-ttu-id="cec4a-305">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-306">modResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-306">modResult</span></span> | <span data-ttu-id="cec4a-307">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-307">Int</span></span> | <span data-ttu-id="cec4a-308">1</span><span class="sxs-lookup"><span data-stu-id="cec4a-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="cec4a-309">mul</span><span class="sxs-lookup"><span data-stu-id="cec4a-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="cec4a-310">Retourne hello multiplication de deux entiers de fourni hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-311">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-311">Parameters</span></span>

| <span data-ttu-id="cec4a-312">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-312">Parameter</span></span> | <span data-ttu-id="cec4a-313">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-313">Required</span></span> | <span data-ttu-id="cec4a-314">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-314">Type</span></span> | <span data-ttu-id="cec4a-315">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-316">operand1</span><span class="sxs-lookup"><span data-stu-id="cec4a-316">operand1</span></span> |<span data-ttu-id="cec4a-317">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-317">Yes</span></span> |<span data-ttu-id="cec4a-318">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-318">int</span></span> |<span data-ttu-id="cec4a-319">Nombre toomultiply.</span><span class="sxs-lookup"><span data-stu-id="cec4a-319">First number toomultiply.</span></span> |
| <span data-ttu-id="cec4a-320">operand2</span><span class="sxs-lookup"><span data-stu-id="cec4a-320">operand2</span></span> |<span data-ttu-id="cec4a-321">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-321">Yes</span></span> |<span data-ttu-id="cec4a-322">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-322">int</span></span> |<span data-ttu-id="cec4a-323">Deuxième nombre toomultiply.</span><span class="sxs-lookup"><span data-stu-id="cec4a-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-324">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-324">Return value</span></span>

<span data-ttu-id="cec4a-325">Une entier représentant hello la multiplication.</span><span class="sxs-lookup"><span data-stu-id="cec4a-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-326">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-326">Example</span></span>

<span data-ttu-id="cec4a-327">Bonjour à l’exemple suivant multiplie un paramètre par un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="cec4a-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

<span data-ttu-id="cec4a-328">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-329">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-329">Name</span></span> | <span data-ttu-id="cec4a-330">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-330">Type</span></span> | <span data-ttu-id="cec4a-331">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-332">mulResult</span></span> | <span data-ttu-id="cec4a-333">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-333">Int</span></span> | <span data-ttu-id="cec4a-334">15</span><span class="sxs-lookup"><span data-stu-id="cec4a-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="cec4a-335">sub</span><span class="sxs-lookup"><span data-stu-id="cec4a-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="cec4a-336">Retourne hello soustraction de deux entiers de fourni hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec4a-337">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cec4a-337">Parameters</span></span>

| <span data-ttu-id="cec4a-338">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cec4a-338">Parameter</span></span> | <span data-ttu-id="cec4a-339">Requis</span><span class="sxs-lookup"><span data-stu-id="cec4a-339">Required</span></span> | <span data-ttu-id="cec4a-340">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-340">Type</span></span> | <span data-ttu-id="cec4a-341">Description</span><span class="sxs-lookup"><span data-stu-id="cec4a-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cec4a-342">operand1</span><span class="sxs-lookup"><span data-stu-id="cec4a-342">operand1</span></span> |<span data-ttu-id="cec4a-343">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-343">Yes</span></span> |<span data-ttu-id="cec4a-344">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-344">int</span></span> |<span data-ttu-id="cec4a-345">nombre de Hello est soustraite.</span><span class="sxs-lookup"><span data-stu-id="cec4a-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="cec4a-346">operand2</span><span class="sxs-lookup"><span data-stu-id="cec4a-346">operand2</span></span> |<span data-ttu-id="cec4a-347">Oui</span><span class="sxs-lookup"><span data-stu-id="cec4a-347">Yes</span></span> |<span data-ttu-id="cec4a-348">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-348">int</span></span> |<span data-ttu-id="cec4a-349">nombre de Hello est soustrait.</span><span class="sxs-lookup"><span data-stu-id="cec4a-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cec4a-350">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="cec4a-350">Return value</span></span>
<span data-ttu-id="cec4a-351">Une soustraction entier représentant hello.</span><span class="sxs-lookup"><span data-stu-id="cec4a-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="cec4a-352">Exemple</span><span class="sxs-lookup"><span data-stu-id="cec4a-352">Example</span></span>

<span data-ttu-id="cec4a-353">Bonjour à l’exemple suivant soustrait un paramètre à partir d’un autre paramètre.</span><span class="sxs-lookup"><span data-stu-id="cec4a-353">hello following example subtracts one parameter from another parameter.</span></span>

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
                "description": "Integer toosubtract"
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

<span data-ttu-id="cec4a-354">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="cec4a-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cec4a-355">Nom</span><span class="sxs-lookup"><span data-stu-id="cec4a-355">Name</span></span> | <span data-ttu-id="cec4a-356">Type</span><span class="sxs-lookup"><span data-stu-id="cec4a-356">Type</span></span> | <span data-ttu-id="cec4a-357">Valeur</span><span class="sxs-lookup"><span data-stu-id="cec4a-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cec4a-358">subResult</span><span class="sxs-lookup"><span data-stu-id="cec4a-358">subResult</span></span> | <span data-ttu-id="cec4a-359">int</span><span class="sxs-lookup"><span data-stu-id="cec4a-359">Int</span></span> | <span data-ttu-id="cec4a-360">4</span><span class="sxs-lookup"><span data-stu-id="cec4a-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cec4a-361">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cec4a-361">Next steps</span></span>
* <span data-ttu-id="cec4a-362">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cec4a-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="cec4a-363">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cec4a-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="cec4a-364">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cec4a-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="cec4a-365">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cec4a-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

