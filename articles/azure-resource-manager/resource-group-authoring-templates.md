---
title: "le Gestionnaire de ressources d’aaaAzure structure de modèle et la syntaxe | Documents Microsoft"
description: "Décrit la structure de hello et les propriétés de modèles Azure Resource Manager à l’aide de la syntaxe déclarative JSON."
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
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="0ebad-103">Comprendre la structure de hello et syntaxe des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ebad-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="0ebad-104">Cette rubrique décrit la structure hello d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ebad-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="0ebad-105">Elle présente hello différentes sections d’un modèle et hello des propriétés qui sont disponibles dans ces sections.</span><span class="sxs-lookup"><span data-stu-id="0ebad-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="0ebad-106">modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="0ebad-107">Pour obtenir un didacticiel étape par étape permettant de créer un modèle, voir [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="0ebad-108">Format de modèle</span><span class="sxs-lookup"><span data-stu-id="0ebad-108">Template format</span></span>
<span data-ttu-id="0ebad-109">Dans la structure la plus simple, un modèle contient hello suivant d’éléments :</span><span class="sxs-lookup"><span data-stu-id="0ebad-109">In its simplest structure, a template contains hello following elements:</span></span>

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

| <span data-ttu-id="0ebad-110">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="0ebad-110">Element name</span></span> | <span data-ttu-id="0ebad-111">Requis</span><span class="sxs-lookup"><span data-stu-id="0ebad-111">Required</span></span> | <span data-ttu-id="0ebad-112">Description</span><span class="sxs-lookup"><span data-stu-id="0ebad-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ebad-113">$schema</span><span class="sxs-lookup"><span data-stu-id="0ebad-113">$schema</span></span> |<span data-ttu-id="0ebad-114">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-114">Yes</span></span> |<span data-ttu-id="0ebad-115">Emplacement du fichier de schéma JSON hello qui décrit la version de hello du langage de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="0ebad-116">Utilisez les URL hello indiqué dans le précédent exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="0ebad-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="0ebad-117">contentVersion</span></span> |<span data-ttu-id="0ebad-118">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-118">Yes</span></span> |<span data-ttu-id="0ebad-119">Version du modèle hello (par exemple, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="0ebad-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="0ebad-120">Vous pouvez fournir n’importe quelle valeur pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="0ebad-120">You can provide any value for this element.</span></span> <span data-ttu-id="0ebad-121">Lorsque vous déployez des ressources à l’aide du modèle de hello, cette valeur peut être utilisé toomake que ce modèle hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0ebad-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="0ebad-122">parameters</span><span class="sxs-lookup"><span data-stu-id="0ebad-122">parameters</span></span> |<span data-ttu-id="0ebad-123">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-123">No</span></span> |<span data-ttu-id="0ebad-124">Les valeurs fournies lorsque le déploiement est exécuté le déploiement de ressources toocustomize.</span><span class="sxs-lookup"><span data-stu-id="0ebad-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="0ebad-125">variables</span><span class="sxs-lookup"><span data-stu-id="0ebad-125">variables</span></span> |<span data-ttu-id="0ebad-126">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-126">No</span></span> |<span data-ttu-id="0ebad-127">Valeurs qui sont utilisées en tant que fragments JSON dans les expressions de langage de modèle hello modèle toosimplify.</span><span class="sxs-lookup"><span data-stu-id="0ebad-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="0ebad-128">les ressources</span><span class="sxs-lookup"><span data-stu-id="0ebad-128">resources</span></span> |<span data-ttu-id="0ebad-129">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-129">Yes</span></span> |<span data-ttu-id="0ebad-130">Types de ressource déployés ou mis à jour dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="0ebad-131">outputs</span><span class="sxs-lookup"><span data-stu-id="0ebad-131">outputs</span></span> |<span data-ttu-id="0ebad-132">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-132">No</span></span> |<span data-ttu-id="0ebad-133">Valeurs retournées après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="0ebad-134">Chaque élément contient des propriétés que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="0ebad-134">Each element contains properties you can set.</span></span> <span data-ttu-id="0ebad-135">Hello, l’exemple suivant contient une syntaxe complète de hello pour un modèle :</span><span class="sxs-lookup"><span data-stu-id="0ebad-135">hello following example contains hello full syntax for a template:</span></span>

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
                "description": "<description-of-hello parameter>" 
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

