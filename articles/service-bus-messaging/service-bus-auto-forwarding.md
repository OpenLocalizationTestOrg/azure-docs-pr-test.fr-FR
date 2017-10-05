---
title: "Transfert automatique d’entités de messagerie Azure Service Bus | Microsoft Docs"
description: "Guide pratique pour chaîner une file d’attente ou un abonnement Service Bus à une autre file d’attente ou rubrique."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 2656b3a276c542ca836b3949e4e493d7c7f48f16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="f2741-103">Chaînage des entités Service Bus avec transfert automatique</span><span class="sxs-lookup"><span data-stu-id="f2741-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="f2741-104">La fonctionnalité de *transfert automatique* de Service Bus vous permet de chaîner une file d’attente ou un abonnement à une autre file d’attente ou rubrique qui fait partie du même espace de noms.</span><span class="sxs-lookup"><span data-stu-id="f2741-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="f2741-105">Lorsque le transfert automatique est activé, Service Bus supprime automatiquement les messages placés dans la première file d’attente ou le premier abonnement (source) pour les placer dans la deuxième file d’attente ou rubrique (destination).</span><span class="sxs-lookup"><span data-stu-id="f2741-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="f2741-106">Notez qu'il est toujours possible d'envoyer un message à l'entité de destination directement.</span><span class="sxs-lookup"><span data-stu-id="f2741-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="f2741-107">Notez également qu’il n’est pas possible de chaîner une sous-file d’attente, comme une file d’attente de rebut, à une autre file d’attente ou rubrique.</span><span class="sxs-lookup"><span data-stu-id="f2741-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="f2741-108">Utilisation du transfert automatique</span><span class="sxs-lookup"><span data-stu-id="f2741-108">Using auto-forwarding</span></span>
<span data-ttu-id="f2741-109">Vous pouvez activer le transfert automatique en définissant les propriétés [QueueDescription.ForwardTo][QueueDescription.ForwardTo] ou [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] sur les objets [QueueDescription][QueueDescription] ou [SubscriptionDescription][SubscriptionDescription] pour la source, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="f2741-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="f2741-110">L'entité de destination doit exister au moment de la création de l'entité source.</span><span class="sxs-lookup"><span data-stu-id="f2741-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="f2741-111">Si l'entité de destination n'existe pas, Service Bus renvoie une exception lorsqu'il lui est demandé de créer l'entité source.</span><span class="sxs-lookup"><span data-stu-id="f2741-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="f2741-112">Vous pouvez utiliser le transfert automatique pour faire évoluer une rubrique particulière.</span><span class="sxs-lookup"><span data-stu-id="f2741-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="f2741-113">Service Bus limite le [nombre d’abonnements à une rubrique donnée](service-bus-quotas.md) à 2 000.</span><span class="sxs-lookup"><span data-stu-id="f2741-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="f2741-114">Vous pouvez créer des abonnements supplémentaires en créant des rubriques de second niveau.</span><span class="sxs-lookup"><span data-stu-id="f2741-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="f2741-115">Même si vous n’êtes pas lié par la limitation de Service Bus sur le nombre d’abonnements, l’ajout d’un deuxième niveau de rubriques peut améliorer le débit global de votre rubrique.</span><span class="sxs-lookup"><span data-stu-id="f2741-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![Scénario de transfert automatique][0]

<span data-ttu-id="f2741-117">Vous pouvez également utiliser le transfert automatique pour découpler les expéditeurs de messages des récepteurs.</span><span class="sxs-lookup"><span data-stu-id="f2741-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="f2741-118">Par exemple, considérez un système ERP qui se compose de trois modules : Traitement des commandes, Gestion des stocks et Gestion des relations client.</span><span class="sxs-lookup"><span data-stu-id="f2741-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="f2741-119">Chacun de ces modules génère des messages qui sont placés en file d’attente dans une rubrique correspondante.</span><span class="sxs-lookup"><span data-stu-id="f2741-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="f2741-120">Alice et Bob sont des représentants commerciaux qui s'intéressent à tous les messages liés à leurs clients.</span><span class="sxs-lookup"><span data-stu-id="f2741-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="f2741-121">Pour recevoir ces messages, Alice et Bob créent chacun une file d’attente personnelle et un abonnement sur chacune des rubriques ERP qui transfèrent automatiquement tous les messages à leur file d’attente.</span><span class="sxs-lookup"><span data-stu-id="f2741-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![Scénario de transfert automatique][1]

