---
title: "les événements de concentrateurs d’événements Azure à l’aide de Java aaaReceive | Documents Microsoft"
description: "Prise en main de la réception d’événements des Event Hubs avec Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="51c9a-103">Recevoir des événements d’Azure Event Hubs avec Java</span><span class="sxs-lookup"><span data-stu-id="51c9a-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="51c9a-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="51c9a-104">Introduction</span></span>
<span data-ttu-id="51c9a-105">Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications.</span><span class="sxs-lookup"><span data-stu-id="51c9a-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="51c9a-106">Une fois collectés dans des hubs d’événements, vous pouvez transformer et stocker des données à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.</span><span class="sxs-lookup"><span data-stu-id="51c9a-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="51c9a-107">Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="51c9a-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="51c9a-108">Ce didacticiel montre comment les événements tooreceive dans un concentrateur d’événements à l’aide d’une application console écrite en langage Java.</span><span class="sxs-lookup"><span data-stu-id="51c9a-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51c9a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="51c9a-109">Prerequisites</span></span>

<span data-ttu-id="51c9a-110">Commande toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="51c9a-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="51c9a-111">Un environnement de développement Java.</span><span class="sxs-lookup"><span data-stu-id="51c9a-111">A Java development environment.</span></span> <span data-ttu-id="51c9a-112">Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="51c9a-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="51c9a-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="51c9a-113">An active Azure account.</span></span> <br/><span data-ttu-id="51c9a-114">Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="51c9a-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="51c9a-115">Pour plus d'informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d'évaluation gratuite d'Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="51c9a-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="51c9a-116">Recevoir des messages avec EventProcessorHost en Java</span><span class="sxs-lookup"><span data-stu-id="51c9a-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="51c9a-117">**EventProcessorHost** est une classe Java qui simplifie la réception d’événements provenant d’Event Hubs grâce à la gestion des points de contrôle permanents et des réceptions en parallèle d’Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="51c9a-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="51c9a-118">EventProcessorHost permet de répartir des événements sur plusieurs récepteurs, même quand ils sont hébergés dans des nœuds différents.</span><span class="sxs-lookup"><span data-stu-id="51c9a-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="51c9a-119">Cet exemple montre comment toouse EventProcessorHost pour un seul destinataire.</span><span class="sxs-lookup"><span data-stu-id="51c9a-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="51c9a-120">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="51c9a-120">Create a storage account</span></span>
<span data-ttu-id="51c9a-121">toouse EventProcessorHost, vous devez avoir un [compte de stockage Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="51c9a-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="51c9a-122">Ouvrez une session sur toohello [portail Azure][Azure portal], puis cliquez sur **+ nouveau** sur la partie gauche de l’écran hello hello.</span><span class="sxs-lookup"><span data-stu-id="51c9a-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="51c9a-123">Cliquez sur **Stockage**, puis sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="51c9a-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="51c9a-124">Bonjour **créer le compte de stockage** panneau, tapez un nom pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="51c9a-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="51c9a-125">Hello terminez les champs hello, sélectionnez la région souhaitée, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="51c9a-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="51c9a-126">Cliquez sur le compte de stockage hello nouvellement créé, puis cliquez sur **gérer les clés d’accès**:</span><span class="sxs-lookup"><span data-stu-id="51c9a-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="51c9a-127">Copiez hello accès primaire tooa clé emplacement temporaire toouse plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="51c9a-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="51c9a-128">Créer un projet Java à l’aide de hello EventProcessor hôte</span><span class="sxs-lookup"><span data-stu-id="51c9a-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="51c9a-129">Hello Java la bibliothèque cliente pour le service Event Hubs est disponible pour une utilisation dans les projets Maven hello [référentiel Central de Maven][Maven Package]et peuvent être référencées à l’aide de hello après la déclaration de dépendance à l’intérieur de votre Fichier de projet Maven :</span><span class="sxs-lookup"><span data-stu-id="51c9a-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="51c9a-130">Pour différents types d’environnements de build, vous pouvez obtenir explicitement des fichiers JAR de hello dernière version publiée de hello [référentiel Central de Maven] [ Maven Package] ou à partir de [hello du point de distribution de mise en production sur GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="51c9a-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="51c9a-131">Pourquoi suivant l’exemple, tout d’abord créer un projet pour une application console/shell Maven dans votre environnement de développement Java favori.</span><span class="sxs-lookup"><span data-stu-id="51c9a-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="51c9a-132">la classe Hello est appelée `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="51c9a-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="51c9a-133">Suivant de hello d’utilisation de code toocreate une nouvelle classe appelée `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="51c9a-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="51c9a-134">Créez une classe plus appelée `EventProcessorSample`, à l’aide hello le code suivant.</span><span class="sxs-lookup"><span data-stu-id="51c9a-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="51c9a-135">Remplacez hello suivant des champs avec des valeurs hello utilisés lors de la création de compte d’événement hello concentrateur et de stockage.</span><span class="sxs-lookup"><span data-stu-id="51c9a-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="51c9a-136">Ce didacticiel utilise une seule instance de EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="51c9a-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="51c9a-137">débit de tooincrease, il est recommandé d’exécuter plusieurs instances de EventProcessorHost, de préférence sur des ordinateurs distincts.</span><span class="sxs-lookup"><span data-stu-id="51c9a-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="51c9a-138">Cela offre également davantage de redondance.</span><span class="sxs-lookup"><span data-stu-id="51c9a-138">This provides redundancy as well.</span></span> <span data-ttu-id="51c9a-139">Dans ce cas, hello que diverses instances automatiquement la coordination entre eux hello de solde tooload ordre reçu des événements.</span><span class="sxs-lookup"><span data-stu-id="51c9a-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="51c9a-140">Si vous souhaitez que le processus de tooeach plusieurs récepteurs *tous les* hello des événements, vous devez utiliser hello **le groupe de consommateurs** concept.</span><span class="sxs-lookup"><span data-stu-id="51c9a-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="51c9a-141">Lors de la réception des événements à partir des ordinateurs différents, il peut être utile toospecify des noms pour les instances de EventProcessorHost basés sur les machines hello (ou des rôles) dans lequel ils sont déployés.</span><span class="sxs-lookup"><span data-stu-id="51c9a-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="51c9a-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51c9a-142">Next steps</span></span>
<span data-ttu-id="51c9a-143">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="51c9a-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="51c9a-144">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="51c9a-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="51c9a-145">[Create an Event Hub](event-hubs-create.md) (Créer un Event Hub)</span><span class="sxs-lookup"><span data-stu-id="51c9a-145">[Create an Event Hub](event-hubs-create.md)</span></span>
* [<span data-ttu-id="51c9a-146">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="51c9a-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
