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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="5e453-103">Recevoir des événements de concentrateurs d’événements Azure à l’aide de hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5e453-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="5e453-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="5e453-104">Introduction</span></span>

<span data-ttu-id="5e453-105">Event Hubs constitue un service qui traite de grandes quantités de données d'événement (télémétrie) à partir de périphériques et d'applications connectés.</span><span class="sxs-lookup"><span data-stu-id="5e453-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="5e453-106">Après avoir recueilli les données aux concentrateurs d’événements, vous pouvez stocker les données de salutation à l’aide d’un cluster de stockage ou transformer à l’aide d’un fournisseur de l’analytique en temps réel.</span><span class="sxs-lookup"><span data-stu-id="5e453-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="5e453-107">Cette fonctionnalité de collecte et de traitement des événements à grande échelle est un composant clé des architectures d’application moderne, y compris hello Internet of Things (IoT).</span><span class="sxs-lookup"><span data-stu-id="5e453-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="5e453-108">Ce didacticiel montre comment toowrite un .NET Framework de la console application qui reçoit des messages à partir d’un concentrateur d’événements à l’aide de hello  **[processeur d’événements hôte][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="5e453-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="5e453-109">événements de toosend à l’aide de hello .NET Framework, consultez hello [envoyer des événements de concentrateurs d’événements tooAzure à l’aide de .NET Framework de hello](event-hubs-dotnet-framework-getstarted-send.md) article, ou cliquez sur hello envoi langue dans la table de gauche hello du contenu.</span><span class="sxs-lookup"><span data-stu-id="5e453-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="5e453-110">Hello [processeur d’événements hôte] [ EventProcessorHost] est une classe .NET qui simplifie la réception d’événements à partir des concentrateurs d’événements par la gestion des points de contrôle persistants et parallèle reçoit les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="5e453-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="5e453-111">À l’aide de hello [processeur d’événements hôte][Event Processor Host], vous pouvez fractionner les événements entre plusieurs destinataires, même lorsque hébergés dans des nœuds différents.</span><span class="sxs-lookup"><span data-stu-id="5e453-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="5e453-112">Cet exemple montre comment toouse hello [processeur d’événements hôte] [ EventProcessorHost] pour un seul destinataire.</span><span class="sxs-lookup"><span data-stu-id="5e453-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="5e453-113">Hello [montée en charge le traitement des événements] [ Scale out Event Processing with Event Hubs] exemple montre comment toouse hello [processeur d’événements hôte] [ EventProcessorHost] à de multiples destinataires.</span><span class="sxs-lookup"><span data-stu-id="5e453-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e453-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5e453-114">Prerequisites</span></span>