<span data-ttu-id="0ebad-136">Nous examinons sections hello du modèle hello plus en détail plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="0ebad-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="0ebad-137">Expressions et fonctions</span><span class="sxs-lookup"><span data-stu-id="0ebad-137">Expressions and functions</span></span>
<span data-ttu-id="0ebad-138">syntaxe de base Hello du modèle de hello est JSON.</span><span class="sxs-lookup"><span data-stu-id="0ebad-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="0ebad-139">Toutefois, les expressions et fonctions étendent hello JSON de valeurs disponibles dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="0ebad-140">Les expressions sont écrites dans les littéraux de chaîne JSON dont le premier et dernier caractères sont des crochets de hello : `[` et `]`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="0ebad-141">valeur de Hello d’expression de hello est évaluée lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="0ebad-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="0ebad-142">Alors qu’écrite sous la forme d’un littéral de chaîne, les résultats hello de l’évaluation d’expression de hello peut être de type JSON différent, tel qu’un tableau ou d’un entier, en fonction de l’expression réelle de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="0ebad-143">toohave une chaîne littérale commencer par un crochet `[`, mais pas soit interprétée comme une expression, ajoutez une crochet supplémentaire toostart hello chaîne `[[`.</span><span class="sxs-lookup"><span data-stu-id="0ebad-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="0ebad-144">En règle générale, vous utilisez des expressions avec les opérations de tooperform des fonctions de configuration de déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="0ebad-145">Comme en JavaScript, les appels de fonction sont formatés comme suit : `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="0ebad-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="0ebad-146">Référencer des propriétés en utilisant des opérateurs de point et [index] hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="0ebad-147">Hello, l’exemple suivant montre comment plusieurs fonctions lors de la construction de toouse valeurs :</span><span class="sxs-lookup"><span data-stu-id="0ebad-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="0ebad-148">Pour hello une liste complète des fonctions de modèle, consultez [fonctions de modèle Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="0ebad-149">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0ebad-149">Parameters</span></span>
<span data-ttu-id="0ebad-150">Dans la section Paramètres de hello du modèle de hello, vous spécifiez les valeurs que vous pouvez entrer lorsque vous déployez hello des ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="0ebad-151">Ces valeurs de paramètres permettent de déploiement de hello toocustomize en fournissant des valeurs qui sont adaptés pour un environnement particulier (par exemple, le développement, test et production).</span><span class="sxs-lookup"><span data-stu-id="0ebad-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="0ebad-152">Vous n’avez pas de paramètres de tooprovide dans votre modèle, mais sans les paramètres de votre modèle est toujours déployer hello ressources mêmes avec hello même des noms, des emplacements et des propriétés.</span><span class="sxs-lookup"><span data-stu-id="0ebad-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="0ebad-153">Vous définissez des paramètres par hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="0ebad-153">You define parameters with hello following structure:</span></span>

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
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="0ebad-154">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="0ebad-154">Element name</span></span> | <span data-ttu-id="0ebad-155">Requis</span><span class="sxs-lookup"><span data-stu-id="0ebad-155">Required</span></span> | <span data-ttu-id="0ebad-156">Description</span><span class="sxs-lookup"><span data-stu-id="0ebad-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ebad-157">nom_paramètre</span><span class="sxs-lookup"><span data-stu-id="0ebad-157">parameterName</span></span> |<span data-ttu-id="0ebad-158">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-158">Yes</span></span> |<span data-ttu-id="0ebad-159">Nom du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-159">Name of hello parameter.</span></span> <span data-ttu-id="0ebad-160">Doit être un identificateur JavaScript valide.</span><span class="sxs-lookup"><span data-stu-id="0ebad-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="0ebad-161">type</span><span class="sxs-lookup"><span data-stu-id="0ebad-161">type</span></span> |<span data-ttu-id="0ebad-162">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-162">Yes</span></span> |<span data-ttu-id="0ebad-163">Type de valeur de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-163">Type of hello parameter value.</span></span> <span data-ttu-id="0ebad-164">Consultez la liste hello des types autorisés après ce tableau.</span><span class="sxs-lookup"><span data-stu-id="0ebad-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="0ebad-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="0ebad-165">defaultValue</span></span> |<span data-ttu-id="0ebad-166">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-166">No</span></span> |<span data-ttu-id="0ebad-167">Valeur par défaut pour le paramètre hello, si aucune valeur n’est fournie pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="0ebad-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="0ebad-168">allowedValues</span></span> |<span data-ttu-id="0ebad-169">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-169">No</span></span> |<span data-ttu-id="0ebad-170">Tableau de valeurs autorisées pour toomake de paramètre hello assurer que la valeur de droite hello est fourni.</span><span class="sxs-lookup"><span data-stu-id="0ebad-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="0ebad-171">minValue</span><span class="sxs-lookup"><span data-stu-id="0ebad-171">minValue</span></span> |<span data-ttu-id="0ebad-172">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-172">No</span></span> |<span data-ttu-id="0ebad-173">valeur minimale de Hello pour les paramètres de type int, cette valeur est incluse.</span><span class="sxs-lookup"><span data-stu-id="0ebad-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="0ebad-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="0ebad-174">maxValue</span></span> |<span data-ttu-id="0ebad-175">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-175">No</span></span> |<span data-ttu-id="0ebad-176">valeur maximale de Hello pour les paramètres de type int, cette valeur est incluse.</span><span class="sxs-lookup"><span data-stu-id="0ebad-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="0ebad-177">minLength</span><span class="sxs-lookup"><span data-stu-id="0ebad-177">minLength</span></span> |<span data-ttu-id="0ebad-178">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-178">No</span></span> |<span data-ttu-id="0ebad-179">longueur minimale de Hello pour secureString, de chaîne et les paramètres de type tableau, cette valeur est incluse.</span><span class="sxs-lookup"><span data-stu-id="0ebad-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="0ebad-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="0ebad-180">maxLength</span></span> |<span data-ttu-id="0ebad-181">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-181">No</span></span> |<span data-ttu-id="0ebad-182">longueur maximale de Hello pour secureString, de chaîne et les paramètres de type tableau, cette valeur est incluse.</span><span class="sxs-lookup"><span data-stu-id="0ebad-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="0ebad-183">description</span><span class="sxs-lookup"><span data-stu-id="0ebad-183">description</span></span> |<span data-ttu-id="0ebad-184">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-184">No</span></span> |<span data-ttu-id="0ebad-185">Description du paramètre hello qui est affichée toousers via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="0ebad-186">Hello les valeurs et les types autorisés sont :</span><span class="sxs-lookup"><span data-stu-id="0ebad-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="0ebad-187">**string**</span><span class="sxs-lookup"><span data-stu-id="0ebad-187">**string**</span></span>
* <span data-ttu-id="0ebad-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="0ebad-188">**secureString**</span></span>
* <span data-ttu-id="0ebad-189">**int**</span><span class="sxs-lookup"><span data-stu-id="0ebad-189">**int**</span></span>
* <span data-ttu-id="0ebad-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="0ebad-190">**bool**</span></span>
* <span data-ttu-id="0ebad-191">**object**</span><span class="sxs-lookup"><span data-stu-id="0ebad-191">**object**</span></span> 
* <span data-ttu-id="0ebad-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="0ebad-192">**secureObject**</span></span>
* <span data-ttu-id="0ebad-193">**array**</span><span class="sxs-lookup"><span data-stu-id="0ebad-193">**array**</span></span>

