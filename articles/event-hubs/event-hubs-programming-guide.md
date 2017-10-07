---
title: "guide d’aaaProgramming pour Azure Event Hubs | Documents Microsoft"
description: "Écrire du code pour les concentrateurs d’événements Azure à l’aide de hello Azure .NET SDK."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Guide de programmation de concentrateurs d’événements

Cet article décrit certains scénarios courants de l’écriture de code à l’aide d’Azure Event Hubs et hello Azure .NET SDK. Il suppose une connaissance préalable des concentrateurs d’événements. Pour obtenir une vue d’ensemble conceptuelle des concentrateurs d’événements, consultez hello [vue d’ensemble des concentrateurs d’événements](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Éditeurs d'événements

Vous envoyez le concentrateur d’événements événements tooan soit à l’aide de HTTP POST ou via une connexion AMQP 1.0. Hello choix de quels toouse et à quel moment varie selon le scénario spécifique de hello à résoudre. Les connexions AMQP 1.0 sont limitées en tant que connexions réparties dans Service Bus et sont plus appropriées dans les scénarios avec des volumes de messages plus importants fréquents et des conditions de latence plus faible, car elles fournissent un canal de messagerie permanent.

Vous créez et gérez des concentrateurs d’événements à l’aide de hello [NamespaceManager][] classe. Lorsque, à l’aide de hello .NET géré API, hello principal construit pour la publication des données tooEvent concentrateurs sont hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) et [EventData][] classes. [EventHubClient][] fournit le canal de communication AMQP hello sur lequel les événements sont envoyés toohello concentrateur d’événements. Hello [EventData][] classe représente un événement et est le concentrateur d’événements utilisé toopublish messages tooan. Cette classe inclut le corps de hello, des métadonnées et les informations d’en-tête sur l’événement hello. Autres propriétés sont ajoutées toohello [EventData][] lorsqu’il transite via un concentrateur d’événements de l’objet.

## <a name="get-started"></a>Prise en main

les classes de .NET Hello qui prennent en charge les concentrateurs d’événements sont fournies dans l’assembly Microsoft.ServiceBus.dll de hello. Hello plus simple de façon tooreference salutation API Service Bus et de tooconfigure votre application avec toutes les dépendances du Service Bus hello est hello de toodownload [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Vous pouvez également utiliser hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) dans Visual Studio. toodo émettre donc hello commande Bonjour suivante [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) fenêtre :

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Création d'un concentrateur d'événements
Vous pouvez utiliser hello [NamespaceManager][] classe toocreate concentrateurs d’événements. Par exemple :

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Dans la plupart des cas, il est recommandé d’utiliser hello [CreateEventHubIfNotExists][] tooavoid méthodes générer des exceptions si hello service redémarre. Par exemple :

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Toutes les opérations de création de concentrateurs d’événements, y compris [CreateEventHubIfNotExists][], nécessitent **gérer** autorisations sur l’espace de noms hello en question. Si vous souhaitez que les autorisations de hello toolimit de vos applications de serveur de publication ou le consommateur, vous pouvez éviter ces créer des appels d’opération dans le code de production lorsque vous utilisez des informations d’identification avec des autorisations limitées.

Hello [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) classe contient des détails sur un concentrateur d’événements, y compris les règles d’autorisation de hello, intervalle de conservation des messages hello, ID de partition, l’état et chemin d’accès. Vous pouvez utiliser ces métadonnées de hello tooupdate classe sur un concentrateur d’événements.

## <a name="create-an-event-hubs-client"></a>Création d’un client de concentrateurs d’événements
classe principale Hello pour interagir avec les concentrateurs d’événements est [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Cette classe fournit les fonctionnalités de l'expéditeur et du récepteur. Vous pouvez instancier cette classe à l’aide de hello [créer](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) méthode, comme indiqué dans hello l’exemple suivant.

```csharp
var client = EventHubClient.Create(description.Path);
```

Cette méthode utilise les informations de connexion de Service Bus hello dans le fichier App.config hello, Bonjour `appSettings` section. Pour obtenir un exemple de hello `appSettings` XML utilisé les informations de connexion de Service Bus toostore hello, consultez la documentation de hello pour hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) (méthode).

