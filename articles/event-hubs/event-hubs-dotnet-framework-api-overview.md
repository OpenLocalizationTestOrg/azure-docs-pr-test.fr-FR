---
title: "Vue d’ensemble des API Azure Event Hubs .NET Framework | Microsoft Docs"
description: "Résumé de certaines des principales API clientes Event Hubs .NET Framework."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bc525e7ca8b21e9e5f1e36b3152d71420b041700
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="d2057-103">Vue d’ensemble de l’API Event Hubs .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d2057-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="d2057-104">Cet article passe en revue certaines des principales API clientes Event Hubs .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d2057-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="d2057-105">Il en existe deux catégories : les API de gestion et les API du runtime.</span><span class="sxs-lookup"><span data-stu-id="d2057-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="d2057-106">Les API du runtime comportent toutes les opérations nécessaires pour envoyer et recevoir un message.</span><span class="sxs-lookup"><span data-stu-id="d2057-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="d2057-107">Les opérations de gestion vous permettent de gérer l’état d’une entité Event Hubs en créant, modifiant et supprimant des entités.</span><span class="sxs-lookup"><span data-stu-id="d2057-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="d2057-108">Les scénarios d’analyse couvrent la gestion et l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d2057-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="d2057-109">Pour obtenir une documentation de référence détaillée sur les API .NET, consultez les informations de référence de [l’API .NET Service Bus](/dotnet/api/microsoft.servicebus.messaging) et de [l’API EventProcessorHost](/dotnet/api/microsoft.azure.eventhubs.processor).</span><span class="sxs-lookup"><span data-stu-id="d2057-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="d2057-110">API de gestion</span><span class="sxs-lookup"><span data-stu-id="d2057-110">Management APIs</span></span>
<span data-ttu-id="d2057-111">Pour effectuer les opérations de gestion suivantes, vous devez avoir des autorisations de **gestion** sur l’espace de noms Event Hubs :</span><span class="sxs-lookup"><span data-stu-id="d2057-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="d2057-112">Créer</span><span class="sxs-lookup"><span data-stu-id="d2057-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="d2057-113">Mettre à jour</span><span class="sxs-lookup"><span data-stu-id="d2057-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="d2057-114">Supprimer</span><span class="sxs-lookup"><span data-stu-id="d2057-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="d2057-115">API de runtime</span><span class="sxs-lookup"><span data-stu-id="d2057-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="d2057-116">Créer un éditeur</span><span class="sxs-lookup"><span data-stu-id="d2057-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="d2057-117">Publier un message</span><span class="sxs-lookup"><span data-stu-id="d2057-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="d2057-118">Créer un consommateur</span><span class="sxs-lookup"><span data-stu-id="d2057-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="d2057-119">Consommer un message</span><span class="sxs-lookup"><span data-stu-id="d2057-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="d2057-120">API de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="d2057-120">Event Processor Host APIs</span></span>
<span data-ttu-id="d2057-121">Ces API offrent une résilience aux processus de travail qui peuvent devenir indisponibles, en distribuant les partitions sur les workers disponibles.</span><span class="sxs-lookup"><span data-stu-id="d2057-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="d2057-122">L’interface [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2057-122">The [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d2057-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2057-123">Next steps</span></span>
<span data-ttu-id="d2057-124">Pour en savoir plus sur les scénarios des concentrateurs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="d2057-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="d2057-125">Nouveautés des concentrateurs d'événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="d2057-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d2057-126">Guide de programmation de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="d2057-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="d2057-127">Les informations de référence de l'API .NET se trouvent ici :</span><span class="sxs-lookup"><span data-stu-id="d2057-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="d2057-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="d2057-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="d2057-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="d2057-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
