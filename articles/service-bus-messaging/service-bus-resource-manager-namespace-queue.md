---
title: "espace de noms aaaCreate Azure Service Bus et de file d’attente à l’aide du modèle Azure Resource Manager | Documents Microsoft"
description: "Créer un espace de noms Service Bus et une file d’attente à l’aide d’un modèle Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a>Créer un espace de noms Service Bus et une file d’attente à l’aide d’un modèle Azure Resource Manager

Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms Service Bus et une file d’attente au sein de cet espace de noms. Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée. Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.

Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].

Pour le modèle complète de hello, consultez hello [modèle d’espace de noms et de file d’attente Service Bus] [ Service Bus namespace and queue template] sur GitHub.

> [!NOTE]
> Hello suivant modèles Azure Resource Manager est disponible pour le téléchargement et déploiement.
> 
> * [Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation](service-bus-resource-manager-namespace-auth-rule.md)
> * [Créer un espace de noms Service Bus par rubrique et abonnement](service-bus-resource-manager-namespace-topic.md)
> * [Création d'un espace de noms Service Bus](service-bus-resource-manager-namespace.md)
> * [Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherchez « Service Bus ».
> 
> 

## <a name="what-will-you-deploy"></a>Qu'allez-vous déployer ?

Avec ce modèle, vous allez déployer un espace de noms Service Bus avec une file d’attente.

[Les files d’attente Service Bus](service-bus-queues-topics-subscriptions.md#queues) offrent la, tooone de remise de message de premier sorti (FIFO) ou plusieurs consommateurs concurrents.

toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :

[![Déployer tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres

Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello. Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même. Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.

modèle de Hello définit hello paramètres suivants.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nom de Hello de toocreate d’espace de noms hello Service Bus.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nom Hello de file d’attente hello créé dans l’espace de noms Service Bus hello.

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
version de l’API Service Bus Hello du modèle de hello.

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Ressources toodeploy
Crée un espace de noms Service Bus standard de type **Messagerie**, avec une file d’attente.

```json
"resources ": [{
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
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé et déployé des ressources à l’aide du Gestionnaire de ressources Azure, découvrez comment toomanage ces ressources en consultant les articles suivants :

* [Gestion de Service Bus avec PowerShell](service-bus-manage-with-ps.md)
* [Gérer les ressources de Service Bus avec hello Explorateur Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
