---
title: "modèle Azure Resource Manager de la première aaaCreate | Documents Microsoft"
description: "Un guide pas à pas de toocreating votre premier modèle Azure Resource Manager. Il vous montre comment toouse hello référence de modèle pour un modèle de stockage compte toocreate hello."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Créer et déployer votre premier modèle Azure Resource Manager
Cette rubrique vous guide tout au long des étapes de hello de création de votre premier modèle Azure Resource Manager. Modèles du Gestionnaire de ressources sont des fichiers JSON qui définissent les ressources hello nécessaires toodeploy pour votre solution. concepts de hello toounderstand associés au déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md). Si vous disposez de ressources et que vous souhaitez tooget un modèle pour ces ressources, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).

toocreate et modifier des modèles, vous avez besoin d’éditeur JSON. [Visual Studio Code](https://code.visualstudio.com/) est un éditeur de code multiplateforme, open source et léger. Nous vous recommandons vivement d’utiliser Visual Studio Code pour créer des modèles Resource Manager. Cette rubrique suppose que vous utilisez VS Code ; toutefois, si vous disposez d’un autre éditeur JSON (tel que Visual Studio), vous pouvez utiliser cet éditeur.

## <a name="prerequisites"></a>Composants requis

* Visual Studio Code. Si nécessaire, installez-le à partir de [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Un abonnement Azure. Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="create-template"></a>Créer un modèle

Commençons par un modèle simple qui déploie un abonnement de tooyour de compte de stockage.

1. Sélectionnez **Fichier** > **Nouveau fichier**. 

   ![Nouveau fichier](./media/resource-manager-create-first-template/new-file.png)

2. Copiez et collez hello suivant la syntaxe JSON dans votre fichier :

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Les noms de compte de stockage ont plusieurs restrictions qui les rendent difficile tooset. nom de Hello doit être comprise entre 3 et 24 caractères de longueur, utiliser uniquement des nombres et des lettres minuscules et doit être unique. le modèle précédent Hello utilise hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate une valeur de hachage de la fonction. valeur de ce hachage toogive plus ce qui signifie que, il ajoute le préfixe de hello *stockage*. 

3. Enregistrez ce fichier sous **azuredeploy.json** tooa les dossier local.

   ![Enregistrer un modèle](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Déployer un modèle

Vous est prêt toodeploy ce modèle. Vous utilisez PowerShell ou CLI d’Azure toocreate un groupe de ressources. Ensuite, vous déployez un groupe de ressources de stockage compte toothat.

* Pour PowerShell, utilisez hello suivant les commandes à partir du dossier hello contenant hello modèle :

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Pour une installation locale de CLI d’Azure, utilisez hello suivant les commandes à partir du dossier hello contenant hello modèle :

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Lorsque le déploiement terminé, votre compte de stockage existe dans le groupe de ressources hello.

## <a name="deploy-template-from-cloud-shell"></a>Déployer le modèle à partir de Cloud Shell

Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) toorun hello CLI d’Azure des commandes pour le déploiement de votre modèle. Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers hello pour votre environnement Cloud. Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).   

2. Sélectionnez votre groupe de ressources Cloud Shell. modèle de nom Hello est `cloud-shell-storage-<region>`.

   ![Sélection du groupe de ressources](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Sélectionnez le compte de stockage hello pour votre environnement Cloud.

   ![Sélectionner le compte de stockage](./media/resource-manager-create-first-template/select-storage.png)

4. Sélectionnez **Fichiers**.

   ![Sélectionner des fichiers](./media/resource-manager-create-first-template/select-files.png)

5. Sélectionnez le partage de fichiers de hello pour Cloud Shell. modèle de nom Hello est `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Sélectionner le partage de fichiers](./media/resource-manager-create-first-template/select-file-share.png)

6. Sélectionnez **Ajouter un répertoire**.

   ![Ajouter un répertoire](./media/resource-manager-create-first-template/select-add-directory.png)

7. Nommez-le **modèles** puis sélectionnez **Ok**.

   ![Nommer le répertoire](./media/resource-manager-create-first-template/name-templates.png)

8. Sélectionnez votre nouveau répertoire.

   ![Sélectionner le répertoire](./media/resource-manager-create-first-template/select-templates.png)

9. Sélectionnez **Télécharger**.

   ![Sélectionner Télécharger](./media/resource-manager-create-first-template/select-upload.png)

10. Recherchez et chargez votre modèle.

   ![Charger le fichier](./media/resource-manager-create-first-template/upload-files.png)

11. Invite de commandes ouverte hello.

   ![Ouvrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Entrez hello suivant les commandes Bonjour Cloud Shell :

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Lorsque le déploiement terminé, votre compte de stockage existe dans le groupe de ressources hello.

## <a name="customize-hello-template"></a>Personnaliser le modèle de hello

modèle de Hello fonctionne correctement, mais il n’est pas flexible. Il déploie toujours un tooSouth stockage localement redondant du centre des États-Unis. nom de Hello est toujours *stockage* suivie d’une valeur de hachage. tooenable à l’aide du modèle de hello pour différents scénarios, ajouter un modèle de toohello de paramètres.

Hello suivant montre section de paramètres hello avec deux paramètres. premier paramètre de Hello `storageSKU` vous permet de type hello de toospecify de redondance. Elle limite les valeurs hello que toovalues qui sont valides pour un compte de stockage, vous pouvez passer. Il spécifie également une valeur par défaut. Hello du deuxième paramètre `storageNamePrefix` est ensemble tooallow un maximum de 11 caractères. Il spécifie une valeur par défaut.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Dans la section de variables hello, ajoutez une variable nommée `storageName`. Il combine la valeur de préfixe hello à partir des paramètres de hello et une valeur de hachage à partir de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (fonction). Il utilise hello [toLower](resource-group-template-functions-string.md#tolower) fonction tooconvert tous les caractères toolowercase.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse ces nouvelles valeurs pour votre compte de stockage, modifiez la définition de ressource hello :

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Notez que hello nom du compte de stockage hello a maintenant la valeur variable toohello que vous avez ajouté. nom de référence (SKU) Hello est valeur toohello paramètre hello. emplacement de Hello a la valeur hello même emplacement que le groupe de ressources hello.

Enregistrez votre fichier. 

Après avoir effectué les étapes de hello dans cet article, votre modèle ressemble à :

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Redéployer le modèle

Redéployez le modèle hello avec des valeurs différentes.

Pour PowerShell, utilisez la commande suivante :

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Pour l’interface de ligne de commande Azure, consultez :

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Pour hello Cloud Shell, téléchargez votre partage de fichiers de modèle modifié toohello. Remplacer le fichier existant de hello. Ensuite, utilisez hello de commande suivante :

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Lorsque vous n’est plus nécessaire, nettoyer les ressources hello que vous avez déployé par la suppression du groupe de ressources hello.

Pour PowerShell, utilisez la commande suivante :

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Pour l’interface de ligne de commande Azure, consultez :

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur la structure de hello d’un modèle, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sur les propriétés hello pour un compte de stockage, consultez [référence du modèle des comptes de stockage](/azure/templates/microsoft.storage/storageaccounts).
* tooview des modèles complète pour divers types de solutions, consultez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).