Une autre option est un client de hello toocreate à partir d’une chaîne de connexion. Cette option fonctionne bien lorsque vous utilisez des rôles de travail Azure, car vous pouvez stocker la chaîne de hello dans les propriétés de configuration hello pour les processus de travail hello. Par exemple :

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

chaîne de connexion Hello sera Bonjour même format tel qu’il apparaît dans le fichier App.config hello pour les méthodes précédentes hello :

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Enfin, il est également possible de toocreate un [EventHubClient][] à partir de l’objet un [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) de l’instance, comme indiqué dans hello l’exemple suivant.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Il est important toonote supplémentaire [EventHubClient][] objets créés à partir d’une instance de fabrique de messagerie réutiliseront hello même les connexion TCP sous-jacente. Par conséquent, ces objets ont une limite de débit côté client. Hello [créer](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) méthode réutilise une fabrique de messagerie unique. Si vous avez besoin du débit très élevé d'un expéditeur unique, vous pouvez créer plusieurs fabriques de messages et un objet [EventHubClient][] à partir de chaque fabrique de messagerie.

## <a name="send-events-tooan-event-hub"></a>Envoyer le concentrateur d’événements événements tooan
Vous envoyez un concentrateur d’événements événements tooan en créant un [EventData][] instance et en l’envoyant via hello [envoyer](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) (méthode). Cette méthode prend un seul [EventData][] paramètre d’instance et l’envoie de manière synchrone tooan concentrateur d’événements.

## <a name="event-serialization"></a>Sérialisation d'événement
Hello [EventData][] classe a [quatre surchargé constructeurs](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) qui accepte divers paramètres, comme un objet et sérialiseur, un tableau d’octets ou un flux de données. Il est également possible de tooinstantiate hello [EventData][] classe et définir le flux du corps de hello après coup. Lors de l’utilisation de JSON avec [EventData][], vous pouvez utiliser **Encoding.UTF8.GetBytes()** tableau d’octets tooretrieve hello pour une chaîne codée au format JSON.

## <a name="partition-key"></a>Clé de partition
Hello [EventData][] classe a un [PartitionKey][] propriété qui permet de hello expéditeur toospecify une valeur qui est hachée tooproduce une attribution de partition. À l’aide d’une clé de partition garantit que tous les hello événements avec la même clé sont envoyés de hello toohello même partition de concentrateur d’événements hello. Les clés de partition courantes incluent des ID de session utilisateur et des ID d’expéditeur uniques. Hello [PartitionKey][] propriété est facultative et peut être fournie lors de l’utilisation de hello [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) ou [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) méthodes. Si vous ne fournissez pas de valeur pour [PartitionKey][], envoyé les événements sont distribuées toopartitions à l’aide d’un modèle de tourniquet.

### <a name="availability-considerations"></a>Considérations relatives à la disponibilité

L’utilisation d’une clé de partition est facultative, et vous devez considérer soigneusement ou non toouse une. Dans de nombreux cas, l’utilisation d’une clé de partition est un bon choix si l’ordre des événements est important. Lorsque vous utilisez une clé de partition, les partitions nécessitent une disponibilité sur un nœud unique, et des interruptions peuvent se produire dans le temps, par exemple, lors du redémarrage et de la correction des nœuds de calcul. Par conséquent, si vous définissez un ID de partition et cette partition devient indisponible pour une raison quelconque, une tentative de tooaccess hello des données de cette partition échouera. Si la haute disponibilité est plus importante, ne spécifiez pas de clé de partition ; Dans ce cas les événements doivent être envoyés toopartitions à l’aide du modèle de tourniquet hello décrit précédemment. Dans ce scénario, vous effectuez un choix explicite entre la disponibilité (aucun ID de partition) et la cohérence (épinglage événements tooa partition ID).

Une autre considération peut être la gestion des retards dans le traitement des événements. Dans certains cas, il peut être une meilleure toodrop données et recommencez à tootry et suivre le traitement, qui peut entraîner des retards de traitement ultérieur en aval. Par exemple, avec un téléscripteur il est mieux toowait pour les données à jour terminées, mais dans une conversation en direct ou un scénario VOIP vous préférez que les données de salutation rapidement, même si elle n’est pas terminée.

Étant donné ces considérations sur la disponibilité, dans ces scénarios vous pouvez choisir une des hello suivant des stratégies de gestion des erreurs :

