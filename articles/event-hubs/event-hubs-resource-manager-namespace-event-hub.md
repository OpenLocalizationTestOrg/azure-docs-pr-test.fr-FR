---
title: "un groupe d’espace de noms et le consommateur concentrateurs d’événements Azure à l’aide d’un modèle d’aaaCreate | Documents Microsoft"
description: "Créer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs à l’aide de modèles Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Créer un espace de noms Event Hubs avec un Event Hub et un groupe de consommateurs à l’aide d’un modèle Azure Resource Manager

Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms de type Event Hubs, avec un concentrateur d’un événements et un groupe de consommateurs. Hello article montre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée. Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins

Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].

Pour le modèle complète de hello, consultez hello [modèle groupe hub et consommateur d’événement] [ Event Hub and consumer group template] sur GitHub.

> [!NOTE]
> toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherche pour les concentrateurs d’événements.
> 
> 

## <a name="what-will-you-deploy"></a>Qu'allez-vous déployer ?
Avec ce modèle, vous allez déployer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs.

[Concentrateurs d’événements](event-hubs-what-is-event-hubs.md) est un événement de traitement de service utilisé tooprovide événement et les données de télémétrie entrée tooAzure à très grande échelle, avec une latence faible et une haute fiabilité.

toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :

[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres
Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello. Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou sur toowhich d’environnement hello que vous déployez. Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques. Chaque valeur de paramètre dans le modèle de hello définit les ressources de hello qui sont déployés.

modèle de Hello définit hello paramètres suivants :

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
nom de Hello de toocreate d’espace de noms hello concentrateurs d’événements.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
nom de Hello du concentrateur d’événements hello créé dans l’espace de noms hello concentrateurs d’événements.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
nom de Hello du groupe de consommateurs hello créé pour le concentrateur d’événements hello.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
version de Hello API du modèle de hello.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Ressources toodeploy
Crée un espace de noms de type **Event Hubs**, avec un concentrateur d’événements et un groupe de consommateurs.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
