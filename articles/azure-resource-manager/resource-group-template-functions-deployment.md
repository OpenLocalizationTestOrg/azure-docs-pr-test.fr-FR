---
title: "Fonctions de modèle Azure Resource Manager - déploiement| Microsoft Docs"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour récupérer des informations de déploiement."
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="785db-103">Fonctions de déploiement pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="785db-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="785db-104">Resource Manager offre les fonctions ci-après pour l’obtention de valeurs à partir des sections du modèle et de valeurs associées au déploiement :</span><span class="sxs-lookup"><span data-stu-id="785db-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="785db-105">deployment</span><span class="sxs-lookup"><span data-stu-id="785db-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="785db-106">parameters</span><span class="sxs-lookup"><span data-stu-id="785db-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="785db-107">variables</span><span class="sxs-lookup"><span data-stu-id="785db-107">variables</span></span>](#variables)

<span data-ttu-id="785db-108">Pour obtenir des valeurs de ressources, de groupes de ressources ou d’abonnements, consultez [Fonctions de ressource](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="785db-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="785db-109">déploiement</span><span class="sxs-lookup"><span data-stu-id="785db-109">deployment</span></span>
`deployment()`

<span data-ttu-id="785db-110">Renvoie des informations sur l’opération de déploiement actuelle.</span><span class="sxs-lookup"><span data-stu-id="785db-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="785db-111">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="785db-111">Return value</span></span>

<span data-ttu-id="785db-112">Cette fonction retourne l’objet transmis au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="785db-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="785db-113">Les propriétés de l’objet renvoyé diffèrent selon que l’objet de déploiement est passé sous forme de lien ou d’objet inline.</span><span class="sxs-lookup"><span data-stu-id="785db-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="785db-114">Quand l’objet de déploiement est passé inline, comme lors de l’utilisation du paramètre **-TemplateFile** dans Azure PowerShell pour pointer vers un fichier local, l’objet renvoyé a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="785db-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="785db-115">Quand l’objet est passé comme lien, par exemple lors de l’utilisation du paramètre **-TemplateUri** pour pointer vers un objet distant, l’objet est retourné dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="785db-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="785db-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="785db-116">Remarks</span></span>

<span data-ttu-id="785db-117">Vous pouvez utiliser deployment() pour établir une liaison à un autre modèle en fonction de l’URI du modèle parent.</span><span class="sxs-lookup"><span data-stu-id="785db-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="785db-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="785db-118">Example</span></span>

<span data-ttu-id="785db-119">L’exemple suivant retourne l’objet de déploiement :</span><span class="sxs-lookup"><span data-stu-id="785db-119">The following example returns the deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="785db-120">L’exemple précédent retourne l’objet suivant :</span><span class="sxs-lookup"><span data-stu-id="785db-120">The preceding example returns the following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="785db-121">parameters</span><span class="sxs-lookup"><span data-stu-id="785db-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="785db-122">Retourne une valeur de paramètre.</span><span class="sxs-lookup"><span data-stu-id="785db-122">Returns a parameter value.</span></span> <span data-ttu-id="785db-123">Le nom de paramètre spécifié doit être défini dans la section parameters du modèle.</span><span class="sxs-lookup"><span data-stu-id="785db-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="785db-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="785db-124">Parameters</span></span>

| <span data-ttu-id="785db-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="785db-125">Parameter</span></span> | <span data-ttu-id="785db-126">Requis</span><span class="sxs-lookup"><span data-stu-id="785db-126">Required</span></span> | <span data-ttu-id="785db-127">Type</span><span class="sxs-lookup"><span data-stu-id="785db-127">Type</span></span> | <span data-ttu-id="785db-128">Description</span><span class="sxs-lookup"><span data-stu-id="785db-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="785db-129">nom_paramètre</span><span class="sxs-lookup"><span data-stu-id="785db-129">parameterName</span></span> |<span data-ttu-id="785db-130">Oui</span><span class="sxs-lookup"><span data-stu-id="785db-130">Yes</span></span> |<span data-ttu-id="785db-131">string</span><span class="sxs-lookup"><span data-stu-id="785db-131">string</span></span> |<span data-ttu-id="785db-132">Nom du paramètre à retourner.</span><span class="sxs-lookup"><span data-stu-id="785db-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="785db-133">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="785db-133">Return value</span></span>

<span data-ttu-id="785db-134">La valeur du paramètre spécifié.</span><span class="sxs-lookup"><span data-stu-id="785db-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="785db-135">Remarques</span><span class="sxs-lookup"><span data-stu-id="785db-135">Remarks</span></span>

<span data-ttu-id="785db-136">En général, vous utilisez les paramètres pour définir les valeurs de la ressource.</span><span class="sxs-lookup"><span data-stu-id="785db-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="785db-137">L’exemple suivant définit le nom du site web sur la valeur du paramètre transmise au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="785db-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="785db-138">Exemple</span><span class="sxs-lookup"><span data-stu-id="785db-138">Example</span></span>

<span data-ttu-id="785db-139">L'exemple suivant montre une utilisation simplifiée de la fonction parameters.</span><span class="sxs-lookup"><span data-stu-id="785db-139">The following example shows a simplified use of the parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="785db-140">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="785db-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="785db-141">Nom</span><span class="sxs-lookup"><span data-stu-id="785db-141">Name</span></span> | <span data-ttu-id="785db-142">Type</span><span class="sxs-lookup"><span data-stu-id="785db-142">Type</span></span> | <span data-ttu-id="785db-143">Valeur</span><span class="sxs-lookup"><span data-stu-id="785db-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="785db-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="785db-144">stringOutput</span></span> | <span data-ttu-id="785db-145">String</span><span class="sxs-lookup"><span data-stu-id="785db-145">String</span></span> | <span data-ttu-id="785db-146">option 1</span><span class="sxs-lookup"><span data-stu-id="785db-146">option 1</span></span> |
| <span data-ttu-id="785db-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="785db-147">intOutput</span></span> | <span data-ttu-id="785db-148">int</span><span class="sxs-lookup"><span data-stu-id="785db-148">Int</span></span> | <span data-ttu-id="785db-149">1</span><span class="sxs-lookup"><span data-stu-id="785db-149">1</span></span> |
| <span data-ttu-id="785db-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="785db-150">objectOutput</span></span> | <span data-ttu-id="785db-151">Object</span><span class="sxs-lookup"><span data-stu-id="785db-151">Object</span></span> | <span data-ttu-id="785db-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="785db-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="785db-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="785db-153">arrayOutput</span></span> | <span data-ttu-id="785db-154">Tableau</span><span class="sxs-lookup"><span data-stu-id="785db-154">Array</span></span> | <span data-ttu-id="785db-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="785db-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="785db-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="785db-156">crossOutput</span></span> | <span data-ttu-id="785db-157">String</span><span class="sxs-lookup"><span data-stu-id="785db-157">String</span></span> | <span data-ttu-id="785db-158">option 1</span><span class="sxs-lookup"><span data-stu-id="785db-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="785db-159">variables</span><span class="sxs-lookup"><span data-stu-id="785db-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="785db-160">Retourne la valeur de la variable.</span><span class="sxs-lookup"><span data-stu-id="785db-160">Returns the value of variable.</span></span> <span data-ttu-id="785db-161">Le nom de variable spécifié doit être défini dans la section variables du modèle.</span><span class="sxs-lookup"><span data-stu-id="785db-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="785db-162">Paramètres</span><span class="sxs-lookup"><span data-stu-id="785db-162">Parameters</span></span>

| <span data-ttu-id="785db-163">Paramètre</span><span class="sxs-lookup"><span data-stu-id="785db-163">Parameter</span></span> | <span data-ttu-id="785db-164">Requis</span><span class="sxs-lookup"><span data-stu-id="785db-164">Required</span></span> | <span data-ttu-id="785db-165">Type</span><span class="sxs-lookup"><span data-stu-id="785db-165">Type</span></span> | <span data-ttu-id="785db-166">Description</span><span class="sxs-lookup"><span data-stu-id="785db-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="785db-167">variableName</span><span class="sxs-lookup"><span data-stu-id="785db-167">variableName</span></span> |<span data-ttu-id="785db-168">Oui</span><span class="sxs-lookup"><span data-stu-id="785db-168">Yes</span></span> |<span data-ttu-id="785db-169">String</span><span class="sxs-lookup"><span data-stu-id="785db-169">String</span></span> |<span data-ttu-id="785db-170">Nom de la variable à retourner.</span><span class="sxs-lookup"><span data-stu-id="785db-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="785db-171">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="785db-171">Return value</span></span>

<span data-ttu-id="785db-172">La valeur de la variable spécifiée.</span><span class="sxs-lookup"><span data-stu-id="785db-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="785db-173">Remarques</span><span class="sxs-lookup"><span data-stu-id="785db-173">Remarks</span></span>

<span data-ttu-id="785db-174">En général, vous utilisez les variables pour simplifier votre modèle en créant des valeurs complexes une seule fois.</span><span class="sxs-lookup"><span data-stu-id="785db-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="785db-175">L’exemple suivant crée un nom unique pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="785db-175">The following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="785db-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="785db-176">Example</span></span>

<span data-ttu-id="785db-177">L’exemple de modèle retourne différentes valeurs de variables.</span><span class="sxs-lookup"><span data-stu-id="785db-177">The example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="785db-178">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="785db-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="785db-179">Nom</span><span class="sxs-lookup"><span data-stu-id="785db-179">Name</span></span> | <span data-ttu-id="785db-180">Type</span><span class="sxs-lookup"><span data-stu-id="785db-180">Type</span></span> | <span data-ttu-id="785db-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="785db-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="785db-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="785db-182">exampleOutput1</span></span> | <span data-ttu-id="785db-183">String</span><span class="sxs-lookup"><span data-stu-id="785db-183">String</span></span> | <span data-ttu-id="785db-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="785db-184">myVariable</span></span> |
| <span data-ttu-id="785db-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="785db-185">exampleOutput2</span></span> | <span data-ttu-id="785db-186">Tableau</span><span class="sxs-lookup"><span data-stu-id="785db-186">Array</span></span> | <span data-ttu-id="785db-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="785db-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="785db-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="785db-188">exampleOutput3</span></span> | <span data-ttu-id="785db-189">String</span><span class="sxs-lookup"><span data-stu-id="785db-189">String</span></span> | <span data-ttu-id="785db-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="785db-190">myVariable</span></span> |
| <span data-ttu-id="785db-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="785db-191">exampleOutput4</span></span> |  <span data-ttu-id="785db-192">Object</span><span class="sxs-lookup"><span data-stu-id="785db-192">Object</span></span> | <span data-ttu-id="785db-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="785db-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="785db-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="785db-194">Next steps</span></span>
* <span data-ttu-id="785db-195">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="785db-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="785db-196">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="785db-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="785db-197">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="785db-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="785db-198">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="785db-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

