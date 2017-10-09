---
title: aaaDeploy ressources tooAzure | Documents Microsoft
description: "Utilisez tooAzure de ressources toodeploy Azure PowerShell ou CLI d’Azure. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Déployer des ressources tooAzure

Cette rubrique montre comment toodeploy ressources tooyour abonnement Azure. Vous pouvez utiliser Azure PowerShell ou CLI d’Azure toodeploy un modèle de gestionnaire de ressources qui définit l’infrastructure hello pour votre solution.

Pour une introduction tooconcepts du Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Étapes de déploiement

Cette rubrique suppose que vous déployez hello [exemple de modèle de stockage](#example-storage-template) dans cette rubrique. Vous pouvez utiliser un autre modèle, mais vous passez des paramètres de hello sont autre que celui indiqué dans cette rubrique.

Après avoir créé un modèle, les étapes générales de hello pour le déploiement de votre modèle sont :

1. Connectez-vous au compte de tooyour
2. Sélectionnez toouse d’abonnement hello (nécessaire uniquement si vous avez plusieurs abonnements et que vous souhaitez toouse qui n’est pas hello par défaut abonnement)
3. Créer un groupe de ressources
4. Déployer le modèle de hello
5. Vérifier l’état de votre déploiement

Hello sections suivantes montrent comment tooperform ces étapes avec [PowerShell](#powershell) ou [CLI d’Azure](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall Azure PowerShell, consultez [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview).

2. tooquickly prise en main déploiement, utilisez hello suivant d’applets de commande :

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Hello `Set-AzureRmContext` applet de commande est uniquement nécessaire si vous souhaitez toouse un abonnement autre que votre abonnement par défaut. toosee tous vos abonnements et leurs ID, utilisez :

  ```powershell
  Get-AzureRmSubscription
  ```

3. déploiement de Hello peut prendre quelques minutes toocomplete. Une fois l’opération terminée, un message similaire à celui apparaît :

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee votre compte de stockage et le groupe de ressources ont été déployés tooyour abonnement, utilisez :

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle. Hello exemple précédent n’incluait pas tous les paramètres de modèle, afin de valeurs par défaut de hello dans le modèle de hello ont été utilisés. toodeploy stockage d’un autre compte et fournir des valeurs de paramètre pour le préfixe du nom de stockage hello et compte de stockage hello référence (SKU), utilisez :

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources. 

## <a name="azure-cli"></a>Interface de ligne de commande Azure

1. tooinstall CLI d’Azure, consultez [installer Azure CLI 2.0](/cli/azure/install-az-cli2).

2. tooquickly prise en main déploiement, utilisez hello suivant les commandes :

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Hello `az account set` commande est uniquement nécessaire si vous souhaitez toouse un abonnement autre que votre abonnement par défaut. toosee tous vos abonnements et leurs ID, utilisez :

  ```azurecli
  az account list
  ```

3. déploiement de Hello peut prendre quelques minutes toocomplete. Une fois l’opération terminée, un message similaire à celui apparaît :

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee votre compte de stockage et le groupe de ressources ont été déployés tooyour abonnement, utilisez :

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Vous pouvez spécifier des modèles de paramètres comme paramètres PowerShell lors du déploiement d’un modèle. Hello exemple précédent n’incluait pas tous les paramètres de modèle, afin de valeurs par défaut de hello dans le modèle de hello ont été utilisés. toodeploy stockage d’un autre compte et fournir des valeurs de paramètre pour le préfixe du nom de stockage hello et compte de stockage hello référence (SKU), utilisez :

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Vous disposez maintenant de deux comptes de stockage dans votre groupe de ressources. 

## <a name="example-storage-template"></a>Exemple de modèle de stockage

Utilisez hello suivant exemple modèle toodeploy un abonnement de tooyour de compte de stockage :

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
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
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’utilisation de modèles de toodeploy PowerShell, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Pour plus d’informations sur l’utilisation de modèles de toodeploy CLI d’Azure, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).



