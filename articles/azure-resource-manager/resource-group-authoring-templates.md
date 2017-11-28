---
title: "Structure et syntaxe du modèle Azure Resource Manager | Microsoft Docs"
description: "Décrit la structure et les propriétés des modèles Azure Resource Manager à l’aide de la syntaxe JSON déclarative."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="8d78c-103">Comprendre la structure et la syntaxe des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d78c-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="8d78c-104">Cette rubrique décrit la structure d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d78c-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="8d78c-105">Elle présente les différentes sections d’un modèle et les propriétés disponibles dans ces sections.</span><span class="sxs-lookup"><span data-stu-id="8d78c-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="8d78c-106">Le modèle se compose d’un JSON et d’expressions que vous pouvez utiliser pour construire des valeurs pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="8d78c-107">Pour obtenir un didacticiel étape par étape permettant de créer un modèle, voir [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="8d78c-108">Format de modèle</span><span class="sxs-lookup"><span data-stu-id="8d78c-108">Template format</span></span>
<span data-ttu-id="8d78c-109">Dans sa structure la plus simple, un modèle contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8d78c-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="8d78c-110">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="8d78c-110">Element name</span></span> | <span data-ttu-id="8d78c-111">Requis</span><span class="sxs-lookup"><span data-stu-id="8d78c-111">Required</span></span> | <span data-ttu-id="8d78c-112">Description</span><span class="sxs-lookup"><span data-stu-id="8d78c-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8d78c-113">$schema</span><span class="sxs-lookup"><span data-stu-id="8d78c-113">$schema</span></span> |<span data-ttu-id="8d78c-114">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-114">Yes</span></span> |<span data-ttu-id="8d78c-115">Emplacement du fichier de schéma JSON qui décrit la version du langage du modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="8d78c-116">Utilisez l’URL indiquée dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="8d78c-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="8d78c-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="8d78c-117">contentVersion</span></span> |<span data-ttu-id="8d78c-118">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-118">Yes</span></span> |<span data-ttu-id="8d78c-119">Version du modèle (par exemple, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="8d78c-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="8d78c-120">Vous pouvez fournir n’importe quelle valeur pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="8d78c-120">You can provide any value for this element.</span></span> <span data-ttu-id="8d78c-121">Quand vous déployez des ressources à l'aide du modèle, cette valeur permet de vous assurer que le bon modèle est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8d78c-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="8d78c-122">parameters</span><span class="sxs-lookup"><span data-stu-id="8d78c-122">parameters</span></span> |<span data-ttu-id="8d78c-123">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-123">No</span></span> |<span data-ttu-id="8d78c-124">Valeurs fournies lors de l'exécution du déploiement pour personnaliser le déploiement des ressources.</span><span class="sxs-lookup"><span data-stu-id="8d78c-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="8d78c-125">variables</span><span class="sxs-lookup"><span data-stu-id="8d78c-125">variables</span></span> |<span data-ttu-id="8d78c-126">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-126">No</span></span> |<span data-ttu-id="8d78c-127">Valeurs utilisées en tant que fragments JSON dans le modèle pour simplifier les expressions du langage du modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="8d78c-128">les ressources</span><span class="sxs-lookup"><span data-stu-id="8d78c-128">resources</span></span> |<span data-ttu-id="8d78c-129">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-129">Yes</span></span> |<span data-ttu-id="8d78c-130">Types de ressource déployés ou mis à jour dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8d78c-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="8d78c-131">outputs</span><span class="sxs-lookup"><span data-stu-id="8d78c-131">outputs</span></span> |<span data-ttu-id="8d78c-132">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-132">No</span></span> |<span data-ttu-id="8d78c-133">Valeurs retournées après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="8d78c-134">Chaque élément contient des propriétés que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="8d78c-134">Each element contains properties you can set.</span></span> <span data-ttu-id="8d78c-135">L’exemple suivant présente la syntaxe complète d’un modèle :</span><span class="sxs-lookup"><span data-stu-id="8d78c-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="8d78c-136">Nous allons examiner les sections du modèle de manière plus approfondie plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="8d78c-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="8d78c-137">Expressions et fonctions</span><span class="sxs-lookup"><span data-stu-id="8d78c-137">Expressions and functions</span></span>
<span data-ttu-id="8d78c-138">La syntaxe de base du modèle est JSON.</span><span class="sxs-lookup"><span data-stu-id="8d78c-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="8d78c-139">Toutefois, les expressions et fonctions étendent les valeurs JSON disponibles dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="8d78c-140">Les expressions sont écrites dans les littéraux de chaîne JSON dont le premier et dernier caractères sont les crochets : `[` et `]`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="8d78c-141">La valeur de l’expression est évaluée lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="8d78c-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="8d78c-142">Bien qu’écrit sous la forme d’un littéral de chaîne, le résultat de l’évaluation de l’expression peut être d’un type différent de JSON, tel qu’un tableau ou un entier, en fonction de l’expression réelle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="8d78c-143">Pour avoir une chaîne littérale qui commence par un crochet `[`, sans qu’elle soit interprétée comme une expression, ajoutez un crochet supplémentaire. La chaîne commence alors par `[[`.</span><span class="sxs-lookup"><span data-stu-id="8d78c-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="8d78c-144">En général, vous utilisez des expressions avec des fonctions pour effectuer des opérations de configuration du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="8d78c-145">Comme en JavaScript, les appels de fonction sont formatés comme suit : `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="8d78c-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="8d78c-146">Pour référencer des propriétés, vous utilisez les opérateurs point et [index].</span><span class="sxs-lookup"><span data-stu-id="8d78c-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="8d78c-147">L'exemple suivant vous indique comment utiliser plusieurs fonctions lors de la construction de valeurs :</span><span class="sxs-lookup"><span data-stu-id="8d78c-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="8d78c-148">Pour obtenir la liste complète des fonctions de modèle, consultez [Fonctions des modèles Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="8d78c-149">parameters</span><span class="sxs-lookup"><span data-stu-id="8d78c-149">Parameters</span></span>
<span data-ttu-id="8d78c-150">C’est dans la section des paramètres du modèle que vous pouvez spécifier les valeurs que vous pouvez saisir lors du déploiement des ressources.</span><span class="sxs-lookup"><span data-stu-id="8d78c-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="8d78c-151">Ces valeurs de paramètre vous permettent de personnaliser le déploiement grâce à des valeurs adaptées à un environnement particulier (par exemple développement, test et production).</span><span class="sxs-lookup"><span data-stu-id="8d78c-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="8d78c-152">Il est inutile de fournir des paramètres dans votre modèle, mais sans les paramètres, votre modèle déploie toujours les mêmes ressources avec les mêmes noms, emplacements et propriétés.</span><span class="sxs-lookup"><span data-stu-id="8d78c-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="8d78c-153">Vous définissez des paramètres avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="8d78c-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="8d78c-154">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="8d78c-154">Element name</span></span> | <span data-ttu-id="8d78c-155">Requis</span><span class="sxs-lookup"><span data-stu-id="8d78c-155">Required</span></span> | <span data-ttu-id="8d78c-156">Description</span><span class="sxs-lookup"><span data-stu-id="8d78c-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8d78c-157">nom_paramètre</span><span class="sxs-lookup"><span data-stu-id="8d78c-157">parameterName</span></span> |<span data-ttu-id="8d78c-158">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-158">Yes</span></span> |<span data-ttu-id="8d78c-159">Nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="8d78c-159">Name of the parameter.</span></span> <span data-ttu-id="8d78c-160">Doit être un identificateur JavaScript valide.</span><span class="sxs-lookup"><span data-stu-id="8d78c-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="8d78c-161">type</span><span class="sxs-lookup"><span data-stu-id="8d78c-161">type</span></span> |<span data-ttu-id="8d78c-162">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-162">Yes</span></span> |<span data-ttu-id="8d78c-163">Type de la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="8d78c-163">Type of the parameter value.</span></span> <span data-ttu-id="8d78c-164">La liste des types autorisés est présentée après ce tableau.</span><span class="sxs-lookup"><span data-stu-id="8d78c-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="8d78c-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="8d78c-165">defaultValue</span></span> |<span data-ttu-id="8d78c-166">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-166">No</span></span> |<span data-ttu-id="8d78c-167">Valeur par défaut du paramètre, si aucune valeur n'est fournie pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="8d78c-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="8d78c-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="8d78c-168">allowedValues</span></span> |<span data-ttu-id="8d78c-169">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-169">No</span></span> |<span data-ttu-id="8d78c-170">Tableau des valeurs autorisées pour le paramètre afin de vous assurer que la bonne valeur a bien été fournie.</span><span class="sxs-lookup"><span data-stu-id="8d78c-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="8d78c-171">minValue</span><span class="sxs-lookup"><span data-stu-id="8d78c-171">minValue</span></span> |<span data-ttu-id="8d78c-172">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-172">No</span></span> |<span data-ttu-id="8d78c-173">Valeur minimale pour les paramètres de type int, cette valeur est inclusive.</span><span class="sxs-lookup"><span data-stu-id="8d78c-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8d78c-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="8d78c-174">maxValue</span></span> |<span data-ttu-id="8d78c-175">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-175">No</span></span> |<span data-ttu-id="8d78c-176">Valeur maximale pour les paramètres de type int. Cette valeur est inclusive.</span><span class="sxs-lookup"><span data-stu-id="8d78c-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8d78c-177">minLength</span><span class="sxs-lookup"><span data-stu-id="8d78c-177">minLength</span></span> |<span data-ttu-id="8d78c-178">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-178">No</span></span> |<span data-ttu-id="8d78c-179">Valeur minimale pour les paramètres de type string, secureString et array. Cette valeur est inclusive.</span><span class="sxs-lookup"><span data-stu-id="8d78c-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8d78c-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="8d78c-180">maxLength</span></span> |<span data-ttu-id="8d78c-181">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-181">No</span></span> |<span data-ttu-id="8d78c-182">Valeur maximale pour les paramètres de type string, secureString et array. Cette valeur est inclusive.</span><span class="sxs-lookup"><span data-stu-id="8d78c-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8d78c-183">Description</span><span class="sxs-lookup"><span data-stu-id="8d78c-183">description</span></span> |<span data-ttu-id="8d78c-184">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-184">No</span></span> |<span data-ttu-id="8d78c-185">Description du paramètre qui apparaît aux utilisateurs dans le portail.</span><span class="sxs-lookup"><span data-stu-id="8d78c-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="8d78c-186">Les valeurs et types autorisés sont :</span><span class="sxs-lookup"><span data-stu-id="8d78c-186">The allowed types and values are:</span></span>

* <span data-ttu-id="8d78c-187">**string**</span><span class="sxs-lookup"><span data-stu-id="8d78c-187">**string**</span></span>
* <span data-ttu-id="8d78c-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="8d78c-188">**secureString**</span></span>
* <span data-ttu-id="8d78c-189">**int**</span><span class="sxs-lookup"><span data-stu-id="8d78c-189">**int**</span></span>
* <span data-ttu-id="8d78c-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="8d78c-190">**bool**</span></span>
* <span data-ttu-id="8d78c-191">**object**</span><span class="sxs-lookup"><span data-stu-id="8d78c-191">**object**</span></span> 
* <span data-ttu-id="8d78c-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="8d78c-192">**secureObject**</span></span>
* <span data-ttu-id="8d78c-193">**array**</span><span class="sxs-lookup"><span data-stu-id="8d78c-193">**array**</span></span>

<span data-ttu-id="8d78c-194">Pour spécifier un paramètre comme facultatif, fournissez une valeur defaultValue (peut être une chaîne vide).</span><span class="sxs-lookup"><span data-stu-id="8d78c-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="8d78c-195">Si vous spécifiez dans votre modèle un nom de paramètre qui correspond à un paramètre de la commande servant à déployer le modèle, il existe une ambiguïté potentielle concernant les valeurs que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="8d78c-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="8d78c-196">Resource Manager élimine ce risque de confusion en ajoutant le suffixe **romTemplate** au paramètre du modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="8d78c-197">Par exemple, si vous incluez dans votre modèle un paramètre nommé **ResourceGroupName**, celui-ci est en conflit avec le paramètre **ResourceGroupName** dans l’applet de commande [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="8d78c-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="8d78c-198">Pendant le déploiement, vous êtes invité à fournir une valeur pour **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="8d78c-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="8d78c-199">En général, vous devez éviter cette confusion en ne nommant pas les paramètres avec un nom identique à celui des paramètres utilisés pour les opérations de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="8d78c-200">Tous les mots de passe, clés et autres secrets doivent utiliser le type **secureString** .</span><span class="sxs-lookup"><span data-stu-id="8d78c-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="8d78c-201">Si vous transmettez des données sensibles dans un objet JSON, utilisez le type **secureObject**.</span><span class="sxs-lookup"><span data-stu-id="8d78c-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="8d78c-202">Il est impossible de lire les paramètres du modèle dont le type est secureString ou secureObject après le déploiement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="8d78c-203">Par exemple, l’entrée suivante dans l’historique de déploiement indique la valeur pour une chaîne et un objet, mais pas pour secureString et secureObject.</span><span class="sxs-lookup"><span data-stu-id="8d78c-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![afficher les valeurs de déploiement](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="8d78c-205">L’exemple suivant vous indique comment définir les paramètres :</span><span class="sxs-lookup"><span data-stu-id="8d78c-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="8d78c-206">Pour plus d’informations sur la saisie des valeurs de paramètre au cours du déploiement, consultez [Déployer une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="8d78c-207">variables</span><span class="sxs-lookup"><span data-stu-id="8d78c-207">Variables</span></span>
<span data-ttu-id="8d78c-208">Dans la section des variables, vous définissez des valeurs pouvant être utilisées dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="8d78c-209">Il est inutile de définir des variables, mais elles simplifient souvent votre modèle en réduisant les expressions complexes.</span><span class="sxs-lookup"><span data-stu-id="8d78c-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="8d78c-210">Vous définissez des variables avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="8d78c-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="8d78c-211">L'exemple suivant vous indique comment définir une variable qui est construite à partir de deux valeurs de paramètre :</span><span class="sxs-lookup"><span data-stu-id="8d78c-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="8d78c-212">L'exemple suivant vous indique une variable qui est un type complexe de JSON et des variables qui sont construites à partir d'autres variables :</span><span class="sxs-lookup"><span data-stu-id="8d78c-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="8d78c-213">les ressources</span><span class="sxs-lookup"><span data-stu-id="8d78c-213">Resources</span></span>
<span data-ttu-id="8d78c-214">Dans la section des ressources, vous définissez les ressources déployées ou mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8d78c-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="8d78c-215">Cette section gagne en complexité, car vous devez connaître les types que vous déployez pour fournir les valeurs adéquates.</span><span class="sxs-lookup"><span data-stu-id="8d78c-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="8d78c-216">Concernant les valeurs spécifiques aux ressources (apiVersion, type et properties) que vous devez définir, voir [Définir les ressources des modèles Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="8d78c-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="8d78c-217">Vous définissez des ressources avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="8d78c-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="8d78c-218">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="8d78c-218">Element name</span></span> | <span data-ttu-id="8d78c-219">Requis</span><span class="sxs-lookup"><span data-stu-id="8d78c-219">Required</span></span> | <span data-ttu-id="8d78c-220">Description</span><span class="sxs-lookup"><span data-stu-id="8d78c-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8d78c-221">condition</span><span class="sxs-lookup"><span data-stu-id="8d78c-221">condition</span></span> | <span data-ttu-id="8d78c-222">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-222">No</span></span> | <span data-ttu-id="8d78c-223">Valeur booléenne indiquant si la ressource est déployée.</span><span class="sxs-lookup"><span data-stu-id="8d78c-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="8d78c-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8d78c-224">apiVersion</span></span> |<span data-ttu-id="8d78c-225">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-225">Yes</span></span> |<span data-ttu-id="8d78c-226">La version de l'API REST à utiliser pour la création de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="8d78c-227">type</span><span class="sxs-lookup"><span data-stu-id="8d78c-227">type</span></span> |<span data-ttu-id="8d78c-228">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-228">Yes</span></span> |<span data-ttu-id="8d78c-229">Type de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-229">Type of the resource.</span></span> <span data-ttu-id="8d78c-230">Cette valeur est une combinaison de l’espace de noms du fournisseur de ressources et du type de ressource (comme **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="8d78c-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="8d78c-231">name</span><span class="sxs-lookup"><span data-stu-id="8d78c-231">name</span></span> |<span data-ttu-id="8d78c-232">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-232">Yes</span></span> |<span data-ttu-id="8d78c-233">Nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-233">Name of the resource.</span></span> <span data-ttu-id="8d78c-234">Le nom doit respecter les restrictions de composant d'URI définies dans le document RFC3986.</span><span class="sxs-lookup"><span data-stu-id="8d78c-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="8d78c-235">En outre, les services Azure qui exposent le nom de la ressource à des parties externes valident du nom pour s’assurer qu’il ne s’agit pas d’une tentative d’usurpation d’identité.</span><span class="sxs-lookup"><span data-stu-id="8d78c-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="8d78c-236">location</span><span class="sxs-lookup"><span data-stu-id="8d78c-236">location</span></span> |<span data-ttu-id="8d78c-237">Varie</span><span class="sxs-lookup"><span data-stu-id="8d78c-237">Varies</span></span> |<span data-ttu-id="8d78c-238">Emplacements géographiques de la ressource fournie pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8d78c-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="8d78c-239">Vous pouvez sélectionner l’un des emplacements disponibles, mais en général, il est judicieux de choisir celui qui est proche de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8d78c-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="8d78c-240">En règle générale, il est également judicieux de placer dans la même région les ressources qui interagissent entre elles.</span><span class="sxs-lookup"><span data-stu-id="8d78c-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="8d78c-241">La plupart des types de ressources nécessitent un emplacement, mais certains types (par exemple, une affectation de rôle) ne nécessitent aucun emplacement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="8d78c-242">Voir [Définir l’emplacement des ressources dans les modèles Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="8d78c-243">tags</span><span class="sxs-lookup"><span data-stu-id="8d78c-243">tags</span></span> |<span data-ttu-id="8d78c-244">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-244">No</span></span> |<span data-ttu-id="8d78c-245">Balises associées à la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="8d78c-246">Voir [Appliquer des balises aux ressources dans les modèles Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="8d78c-247">commentaires</span><span class="sxs-lookup"><span data-stu-id="8d78c-247">comments</span></span> |<span data-ttu-id="8d78c-248">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-248">No</span></span> |<span data-ttu-id="8d78c-249">Vos commentaires pour documenter les ressources dans votre modèle</span><span class="sxs-lookup"><span data-stu-id="8d78c-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="8d78c-250">copy</span><span class="sxs-lookup"><span data-stu-id="8d78c-250">copy</span></span> |<span data-ttu-id="8d78c-251">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-251">No</span></span> |<span data-ttu-id="8d78c-252">Si plusieurs instances sont nécessaires, le nombre de ressources à créer.</span><span class="sxs-lookup"><span data-stu-id="8d78c-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="8d78c-253">Le mode par défaut est parallèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-253">The default mode is parallel.</span></span> <span data-ttu-id="8d78c-254">Spécifiez le mode série si vous ne souhaitez pas que toutes les ressources soient déployées en même temps.</span><span class="sxs-lookup"><span data-stu-id="8d78c-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="8d78c-255">Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="8d78c-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="8d78c-256">dependsOn</span></span> |<span data-ttu-id="8d78c-257">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-257">No</span></span> |<span data-ttu-id="8d78c-258">Les ressources qui doivent être déployées avant le déploiement de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="8d78c-259">Resource Manager évalue les dépendances entre les ressources et les déploie dans le bon ordre.</span><span class="sxs-lookup"><span data-stu-id="8d78c-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="8d78c-260">Quand les ressources ne dépendent les unes des autres, leur déploiement se fait en parallèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="8d78c-261">La valeur peut être une liste séparée par des virgules de noms de ressource ou d’identificateurs de ressource uniques.</span><span class="sxs-lookup"><span data-stu-id="8d78c-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="8d78c-262">Répertoriez uniquement les ressources qui sont déployées dans ce modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="8d78c-263">Les ressources qui ne sont pas définies dans ce modèle doivent déjà exister.</span><span class="sxs-lookup"><span data-stu-id="8d78c-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="8d78c-264">Évitez d’ajouter des dépendances inutiles, car cela risque de ralentir votre déploiement et de créer des dépendances circulaires.</span><span class="sxs-lookup"><span data-stu-id="8d78c-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="8d78c-265">Pour savoir comment définir des dépendances, consultez [Définition de dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="8d78c-266">properties</span><span class="sxs-lookup"><span data-stu-id="8d78c-266">properties</span></span> |<span data-ttu-id="8d78c-267">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-267">No</span></span> |<span data-ttu-id="8d78c-268">Paramètres de configuration spécifiques aux ressources.</span><span class="sxs-lookup"><span data-stu-id="8d78c-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="8d78c-269">Les valeurs de propriétés sont identiques à celles que vous fournissez dans le corps de la requête pour l’opération d’API REST (méthode PUT) pour créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="8d78c-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="8d78c-270">Vous pouvez également spécifier une copie en groupe pour créer plusieurs instances d’une propriété.</span><span class="sxs-lookup"><span data-stu-id="8d78c-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="8d78c-271">Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="8d78c-272">les ressources</span><span class="sxs-lookup"><span data-stu-id="8d78c-272">resources</span></span> |<span data-ttu-id="8d78c-273">Non</span><span class="sxs-lookup"><span data-stu-id="8d78c-273">No</span></span> |<span data-ttu-id="8d78c-274">Ressources enfants qui dépendent de la ressource qui est définie.</span><span class="sxs-lookup"><span data-stu-id="8d78c-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="8d78c-275">Fournissez uniquement des types de ressources qui sont autorisés par le schéma de la ressource parente.</span><span class="sxs-lookup"><span data-stu-id="8d78c-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="8d78c-276">Le type complet de la ressource enfant inclut le type de ressource parente, par exemple **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="8d78c-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="8d78c-277">La dépendance envers la ressource parente n’est pas induite.</span><span class="sxs-lookup"><span data-stu-id="8d78c-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="8d78c-278">Vous devez la définir explicitement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="8d78c-279">La section des ressources contient un tableau des ressources à déployer.</span><span class="sxs-lookup"><span data-stu-id="8d78c-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="8d78c-280">Au sein de chaque ressource, vous pouvez également définir un tableau de ressources enfant.</span><span class="sxs-lookup"><span data-stu-id="8d78c-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="8d78c-281">Par conséquent, la structure de la section de ressources peut ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8d78c-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="8d78c-282">Pour plus d’informations sur la définition des ressources enfants, voir [Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="8d78c-283">L’élément **condition** indique si la ressource est déployée.</span><span class="sxs-lookup"><span data-stu-id="8d78c-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="8d78c-284">La valeur de cet élément est résolue en true ou false.</span><span class="sxs-lookup"><span data-stu-id="8d78c-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="8d78c-285">Par exemple, pour spécifier si un compte de stockage est déployé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="8d78c-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="8d78c-286">Pour obtenir un exemple d’utilisation d’une ressource nouvelle ou existante, voir [Modèle de condition New ou Existing](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="8d78c-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="8d78c-287">Pour spécifier si une machine virtuelle est déployée avec un mot de passe ou une clé SSH, définissez deux versions de la machine virtuelle dans votre modèle, puis utilisez l’élément **condition** pour différencier l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="8d78c-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="8d78c-288">Transmettre un paramètre qui spécifie le scénario à déployer.</span><span class="sxs-lookup"><span data-stu-id="8d78c-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="8d78c-289">Pour obtenir un exemple d’utilisation d’un mot de passe ou d’une clé SSH pour déployer une machine virtuelle, voir [Modèle de condition Username ou SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="8d78c-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="8d78c-290">Sorties</span><span class="sxs-lookup"><span data-stu-id="8d78c-290">Outputs</span></span>
<span data-ttu-id="8d78c-291">Dans la section des sorties, vous spécifiez des valeurs retournées à partir du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d78c-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="8d78c-292">Par exemple, vous pouvez retourner l'URI d'accès à une ressource déployée.</span><span class="sxs-lookup"><span data-stu-id="8d78c-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="8d78c-293">L'exemple suivant illustre la structure de la définition d'une sortie :</span><span class="sxs-lookup"><span data-stu-id="8d78c-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="8d78c-294">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="8d78c-294">Element name</span></span> | <span data-ttu-id="8d78c-295">Requis</span><span class="sxs-lookup"><span data-stu-id="8d78c-295">Required</span></span> | <span data-ttu-id="8d78c-296">Description</span><span class="sxs-lookup"><span data-stu-id="8d78c-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8d78c-297">outputName</span><span class="sxs-lookup"><span data-stu-id="8d78c-297">outputName</span></span> |<span data-ttu-id="8d78c-298">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-298">Yes</span></span> |<span data-ttu-id="8d78c-299">Nom de la valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="8d78c-299">Name of the output value.</span></span> <span data-ttu-id="8d78c-300">Doit être un identificateur JavaScript valide.</span><span class="sxs-lookup"><span data-stu-id="8d78c-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="8d78c-301">type</span><span class="sxs-lookup"><span data-stu-id="8d78c-301">type</span></span> |<span data-ttu-id="8d78c-302">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-302">Yes</span></span> |<span data-ttu-id="8d78c-303">Type de la valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="8d78c-303">Type of the output value.</span></span> <span data-ttu-id="8d78c-304">Les valeurs de sortie prennent en charge les mêmes types que les paramètres d'entrée du modèle.</span><span class="sxs-lookup"><span data-stu-id="8d78c-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="8d78c-305">value</span><span class="sxs-lookup"><span data-stu-id="8d78c-305">value</span></span> |<span data-ttu-id="8d78c-306">Oui</span><span class="sxs-lookup"><span data-stu-id="8d78c-306">Yes</span></span> |<span data-ttu-id="8d78c-307">Expression du langage du modèle évaluée et retournée sous forme de valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="8d78c-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="8d78c-308">L'exemple suivant montre une valeur retournée dans la section des sorties.</span><span class="sxs-lookup"><span data-stu-id="8d78c-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="8d78c-309">Pour plus d’informations sur le fonctionnement de la sortie, consultez [Partage d’état dans les modèles Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="8d78c-310">Limites de modèle</span><span class="sxs-lookup"><span data-stu-id="8d78c-310">Template limits</span></span>

<span data-ttu-id="8d78c-311">Limitez la taille de votre modèle à 1 Mo et celle de chaque fichier de paramètres à 64 ko.</span><span class="sxs-lookup"><span data-stu-id="8d78c-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="8d78c-312">La limite de 1 Mo s’applique à l’état final du modèle une fois développé avec les définitions des ressources itératives et les valeurs des variables et des paramètres.</span><span class="sxs-lookup"><span data-stu-id="8d78c-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="8d78c-313">Vous devez également respecter les limites suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d78c-313">You are also limited to:</span></span>

* <span data-ttu-id="8d78c-314">256 paramètres</span><span class="sxs-lookup"><span data-stu-id="8d78c-314">256 parameters</span></span>
* <span data-ttu-id="8d78c-315">256 variables</span><span class="sxs-lookup"><span data-stu-id="8d78c-315">256 variables</span></span>
* <span data-ttu-id="8d78c-316">800 ressources (incluant le nombre de copies)</span><span class="sxs-lookup"><span data-stu-id="8d78c-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="8d78c-317">64 valeurs de sortie</span><span class="sxs-lookup"><span data-stu-id="8d78c-317">64 output values</span></span>
* <span data-ttu-id="8d78c-318">24 576 caractères dans une expression de modèle</span><span class="sxs-lookup"><span data-stu-id="8d78c-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="8d78c-319">Vous pouvez dépasser certaines limites de modèle en utilisant un modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="8d78c-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="8d78c-320">Pour plus d’informations, consultez l’article [Utilisation de modèles liés lors du déploiement des ressources Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="8d78c-321">Pour réduire le nombre de paramètres, de variables ou de sorties, vous pouvez combiner plusieurs valeurs dans un même objet.</span><span class="sxs-lookup"><span data-stu-id="8d78c-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="8d78c-322">Pour plus d’informations, consultez l’article [Objects as parameters](resource-manager-objects-as-parameters.md) (Utiliser un objet en tant que paramètre).</span><span class="sxs-lookup"><span data-stu-id="8d78c-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d78c-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d78c-323">Next steps</span></span>
* <span data-ttu-id="8d78c-324">Pour afficher des modèles complets pour de nombreux types de solutions, consultez [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="8d78c-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="8d78c-325">Pour plus d’informations sur les fonctions que vous pouvez utiliser dans un modèle, consultez [Fonctions des modèles Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="8d78c-326">Pour combiner plusieurs modèles lors du déploiement, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8d78c-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="8d78c-327">Vous devrez peut-être utiliser des ressources qui existent au sein d'un groupe de ressources différent.</span><span class="sxs-lookup"><span data-stu-id="8d78c-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="8d78c-328">Ce scénario est classique quand vous utilisez des comptes de stockage ou des réseaux virtuels qui sont partagés entre plusieurs groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="8d78c-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="8d78c-329">Pour plus d'informations, consultez la [fonction resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="8d78c-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