<span data-ttu-id="0ebad-194">toospecify un paramètre comme facultatif, fournissent un defaultValue (peut être d’une chaîne vide).</span><span class="sxs-lookup"><span data-stu-id="0ebad-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="0ebad-195">Si vous spécifiez un nom de paramètre dans votre modèle qui correspond à un paramètre de modèle de hello hello commande toodeploy, il est ambiguïté sur les valeurs hello que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="0ebad-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="0ebad-196">Le Gestionnaire de ressources résout cette confusion en ajoutant le suffixe de hello **modèle** paramètre de modèle toohello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="0ebad-197">Par exemple, si vous incluez un paramètre nommé **ResourceGroupName** dans votre modèle, il est en conflit avec hello **ResourceGroupName** paramètre Bonjour [ Nouveau-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="0ebad-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="0ebad-198">Pendant le déploiement, vous êtes invité à tooprovide une valeur pour **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="0ebad-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="0ebad-199">En règle générale, vous devez éviter cette confusion en nommant ne pas de paramètres avec le même nom en tant que paramètres utilisés pour les opérations de déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="0ebad-200">Tous les mots de passe, les clés et autres secrets doivent utiliser hello **secureString** type.</span><span class="sxs-lookup"><span data-stu-id="0ebad-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="0ebad-201">Si vous passez des données sensibles dans un objet JSON, utilisez hello **secureObject** type.</span><span class="sxs-lookup"><span data-stu-id="0ebad-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="0ebad-202">Il est impossible de lire les paramètres du modèle dont le type est secureString ou secureObject après le déploiement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="0ebad-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="0ebad-203">Par exemple, hello entrée suivante dans l’historique de déploiement hello affiche hello valeur pour une chaîne et un objet, mais pas pour secureString et secureObject.</span><span class="sxs-lookup"><span data-stu-id="0ebad-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![afficher les valeurs de déploiement](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="0ebad-205">Hello suivant montre l’exemple de comment toodefine paramètres :</span><span class="sxs-lookup"><span data-stu-id="0ebad-205">hello following example shows how toodefine parameters:</span></span>

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

<span data-ttu-id="0ebad-206">Pour la tooinput hello valeurs de paramètre, au cours du déploiement, consultez [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="0ebad-207">variables</span><span class="sxs-lookup"><span data-stu-id="0ebad-207">Variables</span></span>
<span data-ttu-id="0ebad-208">Dans la section de variables hello, vous construisez des valeurs qui peuvent être utilisées dans l’ensemble de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="0ebad-209">Vous n’avez pas besoin de toodefine variables, mais ils simplifient souvent votre modèle en réduisant les expressions complexes.</span><span class="sxs-lookup"><span data-stu-id="0ebad-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="0ebad-210">Vous définissez des variables avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="0ebad-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="0ebad-211">Hello suivant montre l’exemple de comment toodefine une variable qui est construite à partir de deux valeurs de paramètre :</span><span class="sxs-lookup"><span data-stu-id="0ebad-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="0ebad-212">Hello l’exemple suivant montre une variable qui est un type complexe de JSON et les variables qui sont construits à partir d’autres variables :</span><span class="sxs-lookup"><span data-stu-id="0ebad-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="0ebad-213">Ressources</span><span class="sxs-lookup"><span data-stu-id="0ebad-213">Resources</span></span>
<span data-ttu-id="0ebad-214">Dans la section relative aux ressources hello, vous définissez des ressources hello qui sont déployés ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="0ebad-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="0ebad-215">Cette section peut se compliquer, car vous devez comprendre hello types que vous déployez des valeurs tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="0ebad-216">Hello propres à la ressource valeurs (apiVersion, type et propriétés) que vous avez besoin de tooset [définir des ressources dans les modèles Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="0ebad-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="0ebad-217">Vous définissez des ressources par hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="0ebad-217">You define resources with hello following structure:</span></span>

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

| <span data-ttu-id="0ebad-218">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="0ebad-218">Element name</span></span> | <span data-ttu-id="0ebad-219">Requis</span><span class="sxs-lookup"><span data-stu-id="0ebad-219">Required</span></span> | <span data-ttu-id="0ebad-220">Description</span><span class="sxs-lookup"><span data-stu-id="0ebad-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ebad-221">condition</span><span class="sxs-lookup"><span data-stu-id="0ebad-221">condition</span></span> | <span data-ttu-id="0ebad-222">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-222">No</span></span> | <span data-ttu-id="0ebad-223">Valeur booléenne qui indique si les ressources hello sont déployée.</span><span class="sxs-lookup"><span data-stu-id="0ebad-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="0ebad-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0ebad-224">apiVersion</span></span> |<span data-ttu-id="0ebad-225">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-225">Yes</span></span> |<span data-ttu-id="0ebad-226">Version de toouse d’API REST hello pour la création de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="0ebad-227">type</span><span class="sxs-lookup"><span data-stu-id="0ebad-227">type</span></span> |<span data-ttu-id="0ebad-228">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-228">Yes</span></span> |<span data-ttu-id="0ebad-229">Type de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-229">Type of hello resource.</span></span> <span data-ttu-id="0ebad-230">Cette valeur est une combinaison de l’espace de noms hello de fournisseur de ressources hello et type de ressource hello (tel que **/storageaccounts**).</span><span class="sxs-lookup"><span data-stu-id="0ebad-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="0ebad-231">name</span><span class="sxs-lookup"><span data-stu-id="0ebad-231">name</span></span> |<span data-ttu-id="0ebad-232">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-232">Yes</span></span> |<span data-ttu-id="0ebad-233">Nom de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-233">Name of hello resource.</span></span> <span data-ttu-id="0ebad-234">Hello doit respecter les restrictions de composant URI définies dans la norme RFC 3986.</span><span class="sxs-lookup"><span data-stu-id="0ebad-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="0ebad-235">En outre, les services Azure qui exposent les parties de toooutside de nom de ressource hello valider toomake de nom hello qu’il se n'agit pas d’une tentative toospoof une autre identité.</span><span class="sxs-lookup"><span data-stu-id="0ebad-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="0ebad-236">location</span><span class="sxs-lookup"><span data-stu-id="0ebad-236">location</span></span> |<span data-ttu-id="0ebad-237">Varie</span><span class="sxs-lookup"><span data-stu-id="0ebad-237">Varies</span></span> |<span data-ttu-id="0ebad-238">Emplacements géographiques pris en charge de hello fournissait des ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="0ebad-239">Vous pouvez sélectionner un des emplacements disponibles de hello, mais en général rend sens toopick qui tooyour fermer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0ebad-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="0ebad-240">En règle générale, il peut s’avérer utile ressources tooplace qui interagissent entre eux dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="0ebad-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="0ebad-241">La plupart des types de ressources nécessitent un emplacement, mais certains types (par exemple, une affectation de rôle) ne nécessitent aucun emplacement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="0ebad-242">Voir [Définir l’emplacement des ressources dans les modèles Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="0ebad-243">tags</span><span class="sxs-lookup"><span data-stu-id="0ebad-243">tags</span></span> |<span data-ttu-id="0ebad-244">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-244">No</span></span> |<span data-ttu-id="0ebad-245">Balises qui sont associés à des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="0ebad-246">Voir [Appliquer des balises aux ressources dans les modèles Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="0ebad-247">commentaires</span><span class="sxs-lookup"><span data-stu-id="0ebad-247">comments</span></span> |<span data-ttu-id="0ebad-248">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-248">No</span></span> |<span data-ttu-id="0ebad-249">Vos commentaires pour documenter les ressources hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="0ebad-250">copy</span><span class="sxs-lookup"><span data-stu-id="0ebad-250">copy</span></span> |<span data-ttu-id="0ebad-251">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-251">No</span></span> |<span data-ttu-id="0ebad-252">Si plusieurs instances est nécessaire, hello le nombre de ressources toocreate.</span><span class="sxs-lookup"><span data-stu-id="0ebad-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="0ebad-253">mode par défaut de Hello est parallèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-253">hello default mode is parallel.</span></span> <span data-ttu-id="0ebad-254">Spécifiez le mode série quand ne pas tous ou hello toodeploy de ressources à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="0ebad-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="0ebad-255">Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="0ebad-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="0ebad-256">dependsOn</span></span> |<span data-ttu-id="0ebad-257">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-257">No</span></span> |<span data-ttu-id="0ebad-258">Les ressources qui doivent être déployées avant le déploiement de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="0ebad-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="0ebad-259">Le Gestionnaire de ressources évalue des dépendances hello entre les ressources et les déploie dans l’ordre correct de hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="0ebad-260">Quand les ressources ne dépendent les unes des autres, leur déploiement se fait en parallèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="0ebad-261">Hello valeur peut être une liste séparée par des virgules d’une ressource de noms ou des identificateurs de ressources unique.</span><span class="sxs-lookup"><span data-stu-id="0ebad-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="0ebad-262">Répertoriez uniquement les ressources qui sont déployées dans ce modèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="0ebad-263">Les ressources qui ne sont pas définies dans ce modèle doivent déjà exister.</span><span class="sxs-lookup"><span data-stu-id="0ebad-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="0ebad-264">Évitez d’ajouter des dépendances inutiles, car cela risque de ralentir votre déploiement et de créer des dépendances circulaires.</span><span class="sxs-lookup"><span data-stu-id="0ebad-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="0ebad-265">Pour savoir comment définir des dépendances, consultez [Définition de dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="0ebad-266">properties</span><span class="sxs-lookup"><span data-stu-id="0ebad-266">properties</span></span> |<span data-ttu-id="0ebad-267">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-267">No</span></span> |<span data-ttu-id="0ebad-268">Paramètres de configuration spécifiques aux ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="0ebad-269">les valeurs Hello pour les propriétés de hello sont même hello en tant que valeurs hello vous fournissez dans le corps de la demande hello pour hello API REST opération (méthode PUT) toocreate hello ressource.</span><span class="sxs-lookup"><span data-stu-id="0ebad-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="0ebad-270">Vous pouvez également spécifier un toocreate de tableau copie plusieurs instances d’une propriété.</span><span class="sxs-lookup"><span data-stu-id="0ebad-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="0ebad-271">Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="0ebad-272">les ressources</span><span class="sxs-lookup"><span data-stu-id="0ebad-272">resources</span></span> |<span data-ttu-id="0ebad-273">Non</span><span class="sxs-lookup"><span data-stu-id="0ebad-273">No</span></span> |<span data-ttu-id="0ebad-274">Ressources enfants qui dépendent des ressources hello en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="0ebad-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="0ebad-275">Fournir uniquement les types de ressources qui sont autorisées par schéma hello de ressource du parent hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="0ebad-276">Hello type qualifié complet de la ressource enfant de hello inclut le type de ressource hello parent tels que **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="0ebad-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="0ebad-277">Dépendance sur la ressource parent de hello n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0ebad-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="0ebad-278">Vous devez la définir explicitement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="0ebad-279">section de ressources Hello contient un tableau de toodeploy de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="0ebad-280">Au sein de chaque ressource, vous pouvez également définir un tableau de ressources enfant.</span><span class="sxs-lookup"><span data-stu-id="0ebad-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="0ebad-281">Par conséquent, la structure de la section de ressources peut ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0ebad-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="0ebad-282">Pour plus d’informations sur la définition des ressources enfants, voir [Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="0ebad-283">Hello **condition** élément spécifie si les ressources hello sont déployé.</span><span class="sxs-lookup"><span data-stu-id="0ebad-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="0ebad-284">valeur Hello pour cet élément résout tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="0ebad-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="0ebad-285">Par exemple, toospecify si un compte de stockage est déployé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0ebad-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="0ebad-286">Pour obtenir un exemple d’utilisation d’une ressource nouvelle ou existante, voir [Modèle de condition New ou Existing](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="0ebad-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="0ebad-287">toospecify si un ordinateur virtuel est déployé avec un mot de passe ou la clé SSH, définir deux versions de la machine virtuelle de hello dans votre modèle, **condition** toodifferentiate utilisation.</span><span class="sxs-lookup"><span data-stu-id="0ebad-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="0ebad-288">Transmettre un paramètre qui spécifie quels toodeploy de scénario.</span><span class="sxs-lookup"><span data-stu-id="0ebad-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

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

<span data-ttu-id="0ebad-289">Pour obtenir un exemple de l’utilisation d’un mot de passe ou d’un ordinateur virtuel de toodeploy clé SSH, consultez [modèle de condition de nom d’utilisateur ou de SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="0ebad-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="0ebad-290">outputs</span><span class="sxs-lookup"><span data-stu-id="0ebad-290">Outputs</span></span>
<span data-ttu-id="0ebad-291">Dans la section de sorties hello, vous spécifiez des valeurs qui sont retournées à partir de déploiement.</span><span class="sxs-lookup"><span data-stu-id="0ebad-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="0ebad-292">Par exemple, vous pouvez retourner hello URI tooaccess une ressource déployée.</span><span class="sxs-lookup"><span data-stu-id="0ebad-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="0ebad-293">Hello suivant montre structure hello d’une définition de sortie :</span><span class="sxs-lookup"><span data-stu-id="0ebad-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="0ebad-294">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="0ebad-294">Element name</span></span> | <span data-ttu-id="0ebad-295">Requis</span><span class="sxs-lookup"><span data-stu-id="0ebad-295">Required</span></span> | <span data-ttu-id="0ebad-296">Description</span><span class="sxs-lookup"><span data-stu-id="0ebad-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ebad-297">outputName</span><span class="sxs-lookup"><span data-stu-id="0ebad-297">outputName</span></span> |<span data-ttu-id="0ebad-298">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-298">Yes</span></span> |<span data-ttu-id="0ebad-299">Nom de la valeur de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-299">Name of hello output value.</span></span> <span data-ttu-id="0ebad-300">Doit être un identificateur JavaScript valide.</span><span class="sxs-lookup"><span data-stu-id="0ebad-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="0ebad-301">type</span><span class="sxs-lookup"><span data-stu-id="0ebad-301">type</span></span> |<span data-ttu-id="0ebad-302">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-302">Yes</span></span> |<span data-ttu-id="0ebad-303">Type de valeur de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-303">Type of hello output value.</span></span> <span data-ttu-id="0ebad-304">Les valeurs de sortie prend en charge hello même types en tant que paramètres d’entrée du modèle.</span><span class="sxs-lookup"><span data-stu-id="0ebad-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="0ebad-305">value</span><span class="sxs-lookup"><span data-stu-id="0ebad-305">value</span></span> |<span data-ttu-id="0ebad-306">Oui</span><span class="sxs-lookup"><span data-stu-id="0ebad-306">Yes</span></span> |<span data-ttu-id="0ebad-307">Expression du langage du modèle évaluée et retournée sous forme de valeur de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ebad-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="0ebad-308">Hello suivant montre une valeur qui est retournée dans la section des sorties hello.</span><span class="sxs-lookup"><span data-stu-id="0ebad-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="0ebad-309">Pour plus d’informations sur le fonctionnement de la sortie, consultez [Partage d’état dans les modèles Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="0ebad-310">Limites de modèle</span><span class="sxs-lookup"><span data-stu-id="0ebad-310">Template limits</span></span>

<span data-ttu-id="0ebad-311">Limiter la taille de hello de votre modèle too1 Mo et chaque paramètre Ko d’un fichier too64.</span><span class="sxs-lookup"><span data-stu-id="0ebad-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="0ebad-312">limite de 1 Mo Hello applique état final de toohello du modèle de hello après que qu’il a été développée avec les définitions de ressource itératif et valeurs des variables et paramètres.</span><span class="sxs-lookup"><span data-stu-id="0ebad-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="0ebad-313">Vous devez également respecter les limites suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ebad-313">You are also limited to:</span></span>

* <span data-ttu-id="0ebad-314">256 paramètres</span><span class="sxs-lookup"><span data-stu-id="0ebad-314">256 parameters</span></span>
* <span data-ttu-id="0ebad-315">256 variables</span><span class="sxs-lookup"><span data-stu-id="0ebad-315">256 variables</span></span>
* <span data-ttu-id="0ebad-316">800 ressources (incluant le nombre de copies)</span><span class="sxs-lookup"><span data-stu-id="0ebad-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="0ebad-317">64 valeurs de sortie</span><span class="sxs-lookup"><span data-stu-id="0ebad-317">64 output values</span></span>
* <span data-ttu-id="0ebad-318">24 576 caractères dans une expression de modèle</span><span class="sxs-lookup"><span data-stu-id="0ebad-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="0ebad-319">Vous pouvez dépasser certaines limites de modèle en utilisant un modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="0ebad-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="0ebad-320">Pour plus d’informations, consultez l’article [Utilisation de modèles liés lors du déploiement des ressources Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="0ebad-321">nombre de hello tooreduce de paramètres, des variables ou des sorties, vous pouvez combiner plusieurs valeurs dans un objet.</span><span class="sxs-lookup"><span data-stu-id="0ebad-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="0ebad-322">Pour plus d’informations, consultez l’article [Objects as parameters](resource-manager-objects-as-parameters.md) (Utiliser un objet en tant que paramètre).</span><span class="sxs-lookup"><span data-stu-id="0ebad-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ebad-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ebad-323">Next steps</span></span>
* <span data-ttu-id="0ebad-324">tooview des modèles complète pour divers types de solutions, consultez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="0ebad-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="0ebad-325">Pour plus d’informations sur les fonctions hello que vous pouvez utiliser à partir d’un modèle, consultez [fonctions de modèle Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="0ebad-326">plusieurs modèles pendant le déploiement, reportez-vous à toocombine [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="0ebad-327">Vous devrez peut-être les ressources toouse qui existent dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="0ebad-328">Ce scénario est classique quand vous utilisez des comptes de stockage ou des réseaux virtuels qui sont partagés entre plusieurs groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="0ebad-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="0ebad-329">Pour plus d’informations, consultez hello [fonction resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="0ebad-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
