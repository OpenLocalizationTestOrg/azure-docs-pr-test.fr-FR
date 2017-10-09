---
title: "aaaOverview Hello Azure événement concentrateurs API .NET Framework | Documents Microsoft"
description: "Un résumé de certaines hello clé événement concentrateurs client .NET Framework API."
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
ms.openlocfilehash: b0e12e43f91b025d7aa4ca03e664b9ff31b04097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="c08b7-103">Vue d’ensemble de l’API Event Hubs .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c08b7-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="c08b7-104">Cet article récapitule certaines des clé de hello API clientes de concentrateurs d’événements, .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c08b7-104">This article summarizes some of hello key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="c08b7-105">Il en existe deux catégories : les API de gestion et les API du runtime.</span><span class="sxs-lookup"><span data-stu-id="c08b7-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="c08b7-106">API d’exécution sont constitués de toutes les opérations nécessaires toosend et recevoir un message.</span><span class="sxs-lookup"><span data-stu-id="c08b7-106">Run-time APIs consist of all operations needed toosend and receive a message.</span></span> <span data-ttu-id="c08b7-107">Opérations de gestion activer toomanage un état d’entité de concentrateurs d’événements en création, mise à jour et supprimant des entités.</span><span class="sxs-lookup"><span data-stu-id="c08b7-107">Management operations enable you toomanage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="c08b7-108">Les scénarios d’analyse couvrent la gestion et l’exécution.</span><span class="sxs-lookup"><span data-stu-id="c08b7-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="c08b7-109">Pour la documentation de référence détaillée sur hello API .NET, consultez hello [.NET Service Bus](/dotnet/api/microsoft.servicebus.messaging) et [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) références.</span><span class="sxs-lookup"><span data-stu-id="c08b7-109">For detailed reference documentation on hello .NET APIs, see hello [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="c08b7-110">API de gestion</span><span class="sxs-lookup"><span data-stu-id="c08b7-110">Management APIs</span></span>
<span data-ttu-id="c08b7-111">tooperform hello après les opérations de gestion, vous devez avoir **gérer** autorisations sur l’espace de noms hello concentrateurs d’événements :</span><span class="sxs-lookup"><span data-stu-id="c08b7-111">tooperform hello following management operations, you must have **Manage** permissions on hello Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="c08b7-112">Créer</span><span class="sxs-lookup"><span data-stu-id="c08b7-112">Create</span></span>
```csharp
// Create hello event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="c08b7-113">Mettre à jour</span><span class="sxs-lookup"><span data-stu-id="c08b7-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="c08b7-114">Supprimer</span><span class="sxs-lookup"><span data-stu-id="c08b7-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="c08b7-115">API de runtime</span><span class="sxs-lookup"><span data-stu-id="c08b7-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="c08b7-116">Créer un éditeur</span><span class="sxs-lookup"><span data-stu-id="c08b7-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="c08b7-117">Publier un message</span><span class="sxs-lookup"><span data-stu-id="c08b7-117">Publish message</span></span>
```csharp
// Create hello device/temperature metric
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

### <a name="create-consumer"></a><span data-ttu-id="c08b7-118">Créer un consommateur</span><span class="sxs-lookup"><span data-stu-id="c08b7-118">Create consumer</span></span>
```csharp
// Create hello Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get hello default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="c08b7-119">Consommer un message</span><span class="sxs-lookup"><span data-stu-id="c08b7-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="c08b7-120">API de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="c08b7-120">Event Processor Host APIs</span></span>
<span data-ttu-id="c08b7-121">Ces API fournissent des processus tooworker résilience qui peuvent devenir indisponibles, en répartissant les partitions sur la disposition des employés.</span><span class="sxs-lookup"><span data-stu-id="c08b7-121">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use hello EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// tooclose
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="c08b7-122">Hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="c08b7-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c08b7-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c08b7-123">Next steps</span></span>
<span data-ttu-id="c08b7-124">toolearn en savoir plus sur les scénarios de concentrateurs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="c08b7-124">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="c08b7-125">Nouveautés des concentrateurs d'événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="c08b7-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c08b7-126">Guide de programmation de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="c08b7-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="c08b7-127">références de l’API .NET Hello sont ici :</span><span class="sxs-lookup"><span data-stu-id="c08b7-127">hello .NET API references are here:</span></span>

* [<span data-ttu-id="c08b7-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="c08b7-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="c08b7-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c08b7-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
