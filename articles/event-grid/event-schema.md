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
# <a name="event-grid-event-schema"></a><span data-ttu-id="0df7f-103">Schéma d’événement Event Grid</span><span class="sxs-lookup"><span data-stu-id="0df7f-103">Event Grid event schema</span></span>

<span data-ttu-id="0df7f-104">Cet article fournit des propriétés de hello et de schéma pour les événements.</span><span class="sxs-lookup"><span data-stu-id="0df7f-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="0df7f-105">Les événements se composent de cinq propriétés de chaîne et d’un objet **données** obligatoires.</span><span class="sxs-lookup"><span data-stu-id="0df7f-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="0df7f-106">les propriétés de Hello sont des événements tooall communs à partir de n’importe quel éditeur.</span><span class="sxs-lookup"><span data-stu-id="0df7f-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="0df7f-107">Hello **données** objet contient des propriétés de serveur de publication tooeach spécifique.</span><span class="sxs-lookup"><span data-stu-id="0df7f-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="0df7f-108">Les rubriques du système, ces propriétés sont fournisseur de ressources toohello spécifique, comme le stockage ou les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="0df7f-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="0df7f-109">Les événements sont envoyés tooAzure grille d’événement dans un tableau, qui peut contenir plusieurs objets d’événement.</span><span class="sxs-lookup"><span data-stu-id="0df7f-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="0df7f-110">S’il existe uniquement un seul événement, hello longueur du tableau est de 1.</span><span class="sxs-lookup"><span data-stu-id="0df7f-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="0df7f-111">Propriétés d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-111">Event properties</span></span>

<span data-ttu-id="0df7f-112">Tous les événements contiendront hello même après les données de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="0df7f-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="0df7f-113">Propriété</span><span class="sxs-lookup"><span data-stu-id="0df7f-113">Property</span></span> | <span data-ttu-id="0df7f-114">Type</span><span class="sxs-lookup"><span data-stu-id="0df7f-114">Type</span></span> | <span data-ttu-id="0df7f-115">Description</span><span class="sxs-lookup"><span data-stu-id="0df7f-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0df7f-116">rubrique</span><span class="sxs-lookup"><span data-stu-id="0df7f-116">topic</span></span> | <span data-ttu-id="0df7f-117">string</span><span class="sxs-lookup"><span data-stu-id="0df7f-117">string</span></span> | <span data-ttu-id="0df7f-118">Source d’événement toohello ressources complet chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0df7f-118">Full resource path toohello event source.</span></span> <span data-ttu-id="0df7f-119">Ce champ n’est pas modifiable.</span><span class="sxs-lookup"><span data-stu-id="0df7f-119">This field is not writeable.</span></span> |
| <span data-ttu-id="0df7f-120">subject</span><span class="sxs-lookup"><span data-stu-id="0df7f-120">subject</span></span> | <span data-ttu-id="0df7f-121">string</span><span class="sxs-lookup"><span data-stu-id="0df7f-121">string</span></span> | <span data-ttu-id="0df7f-122">Objet de serveur de publication défini de chemin d’accès toohello événement.</span><span class="sxs-lookup"><span data-stu-id="0df7f-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="0df7f-123">eventType</span><span class="sxs-lookup"><span data-stu-id="0df7f-123">eventType</span></span> | <span data-ttu-id="0df7f-124">string</span><span class="sxs-lookup"><span data-stu-id="0df7f-124">string</span></span> | <span data-ttu-id="0df7f-125">Un des hello inscrit les types d’événements pour cette source d’événements.</span><span class="sxs-lookup"><span data-stu-id="0df7f-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="0df7f-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="0df7f-126">eventTime</span></span> | <span data-ttu-id="0df7f-127">string</span><span class="sxs-lookup"><span data-stu-id="0df7f-127">string</span></span> | <span data-ttu-id="0df7f-128">événement hello Hello est généré en fonction de l’heure UTC du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="0df7f-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="0df7f-129">id</span><span class="sxs-lookup"><span data-stu-id="0df7f-129">id</span></span> | <span data-ttu-id="0df7f-130">string</span><span class="sxs-lookup"><span data-stu-id="0df7f-130">string</span></span> | <span data-ttu-id="0df7f-131">Identificateur unique de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="0df7f-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="0df7f-132">données</span><span class="sxs-lookup"><span data-stu-id="0df7f-132">data</span></span> | <span data-ttu-id="0df7f-133">objet</span><span class="sxs-lookup"><span data-stu-id="0df7f-133">object</span></span> | <span data-ttu-id="0df7f-134">Fournisseur de ressources de toohello spécifique des données d’événement.</span><span class="sxs-lookup"><span data-stu-id="0df7f-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="0df7f-135">Sources d’événement disponibles</span><span class="sxs-lookup"><span data-stu-id="0df7f-135">Available event sources</span></span>

