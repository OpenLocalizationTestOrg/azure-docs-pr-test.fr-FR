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
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Fonctions de déploiement pour les modèles Azure Resource Manager 

Gestionnaire de ressources fournit suivant de hello fonctionne pour l’obtention des valeurs à partir des sections du modèle de hello et valeurs connexes toohello déploiement :

* [deployment](#deployment)
* [parameters](#parameters)
* [variables](#variables)

valeurs tooget à partir de ressources, les groupes de ressources ou les abonnements, consultez [fonctions de ressources](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>déploiement
`deployment()`

Retourne des informations sur l’opération de déploiement actuelle hello.

### <a name="return-value"></a>Valeur de retour

Cette fonction retourne un objet hello qui est passée au cours du déploiement. propriétés Hello Bonjour retourné d’objet diffèrent selon si hello objet de déploiement est passé sous forme de lien ou en tant qu’objet en ligne. Lorsque l’objet de déploiement hello est transmis en ligne, comme lors de l’utilisation de hello **- TemplateFile** paramètre dans un fichier local Azure PowerShell toopoint tooa, hello retourné objet a hello suivant le format :

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

Lorsqu’un objet de hello est passé sous forme de lien, tels que lorsque l’aide de hello **- TemplateUri** tooa à distance toopoint de paramètre de l’objet, hello est retourné dans hello suivant le format : 

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

### <a name="remarks"></a>Remarques

Vous pouvez utiliser le déploiement() toolink tooanother modèle basé sur hello URI du modèle parent de hello.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Exemple

Hello exemple suivant renvoie hello déploiement objet :

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

Hello exemple précédent retourne hello objet :

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

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Retourne une valeur de paramètre. nom de paramètre spécifié Hello doit être défini dans la section des paramètres de modèle de hello hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| nom_paramètre |Oui |string |nom de Hello de hello paramètre tooreturn. |

### <a name="return-value"></a>Valeur de retour

valeur Hello hello spécifiée de paramètre.

### <a name="remarks"></a>Remarques

En règle générale, vous utilisez des valeurs de ressource de tooset de paramètres. Hello exemple suivant définit nom hello valeur du paramètre de site web toohello passé durant le déploiement.

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

### <a name="example"></a>Exemple

Hello suivant montre une utilisation simplifiée de la fonction de paramètres hello.

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

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| stringOutput | String | option 1 |
| intOutput | int | 1 |
| objectOutput | Object | {"one": "a", "two": "b"} |
| arrayOutput | Tableau | [1, 2, 3] |
| crossOutput | String | option 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

Retourne hello la valeur de variable. nom de variable spécifié Hello doit être défini dans la section sur les variables du modèle de hello hello.

### <a name="parameters"></a>Paramètres

| Paramètre | Requis | Type | Description |
|:--- |:--- |:--- |:--- |
| variableName |Oui |String |nom de Hello de tooreturn de variable hello. |

### <a name="return-value"></a>Valeur de retour

valeur Hello de hello.

### <a name="remarks"></a>Remarques

En règle générale, vous utilisez variables toosimplify votre modèle en créant des valeurs complexes qu’une seule fois. Hello exemple suivant crée un nom unique pour un compte de stockage.

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

### <a name="example"></a>Exemple

exemple de modèle de Hello retourne des valeurs de variables différentes.

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

Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :

| Nom | Type | Valeur |
| ---- | ---- | ----- |
| exampleOutput1 | String | myVariable |
| exampleOutput2 | Tableau | [1, 2, 3, 4] |
| exampleOutput3 | String | myVariable |
| exampleOutput4 |  Object | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).
* toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

