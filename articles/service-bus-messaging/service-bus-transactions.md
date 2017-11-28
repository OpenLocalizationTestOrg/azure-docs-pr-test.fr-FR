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
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="83bf9-103">Vue d’ensemble du traitement des transactions Service Bus</span><span class="sxs-lookup"><span data-stu-id="83bf9-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="83bf9-104">Cet article décrit les fonctionnalités de transaction hello du Bus des services Azure.</span><span class="sxs-lookup"><span data-stu-id="83bf9-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="83bf9-105">Une grande partie de la discussion de hello est illustrée par hello [des Transactions atomiques avec l’exemple de Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="83bf9-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="83bf9-106">Cet article est la vue d’ensemble de tooan limitée de traitement des transactions et hello *envoi via* fonctionnalité dans Service Bus, tandis que l’exemple de Transactions atomiques hello est plus large et plus complexe dans la portée.</span><span class="sxs-lookup"><span data-stu-id="83bf9-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="83bf9-107">Transactions dans Service Bus</span><span class="sxs-lookup"><span data-stu-id="83bf9-107">Transactions in Service Bus</span></span>
<span data-ttu-id="83bf9-108">Une [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) regroupe plusieurs opérations dans une *étendue d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="83bf9-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="83bf9-109">Par nature, ce type de transaction doit s’assurer que toutes les opérations appartenant tooa groupe d’opérations réussissent ou échouent conjointement.</span><span class="sxs-lookup"><span data-stu-id="83bf9-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="83bf9-110">À cet égard transactions agissent comme une seule unité, ce qui est souvent désignée tooas *atomicité*.</span><span class="sxs-lookup"><span data-stu-id="83bf9-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="83bf9-111">Service Bus est un courtier de messages transactionnel. Il garantit l’intégrité transactionnelle de toutes les opérations internes par rapport à ses banques de messages.</span><span class="sxs-lookup"><span data-stu-id="83bf9-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="83bf9-112">Tous les transferts de messages à l’intérieur du Bus des services, tels que déplacer les messages tooa [file d’attente de lettres mortes](service-bus-dead-letter-queues.md) ou [transfert automatique](service-bus-auto-forwarding.md) de messages entre des entités, sont transactionnelles.</span><span class="sxs-lookup"><span data-stu-id="83bf9-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="83bf9-113">Par conséquent, si Service Bus accepte un message, il a déjà été stocké et étiqueté avec un numéro de séquence.</span><span class="sxs-lookup"><span data-stu-id="83bf9-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="83bf9-114">Dès lors, les transferts de messages au sein du Service Bus sont des opérations coordonnées entre les entités, et entraîne ni tooloss (réussit de la source et cible échoue) ou tooduplication (Échec de la source et cible réussit) du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="83bf9-115">Service Bus prend en charge les opérations de regroupement par rapport à une seule entité de messagerie (file d’attente, rubrique, abonnement) au sein de la portée de hello d’une transaction.</span><span class="sxs-lookup"><span data-stu-id="83bf9-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="83bf9-116">Par exemple, vous pouvez envoyer plusieurs messages tooone file d’attente au sein d’une étendue de transaction et messages hello ne sera journal de file d’attente toohello validée lorsque la transaction hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="83bf9-117">Opérations au sein d’une étendue de transaction</span><span class="sxs-lookup"><span data-stu-id="83bf9-117">Operations within a transaction scope</span></span>
<span data-ttu-id="83bf9-118">opérations Hello qui peuvent être effectuées dans une étendue de transaction sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="83bf9-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="83bf9-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)** : Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="83bf9-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="83bf9-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)** : Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="83bf9-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="83bf9-121">Recevoir des opérations ne sont pas incluses, car il est supposé qu’application hello acquiert des messages à l’aide de hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, certaines la boucle de réception ou avec un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) rappel, et ouvre n’est qu’une transaction d’étendue pour le traitement du message hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="83bf9-122">Hello disposition de message de type hello (terminé, abandon, de lettres mortes, différer), se produit dans étendue hello d’et dépendant, hello résultat global de la transaction de hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="83bf9-123">Transferts</span><span class="sxs-lookup"><span data-stu-id="83bf9-123">Transfers and "send via"</span></span>
<span data-ttu-id="83bf9-124">prend en charge de Service Bus tooenable transfert transactionnelle des données d’un processeur tooa de file d’attente et file d’attente tooanother, *transferts*.</span><span class="sxs-lookup"><span data-stu-id="83bf9-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="83bf9-125">Dans une opération de transfert, un expéditeur envoie tout d’abord un message tooa « file d’attente de transfert » et la file d’attente de transfert hello déplace immédiatement hello message toohello prévu de file d’attente de destination à l’aide de hello fiable même transférer l’implémentation de la fonctionnalité de transfert automatique de hello s’appuie sur.</span><span class="sxs-lookup"><span data-stu-id="83bf9-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="83bf9-126">message de type Hello est jamais journal validée toohello transfert la file d’attente d’une manière qu’il devienne visible pour les consommateurs de hello transfert la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="83bf9-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="83bf9-127">alimentation Hello de cette fonctionnalité transactionnelle devient évidente lorsque la file d’attente de transfert hello elle-même est source de hello des messages d’entrée de l’expéditeur hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="83bf9-128">En d’autres termes, Service Bus peut transférer hello toohello destination file d’attente « par « file d’attente de transfert hello, lors de l’exécution complète (ou différer, ou de lettres mortes) opération sur le message d’entrée de type hello, dans une opération atomique.</span><span class="sxs-lookup"><span data-stu-id="83bf9-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="83bf9-129">Apparence dans le code</span><span class="sxs-lookup"><span data-stu-id="83bf9-129">See it in code</span></span>
<span data-ttu-id="83bf9-130">tooset des transferts de ce type, vous créez un expéditeur de message qui cible la file d’attente de destination hello via la file d’attente de transfert hello.</span><span class="sxs-lookup"><span data-stu-id="83bf9-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="83bf9-131">Il vous faudra également un destinataire qui extrait les messages de cette même file d’attente.</span><span class="sxs-lookup"><span data-stu-id="83bf9-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="83bf9-132">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="83bf9-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="83bf9-133">Une transaction simple puis utilise ces éléments, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="83bf9-133">A simple transaction then uses these elements, as in hello following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="83bf9-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83bf9-134">Next steps</span></span>

<span data-ttu-id="83bf9-135">Consultez hello suivant des articles pour plus d’informations sur les files d’attente Service Bus :</span><span class="sxs-lookup"><span data-stu-id="83bf9-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="83bf9-136">Chaînage des entités Service Bus avec transfert automatique</span><span class="sxs-lookup"><span data-stu-id="83bf9-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* <span data-ttu-id="83bf9-137">Exemple [Auto-forward](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward) (Transfert automatique)</span><span class="sxs-lookup"><span data-stu-id="83bf9-137">[Auto-forward sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)</span></span>
* <span data-ttu-id="83bf9-138">Exemple [Atomic Transactions with Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions) (Transactions atomiques avec Service Bus)</span><span class="sxs-lookup"><span data-stu-id="83bf9-138">[Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)</span></span>
* [<span data-ttu-id="83bf9-139">Comparaison des files d’attente Azure et Service Bus</span><span class="sxs-lookup"><span data-stu-id="83bf9-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="83bf9-140">Comment les files d’attente de toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="83bf9-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
