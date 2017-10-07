---
title: "ressources d’Azure Service Bus aaaCreate à l’aide de modèles Azure Resource Manager | Documents Microsoft"
description: "Utilisez Azure Resource Manager modèles tooautomate hello la création de ressources de Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Création de ressources Service Bus à l’aide de modèles Azure Resource Manager

Cet article décrit comment toocreate et déployer des ressources Service Bus à l’aide de modèles Azure Resource Manager, PowerShell et fournisseur de ressources de Service Bus hello.

Modèles de gestionnaire de ressources Azure vous permettent de définir toodeploy de ressources hello pour une solution et les paramètres toospecify et les variables qui vous permettent de valeurs tooinput pour différents environnements. modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement. Pour plus d’informations sur l’écriture de modèles Azure Resource Manager et une description de format de modèle hello, consultez [structure et la syntaxe des modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Hello les exemples de cette montrent l’article comment toouse Azure Resource Manager toocreate un espace de noms Service Bus et la messagerie de l’entité (file d’attente). Pour obtenir des exemples de modèle, visitez hello [la galerie de modèles de démarrage rapide Azure] [ Azure Quickstart Templates gallery] et recherchez « Service Bus ».
>
>

## <a name="service-bus-resource-manager-templates"></a>Modèles Resource Manager Service Bus

Ces modèles Azure Resource Manager Service Bus sont disponibles au téléchargement et au déploiement. Cliquez sur hello suivant les liens pour plus d’informations sur chacune d’elles, avec des modèles de toohello de liens sur GitHub :

* [Création d'un espace de noms Service Bus](service-bus-resource-manager-namespace.md)
* [Créer un espace de noms Service Bus avec file d’attente](service-bus-resource-manager-namespace-queue.md)
* [Créer un espace de noms Service Bus par rubrique et abonnement](service-bus-resource-manager-namespace-topic.md)
* [Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation](service-bus-resource-manager-namespace-auth-rule.md)
* [Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Déployer avec PowerShell

Hello procédure suivante décrit comment toouse PowerShell toodeploy un modèle Azure Resource Manager qui crée un **Standard** de niveau espace de noms Service Bus et une file d’attente au sein de cet espace de noms. Cet exemple est basé sur hello [créer un espace de noms Service Bus avec la file d’attente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modèle. flux de travail approximatif Hello est comme suit :

1. Installez PowerShell.
2. Créer le modèle de hello et (facultativement) d’un fichier de paramètres.
3. Dans PowerShell, connectez-vous tooyour compte Azure.
4. Créez un groupe de ressources s'il n'en existe pas.
5. Tester le déploiement de hello.
6. Si vous le souhaitez, définissez le mode de déploiement hello.
7. Déployer le modèle de hello.

Pour des informations complètes sur le déploiement de modèles Azure Resource Manager, consultez [Déployer des ressources à l’aide de modèles Azure Resource Manager][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Installer PowerShell

Installez Azure PowerShell en suivant les instructions de hello dans [prise en main d’Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Créer un modèle

Clone ou copie hello [201-servicebus-créer-file d’attente](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modèle à partir de GitHub :

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Créer un fichier de paramètres (facultatif)

toouse un fichier de paramètres facultatifs, hello de copie [201-servicebus-créer-file d’attente](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) fichier. Remplacez la valeur hello `serviceBusNamespaceName` avec nom hello d’espace de noms Service Bus hello votre choix toocreate dans ce déploiement, remplacez la valeur hello `serviceBusQueueName` avec nom hello de file d’attente hello souhaité toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Pour plus d’informations, consultez hello [paramètres](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) rubrique.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Connectez-vous à tooAzure et définir hello abonnement Azure

À partir d’une invite de PowerShell, exécutez hello de commande suivante :

```powershell
Login-AzureRmAccount
```

Vous êtes invité à toolog sur tooyour compte Azure. Après l’ouverture de session, exécutez hello suivant commande tooview vos abonnements disponibles.

```powershell
Get-AzureRMSubscription
```

Cette commande renvoie la liste des abonnements Azure disponibles. Choisissez un abonnement pour hello session en cours en exécutant hello commande suivante. Remplacez `<YourSubscriptionId>` par hello GUID pour hello abonnement Azure, vous souhaitez toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Définir le groupe de ressources hello

Si vous n’avez pas une ressource existante, créer un groupe de ressources avec hello ** New-AzureRmResourceGroup ** commande. Fournir le nom hello du groupe de ressources hello et un emplacement toouse. Par exemple :

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

En cas de réussite, un résumé du nouveau groupe de ressources hello s’affiche.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Déploiement de test hello

Valider votre déploiement en exécutant hello `Test-AzureRmResourceGroupDeployment` applet de commande. Lorsque vous testez le déploiement de hello, spécifiez les paramètres exactement comme vous le feriez lors de l’exécution du déploiement de hello.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Créer le déploiement de hello

toocreate hello nouveau déploiement, exécutez hello `New-AzureRmResourceGroupDeployment` applet de commande et fournir les paramètres nécessaires hello lorsque vous y êtes invité. les paramètres de Hello incluent un nom pour votre déploiement, le nom de votre groupe de ressources et le chemin d’accès hello ou le fichier de modèle d’URL toohello de hello. Si hello **Mode** paramètre n’est pas spécifié, hello la valeur par défaut de **incrémentiel** est utilisé. Pour plus d’informations, consultez [Déploiements incrémentiels et complets](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Hello après les invites de commandes vous pour les paramètres dans la fenêtre de PowerShell hello hello trois :

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify un fichier de paramètres, utilisez hello commande suivante.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Vous pouvez également utiliser des paramètres inclus lorsque vous exécutez l’applet de commande de déploiement hello. commande Hello est comme suit :

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun un [complète](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) hello d’ensemble du déploiement, **Mode** paramètre trop**Complete**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Vérifier le déploiement de hello
Si les ressources hello sont déployées avec succès, un résumé du déploiement de hello s’affiche dans la fenêtre de PowerShell hello :

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Étapes suivantes
Vous avez maintenant vu des flux de travail hello et les commandes pour le déploiement d’un modèle Azure Resource Manager. Pour plus d’informations, visitez hello suivant liens :

* [Présentation d’Azure Resource Manager][Azure Resource Manager overview]
* [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