<span data-ttu-id="5e453-115">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="5e453-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="5e453-116">[Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="5e453-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="5e453-117">captures d’écran Hello dans ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5e453-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="5e453-118">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5e453-118">An active Azure account.</span></span> <span data-ttu-id="5e453-119">Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5e453-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="5e453-120">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5e453-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="5e453-121">Création d’un espace de noms Event Hubs et d’un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="5e453-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="5e453-122">première étape de Hello est toouse hello [portail Azure](https://portal.azure.com) toocreate un espace de noms de concentrateurs d’événements de type et obtenir des informations d’identification d’administration votre application doit toocommunicate avec un concentrateur d’événements hello hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="5e453-123">toocreate un espace de noms et le concentrateur d’événements, suivez la procédure hello dans [cet article](event-hubs-create.md), puis poursuivez hello suivant les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5e453-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="5e453-124">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5e453-124">Create an Azure Storage account</span></span>

<span data-ttu-id="5e453-125">toouse hello [processeur d’événements hôte][EventProcessorHost], vous devez avoir un [compte de stockage Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="5e453-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="5e453-126">Session toohello [portail Azure][Azure portal], puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="5e453-127">Cliquez sur **Stockage**, puis sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="5e453-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="5e453-128">Bonjour **créer le compte de stockage** panneau, tapez un nom pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="5e453-129">Choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="5e453-130">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5e453-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="5e453-131">Dans la liste de hello des comptes de stockage, cliquez sur hello compte de stockage nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="5e453-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="5e453-132">Dans le panneau de compte de stockage hello, cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="5e453-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="5e453-133">Copiez la valeur hello **key1** toouse plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5e453-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="5e453-134">Créer une application de console de destinataire</span><span class="sxs-lookup"><span data-stu-id="5e453-134">Create a receiver console application</span></span>

1. <span data-ttu-id="5e453-135">Dans Visual Studio, créez un nouveau projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="5e453-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="5e453-136">Projet de hello nom **récepteur**.</span><span class="sxs-lookup"><span data-stu-id="5e453-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="5e453-137">Dans l’Explorateur de solutions, cliquez sur hello **récepteur** de projet, puis cliquez sur **gérer les Packages NuGet pour la Solution**.</span><span class="sxs-lookup"><span data-stu-id="5e453-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="5e453-138">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="5e453-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="5e453-139">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="5e453-140">Visual Studio télécharge, installe et ajoute une référence toohello [concentrateur d’événements Azure Service Bus - package NuGet de EventProcessorHost](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), avec toutes ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="5e453-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="5e453-141">Avec le bouton hello **récepteur** de projet, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="5e453-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="5e453-142">Nommez la nouvelle classe de hello **SimpleEventProcessor**, puis cliquez sur **ajouter** classe hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="5e453-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="5e453-143">Ajoutez hello suivant les instructions haut hello du fichier de SimpleEventProcessor.cs hello :</span><span class="sxs-lookup"><span data-stu-id="5e453-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="5e453-144">Ensuite, remplacez hello suivant de code pour le corps de hello de classe hello :</span><span class="sxs-lookup"><span data-stu-id="5e453-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
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
    
  <span data-ttu-id="5e453-145">Cette classe est appelée par hello **EventProcessorHost** tooprocess les événements provenant du concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="5e453-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="5e453-146">Hello `SimpleEventProcessor` classe utilise une méthode de point de contrôle de chronomètre tooperiodically appel hello sur hello **EventProcessorHost** contexte.</span><span class="sxs-lookup"><span data-stu-id="5e453-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="5e453-147">Ce traitement permet de s’assurer que, si le récepteur de hello est redémarré, il perd pas plus de cinq minutes de traitement de la tâche.</span><span class="sxs-lookup"><span data-stu-id="5e453-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="5e453-148">Bonjour **programme** de classe, ajoutez hello `using` instruction début hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="5e453-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="5e453-149">Ensuite, remplacez hello `Main` méthode Bonjour `Program` hello suivant le code de classe, en remplaçant le nom de hub d’événements hello et la connexion au niveau de l’espace de noms de hello de chaîne que vous avez enregistré précédemment, hello compte de stockage et de la clé que vous avez copié dans hello sections précédentes.</span><span class="sxs-lookup"><span data-stu-id="5e453-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
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

7. <span data-ttu-id="5e453-150">Exécuter le programme de hello et vérifiez qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="5e453-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="5e453-151">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="5e453-151">Congratulations!</span></span> <span data-ttu-id="5e453-152">Vous avez désormais reçu des messages à partir d’un concentrateur d’événements à l’aide de hello processeur d’événements hôte.</span><span class="sxs-lookup"><span data-stu-id="5e453-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="5e453-153">Ce didacticiel utilise une seule instance de [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="5e453-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="5e453-154">tooincrease débit, il est recommandé d’exécuter plusieurs instances de [EventProcessorHost][EventProcessorHost], comme indiqué dans hello [mise à l’échelle des traitement de l’événement] [mise à l’échelle des traitement de l’événement] exemple.</span><span class="sxs-lookup"><span data-stu-id="5e453-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="5e453-155">Dans ce cas, hello différentes instances automatiquement coordonnent entre eux les événements tooload solde hello reçu.</span><span class="sxs-lookup"><span data-stu-id="5e453-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="5e453-156">Si vous souhaitez que le processus de tooeach plusieurs récepteurs *tous les* hello des événements, vous devez utiliser hello **le groupe de consommateurs** concept.</span><span class="sxs-lookup"><span data-stu-id="5e453-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="5e453-157">Lors de la réception des événements à partir des ordinateurs différents, il peut être utile toospecify des noms pour [EventProcessorHost] [ EventProcessorHost] instances basées sur les ordinateurs hello (ou des rôles) dans lequel ils sont déployés.</span><span class="sxs-lookup"><span data-stu-id="5e453-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="5e453-158">Pour plus d’informations sur ces sujets, consultez hello [vue d’ensemble des concentrateurs d’événements] [ Event Hubs overview] et hello [guide de programmation de concentrateurs d’événements] [ Event Hubs Programming Guide] rubriques.</span><span class="sxs-lookup"><span data-stu-id="5e453-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5e453-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e453-159">Next steps</span></span>

<span data-ttu-id="5e453-160">Maintenant que vous avez créé une application opérationnelle qui crée un concentrateur d’événements et envoie et reçoit des données, vous pouvez en apprendre plus en consultant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="5e453-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="5e453-161">[Hôte du processeur d’événements][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="5e453-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="5e453-162">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="5e453-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="5e453-163">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="5e453-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
