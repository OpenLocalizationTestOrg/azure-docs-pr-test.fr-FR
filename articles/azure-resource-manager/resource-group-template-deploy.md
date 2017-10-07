---
title: "ressources aaaDeploy avec PowerShell et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et d’Azure PowerShell toodeploy un tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell

Cette rubrique explique comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources. Si vous n’êtes pas familiarisé avec les concepts de hello du déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

modèle de gestionnaire de ressources Hello que vous déployez peut être un fichier local sur votre ordinateur, ou un fichier externe qui se trouve dans un référentiel comme GitHub. modèle de Hello vous déployez dans cet article est disponible dans hello [exemple de modèle](#sample-template) section, ou en tant que [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Déployer un modèle à partir de votre ordinateur local

Lors du déploiement de ressources tooAzure, vous :

1. Ouvrez une session dans tooyour compte Azure
2. Créer un groupe de ressources qui sert de conteneur hello pour les ressources de hello déployé. nom Hello hello du groupe de ressources peut inclure uniquement les parenthèses, des points, des traits de soulignement, des traits d’union et des caractères alphanumériques. Il peut être too90 caractères. Il ne peut pas se terminer par un point.
3. Déployer toohello ressource groupe hello modèle qui définit hello ressources toocreate

Un modèle peut inclure des paramètres qui vous permettent de déploiement de hello toocustomize. Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production). exemple de modèle de Hello définit un paramètre pour le compte de stockage hello référence (SKU).

Bonjour à l’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

déploiement de Hello peut prendre quelques minutes toocomplete. Lorsqu’elle est terminée, vous voyez un message qui inclut le résultat de hello :

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Déployer un modèle à partir d’une source externe

Au lieu de stocker les modèles de gestionnaire de ressources sur votre ordinateur local, vous souhaiterez peut-être toostore dans un emplacement externe. Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub). Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.

toodeploy un modèle externe, utilisez hello **TemplateUri** paramètre. Utilisez hello URI dans hello exemple toodeploy hello exemple de modèle à partir de GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Hello exemple précédent requiert un URI accessible publiquement pour modèle hello, qui fonctionne pour la plupart des scénarios, car votre modèle ne doit pas inclure les données sensibles. Si vous avez besoin de toospecify des données sensibles (par exemple, un mot de passe administrateur), passez cette valeur comme paramètre sécurisé. Toutefois, si vous ne souhaitez pas votre toobe modèle accessible publiquement, vous pouvez le protéger en les stockant dans un conteneur de stockage privé. Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-powershell-sas-token.md).

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

toopass un fichier local de paramètre, utilisez hello **TemplateParameterFile** paramètre :

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass un fichier de paramètres externe, utilisez hello **TemplateParameterUri** paramètre :

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Vous pouvez utiliser les paramètres inline et un paramètre local du fichier Bonjour même opération de déploiement. Par exemple, vous pouvez spécifier certaines valeurs dans le fichier de paramètre local hello et ajouter d’autres en ligne des valeurs pendant le déploiement. Si vous indiquez des valeurs pour un paramètre dans le fichier de paramètre local hello et inline, valeur de hello inline est prioritaire.

Cependant, lorsque vous utilisez un fichier de paramètres externe, vous ne pouvez pas passer d’autres valeurs inline ou tirées d’un fichier local. Lorsque vous spécifiez un fichier de paramètres dans hello **TemplateParameterUri** paramètre, inline tous les paramètres sont ignorés. Fournir toutes les valeurs de paramètre dans un fichier externe de hello. Si votre modèle inclut une valeur sensible que vous ne pouvez pas inclure dans le fichier de paramètres hello, ajoutez ce coffre de clés tooa valeur, ou fournir de manière dynamique en ligne toutes des valeurs de paramètre.

Si votre modèle inclut un paramètre avec le même nom qu’un des paramètres hello Bonjour de commande PowerShell de hello, PowerShell présente le paramètre hello à partir de votre modèle avec le suffixe de hello **modèle**. Par exemple, un paramètre nommé **ResourceGroupName** dans votre modèle est en conflit avec hello **ResourceGroupName** paramètre Bonjour [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)applet de commande. Vous êtes invité à tooprovide une valeur pour **ResourceGroupNameFromTemplate**. En règle générale, vous devez éviter cette confusion en nommant ne pas de paramètres avec le même nom en tant que paramètres utilisés pour les opérations de déploiement de hello.

## <a name="test-a-template-deployment"></a>Tester le déploiement d’un modèle

utilisation de vos valeurs de paramètres et de modèle sans réellement déployer des ressources, tootest [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Si aucune erreur n’est détectée, la commande hello se termine sans réponse. Si une erreur est détectée, la commande hello renvoie un message d’erreur. Par exemple, la tentative de toopass une valeur incorrecte pour le compte de stockage hello référence (SKU), retourne hello l’erreur suivante :

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Si votre modèle comporte une erreur de syntaxe, commande hello renvoie une erreur indiquant qu’il a pas pu analyser le modèle de hello. message de type Hello indique le numéro de ligne hello et la position de l’erreur d’analyse de hello.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

en mode toouse terminée, utilisez hello `Mode` paramètre :

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
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
* exemples de Hello dans cet article déploiement un groupe de ressources tooa ressources dans votre abonnement par défaut. toouse un autre abonnement, consultez [gérer plusieurs abonnements Azure](/powershell/azure/manage-subscriptions-azureps).
* Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-powershell-deploy.md).
* toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).
* Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

