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
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Recevoir des événements d’Azure Event Hubs avec Java


## <a name="introduction"></a>Introduction
Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Une fois collectés dans des hubs d’événements, vous pouvez transformer et stocker des données à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.

Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements][Event Hubs overview].

Ce didacticiel montre comment les événements tooreceive dans un concentrateur d’événements à l’aide d’une application console écrite en langage Java.

## <a name="prerequisites"></a>Composants requis

Commande toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* Un environnement de développement Java. Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).
* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d'informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d'évaluation gratuite d'Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Recevoir des messages avec EventProcessorHost en Java

**EventProcessorHost** est une classe Java qui simplifie la réception d’événements provenant d’Event Hubs grâce à la gestion des points de contrôle permanents et des réceptions en parallèle d’Event Hubs. EventProcessorHost permet de répartir des événements sur plusieurs récepteurs, même quand ils sont hébergés dans des nœuds différents. Cet exemple montre comment toouse EventProcessorHost pour un seul destinataire.

### <a name="create-a-storage-account"></a>Créez un compte de stockage.
toouse EventProcessorHost, vous devez avoir un [compte de stockage Azure][Azure Storage account]:

1. Ouvrez une session sur toohello [portail Azure][Azure portal], puis cliquez sur **+ nouveau** sur la partie gauche de l’écran hello hello.
2. Cliquez sur **Stockage**, puis sur **Compte de stockage**. Bonjour **créer le compte de stockage** panneau, tapez un nom pour le compte de stockage hello. Hello terminez les champs hello, sélectionnez la région souhaitée, puis cliquez sur **créer**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Cliquez sur le compte de stockage hello nouvellement créé, puis cliquez sur **gérer les clés d’accès**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Copiez hello accès primaire tooa clé emplacement temporaire toouse plus loin dans ce didacticiel.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Créer un projet Java à l’aide de hello EventProcessor hôte
Hello Java la bibliothèque cliente pour le service Event Hubs est disponible pour une utilisation dans les projets Maven hello [référentiel Central de Maven][Maven Package]et peuvent être référencées à l’aide de hello après la déclaration de dépendance à l’intérieur de votre Fichier de projet Maven :    

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

Pour différents types d’environnements de build, vous pouvez obtenir explicitement des fichiers JAR de hello dernière version publiée de hello [référentiel Central de Maven] [ Maven Package] ou à partir de [hello du point de distribution de mise en production sur GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Pourquoi suivant l’exemple, tout d’abord créer un projet pour une application console/shell Maven dans votre environnement de développement Java favori. la classe Hello est appelée `ErrorNotificationHandler`.     
   
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
2. Suivant de hello d’utilisation de code toocreate une nouvelle classe appelée `EventProcessor`.
   
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
3. Créez une classe plus appelée `EventProcessorSample`, à l’aide hello le code suivant.
   
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
4. Remplacez hello suivant des champs avec des valeurs hello utilisés lors de la création de compte d’événement hello concentrateur et de stockage.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Ce didacticiel utilise une seule instance de EventProcessorHost. débit de tooincrease, il est recommandé d’exécuter plusieurs instances de EventProcessorHost, de préférence sur des ordinateurs distincts.  Cela offre également davantage de redondance. Dans ce cas, hello que diverses instances automatiquement la coordination entre eux hello de solde tooload ordre reçu des événements. Si vous souhaitez que le processus de tooeach plusieurs récepteurs *tous les* hello des événements, vous devez utiliser hello **le groupe de consommateurs** concept. Lors de la réception des événements à partir des ordinateurs différents, il peut être utile toospecify des noms pour les instances de EventProcessorHost basés sur les machines hello (ou des rôles) dans lequel ils sont déployés.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Créer un Event Hub)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
