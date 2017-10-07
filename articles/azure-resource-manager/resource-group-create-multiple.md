---
title: aaaDeploy plusieurs instances de ressources Azure | Documents Microsoft
description: "Utilisez opération de copie et de tableaux dans un tooiterate de modèle Azure Resource Manager plusieurs fois lors du déploiement de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Déployer plusieurs instances d’une ressource ou d’une propriété dans des modèles Azure Resource Manager
Cette rubrique vous montre comment tooiterate dans votre toocreate de modèle Azure Resource Manager plusieurs instances d’une ressource, ou plusieurs instances d’une propriété sur une ressource.

Si vous avez besoin tooadd logique tooyour modèle qui vous permet de toospecify qu’une ressource est déployée, consultez [déployer de manière conditionnelle ressource](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Itération de ressource
Ajout de plusieurs instances d’un type de ressource, toocreate un `copy` type d’élément de ressource toohello. Dans l’élément de copie hello, vous spécifiez nombre hello des itérations et un nom pour cette boucle. valeur du nombre Hello doit être un entier positif et ne peut pas dépasser 800. Le Gestionnaire de ressources crée les ressources hello en parallèle. Par conséquent, la commande hello dans lequel ils sont créés n’est pas garantie. ressources toocreate itérée dans l’ordre, consultez [copie série](#serial-copy). 

Hello ressource toocreate plusieurs fois prend hello suivant le format :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

Notez que hello nom de chaque ressource inclut hello `copyIndex()` fonction, qui retourne l’itération actuelle de hello dans la boucle de hello. `copyIndex()` est basé sur zéro. Hello c’est le cas, l’exemple suivant :

```json
"name": "[concat('storage', copyIndex())]",
```

Crée les noms suivants :

* storage0
* storage1
* storage2.

valeur d’index toooffset hello, vous pouvez passer une valeur dans la fonction de copyIndex() hello. Hello nombre d’itérations tooperform est toujours spécifié dans l’élément de copie hello, mais valeur hello copyIndex est décalé par hello spécifié valeur. Hello c’est le cas, l’exemple suivant :

```json
"name": "[concat('storage', copyIndex(1))]",
```

Crée les noms suivants :

* storage1
* storage2
* storage3

opération de copie Hello est utile lorsque vous travaillez avec des tableaux, car vous pouvez itérer dans chaque élément de tableau de hello. Hello d’utilisation `length` fonction hello tableau toospecify hello termes de nombre d’itérations, et `copyIndex` tooretrieve hello actuel index hello tableau. Hello c’est le cas, l’exemple suivant :

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Crée les noms suivants :

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Copie en série

Lorsque vous utilisez hello copie élément toocreate plusieurs instances d’un type de ressource, le Gestionnaire de ressources, par défaut, déploie ces instances en parallèle. Toutefois, vous souhaiterez peut-être toospecify que hello ressources sont déployées dans la séquence. Par exemple, lors de la mise à jour d’un environnement de production, vous pouvez choisir toostagger hello et seul un certain nombre des mises à jour sont mis à jour à tout moment.

Le Gestionnaire de ressources fournit des propriétés qui permettent de vous tooserially sur l’élément de copie hello déploiement plusieurs instances. Dans l’élément de copie hello, définissez `mode` trop**série** et `batchSize` nombre toohello de toodeploy d’instances à la fois. En mode série, le Gestionnaire de ressources crée une dépendance sur les instances plus haut dans la boucle de hello, afin qu’il ne démarre pas un lot jusqu'à ce que le lot précédent de hello se termine.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Hello propriété mode accepte également **parallèles**, qui est la valeur par défaut de hello.

tootest série copie sans créer de ressources réelles, hello utilisation suivant le modèle qui déploie des modèles imbriqués vides :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

Dans l’historique de déploiement hello, notez que hello déploiements imbriquées sont traitées dans la séquence.

![déploiement en série](./media/resource-group-create-multiple/serial-copy.png)

Pour un scénario plus réaliste, hello exemple suivant déploie les deux instances à la fois d’un VM Linux à partir d’un modèle imbriqué :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Itération de propriété

Ajout de plusieurs valeurs pour une propriété sur une ressource, toocreate un `copy` tableau dans l’élément de propriétés hello. Ce tableau contient des objets, et chaque objet a hello propriétés suivantes :

* nom : nom de hello de hello propriété toocreate plusieurs valeurs pour
* Count : nombre de hello de valeurs toocreate
* entrée - un objet qui contient la propriété hello valeurs tooassign toohello  

Hello suivant montre l’exemple de comment tooapply `copy` propriété dataDisks de toohello sur un ordinateur virtuel :

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Notez que lorsque vous utilisez `copyIndex` à l’intérieur d’une itération de la propriété, vous devez fournir le nom hello d’itération de hello. Vous n’avez pas de nom de hello tooprovide lorsqu’il est utilisé avec l’itération de la ressource.

Le Gestionnaire de ressources se développe hello `copy` tableau durant le déploiement. nom de Hello du tableau de hello devient nom hello de propriété de hello. les valeurs d’entrée Hello deviennent des propriétés de l’objet hello. modèle de Hello déployé devient :

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Vous pouvez utiliser des itérations de ressource et de propriété ensemble. Référence hello propriété l’itération par nom.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

Vous ne pouvez inclure qu’un seul élément de la copie dans les propriétés de hello pour chaque ressource. toospecify une boucle d’itération pour plus d’une propriété, définir plusieurs objets dans le tableau de copie hello. Chaque objet est itéré séparément. Par exemple, toocreate plusieurs instances de ces deux hello `frontendIPConfigurations` propriété et hello `loadBalancingRules` propriété sur un équilibrage de charge, définir les deux objets dans un élément de copie unique : 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>En fonction des ressources dans une boucle
Vous spécifiez qu’une ressource est déployée après une autre ressource à l’aide de hello `dependsOn` élément. toodeploy une ressource dont dépend la collection hello des ressources dans une boucle, fournir un nom hello de boucle de copie hello dans l’élément dependsOn de hello. Bonjour à l’exemple suivant montre comment toodeploy trois comptes de stockage avant de déployer hello Machine virtuelle. définition de Machine virtuelle complète Hello n’est pas affichée. Notez que cet élément de la copie hello a le nom défini trop`storagecopy` et élément de dependsOn hello pour les Machines virtuelles de hello est également défini trop`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Création de plusieurs instances d’une ressource enfant
Vous ne pouvez pas utiliser une boucle de copie pour une ressource enfant. toocreate plusieurs instances d’une ressource que vous définissez généralement comme imbriquées dans une autre ressource, vous devez créer à la place cette ressource en tant qu’une ressource de niveau supérieur. Vous définissez la relation de hello avec la ressource parent de hello via les propriétés de type et le nom hello.

Par exemple, supposons que vous définissez généralement un jeu de données comme une ressource enfant dans une fabrique de données.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate plusieurs instances de jeux de données, déplacez-la en dehors de la fabrique de données hello. Hello dataset doit être au même niveau en tant que fabrique de données hello de hello, mais il est toujours une ressource enfant hello fabrique de données. Vous conservez la relation hello entre le jeu de données et de la fabrique de données via les propriétés de type et le nom hello. Étant donné que le type n’est plus peut être déduit qu’à partir de sa position dans le modèle de hello, vous devez fournir le type hello complet au format de hello : `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish une relation parent/enfant avec une instance de la fabrique de données hello, fournissez un nom pour le jeu de données hello qui inclut le nom de la ressource parent hello. Utilisez le format hello : `{parent-resource-name}/{child-resource-name}`.  

Hello exemple suivant illustre hello implémentation :

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Déployer une ressource de manière conditionnelle

toospecify si une ressource est déployée, utilisez hello `condition` élément. valeur Hello pour cet élément résout tootrue ou false. Lorsque la valeur de hello est true, les ressources hello sont déployé. Lorsque la valeur de hello est false, les ressources hello ne sont pas déployée. Par exemple, toospecify si un compte de stockage est déployé ou un compte de stockage existant est utilisé, utilisez :

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

Pour obtenir un exemple d’utilisation d’une ressource nouvelle ou existante, voir [Modèle de condition New ou Existing](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Pour obtenir un exemple de l’utilisation d’un mot de passe ou d’un ordinateur virtuel de toodeploy clé SSH, consultez [modèle de condition de nom d’utilisateur ou de SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Étapes suivantes
* Si vous souhaitez toolearn sur les sections hello d’un modèle, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md).
* toolearn comment toodeploy votre modèle, consultez [déployer une application avec le modèle de gestionnaire de ressources Azure](resource-group-template-deploy.md).