- Arrêter (arrêter la lecture à partir de concentrateurs d’événements jusqu’à la résolution des problèmes)
- Supprimer (les messages ne sont pas importants, les supprimer)
- Nouvelle tentative (hello Réessayer les messages que vous consultez ajuster)
- [Lettres mortes](../service-bus-messaging/service-bus-dead-letter-queues.md) (utilisez une file d’attente ou un autre toodead de concentrateur d’événements lettre uniquement les messages hello vous n’a pas pu traiter)

Pour plus d’informations et une discussion à propos de hello compromis entre la disponibilité et la cohérence, consultez [disponibilité et la cohérence dans les concentrateurs d’événements](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Opérations d'envoi d’événements par lot
L’envoi d'événements par lots peut augmenter considérablement le débit. Hello [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) méthode prend un **IEnumerable** paramètre de type [EventData][] et envoie hello lot entier comme un concentrateur d’événements toohello opération atomique.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Notez qu’un seul lot ne doit pas dépasser hello 256 Ko d’un événement. En outre, chaque message hello lot utilise hello même identité du serveur de publication. Il s’agit de responsabilité hello de hello expéditeur tooensure qui hello lot ne dépasse pas la taille d’événement maximale hello. Le cas échéant, une erreur **Send** cliente est générée.

## <a name="send-asynchronously-and-send-at-scale"></a>Envoi de manière asynchrone et envoi à l'échelle
Vous pouvez également envoyer le concentrateur d’événements événements tooan en mode asynchrone. Envoi de façon asynchrone peut augmenter la vitesse hello à laquelle un client est en mesure de toosend événements. Les deux hello [envoyer](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) et [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) méthodes sont disponibles dans les versions asynchrones qui retournent un [tâche](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) objet. Alors que cette technique peut augmenter le débit, il peut également entraîner hello client toocontinue toosend événements même si elle est limitée par hello service Event Hubs et peut entraîner le dysfonctionnement client hello ou messages perdus si n’est pas correctement implémenté. En outre, vous pouvez utiliser hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) propriété sur les options de nouvelle tentative hello client toocontrol client.

## <a name="create-a-partition-sender"></a>Création d'un expéditeur de partition
Bien qu’il soit plus courantes hub de l’événement tooan de l’événements toosend sans une clé de partition, dans certains cas, vous pouvez choisir les événements toosend directement les tooa une partition donnée. Par exemple :

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) retourne un [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) de l’objet que vous pouvez utiliser la partition de concentrateur toopublish événements tooa événement spécifique.

## <a name="event-consumers"></a>Consommateurs d'événements
Les concentrateurs d’événements ont deux modèles principaux pour la consommation d'événements : des récepteurs directs et des abstractions de niveau supérieur, comme [EventProcessorHost][]par exemple. Récepteurs directs sont responsables de leur propre coordination de toopartitions d’accès dans un groupe de consommateurs.

### <a name="direct-consumer"></a>Consommateur direct
Hello tooread de façon la plus directe d’une partition dans un groupe de consommateurs est toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) classe. toocreate une instance de cette classe, vous devez utiliser une instance de hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) classe. Dans l’exemple suivant de hello, hello partition QU'ID doit être spécifié lors de la création du récepteur hello pour le groupe de consommateurs hello.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Hello [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) méthode a plusieurs surcharges qui facilitent le contrôle sur le lecteur hello en cours de création. Ces méthodes incluent la spécification d’un décalage comme une chaîne ou un horodatage et hello capacité toospecify si tooinclude ce décalage spécifié Bonjour retourné de flux, ou démarrer après elle. Après avoir créé le récepteur de hello, vous pouvez démarrer la réception des événements sur hello retourné d’objet. Hello [réception](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) méthode comporte quatre surcharges que hello contrôle recevoir les paramètres de l’opération, telles que la taille de lot et le temps d’attente. Vous pouvez utiliser des versions asynchrones de hello de ces méthodes tooincrease hello de débit d’un consommateur. Par exemple :

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Avec une partition spécifique de tooa égard, messages hello sont reçus dans l’ordre de hello dans lequel ils ont été envoyés toohello concentrateur d’événements. décalage de Hello est un tooidentify utilisé jeton chaîne un message dans une partition.

