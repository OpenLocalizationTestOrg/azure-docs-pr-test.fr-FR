---
title: "un espace de noms Azure Event Hubs et l’activer à l’aide d’un modèle de Capture d’aaaCreate | Documents Microsoft"
description: "Créer un espace de noms Azure Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Créer un espace de noms Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager

Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms du service Event Hubs, instance de concentrateur d’un événement, mais aussi Active hello [la fonctionnalité de Capture](event-hubs-capture-overview.md) sur le concentrateur d’événements hello. Hello explique comment toodefine quelles ressources sont déployées, et comment toodefine les paramètres qui sont spécifiés lorsque le déploiement de hello est exécutée. Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.

Cet article également indique comment toospecify que les événements sont capturés dans des objets BLOB de stockage Azure ou d’un Azure Data Lake Store, en se basant sur hello destination que vous choisissez.

Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].

Pour plus d’informations sur les modèles et les pratiques des conventions d’affectation de noms des ressources Azure, consultez [Conventions d’affectation de noms des ressources Azure][Azure Resources naming conventions].

Pour les modèles de hello terminée, cliquez sur hello suivant les liens de GitHub :

- [Modèle de tooStorage Capture hub et activer des événements][Event Hub and enable Capture tooStorage template] 
- [Concentrateur et activer la Capture tooAzure Data Lake Store modèle d’événement][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherche pour les concentrateurs d’événements.
> 
> 

## <a name="what-will-you-deploy"></a>Qu'allez-vous déployer ?

Avec ce modèle, vous déployez un espace de noms Event Hubs avec un concentrateur d’événements, et activez [Event Hubs Capture](event-hubs-capture-overview.md).

[Concentrateurs d’événements](event-hubs-what-is-event-hubs.md) est un événement de traitement de service utilisé tooprovide événement et les données de télémétrie entrée tooAzure à très grande échelle, avec une latence faible et une haute fiabilité. Événement concentrateurs Capture permet de vous tooautomatically remettre hello de diffusion en continu des données dans le stockage d’objets Blob tooAzure concentrateurs d’événements ou Azure Data Lake Store dans un intervalle de taille de votre choix ou de temps spécifié.

Cliquez sur hello suivant tooenable bouton capturer des concentrateurs d’événements dans le stockage Azure :

[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Cliquez sur hello suivant tooenable bouton capturer des concentrateurs d’événements dans Azure Data Lake Store :

[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres

Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello. Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques. Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.

modèle de Hello définit hello paramètres suivants.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

nom Hello Hello [espace de noms de concentrateurs d’événements](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

nom de Hello du concentrateur d’événements hello créé Bonjour [espace de noms de concentrateurs d’événements](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

nombre de Hello de messages de type hello tooretain jours dans le concentrateur d’événements hello. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

nombre de Hello de toocreate de partitions dans le concentrateur d’événements hello.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Activer la Capture sur le concentrateur d’événements hello.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

format d’encodage Hello vous spécifiez les données d’événement tooserialize hello.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

intervalle de temps Hello dans lequel capturer des concentrateurs d’événements démarre la capture des données de hello.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
intervalle de salutation taille à laquelle la Capture démarre la capture des données de hello.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

format du nom Hello utilisé par les fichiers d’Avro capturer des concentrateurs d’événements toowrite hello. Notez qu’un format de nom de Capture doit contenir les champs `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` et `{Second}`. Ceux-ci peuvent être organisés dans n’importe quel ordre, avec ou sans délimiteurs.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

version de Hello API du modèle de hello.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Utilisez hello paramètres suivants si vous choisissez le stockage Azure comme destination.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Capture requiert un compte de stockage Azure ressource tooenable ID capture tooyour souhaité compte de stockage.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Bonjour conteneur d’objets blob qui toocapture vos données d’événement.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Utilisez hello paramètres suivants si vous choisissez Azure Data Lake Store comme destination. Vous devez définir des autorisations sur votre chemin d’accès Data Lake Store, dans lequel vous souhaitez les événements de hello tooCapture. autorisations de tooset, consultez [cet article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

ID d’abonnement pour l’espace de noms de concentrateurs d’événements hello et Azure Data Lake Store. Les deux ces ressources doivent être sous hello même ID d’abonnement.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nom d’Azure Data Lake Store Hello pourquoi les événements capturés.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

chemin d’accès du dossier de destination Hello pourquoi les événements capturés.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy de ressources pour le stockage Azure en tant qu’événements toocaptured de destination

Crée un espace de noms de type **EventHubs**, concentrateur d’un événements et également permet de capturer tooAzure stockage d’objets Blob.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy de ressources pour Azure Data Lake Store en tant que destination

Crée un espace de noms de type **EventHubs**, concentrateur d’un événements et également Active Capture tooAzure Data Lake Store.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Déployer votre tooenable modèle capturer des concentrateurs d’événements dans le stockage Azure :
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Déployer votre tooenable modèle capturer des concentrateurs d’événements dans Azure Data Lake Store :

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure

Choisir le stockage Blob Azure comme destination :

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Choisir Azure Data Lake Store comme destination :

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également configurer capturer des concentrateurs d’événements via hello [portail Azure](https://portal.azure.com). Pour plus d’informations, consultez [à l’aide d’activer la Capture de concentrateurs événement hello Azure portal](event-hubs-capture-enable-through-portal.md).

Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
