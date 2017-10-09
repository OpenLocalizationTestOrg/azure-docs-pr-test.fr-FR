---
title: "aaaOverview Hello API Standard du .NET concentrateurs d’événements Azure | Documents Microsoft"
description: "Vue d’ensemble de l’API .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="4085f-103">Vue d’ensemble de l’API .NET Standard des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="4085f-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="4085f-104">Cet article récapitule certaines des clé de hello des API clientes événement concentrateurs .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="4085f-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="4085f-105">Il existe actuellement deux bibliothèques clientes .NET Standard :</span><span class="sxs-lookup"><span data-stu-id="4085f-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="4085f-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="4085f-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="4085f-107">Cette bibliothèque fournit toutes les opérations de runtime de base.</span><span class="sxs-lookup"><span data-stu-id="4085f-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="4085f-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="4085f-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="4085f-109">Cette bibliothèque ajoute une fonctionnalité supplémentaire qui permet le suivi des événements traités et est hello tooread de façon plus simple à partir d’un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="4085f-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="4085f-110">Client de concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="4085f-110">Event Hubs client</span></span>
<span data-ttu-id="4085f-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est hello objet principal, vous utilisez les événements toosend, créer des récepteurs et des informations sur l’exécution tooget.</span><span class="sxs-lookup"><span data-stu-id="4085f-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="4085f-112">Ce client est lié tooa événement particulier hub et crée un point de terminaison de connexion toohello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="4085f-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="4085f-113">Création d’un client de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="4085f-113">Create an Event Hubs client</span></span>
<span data-ttu-id="4085f-114">Un objet [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est créé à partir d’une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="4085f-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="4085f-115">tooinstantiate de façon la plus simple Hello un nouveau client est présenté dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4085f-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="4085f-116">tooprogrammatically modifier la chaîne de connexion hello, vous pouvez utiliser hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe et de passer de chaîne de connexion hello en tant que paramètre trop[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="4085f-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="4085f-117">Envoyer des événements</span><span class="sxs-lookup"><span data-stu-id="4085f-117">Send events</span></span>
<span data-ttu-id="4085f-118">concentrateur d’événements tooan toosend événements, utilisez hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe.</span><span class="sxs-lookup"><span data-stu-id="4085f-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="4085f-119">Hello corps doit être un `byte` tableau, ou un `byte` segment de tableau.</span><span class="sxs-lookup"><span data-stu-id="4085f-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="4085f-120">Recevoir des événements</span><span class="sxs-lookup"><span data-stu-id="4085f-120">Receive events</span></span>
<span data-ttu-id="4085f-121">Hello recommandé tooreceive façon dont les événements de concentrateurs d’événements à l’aide de hello [processeur d’événements hôte](#event-processor-host-apis), qui fournit des fonctionnalités tooautomatically effectuer le suivi de décalage et des informations de partition.</span><span class="sxs-lookup"><span data-stu-id="4085f-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="4085f-122">Toutefois, il existe certaines situations dans lesquelles vous voudrez offrir de hello de toouse d’événements de tooreceive bibliothèque hello core concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="4085f-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="4085f-123">Créer un destinataire</span><span class="sxs-lookup"><span data-stu-id="4085f-123">Create a receiver</span></span>
<span data-ttu-id="4085f-124">Récepteurs sont des partitions toospecific liée, par conséquent, dans commande tooreceive tous les événements dans un concentrateur d’événements, vous devez toocreate plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="4085f-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="4085f-125">En règle générale, il est une bonne pratique tooget hello partition d’informations de par programmation, plutôt que de coder en dur des ID de partition hello.</span><span class="sxs-lookup"><span data-stu-id="4085f-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="4085f-126">Dans commande toodo, vous pouvez utiliser hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) (méthode).</span><span class="sxs-lookup"><span data-stu-id="4085f-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="4085f-127">Étant donné que les événements ne sont jamais supprimés à partir d’un concentrateur d’événements (et uniquement expirent), vous avez besoin de point de départ appropriée toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="4085f-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="4085f-128">Hello suivant montre les combinaisons possibles.</span><span class="sxs-lookup"><span data-stu-id="4085f-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="4085f-129">Consommer un événement</span><span class="sxs-lookup"><span data-stu-id="4085f-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="4085f-130">API de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="4085f-130">Event Processor Host APIs</span></span>
<span data-ttu-id="4085f-131">Ces API fournissent des processus tooworker résilience qui peuvent devenir indisponibles, en répartissant les partitions sur la disposition des employés.</span><span class="sxs-lookup"><span data-stu-id="4085f-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="4085f-132">Hello Voici un exemple d’implémentation de hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="4085f-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="4085f-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4085f-133">Next steps</span></span>
<span data-ttu-id="4085f-134">toolearn en savoir plus sur les scénarios de concentrateurs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="4085f-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="4085f-135">Nouveautés des concentrateurs d'événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="4085f-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4085f-136">API des hubs d’événements disponibles</span><span class="sxs-lookup"><span data-stu-id="4085f-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="4085f-137">références de l’API .NET Hello sont ici :</span><span class="sxs-lookup"><span data-stu-id="4085f-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="4085f-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="4085f-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="4085f-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="4085f-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)