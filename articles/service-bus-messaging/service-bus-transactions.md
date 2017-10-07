---
title: aaaOverview de traitement des transactions dans le Bus des services Azure | Documents Microsoft
description: "Vue d’ensemble des transactions atomiques Azure Service Bus et de la fonctionnalité de transfert"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>Vue d’ensemble du traitement des transactions Service Bus
Cet article décrit les fonctionnalités de transaction hello du Bus des services Azure. Une grande partie de la discussion de hello est illustrée par hello [des Transactions atomiques avec l’exemple de Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Cet article est la vue d’ensemble de tooan limitée de traitement des transactions et hello *envoi via* fonctionnalité dans Service Bus, tandis que l’exemple de Transactions atomiques hello est plus large et plus complexe dans la portée.

## <a name="transactions-in-service-bus"></a>Transactions dans Service Bus
Une [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) regroupe plusieurs opérations dans une *étendue d’exécution*. Par nature, ce type de transaction doit s’assurer que toutes les opérations appartenant tooa groupe d’opérations réussissent ou échouent conjointement. À cet égard transactions agissent comme une seule unité, ce qui est souvent désignée tooas *atomicité*. 

Service Bus est un courtier de messages transactionnel. Il garantit l’intégrité transactionnelle de toutes les opérations internes par rapport à ses banques de messages. Tous les transferts de messages à l’intérieur du Bus des services, tels que déplacer les messages tooa [file d’attente de lettres mortes](service-bus-dead-letter-queues.md) ou [transfert automatique](service-bus-auto-forwarding.md) de messages entre des entités, sont transactionnelles. Par conséquent, si Service Bus accepte un message, il a déjà été stocké et étiqueté avec un numéro de séquence. Dès lors, les transferts de messages au sein du Service Bus sont des opérations coordonnées entre les entités, et entraîne ni tooloss (réussit de la source et cible échoue) ou tooduplication (Échec de la source et cible réussit) du message de type hello.

Service Bus prend en charge les opérations de regroupement par rapport à une seule entité de messagerie (file d’attente, rubrique, abonnement) au sein de la portée de hello d’une transaction. Par exemple, vous pouvez envoyer plusieurs messages tooone file d’attente au sein d’une étendue de transaction et messages hello ne sera journal de file d’attente toohello validée lorsque la transaction hello.

## <a name="operations-within-a-transaction-scope"></a>Opérations au sein d’une étendue de transaction
opérations Hello qui peuvent être effectuées dans une étendue de transaction sont les suivantes :

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)** : Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)** : Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Recevoir des opérations ne sont pas incluses, car il est supposé qu’application hello acquiert des messages à l’aide de hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, certaines la boucle de réception ou avec un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) rappel, et ouvre n’est qu’une transaction d’étendue pour le traitement du message hello.

Hello disposition de message de type hello (terminé, abandon, de lettres mortes, différer), se produit dans étendue hello d’et dépendant, hello résultat global de la transaction de hello.

## <a name="transfers-and-send-via"></a>Transferts
prend en charge de Service Bus tooenable transfert transactionnelle des données d’un processeur tooa de file d’attente et file d’attente tooanother, *transferts*. Dans une opération de transfert, un expéditeur envoie tout d’abord un message tooa « file d’attente de transfert » et la file d’attente de transfert hello déplace immédiatement hello message toohello prévu de file d’attente de destination à l’aide de hello fiable même transférer l’implémentation de la fonctionnalité de transfert automatique de hello s’appuie sur. message de type Hello est jamais journal validée toohello transfert la file d’attente d’une manière qu’il devienne visible pour les consommateurs de hello transfert la file d’attente.

alimentation Hello de cette fonctionnalité transactionnelle devient évidente lorsque la file d’attente de transfert hello elle-même est source de hello des messages d’entrée de l’expéditeur hello. En d’autres termes, Service Bus peut transférer hello toohello destination file d’attente « par « file d’attente de transfert hello, lors de l’exécution complète (ou différer, ou de lettres mortes) opération sur le message d’entrée de type hello, dans une opération atomique. 

### <a name="see-it-in-code"></a>Apparence dans le code
tooset des transferts de ce type, vous créez un expéditeur de message qui cible la file d’attente de destination hello via la file d’attente de transfert hello. Il vous faudra également un destinataire qui extrait les messages de cette même file d’attente. Par exemple :

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Une transaction simple puis utilise ces éléments, comme dans hello l’exemple suivant :

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>Étapes suivantes

Consultez hello suivant des articles pour plus d’informations sur les files d’attente Service Bus :

* [Chaînage des entités Service Bus avec transfert automatique](service-bus-auto-forwarding.md)
* Exemple [Auto-forward](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward) (Transfert automatique)
* Exemple [Atomic Transactions with Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions) (Transactions atomiques avec Service Bus)
* [Comparaison des files d’attente Azure et Service Bus](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Comment les files d’attente de toouse Service Bus](service-bus-dotnet-get-started-with-queues.md)

