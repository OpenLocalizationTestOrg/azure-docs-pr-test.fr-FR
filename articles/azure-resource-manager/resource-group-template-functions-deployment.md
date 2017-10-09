---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - déploiement | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans les informations de déploiement du tooretrieve modèle Azure Resource Manager."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c1753-103">Fonctions de déploiement pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1753-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="c1753-104">Gestionnaire de ressources fournit suivant de hello fonctionne pour l’obtention des valeurs à partir des sections du modèle de hello et valeurs connexes toohello déploiement :</span><span class="sxs-lookup"><span data-stu-id="c1753-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="c1753-105">deployment</span><span class="sxs-lookup"><span data-stu-id="c1753-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="c1753-106">parameters</span><span class="sxs-lookup"><span data-stu-id="c1753-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="c1753-107">variables</span><span class="sxs-lookup"><span data-stu-id="c1753-107">variables</span></span>](#variables)

<span data-ttu-id="c1753-108">valeurs tooget à partir de ressources, les groupes de ressources ou les abonnements, consultez [fonctions de ressources](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c1753-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="c1753-109">déploiement</span><span class="sxs-lookup"><span data-stu-id="c1753-109">deployment</span></span>
`deployment()`

<span data-ttu-id="c1753-110">Retourne des informations sur l’opération de déploiement actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="c1753-111">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="c1753-111">Return value</span></span>

<span data-ttu-id="c1753-112">Cette fonction retourne un objet hello qui est passée au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1753-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="c1753-113">propriétés Hello Bonjour retourné d’objet diffèrent selon si hello objet de déploiement est passé sous forme de lien ou en tant qu’objet en ligne.</span><span class="sxs-lookup"><span data-stu-id="c1753-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="c1753-114">Lorsque l’objet de déploiement hello est transmis en ligne, comme lors de l’utilisation de hello **- TemplateFile** paramètre dans un fichier local Azure PowerShell toopoint tooa, hello retourné objet a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c1753-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

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

<span data-ttu-id="c1753-115">Lorsqu’un objet de hello est passé sous forme de lien, tels que lorsque l’aide de hello **- TemplateUri** tooa à distance toopoint de paramètre de l’objet, hello est retourné dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c1753-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="c1753-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="c1753-116">Remarks</span></span>

<span data-ttu-id="c1753-117">Vous pouvez utiliser le déploiement() toolink tooanother modèle basé sur hello URI du modèle parent de hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="c1753-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="c1753-118">Example</span></span>

<span data-ttu-id="c1753-119">Hello exemple suivant renvoie hello déploiement objet :</span><span class="sxs-lookup"><span data-stu-id="c1753-119">hello following example returns hello deployment object:</span></span>

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

<span data-ttu-id="c1753-120">Hello exemple précédent retourne hello objet :</span><span class="sxs-lookup"><span data-stu-id="c1753-120">hello preceding example returns hello following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="c1753-121">parameters</span><span class="sxs-lookup"><span data-stu-id="c1753-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="c1753-122">Retourne une valeur de paramètre.</span><span class="sxs-lookup"><span data-stu-id="c1753-122">Returns a parameter value.</span></span> <span data-ttu-id="c1753-123">nom de paramètre spécifié Hello doit être défini dans la section des paramètres de modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="c1753-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c1753-124">Parameters</span></span>

| <span data-ttu-id="c1753-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c1753-125">Parameter</span></span> | <span data-ttu-id="c1753-126">Requis</span><span class="sxs-lookup"><span data-stu-id="c1753-126">Required</span></span> | <span data-ttu-id="c1753-127">Type</span><span class="sxs-lookup"><span data-stu-id="c1753-127">Type</span></span> | <span data-ttu-id="c1753-128">Description</span><span class="sxs-lookup"><span data-stu-id="c1753-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1753-129">nom_paramètre</span><span class="sxs-lookup"><span data-stu-id="c1753-129">parameterName</span></span> |<span data-ttu-id="c1753-130">Oui</span><span class="sxs-lookup"><span data-stu-id="c1753-130">Yes</span></span> |<span data-ttu-id="c1753-131">string</span><span class="sxs-lookup"><span data-stu-id="c1753-131">string</span></span> |<span data-ttu-id="c1753-132">nom de Hello de hello paramètre tooreturn.</span><span class="sxs-lookup"><span data-stu-id="c1753-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c1753-133">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="c1753-133">Return value</span></span>

<span data-ttu-id="c1753-134">valeur Hello hello spécifiée de paramètre.</span><span class="sxs-lookup"><span data-stu-id="c1753-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="c1753-135">Remarques</span><span class="sxs-lookup"><span data-stu-id="c1753-135">Remarks</span></span>

<span data-ttu-id="c1753-136">En règle générale, vous utilisez des valeurs de ressource de tooset de paramètres.</span><span class="sxs-lookup"><span data-stu-id="c1753-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="c1753-137">Hello exemple suivant définit nom hello valeur du paramètre de site web toohello passé durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1753-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="c1753-138">Exemple</span><span class="sxs-lookup"><span data-stu-id="c1753-138">Example</span></span>

<span data-ttu-id="c1753-139">Hello suivant montre une utilisation simplifiée de la fonction de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-139">hello following example shows a simplified use of hello parameters function.</span></span>

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

<span data-ttu-id="c1753-140">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="c1753-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c1753-141">Nom</span><span class="sxs-lookup"><span data-stu-id="c1753-141">Name</span></span> | <span data-ttu-id="c1753-142">Type</span><span class="sxs-lookup"><span data-stu-id="c1753-142">Type</span></span> | <span data-ttu-id="c1753-143">Valeur</span><span class="sxs-lookup"><span data-stu-id="c1753-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c1753-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c1753-144">stringOutput</span></span> | <span data-ttu-id="c1753-145">String</span><span class="sxs-lookup"><span data-stu-id="c1753-145">String</span></span> | <span data-ttu-id="c1753-146">option 1</span><span class="sxs-lookup"><span data-stu-id="c1753-146">option 1</span></span> |
| <span data-ttu-id="c1753-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="c1753-147">intOutput</span></span> | <span data-ttu-id="c1753-148">int</span><span class="sxs-lookup"><span data-stu-id="c1753-148">Int</span></span> | <span data-ttu-id="c1753-149">1</span><span class="sxs-lookup"><span data-stu-id="c1753-149">1</span></span> |
| <span data-ttu-id="c1753-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c1753-150">objectOutput</span></span> | <span data-ttu-id="c1753-151">Object</span><span class="sxs-lookup"><span data-stu-id="c1753-151">Object</span></span> | <span data-ttu-id="c1753-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="c1753-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="c1753-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c1753-153">arrayOutput</span></span> | <span data-ttu-id="c1753-154">Tableau</span><span class="sxs-lookup"><span data-stu-id="c1753-154">Array</span></span> | <span data-ttu-id="c1753-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="c1753-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="c1753-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="c1753-156">crossOutput</span></span> | <span data-ttu-id="c1753-157">String</span><span class="sxs-lookup"><span data-stu-id="c1753-157">String</span></span> | <span data-ttu-id="c1753-158">option 1</span><span class="sxs-lookup"><span data-stu-id="c1753-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="c1753-159">variables</span><span class="sxs-lookup"><span data-stu-id="c1753-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="c1753-160">Retourne hello la valeur de variable.</span><span class="sxs-lookup"><span data-stu-id="c1753-160">Returns hello value of variable.</span></span> <span data-ttu-id="c1753-161">nom de variable spécifié Hello doit être défini dans la section sur les variables du modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="c1753-162">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c1753-162">Parameters</span></span>

| <span data-ttu-id="c1753-163">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c1753-163">Parameter</span></span> | <span data-ttu-id="c1753-164">Requis</span><span class="sxs-lookup"><span data-stu-id="c1753-164">Required</span></span> | <span data-ttu-id="c1753-165">Type</span><span class="sxs-lookup"><span data-stu-id="c1753-165">Type</span></span> | <span data-ttu-id="c1753-166">Description</span><span class="sxs-lookup"><span data-stu-id="c1753-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1753-167">variableName</span><span class="sxs-lookup"><span data-stu-id="c1753-167">variableName</span></span> |<span data-ttu-id="c1753-168">Oui</span><span class="sxs-lookup"><span data-stu-id="c1753-168">Yes</span></span> |<span data-ttu-id="c1753-169">String</span><span class="sxs-lookup"><span data-stu-id="c1753-169">String</span></span> |<span data-ttu-id="c1753-170">nom de Hello de tooreturn de variable hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c1753-171">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="c1753-171">Return value</span></span>

<span data-ttu-id="c1753-172">valeur Hello de hello.</span><span class="sxs-lookup"><span data-stu-id="c1753-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="c1753-173">Remarques</span><span class="sxs-lookup"><span data-stu-id="c1753-173">Remarks</span></span>

<span data-ttu-id="c1753-174">En règle générale, vous utilisez variables toosimplify votre modèle en créant des valeurs complexes qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="c1753-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="c1753-175">Hello exemple suivant crée un nom unique pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c1753-175">hello following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="c1753-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="c1753-176">Example</span></span>

<span data-ttu-id="c1753-177">exemple de modèle de Hello retourne des valeurs de variables différentes.</span><span class="sxs-lookup"><span data-stu-id="c1753-177">hello example template returns different variable values.</span></span>

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

<span data-ttu-id="c1753-178">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="c1753-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c1753-179">Nom</span><span class="sxs-lookup"><span data-stu-id="c1753-179">Name</span></span> | <span data-ttu-id="c1753-180">Type</span><span class="sxs-lookup"><span data-stu-id="c1753-180">Type</span></span> | <span data-ttu-id="c1753-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="c1753-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c1753-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="c1753-182">exampleOutput1</span></span> | <span data-ttu-id="c1753-183">String</span><span class="sxs-lookup"><span data-stu-id="c1753-183">String</span></span> | <span data-ttu-id="c1753-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="c1753-184">myVariable</span></span> |
| <span data-ttu-id="c1753-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="c1753-185">exampleOutput2</span></span> | <span data-ttu-id="c1753-186">Tableau</span><span class="sxs-lookup"><span data-stu-id="c1753-186">Array</span></span> | <span data-ttu-id="c1753-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="c1753-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="c1753-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="c1753-188">exampleOutput3</span></span> | <span data-ttu-id="c1753-189">String</span><span class="sxs-lookup"><span data-stu-id="c1753-189">String</span></span> | <span data-ttu-id="c1753-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="c1753-190">myVariable</span></span> |
| <span data-ttu-id="c1753-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="c1753-191">exampleOutput4</span></span> |  <span data-ttu-id="c1753-192">Object</span><span class="sxs-lookup"><span data-stu-id="c1753-192">Object</span></span> | <span data-ttu-id="c1753-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="c1753-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1753-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1753-194">Next steps</span></span>
* <span data-ttu-id="c1753-195">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c1753-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c1753-196">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c1753-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c1753-197">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c1753-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c1753-198">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c1753-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

