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
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Comprendre la structure de hello et syntaxe des modèles Azure Resource Manager
Cette rubrique décrit la structure hello d’un modèle Azure Resource Manager. Elle présente hello différentes sections d’un modèle et hello des propriétés qui sont disponibles dans ces sections. modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement. Pour obtenir un didacticiel étape par étape permettant de créer un modèle, voir [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Format de modèle
Dans la structure la plus simple, un modèle contient hello suivant d’éléments :

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

| Nom de l'élément | Requis | Description |
|:--- |:--- |:--- |
| $schema |Oui |Emplacement du fichier de schéma JSON hello qui décrit la version de hello du langage de modèle hello. Utilisez les URL hello indiqué dans le précédent exemple de hello. |
| contentVersion |Oui |Version du modèle hello (par exemple, 1.0.0.0). Vous pouvez fournir n’importe quelle valeur pour cet élément. Lorsque vous déployez des ressources à l’aide du modèle de hello, cette valeur peut être utilisé toomake que ce modèle hello est utilisé. |
| parameters |Non |Les valeurs fournies lorsque le déploiement est exécuté le déploiement de ressources toocustomize. |
| variables |Non |Valeurs qui sont utilisées en tant que fragments JSON dans les expressions de langage de modèle hello modèle toosimplify. |
| les ressources |Oui |Types de ressource déployés ou mis à jour dans un groupe de ressources. |
| outputs |Non |Valeurs retournées après le déploiement. |

Chaque élément contient des propriétés que vous définissez. Hello, l’exemple suivant contient une syntaxe complète de hello pour un modèle :

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

Nous examinons sections hello du modèle hello plus en détail plus loin dans cette rubrique.

## <a name="expressions-and-functions"></a>Expressions et fonctions
syntaxe de base Hello du modèle de hello est JSON. Toutefois, les expressions et fonctions étendent hello JSON de valeurs disponibles dans le modèle de hello.  Les expressions sont écrites dans les littéraux de chaîne JSON dont le premier et dernier caractères sont des crochets de hello : `[` et `]`, respectivement. valeur de Hello d’expression de hello est évaluée lorsque le modèle de hello est déployé. Alors qu’écrite sous la forme d’un littéral de chaîne, les résultats hello de l’évaluation d’expression de hello peut être de type JSON différent, tel qu’un tableau ou d’un entier, en fonction de l’expression réelle de hello.  toohave une chaîne littérale commencer par un crochet `[`, mais pas soit interprétée comme une expression, ajoutez une crochet supplémentaire toostart hello chaîne `[[`.

En règle générale, vous utilisez des expressions avec les opérations de tooperform des fonctions de configuration de déploiement de hello. Comme en JavaScript, les appels de fonction sont formatés comme suit : `functionName(arg1,arg2,arg3)`. Référencer des propriétés en utilisant des opérateurs de point et [index] hello.

Hello, l’exemple suivant montre comment plusieurs fonctions lors de la construction de toouse valeurs :

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Pour hello une liste complète des fonctions de modèle, consultez [fonctions de modèle Azure Resource Manager](resource-group-template-functions.md). 

## <a name="parameters"></a>Paramètres
Dans la section Paramètres de hello du modèle de hello, vous spécifiez les valeurs que vous pouvez entrer lorsque vous déployez hello des ressources. Ces valeurs de paramètres permettent de déploiement de hello toocustomize en fournissant des valeurs qui sont adaptés pour un environnement particulier (par exemple, le développement, test et production). Vous n’avez pas de paramètres de tooprovide dans votre modèle, mais sans les paramètres de votre modèle est toujours déployer hello ressources mêmes avec hello même des noms, des emplacements et des propriétés.

Vous définissez des paramètres par hello suivant structure :

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

| Nom de l'élément | Requis | Description |
|:--- |:--- |:--- |
| nom_paramètre |Oui |Nom du paramètre hello. Doit être un identificateur JavaScript valide. |
| type |Oui |Type de valeur de paramètre hello. Consultez la liste hello des types autorisés après ce tableau. |
| defaultValue |Non |Valeur par défaut pour le paramètre hello, si aucune valeur n’est fournie pour le paramètre hello. |
| allowedValues |Non |Tableau de valeurs autorisées pour toomake de paramètre hello assurer que la valeur de droite hello est fourni. |
| minValue |Non |valeur minimale de Hello pour les paramètres de type int, cette valeur est incluse. |
| maxValue |Non |valeur maximale de Hello pour les paramètres de type int, cette valeur est incluse. |
| minLength |Non |longueur minimale de Hello pour secureString, de chaîne et les paramètres de type tableau, cette valeur est incluse. |
| maxLength |Non |longueur maximale de Hello pour secureString, de chaîne et les paramètres de type tableau, cette valeur est incluse. |
| description |Non |Description du paramètre hello qui est affichée toousers via le portail de hello. |

Hello les valeurs et les types autorisés sont :

* **string**
* **secureString**
* **int**
* **bool**
* **object** 
* **secureObject**
* **array**

toospecify un paramètre comme facultatif, fournissent un defaultValue (peut être d’une chaîne vide). 

Si vous spécifiez un nom de paramètre dans votre modèle qui correspond à un paramètre de modèle de hello hello commande toodeploy, il est ambiguïté sur les valeurs hello que vous fournissez. Le Gestionnaire de ressources résout cette confusion en ajoutant le suffixe de hello **modèle** paramètre de modèle toohello. Par exemple, si vous incluez un paramètre nommé **ResourceGroupName** dans votre modèle, il est en conflit avec hello **ResourceGroupName** paramètre Bonjour [ Nouveau-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) applet de commande. Pendant le déploiement, vous êtes invité à tooprovide une valeur pour **ResourceGroupNameFromTemplate**. En règle générale, vous devez éviter cette confusion en nommant ne pas de paramètres avec le même nom en tant que paramètres utilisés pour les opérations de déploiement de hello.

> [!NOTE]
> Tous les mots de passe, les clés et autres secrets doivent utiliser hello **secureString** type. Si vous passez des données sensibles dans un objet JSON, utilisez hello **secureObject** type. Il est impossible de lire les paramètres du modèle dont le type est secureString ou secureObject après le déploiement de la ressource. 
> 
> Par exemple, hello entrée suivante dans l’historique de déploiement hello affiche hello valeur pour une chaîne et un objet, mais pas pour secureString et secureObject.
>
> ![afficher les valeurs de déploiement](./media/resource-group-authoring-templates/show-parameters.png)  
>

Hello suivant montre l’exemple de comment toodefine paramètres :

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

Pour la tooinput hello valeurs de paramètre, au cours du déploiement, consultez [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md). 

## <a name="variables"></a>variables
Dans la section de variables hello, vous construisez des valeurs qui peuvent être utilisées dans l’ensemble de votre modèle. Vous n’avez pas besoin de toodefine variables, mais ils simplifient souvent votre modèle en réduisant les expressions complexes.

Vous définissez des variables avec hello suivant structure :

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Hello suivant montre l’exemple de comment toodefine une variable qui est construite à partir de deux valeurs de paramètre :

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Hello l’exemple suivant montre une variable qui est un type complexe de JSON et les variables qui sont construits à partir d’autres variables :

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

## <a name="resources"></a>Ressources
Dans la section relative aux ressources hello, vous définissez des ressources hello qui sont déployés ou mis à jour. Cette section peut se compliquer, car vous devez comprendre hello types que vous déployez des valeurs tooprovide hello. Hello propres à la ressource valeurs (apiVersion, type et propriétés) que vous avez besoin de tooset [définir des ressources dans les modèles Azure Resource Manager](/azure/templates/). 

Vous définissez des ressources par hello suivant structure :

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

| Nom de l'élément | Requis | Description |
|:--- |:--- |:--- |
| condition | Non | Valeur booléenne qui indique si les ressources hello sont déployée. |
| apiVersion |Oui |Version de toouse d’API REST hello pour la création de ressources de hello. |
| type |Oui |Type de ressource de hello. Cette valeur est une combinaison de l’espace de noms hello de fournisseur de ressources hello et type de ressource hello (tel que **/storageaccounts**). |
| name |Oui |Nom de ressource de hello. Hello doit respecter les restrictions de composant URI définies dans la norme RFC 3986. En outre, les services Azure qui exposent les parties de toooutside de nom de ressource hello valider toomake de nom hello qu’il se n'agit pas d’une tentative toospoof une autre identité. |
| location |Varie |Emplacements géographiques pris en charge de hello fournissait des ressources. Vous pouvez sélectionner un des emplacements disponibles de hello, mais en général rend sens toopick qui tooyour fermer des utilisateurs. En règle générale, il peut s’avérer utile ressources tooplace qui interagissent entre eux dans hello même région. La plupart des types de ressources nécessitent un emplacement, mais certains types (par exemple, une affectation de rôle) ne nécessitent aucun emplacement. Voir [Définir l’emplacement des ressources dans les modèles Azure Resource Manager](resource-manager-template-location.md). |
| tags |Non |Balises qui sont associés à des ressources de hello. Voir [Appliquer des balises aux ressources dans les modèles Azure Resource Manager](resource-manager-template-tags.md). |
| commentaires |Non |Vos commentaires pour documenter les ressources hello dans votre modèle. |
| copy |Non |Si plusieurs instances est nécessaire, hello le nombre de ressources toocreate. mode par défaut de Hello est parallèle. Spécifiez le mode série quand ne pas tous ou hello toodeploy de ressources à hello même temps. Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |Non |Les ressources qui doivent être déployées avant le déploiement de cette ressource. Le Gestionnaire de ressources évalue des dépendances hello entre les ressources et les déploie dans l’ordre correct de hello. Quand les ressources ne dépendent les unes des autres, leur déploiement se fait en parallèle. Hello valeur peut être une liste séparée par des virgules d’une ressource de noms ou des identificateurs de ressources unique. Répertoriez uniquement les ressources qui sont déployées dans ce modèle. Les ressources qui ne sont pas définies dans ce modèle doivent déjà exister. Évitez d’ajouter des dépendances inutiles, car cela risque de ralentir votre déploiement et de créer des dépendances circulaires. Pour savoir comment définir des dépendances, consultez [Définition de dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md). |
| properties |Non |Paramètres de configuration spécifiques aux ressources. les valeurs Hello pour les propriétés de hello sont même hello en tant que valeurs hello vous fournissez dans le corps de la demande hello pour hello API REST opération (méthode PUT) toocreate hello ressource. Vous pouvez également spécifier un toocreate de tableau copie plusieurs instances d’une propriété. Pour plus d’informations, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md). |
| les ressources |Non |Ressources enfants qui dépendent des ressources hello en cours de définition. Fournir uniquement les types de ressources qui sont autorisées par schéma hello de ressource du parent hello. Hello type qualifié complet de la ressource enfant de hello inclut le type de ressource hello parent tels que **Microsoft.Web/sites/extensions**. Dépendance sur la ressource parent de hello n’est pas nécessaire. Vous devez la définir explicitement. |