<span data-ttu-id="0df7f-136">Hello sources d’événements suivantes publie des événements pour la consommation de grille d’événement :</span><span class="sxs-lookup"><span data-stu-id="0df7f-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="0df7f-137">Groupes de ressources (opérations de gestion)</span><span class="sxs-lookup"><span data-stu-id="0df7f-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="0df7f-138">Abonnements Azure (opérations de gestion)</span><span class="sxs-lookup"><span data-stu-id="0df7f-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="0df7f-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0df7f-139">Event Hubs</span></span>
* <span data-ttu-id="0df7f-140">Rubriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="0df7f-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="0df7f-141">Abonnements Azure</span><span class="sxs-lookup"><span data-stu-id="0df7f-141">Azure Subscriptions</span></span>

<span data-ttu-id="0df7f-142">Les abonnements Azure peuvent désormais émettre des événements de gestion à partir d’Azure Resource Manager, par exemple lors de la création d’une machine virtuelle ou de la suppression d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0df7f-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0df7f-143">Types d’événement disponibles</span><span class="sxs-lookup"><span data-stu-id="0df7f-143">Available event types</span></span>

- <span data-ttu-id="0df7f-144">**Microsoft.Resources.ResourceWriteSuccess** : événement déclenché lors de l’aboutissement d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="0df7f-145">**Microsoft.Resources.ResourceWriteFailure** : événement déclenché lors de l’échec d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="0df7f-146">**Microsoft.Resources.ResourceWriteCancel** : événement déclenché lors de l’annulation d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="0df7f-147">**Microsoft.Resources.ResourceDeleteSuccess** : événement déclenché lors de l’aboutissement d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="0df7f-148">**Microsoft.Resources.ResourceDeleteFailure** : événement déclenché lors de l’échec d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="0df7f-149">**Microsoft.Resources.ResourceDeleteCancel** : événement déclenché lors de l’annulation d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="0df7f-150">Cela se produit lorsque le déploiement d’un modèle est annulé.</span><span class="sxs-lookup"><span data-stu-id="0df7f-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="0df7f-151">Exemple de schéma d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="0df7f-152">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="0df7f-152">Resource Groups</span></span>

<span data-ttu-id="0df7f-153">Les groupes de ressources peuvent désormais émettre des événements de gestion à partir d’Azure Resource Manager, par exemple lors de la création d’une machine virtuelle ou de la suppression d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0df7f-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0df7f-154">Types d’événement disponibles</span><span class="sxs-lookup"><span data-stu-id="0df7f-154">Available event types</span></span>

- <span data-ttu-id="0df7f-155">**Microsoft.Resources.ResourceWriteSuccess** : événement déclenché lors de l’aboutissement d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="0df7f-156">**Microsoft.Resources.ResourceWriteFailure** : événement déclenché lors de l’échec d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="0df7f-157">**Microsoft.Resources.ResourceWriteCancel** : événement déclenché lors de l’annulation d’une opération de création ou de mise à jour de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="0df7f-158">**Microsoft.Resources.ResourceDeleteSuccess** : événement déclenché lors de l’aboutissement d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="0df7f-159">**Microsoft.Resources.ResourceDeleteFailure** : événement déclenché lors de l’échec d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="0df7f-160">**Microsoft.Resources.ResourceDeleteCancel** : événement déclenché lors de l’annulation d’une opération de suppression de ressource.</span><span class="sxs-lookup"><span data-stu-id="0df7f-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="0df7f-161">Cela se produit lorsque le déploiement d’un modèle est annulé.</span><span class="sxs-lookup"><span data-stu-id="0df7f-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="0df7f-162">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="0df7f-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0df7f-163">Event Hubs</span></span>

