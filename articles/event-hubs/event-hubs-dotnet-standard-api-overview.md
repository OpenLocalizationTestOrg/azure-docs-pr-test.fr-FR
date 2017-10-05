---
title: "Vue d’ensemble des API Azure Event Hubs .NET Standard | Microsoft Docs"
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
ms.openlocfilehash: eea682c40cd415b383a8b2f0004a5f3648e2f01f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="fc5b3-103">Vue d’ensemble de l’API .NET Standard des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="fc5b3-104">Cet article passe en revue certaines des principales API clientes .NET Standard des hubs d’événements.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-104">This article summarizes some of the key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="fc5b3-105">Il existe actuellement deux bibliothèques clientes .NET Standard :</span><span class="sxs-lookup"><span data-stu-id="fc5b3-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="fc5b3-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="fc5b3-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="fc5b3-107">Cette bibliothèque fournit toutes les opérations de runtime de base.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="fc5b3-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="fc5b3-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="fc5b3-109">Cette bibliothèque ajoute des fonctionnalités supplémentaires pour suivre les événements traités. Elle offre le moyen le plus simple pour lire à partir d’un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-109">This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="fc5b3-110">Client de concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-110">Event Hubs client</span></span>
<span data-ttu-id="fc5b3-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est l’objet principal utilisé pour envoyer des événements, créer des destinataires et obtenir des informations de runtime.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="fc5b3-112">Ce client est lié à un hub d’événements particulier et crée une connexion au point de terminaison des concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-112">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="fc5b3-113">Création d’un client de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-113">Create an Event Hubs client</span></span>
<span data-ttu-id="fc5b3-114">Un objet [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est créé à partir d’une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="fc5b3-115">L’exemple suivant présente la méthode la plus simple pour instancier un nouveau client :</span><span class="sxs-lookup"><span data-stu-id="fc5b3-115">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="fc5b3-116">Pour modifier la chaîne de connexion par programmation, vous pouvez utiliser la classe [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) et transmettre la chaîne de connexion en tant que paramètre à [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="fc5b3-116">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="fc5b3-117">Envoyer des événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-117">Send events</span></span>
<span data-ttu-id="fc5b3-118">Pour envoyer des événements vers un concentrateur d’événements, utilisez la classe [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata).</span><span class="sxs-lookup"><span data-stu-id="fc5b3-118">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="fc5b3-119">Le corps doit être un tableau `byte` ou un segment de tableau `byte`.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-119">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="fc5b3-120">Recevoir des événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-120">Receive events</span></span>
<span data-ttu-id="fc5b3-121">Pour recevoir des événements des concentrateurs d’événements, nous vous recommandons d’utiliser [l’hôte du processeur d’événements](#event-processor-host-apis), qui fournit une fonctionnalité de suivi automatique du décalage et des informations de partition.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-121">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of offset, and partition information.</span></span> <span data-ttu-id="fc5b3-122">Toutefois, il peut arriver que vous souhaitiez vous reposer sur la flexibilité de la bibliothèque principale des hubs d’événements pour recevoir des événements.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-122">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="fc5b3-123">Créer un destinataire</span><span class="sxs-lookup"><span data-stu-id="fc5b3-123">Create a receiver</span></span>
<span data-ttu-id="fc5b3-124">Les destinataires sont liés à des partitions spécifiques. Par conséquent, pour recevoir tous les événements dans un concentrateur d’événements, vous devez créer plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-124">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances.</span></span> <span data-ttu-id="fc5b3-125">En règle générale, il est recommandé d’obtenir les informations de partition par programmation, au lieu de coder en dur les ID de partition.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-125">Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids.</span></span> <span data-ttu-id="fc5b3-126">Pour ce faire, vous pouvez utiliser la méthode [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync).</span><span class="sxs-lookup"><span data-stu-id="fc5b3-126">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="fc5b3-127">Dans la mesure où les événements ne sont jamais supprimés d’un concentrateur d’événements (ils arrivent seulement à expiration), vous devez spécifier le point de départ approprié.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-127">Since events are never removed from an event hub (and only expire), you need to specify the proper starting point.</span></span> <span data-ttu-id="fc5b3-128">L’exemple suivant montre les combinaisons possibles.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-128">The following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="fc5b3-129">Consommer un événement</span><span class="sxs-lookup"><span data-stu-id="fc5b3-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="fc5b3-130">API de l’hôte du processeur d’événements</span><span class="sxs-lookup"><span data-stu-id="fc5b3-130">Event Processor Host APIs</span></span>
<span data-ttu-id="fc5b3-131">Ces API offrent une résilience aux processus de travail qui peuvent devenir indisponibles, en distribuant les partitions sur les workers disponibles.</span><span class="sxs-lookup"><span data-stu-id="fc5b3-131">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="fc5b3-132">Voici un exemple d’implémentation de [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="fc5b3-132">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fc5b3-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc5b3-133">Next steps</span></span>
<span data-ttu-id="fc5b3-134">Pour en savoir plus sur les scénarios des concentrateurs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="fc5b3-134">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="fc5b3-135">Nouveautés des concentrateurs d'événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="fc5b3-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="fc5b3-136">API des hubs d’événements disponibles</span><span class="sxs-lookup"><span data-stu-id="fc5b3-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="fc5b3-137">Les informations de référence de l'API .NET se trouvent ici :</span><span class="sxs-lookup"><span data-stu-id="fc5b3-137">The .NET API references are here:</span></span>

* [<span data-ttu-id="fc5b3-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="fc5b3-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="fc5b3-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="fc5b3-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)