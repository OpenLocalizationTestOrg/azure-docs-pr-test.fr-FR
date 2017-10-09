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
# <a name="event-hubs-net-standard-api-overview"></a>Vue d’ensemble de l’API .NET Standard des hubs d’événements
Cet article récapitule certaines des clé de hello des API clientes événement concentrateurs .NET Standard. Il existe actuellement deux bibliothèques clientes .NET Standard :
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Cette bibliothèque fournit toutes les opérations de runtime de base.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Cette bibliothèque ajoute une fonctionnalité supplémentaire qui permet le suivi des événements traités et est hello tooread de façon plus simple à partir d’un concentrateur d’événements.

## <a name="event-hubs-client"></a>Client de concentrateur d’événements
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est hello objet principal, vous utilisez les événements toosend, créer des récepteurs et des informations sur l’exécution tooget. Ce client est lié tooa événement particulier hub et crée un point de terminaison de connexion toohello concentrateurs d’événements.

### <a name="create-an-event-hubs-client"></a>Création d’un client de concentrateurs d’événements
Un objet [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) est créé à partir d’une chaîne de connexion. tooinstantiate de façon la plus simple Hello un nouveau client est présenté dans hello l’exemple suivant :

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically modifier la chaîne de connexion hello, vous pouvez utiliser hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe et de passer de chaîne de connexion hello en tant que paramètre trop[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Envoyer des événements
concentrateur d’événements tooan toosend événements, utilisez hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe. Hello corps doit être un `byte` tableau, ou un `byte` segment de tableau.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Recevoir des événements
Hello recommandé tooreceive façon dont les événements de concentrateurs d’événements à l’aide de hello [processeur d’événements hôte](#event-processor-host-apis), qui fournit des fonctionnalités tooautomatically effectuer le suivi de décalage et des informations de partition. Toutefois, il existe certaines situations dans lesquelles vous voudrez offrir de hello de toouse d’événements de tooreceive bibliothèque hello core concentrateurs d’événements.

#### <a name="create-a-receiver"></a>Créer un destinataire
Récepteurs sont des partitions toospecific liée, par conséquent, dans commande tooreceive tous les événements dans un concentrateur d’événements, vous devez toocreate plusieurs instances. En règle générale, il est une bonne pratique tooget hello partition d’informations de par programmation, plutôt que de coder en dur des ID de partition hello. Dans commande toodo, vous pouvez utiliser hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) (méthode).

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

Étant donné que les événements ne sont jamais supprimés à partir d’un concentrateur d’événements (et uniquement expirent), vous avez besoin de point de départ appropriée toospecify hello. Hello suivant montre les combinaisons possibles.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Consommer un événement
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

## <a name="event-processor-host-apis"></a>API de l’hôte du processeur d’événements
Ces API fournissent des processus tooworker résilience qui peuvent devenir indisponibles, en répartissant les partitions sur la disposition des employés.

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

Hello Voici un exemple d’implémentation de hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les scénarios de concentrateurs d’événements, consultez ces liens :

* [Nouveautés des concentrateurs d'événements Azure ?](event-hubs-what-is-event-hubs.md)
* [API des hubs d’événements disponibles](event-hubs-api-overview.md)

références de l’API .NET Hello sont ici :

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)