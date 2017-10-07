---
title: "ressources aaaDeploy avec CLI d’Azure et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et Azure CLI toodeploy un tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Déployer des ressources à l’aide de modèles Resource Manager et dAzure CLI

Cette rubrique explique comment toouse Azure CLI 2.0 avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources. Si vous n’êtes pas familiarisé avec les concepts de hello du déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).  

modèle de gestionnaire de ressources Hello que vous déployez peut être un fichier local sur votre ordinateur, ou un fichier externe qui se trouve dans un référentiel comme GitHub. modèle Hello que vous déployez dans cet article est disponible dans hello [exemple de modèle](#sample-template) section, ou comme un [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Si vous n’avez pas installé CLI d’Azure, vous pouvez utiliser hello [Cloud Shell](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Déployer un modèle local

Lors du déploiement de ressources tooAzure, vous :

1. Ouvrez une session dans tooyour compte Azure
2. Créer un groupe de ressources qui sert de conteneur hello pour les ressources de hello déployé. nom Hello hello du groupe de ressources peut inclure uniquement les parenthèses, des points, des traits de soulignement, des traits d’union et des caractères alphanumériques. Il peut être too90 caractères. Il ne peut pas se terminer par un point.
3. Déployer toohello ressource groupe hello modèle qui définit hello ressources toocreate

Un modèle peut inclure des paramètres qui vous permettent de déploiement de hello toocustomize. Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production). exemple de modèle de Hello définit un paramètre pour le compte de stockage hello référence (SKU). 

Bonjour à l’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

déploiement de Hello peut prendre quelques minutes toocomplete. Lorsqu’elle est terminée, vous voyez un message qui inclut le résultat de hello :

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Déployer un modèle externe

Au lieu de stocker les modèles de gestionnaire de ressources sur votre ordinateur local, vous souhaiterez peut-être toostore dans un emplacement externe. Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub). Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.

toodeploy un modèle externe, utilisez hello **-l’uri du modèle** paramètre. Utilisez hello URI dans hello exemple toodeploy hello exemple de modèle à partir de GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Hello exemple précédent requiert un URI accessible publiquement pour modèle hello, qui fonctionne pour la plupart des scénarios, car votre modèle ne doit pas inclure les données sensibles. Si vous avez besoin de toospecify des données sensibles (par exemple, un mot de passe administrateur), passez cette valeur comme paramètre sécurisé. Toutefois, si vous ne souhaitez pas votre toobe modèle accessible publiquement, vous pouvez le protéger en les stockant dans un conteneur de stockage privé. Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Déployer le modèle à partir de Cloud Shell

Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) toorun hello CLI d’Azure des commandes pour le déploiement de votre modèle. Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers hello pour votre environnement Cloud. Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).   

2. Sélectionnez votre groupe de ressources Cloud Shell. modèle de nom Hello est `cloud-shell-storage-<region>`.

   ![Sélection du groupe de ressources](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Sélectionnez le compte de stockage hello pour votre environnement Cloud.

   ![Sélectionner le compte de stockage](./media/resource-group-template-deploy-cli/select-storage.png)

4. Sélectionnez **Fichiers**.

   ![Sélectionner des fichiers](./media/resource-group-template-deploy-cli/select-files.png)

5. Sélectionnez le partage de fichiers de hello pour Cloud Shell. modèle de nom Hello est `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Sélectionner le partage de fichiers](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Sélectionnez **Ajouter un répertoire**.

   ![Ajouter un répertoire](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Nommez-le **modèles** puis sélectionnez **Ok**.

   ![Nommer le répertoire](./media/resource-group-template-deploy-cli/name-templates.png)

8. Sélectionnez votre nouveau répertoire.

   ![Sélectionner le répertoire](./media/resource-group-template-deploy-cli/select-templates.png)

9. Sélectionnez **Télécharger**.

   ![Sélectionner Télécharger](./media/resource-group-template-deploy-cli/select-upload.png)

10. Recherchez et chargez votre modèle.

   ![Charger le fichier](./media/resource-group-template-deploy-cli/upload-files.png)

11. Invite de commandes ouverte hello.

   ![Ouvrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Entrez hello suivant les commandes Bonjour Cloud Shell :

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a>Fichiers de paramètres

Au lieu de passer des paramètres en tant que valeurs inline dans votre script, il peut s’avérer plus facile toouse un fichier JSON qui contient des valeurs de paramètre hello. fichier de paramètres Hello doit être Bonjour suivant le format :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Notez que hello paramètres comprend un nom de paramètre qui correspond au paramètre hello défini dans votre modèle (storageAccountType). fichier de paramètres Hello contient une valeur pour le paramètre hello. Cette valeur est automatiquement passée toohello modèle durant le déploiement. Vous pouvez créer plusieurs fichiers de paramètres pour différents scénarios de déploiement et passez dans un fichier de paramètres appropriés de hello. 

Copier hello précédent exemple et l’enregistrer en tant qu’un fichier nommé `storage.parameters.json`.

toopass un fichier local de paramètre, utilisez `@` toospecify un fichier local nommé storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Tester le déploiement d’un modèle

utilisation de vos valeurs de paramètres et de modèle sans réellement déployer des ressources, tootest [valider du déploiement d’un groupe az](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Si aucune erreur n’est détectée, commande hello retourne des informations sur le déploiement de test hello. En particulier, notez que hello **erreur** la valeur est null.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Si une erreur est détectée, la commande hello renvoie un message d’erreur. Par exemple, la tentative de toopass une valeur incorrecte pour le compte de stockage hello référence (SKU), retourne hello l’erreur suivante :

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Si votre modèle comporte une erreur de syntaxe, commande hello renvoie une erreur indiquant qu’il a pas pu analyser le modèle de hello. message de type Hello indique le numéro de ligne hello et la position de l’erreur d’analyse de hello.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

en mode toouse terminée, utilisez hello `mode` paramètre :

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a>Exemple de modèle

Hello modèle suivant est utilisé pour obtenir des exemples hello dans cette rubrique. Copiez et enregistrez-le dans un fichier nommé storage.json. toounderstand comment toocreate ce modèle, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Étapes suivantes
* exemples de Hello dans cet article déploiement un groupe de ressources tooa ressources dans votre abonnement par défaut. toouse un autre abonnement, consultez [gérer plusieurs abonnements Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-cli-deploy.md).
* toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).
* Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-cli-sas-token.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).