<span data-ttu-id="0df7f-164">Événements de concentrateurs d’événements sont actuellement émis uniquement lorsqu’un fichier est envoyé automatiquement toostorage à l’aide de la fonctionnalité de Capture hello.</span><span class="sxs-lookup"><span data-stu-id="0df7f-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0df7f-165">Types d’événement disponibles</span><span class="sxs-lookup"><span data-stu-id="0df7f-165">Available event types</span></span>

- <span data-ttu-id="0df7f-166">**Microsoft.EventHub.CaptureFileCreated** : événement déclenché lors de la création d’un fichier de capture.</span><span class="sxs-lookup"><span data-stu-id="0df7f-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="0df7f-167">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-167">Example event</span></span>

<span data-ttu-id="0df7f-168">Cet événement de l’exemple montre le schéma hello d’un événement de concentrateurs d’événements déclenché lors de la Capture stocke un fichier.</span><span class="sxs-lookup"><span data-stu-id="0df7f-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="0df7f-169">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="0df7f-169">Azure Blob Storage</span></span>

<span data-ttu-id="0df7f-170">Stockage Blob Azure disponible en version préliminaire privée avec inscription pour l’intégration à Event Grid.</span><span class="sxs-lookup"><span data-stu-id="0df7f-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0df7f-171">Types d’événement disponibles</span><span class="sxs-lookup"><span data-stu-id="0df7f-171">Available event types</span></span>

- <span data-ttu-id="0df7f-172">**Microsoft.Storage.BlobCreated** : événement déclenché lors de la création d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="0df7f-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="0df7f-173">**Microsoft.Storage.BlobDeleted** : événement déclenché lors de la suppression d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="0df7f-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="0df7f-174">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-174">Example event</span></span>

<span data-ttu-id="0df7f-175">Cet exemple d’événement montre le schéma hello d’un événement de stockage déclenché lorsqu’un objet blob est créé.</span><span class="sxs-lookup"><span data-stu-id="0df7f-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="0df7f-176">Rubriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="0df7f-176">Custom Topics</span></span>

<span data-ttu-id="0df7f-177">charge utile de données Hello de vos événements personnalisés est défini par vous et peut être n’importe quel JSON bien formatée.</span><span class="sxs-lookup"><span data-stu-id="0df7f-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="0df7f-178">les données de niveau supérieur Hello doivent contenir hello même les champs en tant qu’événements de ressources standard défini.</span><span class="sxs-lookup"><span data-stu-id="0df7f-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="0df7f-179">Lors de la publication des rubriques toocustom des événements, vous devez envisager de modélisation sujet hello de votre tooaid d’événements dans le routage et le filtrage.</span><span class="sxs-lookup"><span data-stu-id="0df7f-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="0df7f-180">Exemple d’événement</span><span class="sxs-lookup"><span data-stu-id="0df7f-180">Example event</span></span>

<span data-ttu-id="0df7f-181">Hello, l’exemple suivant montre un événement pour une rubrique personnalisée :</span><span class="sxs-lookup"><span data-stu-id="0df7f-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="0df7f-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0df7f-182">Next steps</span></span>

* <span data-ttu-id="0df7f-183">Pour une introduction tooEvent grille, consultez [quelle est la grille d’événement ?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="0df7f-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="0df7f-184">toolearn sur la création d’un abonnement de la grille d’événement, consultez [schéma d’abonnement de grille d’événement](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="0df7f-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