section de ressources Hello contient un tableau de toodeploy de ressources hello. Au sein de chaque ressource, vous pouvez également définir un tableau de ressources enfant. Par conséquent, la structure de la section de ressources peut ressembler à ce qui suit :

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

Pour plus d’informations sur la définition des ressources enfants, voir [Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager](resource-manager-template-child-resource.md).

Hello **condition** élément spécifie si les ressources hello sont déployé. valeur Hello pour cet élément résout tootrue ou false. Par exemple, toospecify si un compte de stockage est déployé, utilisez :

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

toospecify si un ordinateur virtuel est déployé avec un mot de passe ou la clé SSH, définir deux versions de la machine virtuelle de hello dans votre modèle, **condition** toodifferentiate utilisation. Transmettre un paramètre qui spécifie quels toodeploy de scénario.

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

Pour obtenir un exemple de l’utilisation d’un mot de passe ou d’un ordinateur virtuel de toodeploy clé SSH, consultez [modèle de condition de nom d’utilisateur ou de SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>outputs
Dans la section de sorties hello, vous spécifiez des valeurs qui sont retournées à partir de déploiement. Par exemple, vous pouvez retourner hello URI tooaccess une ressource déployée.

Hello suivant montre structure hello d’une définition de sortie :

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Nom de l'élément | Requis | Description |
|:--- |:--- |:--- |
| outputName |Oui |Nom de la valeur de sortie hello. Doit être un identificateur JavaScript valide. |
| type |Oui |Type de valeur de sortie hello. Les valeurs de sortie prend en charge hello même types en tant que paramètres d’entrée du modèle. |
| value |Oui |Expression du langage du modèle évaluée et retournée sous forme de valeur de sortie. |

Hello suivant montre une valeur qui est retournée dans la section des sorties hello.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Pour plus d’informations sur le fonctionnement de la sortie, consultez [Partage d’état dans les modèles Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Limites de modèle

Limiter la taille de hello de votre modèle too1 Mo et chaque paramètre Ko d’un fichier too64. limite de 1 Mo Hello applique état final de toohello du modèle de hello après que qu’il a été développée avec les définitions de ressource itératif et valeurs des variables et paramètres. 

Vous devez également respecter les limites suivantes :

* 256 paramètres
* 256 variables
* 800 ressources (incluant le nombre de copies)
* 64 valeurs de sortie
* 24 576 caractères dans une expression de modèle

Vous pouvez dépasser certaines limites de modèle en utilisant un modèle imbriqué. Pour plus d’informations, consultez l’article [Utilisation de modèles liés lors du déploiement des ressources Azure](resource-group-linked-templates.md). nombre de hello tooreduce de paramètres, des variables ou des sorties, vous pouvez combiner plusieurs valeurs dans un objet. Pour plus d’informations, consultez l’article [Objects as parameters](resource-manager-objects-as-parameters.md) (Utiliser un objet en tant que paramètre).

## <a name="next-steps"></a>Étapes suivantes
* tooview des modèles complète pour divers types de solutions, consultez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).
* Pour plus d’informations sur les fonctions hello que vous pouvez utiliser à partir d’un modèle, consultez [fonctions de modèle Azure Resource Manager](resource-group-template-functions.md).
* plusieurs modèles pendant le déploiement, reportez-vous à toocombine [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).
* Vous devrez peut-être les ressources toouse qui existent dans un autre groupe de ressources. Ce scénario est classique quand vous utilisez des comptes de stockage ou des réseaux virtuels qui sont partagés entre plusieurs groupes de ressources. Pour plus d’informations, consultez hello [fonction resourceId](resource-group-template-functions-resource.md#resourceid).
