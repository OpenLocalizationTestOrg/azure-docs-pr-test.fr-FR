---
title: "schéma d’événement aaaAzure grille d’événement"
description: "Décrit les propriétés de hello sont fournies pour les événements avec la grille d’événement Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a>Schéma d’événement Event Grid

Cet article fournit des propriétés de hello et de schéma pour les événements. Les événements se composent de cinq propriétés de chaîne et d’un objet **données** obligatoires. les propriétés de Hello sont des événements tooall communs à partir de n’importe quel éditeur. Hello **données** objet contient des propriétés de serveur de publication tooeach spécifique. Les rubriques du système, ces propriétés sont fournisseur de ressources toohello spécifique, comme le stockage ou les concentrateurs d’événements.

Les événements sont envoyés tooAzure grille d’événement dans un tableau, qui peut contenir plusieurs objets d’événement. S’il existe uniquement un seul événement, hello longueur du tableau est de 1. 
 
## <a name="event-properties"></a>Propriétés d’événement

Tous les événements contiendront hello même après les données de niveau supérieur.

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| rubrique | string | Source d’événement toohello ressources complet chemin d’accès. Ce champ n’est pas modifiable. |
| subject | string | Objet de serveur de publication défini de chemin d’accès toohello événement. |
| eventType | string | Un des hello inscrit les types d’événements pour cette source d’événements. |
| eventTime | string | événement hello Hello est généré en fonction de l’heure UTC du fournisseur hello. |
| id | string | Identificateur unique de l’événement de hello. |
| données | objet | Fournisseur de ressources de toohello spécifique des données d’événement. |

## <a name="available-event-sources"></a>Sources d’événement disponibles

Hello sources d’événements suivantes publie des événements pour la consommation de grille d’événement :

* Groupes de ressources (opérations de gestion)
* Abonnements Azure (opérations de gestion)
* Event Hubs
* Rubriques personnalisées

## <a name="azure-subscriptions"></a>Abonnements Azure

Les abonnements Azure peuvent désormais émettre des événements de gestion à partir d’Azure Resource Manager, par exemple lors de la création d’une machine virtuelle ou de la suppression d’un compte de stockage.

### <a name="available-event-types"></a>Types d’événement disponibles

- **Microsoft.Resources.ResourceWriteSuccess** : événement déclenché lors de l’aboutissement d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceWriteFailure** : événement déclenché lors de l’échec d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceWriteCancel** : événement déclenché lors de l’annulation d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceDeleteSuccess** : événement déclenché lors de l’aboutissement d’une opération de suppression de ressource.  
- **Microsoft.Resources.ResourceDeleteFailure** : événement déclenché lors de l’échec d’une opération de suppression de ressource.  
- **Microsoft.Resources.ResourceDeleteCancel** : événement déclenché lors de l’annulation d’une opération de suppression de ressource. Cela se produit lorsque le déploiement d’un modèle est annulé.

### <a name="example-event-schema"></a>Exemple de schéma d’événement

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a>Groupes de ressources

Les groupes de ressources peuvent désormais émettre des événements de gestion à partir d’Azure Resource Manager, par exemple lors de la création d’une machine virtuelle ou de la suppression d’un compte de stockage.

### <a name="available-event-types"></a>Types d’événement disponibles

- **Microsoft.Resources.ResourceWriteSuccess** : événement déclenché lors de l’aboutissement d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceWriteFailure** : événement déclenché lors de l’échec d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceWriteCancel** : événement déclenché lors de l’annulation d’une opération de création ou de mise à jour de ressource.  
- **Microsoft.Resources.ResourceDeleteSuccess** : événement déclenché lors de l’aboutissement d’une opération de suppression de ressource.  
- **Microsoft.Resources.ResourceDeleteFailure** : événement déclenché lors de l’échec d’une opération de suppression de ressource.  
- **Microsoft.Resources.ResourceDeleteCancel** : événement déclenché lors de l’annulation d’une opération de suppression de ressource. Cela se produit lorsque le déploiement d’un modèle est annulé.

### <a name="example-event"></a>Exemple d’événement

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a>Event Hubs

Événements de concentrateurs d’événements sont actuellement émis uniquement lorsqu’un fichier est envoyé automatiquement toostorage à l’aide de la fonctionnalité de Capture hello.

### <a name="available-event-types"></a>Types d’événement disponibles

- **Microsoft.EventHub.CaptureFileCreated** : événement déclenché lors de la création d’un fichier de capture.

### <a name="example-event"></a>Exemple d’événement

Cet événement de l’exemple montre le schéma hello d’un événement de concentrateurs d’événements déclenché lors de la Capture stocke un fichier. 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a>un stockage Azure Blob

Stockage Blob Azure disponible en version préliminaire privée avec inscription pour l’intégration à Event Grid.

### <a name="available-event-types"></a>Types d’événement disponibles

- **Microsoft.Storage.BlobCreated** : événement déclenché lors de la création d’un objet blob.
- **Microsoft.Storage.BlobDeleted** : événement déclenché lors de la suppression d’un objet blob.

### <a name="example-event"></a>Exemple d’événement

Cet exemple d’événement montre le schéma hello d’un événement de stockage déclenché lorsqu’un objet blob est créé. 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a>Rubriques personnalisées

charge utile de données Hello de vos événements personnalisés est défini par vous et peut être n’importe quel JSON bien formatée. les données de niveau supérieur Hello doivent contenir hello même les champs en tant qu’événements de ressources standard défini. Lors de la publication des rubriques toocustom des événements, vous devez envisager de modélisation sujet hello de votre tooaid d’événements dans le routage et le filtrage.

### <a name="example-event"></a>Exemple d’événement

Hello, l’exemple suivant montre un événement pour une rubrique personnalisée :
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction tooEvent grille, consultez [quelle est la grille d’événement ?](overview.md)
* toolearn sur la création d’un abonnement de la grille d’événement, consultez [schéma d’abonnement de grille d’événement](subscription-creation-schema.md).