Notez qu'une partition unique dans un groupe de consommateurs ne peut pas avoir plus de 5 lecteurs simultanés connectés à tout moment. Comme les lecteurs se connectent ou sont déconnectent, leurs sessions peuvent rester actives pendant plusieurs minutes avant que le service de hello reconnaît leur déconnexion. Pendant ce temps, la reconnexion tooa partition risque d’échouer. Pour obtenir un exemple complet de l’écriture de récepteur direct pour les concentrateurs d’événements, consultez hello [récepteurs directs de concentrateurs d’événements](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) exemple.

### <a name="event-processor-host"></a>Hôte du processeur d’événements
Hello [EventProcessorHost][] classe traite les données à partir de concentrateurs d’événements. Vous devez utiliser cette implémentation lors de la création de lecteurs d’événements sur la plateforme .NET de hello. [EventProcessorHost][] fournit un environnement d'exécution sécurisé, multiprocessus, thread-safe pour des implémentations d’événements qui fournissent également une gestion de contrôle et de location de partition.

toouse hello [EventProcessorHost][] (classe), vous pouvez implémenter [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Cette interface contient trois méthodes :

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

traitement des événements toostart instancier [EventProcessorHost][], en fournissant les paramètres appropriés hello pour votre concentrateur d’événements. Ensuite, appelez [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister votre [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implémentation avec hello runtime. À ce stade, les hôtes hello va tenter de tooacquire un bail sur chaque partition dans le concentrateur d’événements hello à l’aide d’un algorithme « greedy ». Ces baux sont valables pour une période donnée et doivent ensuite être renouvelés. Comme les nouveaux nœuds dans ce cas, les instances de processus de travail en ligne, ils placent des réservations de baux et au fil du temps chargement de hello déplace entre les nœuds que chacun tentatives tooacquire baux supplémentaires.

![Hôte du processeur d’événements](./media/event-hubs-programming-guide/IC759863.png)

Au fil du temps, un équilibre est établi. Cette capacité dynamique permet tooconsumers toobe appliqué de processeur l’échelle pour la montée en puissance parallèle et l’échelle vers le bas. Concentrateurs d’événements n’ont pas de concept direct de nombres de messages, l’utilisation moyenne du processeur est souvent hello mécanisme toomeasure arrière principale ou consommateur mieux. Si les éditeurs commencent toopublish que plus d’événements que les consommateurs peuvent traiter, augmentation du processeur hello consommateurs peut être utilisé toocause une à l’échelle automatique sur le nombre d’instances de processus de travail.

Hello [EventProcessorHost][] classe implémente également un mécanisme de points de contrôle basée sur le stockage Azure. Cette hello magasins de mécanisme de décalage sur une base par partition, pour que chaque consommateur puisse déterminer quelles hello dernier point de contrôle à partir de consommateur précédente de hello s’est produite. En tant que partitions transitent entre les nœuds via des baux, il s’agit d’un mécanisme de synchronisation de hello qui facilite le décalage de charge.

## <a name="publisher-revocation"></a>Révocation de l’éditeur
En outre toohello avancés des fonctionnalités d’exécution de [EventProcessorHost][], concentrateurs d’événements permet la révocation d’éditeur dans l’ordre tooblock des éditeurs spécifiques d’envoi de concentrateur d’événements événements tooan. Ces fonctionnalités sont particulièrement utiles si un jeton de serveur de publication a été compromis, ou une mise à jour logicielle est à l’origine les toobehave inappropriée. Dans ces situations, l’identité du serveur de publication hello, qui fait partie de leur jeton SAS, peut être bloquée à partir d’événements de publication.

Pour plus d’informations sur la révocation d’éditeur et toosend concentrateurs tooEvent en tant qu’éditeur, voir hello [publication concentrateurs d’événements grande échelle Secure](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) exemple.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les scénarios de concentrateurs d’événements, consultez ces liens :

* [Vue d’ensemble de l'API Event Hubs](event-hubs-api-overview.md)
* [Qu’est-ce qu’Event Hubs](event-hubs-what-is-event-hubs.md)
* [Disponibilité et cohérence dans Event Hubs](event-hubs-availability-and-consistency.md)
* [Informations de référence des API hôtes du processeur d’événements](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
