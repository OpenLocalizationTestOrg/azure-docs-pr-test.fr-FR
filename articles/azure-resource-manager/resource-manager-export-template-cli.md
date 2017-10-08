---
title: "modèle de gestionnaire de ressources aaaExport avec CLI d’Azure | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et Azure CLI tooexport un modèle à partir d’un groupe de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Exporter des modèles Azure Resource Manager avec Azure CLI

Le Gestionnaire de ressources vous permet de tooexport un modèle de gestionnaire de ressources à partir de ressources existants dans votre abonnement. Vous pouvez utiliser ce toolearn modèle généré sur hello modèle syntaxe ou tooautomate hello redéploiement de votre solution en fonction des besoins.

Il est important toonote qu’il existe deux façons différentes tooexport un modèle :

* Vous pouvez exporter le modèle hello réel que vous avez utilisé pour le déploiement. modèle exporté du Hello inclut toutes les variables et les paramètres de hello exactement comme ils apparaissent dans le modèle d’origine de hello. Cette approche est utile lorsque vous avez besoin d’un modèle de tooretrieve.
* Vous pouvez exporter un modèle qui représente l’état actuel de hello hello du groupe de ressources. modèle exporté du Hello n’est pas basé sur un modèle que vous avez utilisé pour le déploiement. Au lieu de cela, il crée un modèle qui est un instantané hello du groupe de ressources. modèle exporté du Hello possède de nombreuses valeurs codées en dur et probablement pas autant de paramètres que vous définissez généralement. Cette approche est utile lorsque vous avez modifié le groupe de ressources hello. Maintenant, vous devez le groupe de ressources toocapture hello en tant que modèle.

Cette rubrique illustre les deux approches.

## <a name="deploy-a-solution"></a>Déployer une solution

tooillustrate les deux approches pour l’exportation d’un modèle, nous allons commencer en déployant un abonnement tooyour de solution. Si vous avez déjà un groupe de ressources dans votre abonnement que vous souhaitez tooexport, il est inutile toodeploy cette solution. Toutefois, reste hello de cet article fait référence toohello modèle pour cette solution. exemple de script Hello déploie un compte de stockage.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>Enregistrer un modèle à partir de l’historique de déploiement

Vous pouvez récupérer un modèle à partir de l’historique de votre déploiement à l’aide de hello [exportation de déploiement de groupe az](/cli/azure/group/deployment#export) commande. Hello suit exemple enregistre hello template que vous déployez précédemment :

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Il retourne le modèle de hello. Copier hello JSON et les enregistrer en tant que fichier. Notez qu’il s’agit de modèle exact de hello utilisé pour le déploiement. variables et des paramètres de hello correspond à modèle hello à partir de GitHub. Vous pouvez redéployer ce modèle.


## <a name="export-resource-group-as-template"></a>Exporter un groupe de ressources en tant que modèle

Au lieu de récupérer un modèle à partir de l’historique de déploiement hello, vous pouvez récupérer un modèle qui représente l’état actuel de hello d’un groupe de ressources à l’aide de hello [exportation de groupe az](/cli/azure/group#export) commande. Vous utilisez cette commande lorsque vous avez effectué le groupe de ressources de nombreuses modifications tooyour et aucun modèle existant ne représente toutes les modifications de hello.

```azurecli
az group export --name ExampleGroup
```

Il retourne le modèle de hello. Copier hello JSON et les enregistrer en tant que fichier. Notez qu’il est différent de celui modèle hello dans GitHub. Il a des paramètres différents et aucune variable. stockage de Hello référence (SKU) et l’emplacement sont codées en dur les toovalues. Hello suivant montre les modèles exportés hello, mais votre modèle a un nom de paramètre légèrement différentes :

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

Vous pouvez redéployer ce modèle, mais elle nécessite le déchiffrement d’un nom unique pour le compte de stockage hello. nom du paramètre de Hello est légèrement différente.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>Personnaliser un modèle exporté

Vous pouvez modifier cette toomake modèle il toouse plus facile et plus souple. tooallow pour d’autres emplacements, modification hello emplacement propriété toouse hello même emplacement que le groupe de ressources hello :

```json
"location": "[resourceGroup().location]",
```

tooavoid avoir tooguess un nom uniques pour le compte de stockage, paramètre de hello remove pour le nom de compte de stockage hello. Ajoutez un paramètre pour un suffixe de nom de stockage et une référence (SKU) de stockage :

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Ajoutez une variable qui construit le nom du compte de stockage avec fonction d’uniqueString hello hello :

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Définir le nom hello hello compte toohello de variable de stockage :

```json
"name": "[variables('storageAccountName')]",
```

Affectez au paramètre de toohello hello référence (SKU) :

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

Votre modèle doit maintenant ressembler à ceci :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Redéployez le modèle modifié de hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’utilisation de tooexport de portail hello un modèle, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).
* paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).
* Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).