<span data-ttu-id="f2741-123">Si Alice part en vacances, sa file d’attente personnelle, et non la rubrique ERP, se remplit.</span><span class="sxs-lookup"><span data-stu-id="f2741-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="f2741-124">Dans ce scénario, étant donné qu’un représentant commercial n’a pas reçu les messages, aucun des rubriques ERP n’atteint jamais son quota.</span><span class="sxs-lookup"><span data-stu-id="f2741-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="f2741-125">Considérations sur le transfert automatique</span><span class="sxs-lookup"><span data-stu-id="f2741-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="f2741-126">Si l’entité de destination accumule de nombreux messages et dépasse le quota, ou si l’entité de destination est désactivée, l’entité source ajoute les messages à sa [file d’attente de rebut](service-bus-dead-letter-queues.md) jusqu’à ce qu’il y ait de l’espace dans la destination (ou que l’entité soit réactivée).</span><span class="sxs-lookup"><span data-stu-id="f2741-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="f2741-127">Ces messages continuent de résider dans la file d'attente de rebut, donc vous devez explicitement les recevoir et les traiter à partir de la file d'attente de rebut.</span><span class="sxs-lookup"><span data-stu-id="f2741-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="f2741-128">Lors du chaînage de rubriques individuelles pour obtenir une rubrique composite avec de nombreux abonnements, nous vous recommandons d’avoir un nombre modéré d’abonnements à la rubrique de premier niveau et beaucoup d’abonnements aux rubriques de second niveau.</span><span class="sxs-lookup"><span data-stu-id="f2741-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="f2741-129">Par exemple, une rubrique de premier niveau avec 20 abonnements, chacun étant chaîné à une rubrique de second niveau possédant 200 abonnements, permet d’obtenir un débit plus élevé qu’une rubrique de premier niveau possédant 200 abonnements, chacun étant chaîné à une rubrique de second niveau possédant 20 abonnements.</span><span class="sxs-lookup"><span data-stu-id="f2741-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="f2741-130">Service Bus facture une opération pour chaque message transféré.</span><span class="sxs-lookup"><span data-stu-id="f2741-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="f2741-131">Par exemple, l’envoi d’un message à une rubrique possédant 20 abonnements, chacun d’eux étant configuré pour transférer automatiquement les messages vers une autre file d’attente ou rubrique, est facturé en tant que 21 opérations si tous les abonnements de premier niveau reçoivent une copie du message.</span><span class="sxs-lookup"><span data-stu-id="f2741-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="f2741-132">Pour créer un abonnement qui est chaîné à une autre file d’attente ou rubrique, le créateur de l’abonnement doit disposer des autorisations de **gestion** de l’entité source et l’entité de destination.</span><span class="sxs-lookup"><span data-stu-id="f2741-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="f2741-133">L’envoi de messages à la rubrique source ne nécessite que des autorisations **d’envoi** sur la rubrique source.</span><span class="sxs-lookup"><span data-stu-id="f2741-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2741-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2741-134">Next steps</span></span>

<span data-ttu-id="f2741-135">Pour plus d’informations sur le transfert automatique, consultez les rubriques de référence suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2741-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="f2741-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="f2741-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="f2741-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="f2741-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="f2741-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="f2741-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="f2741-139">Pour en savoir plus sur les améliorations des performances de Service Bus, consultez</span><span class="sxs-lookup"><span data-stu-id="f2741-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="f2741-140">Meilleures pratiques relatives aux améliorations de performances à l’aide de la messagerie Service Bus</span><span class="sxs-lookup"><span data-stu-id="f2741-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="f2741-141">[Files d’attente et rubriques partitionnées][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="f2741-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
