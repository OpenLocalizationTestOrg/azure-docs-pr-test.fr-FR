---
title: "événements aaaReceive à l’aide de concentrateurs d’événements Azure hello .NET Framework | Documents Microsoft"
description: "Suivez ce didacticiel tooreceive les événements de concentrateurs d’événements Azure à l’aide de hello .NET Framework."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Recevoir des événements de concentrateurs d’événements Azure à l’aide de hello .NET Framework

## <a name="introduction"></a>Introduction

Event Hubs constitue un service qui traite de grandes quantités de données d'événement (télémétrie) à partir de périphériques et d'applications connectés. Après avoir recueilli les données aux concentrateurs d’événements, vous pouvez stocker les données de salutation à l’aide d’un cluster de stockage ou transformer à l’aide d’un fournisseur de l’analytique en temps réel. Cette fonctionnalité de collecte et de traitement des événements à grande échelle est un composant clé des architectures d’application moderne, y compris hello Internet of Things (IoT).

Ce didacticiel montre comment toowrite un .NET Framework de la console application qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de hello  **[processeur d’événements hôte][EventProcessorHost]**. événements de toosend à l’aide de hello .NET Framework, consultez hello [envoyer des événements de concentrateurs d’événements tooAzure à l’aide de .NET Framework de hello](event-hubs-dotnet-framework-getstarted-send.md) article, ou cliquez sur hello envoi langue dans la table de gauche hello du contenu.

Hello [processeur d’événements hôte] [ EventProcessorHost] est une classe .NET qui simplifie la réception d’événements à partir des concentrateurs d’événements par la gestion des points de contrôle persistants et parallèle reçoit les concentrateurs d’événements. À l’aide de hello [processeur d’événements hôte][Event Processor Host], vous pouvez fractionner les événements entre plusieurs destinataires, même lorsque hébergés dans des nœuds différents. Cet exemple montre comment toouse hello [processeur d’événements hôte] [ EventProcessorHost] pour un seul destinataire. Hello [montée en charge le traitement des événements] [ Scale out Event Processing with Event Hubs] exemple montre comment toouse hello [processeur d’événements hôte] [ EventProcessorHost] à de multiples destinataires.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* [Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com). captures d’écran Hello dans ce didacticiel utilisent Visual Studio 2017.
* Un compte Azure actif. Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Création d’un espace de noms Event Hubs et d’un concentrateur d’événements

première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms de concentrateurs d’événements de type et obtenir des informations d’identification d’administration votre application doit toocommunicate avec un concentrateur d’événements hello hello. toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello suivant les étapes de ce didacticiel.

## <a name="create-an-azure-storage-account"></a>Création d'un compte Azure Storage

toouse hello [processeur d’événements hôte][EventProcessorHost], vous devez avoir un [compte de stockage Azure][Azure Storage account]:

1. Session toohello [portail Azure][Azure portal], puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.
2. Cliquez sur **Stockage**, puis sur **Compte de stockage**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. Bonjour **créer le compte de stockage** panneau, tapez un nom pour le compte de stockage hello. Choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello. Cliquez ensuite sur **Créer**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Dans la liste de hello des comptes de stockage, cliquez sur hello compte de stockage nouvellement créé.
5. Dans le panneau de compte de stockage hello, cliquez sur **clés d’accès**. Copiez la valeur hello **key1** toouse plus loin dans ce didacticiel.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Créer une application de console de destinataire

1. Dans Visual Studio, créez un nouveau projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **récepteur**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. Dans l’Explorateur de solutions, cliquez sur hello **récepteur** de projet, puis cliquez sur **gérer les Packages NuGet pour la Solution**.
3. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio télécharge, installe et ajoute une référence toohello [concentrateur d’événements Azure Service Bus - package NuGet de EventProcessorHost](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), avec toutes ses dépendances.
4. Avec le bouton hello **récepteur** de projet, cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **SimpleEventProcessor**, puis cliquez sur **ajouter** classe hello de toocreate.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Ajoutez hello suivant les instructions haut hello du fichier de SimpleEventProcessor.cs hello :
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Ensuite, remplacez hello suivant de code pour le corps de hello de classe hello :
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  Cette classe est appelée par hello **EventProcessorHost** tooprocess les événements provenant du concentrateur d’événements hello. Hello `SimpleEventProcessor` classe utilise une méthode de point de contrôle de chronomètre tooperiodically appel hello sur hello **EventProcessorHost** contexte. Ce traitement permet de s’assurer que, si le récepteur de hello est redémarré, il perd pas plus de cinq minutes de traitement de la tâche.
6. Bonjour **programme** de classe, ajoutez hello `using` instruction début hello du fichier de hello :
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Ensuite, remplacez hello `Main` méthode Bonjour `Program` hello suivant le code de classe, en remplaçant le nom de hub d’événements hello et la connexion au niveau de l’espace de noms de hello de chaîne que vous avez enregistré précédemment, hello compte de stockage et de la clé que vous avez copié dans hello sections précédentes. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.
  
Félicitations ! Vous avez désormais reçu des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.


> [!NOTE]
> Ce didacticiel utilise une seule instance de [EventProcessorHost][EventProcessorHost]. tooincrease débit, il est recommandé d’exécuter plusieurs instances de [EventProcessorHost][EventProcessorHost], comme indiqué dans hello [mise à l’échelle des traitement de l’événement] [mise à l’échelle des traitement de l’événement] exemple. Dans ce cas, hello différentes instances automatiquement coordonnent entre eux les événements tooload solde hello reçu. Si vous souhaitez que le processus de tooeach plusieurs récepteurs *tous les* hello des événements, vous devez utiliser hello **le groupe de consommateurs** concept. Lors de la réception des événements à partir des ordinateurs différents, il peut être utile toospecify des noms pour [EventProcessorHost] [ EventProcessorHost] instances basées sur les ordinateurs hello (ou des rôles) dans lequel ils sont déployés. Pour plus d’informations sur ces sujets, consultez hello [vue d’ensemble des concentrateurs d’événements] [ Event Hubs overview] et hello [guide de programmation de concentrateurs d’événements] [ Event Hubs Programming Guide] rubriques.
> 
> 

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez créé une application opérationnelle qui crée un concentrateur d’événements et envoie et reçoit des données, vous pouvez en apprendre plus en consultant hello suivant liens :

* [Hôte du processeur d’événements][Event Processor Host]
* [Vue d’ensemble des hubs d’événements][Event Hubs overview]
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
