---
title: "entités de messagerie Azure Service Bus aaaAuto transfert | Documents Microsoft"
description: "Comment toochain un Bus de Service de file d’attente ou une rubrique ou file d’attente de tooanother abonnement."
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
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Chaînage des entités Service Bus avec transfert automatique

Hello Service Bus *transfert automatique* fonctionnalité vous permet de file d’attente de tooanother abonnement ou toochain une file d’attente ou une rubrique qui fait partie de hello même espace de noms. Lorsque le transfert automatique est activé, Service Bus automatiquement supprime les messages sont placés dans la file d’attente de la première hello ou un abonnement (source) et les place dans la file d’attente de la deuxième hello ou une rubrique (destination). Notez qu’il est toujours possible de toosend une entité de destination de message toohello directement. En outre, il n’est pas possible de toochain une sous-file d’attente, tel qu’une file d’attente de lettres mortes, la file d’attente tooanother ou la rubrique.

## <a name="using-auto-forwarding"></a>Utilisation du transfert automatique
Vous pouvez activer le transfert automatique en définissant un hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] ou [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] propriétés de hello [QueueDescription] [ QueueDescription] ou [SubscriptionDescription] [ SubscriptionDescription] objets de source de hello, comme dans hello exemple suivant.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

entité de destination Hello doit exister au moment de hello hello source entité est créée. Si l’entité de destination hello n’existe pas, le Service Bus retourne une exception lorsque toocreate posée hello entité source.

Vous pouvez utiliser tooscale de transfert automatique à une rubrique particulière. Service Bus limites hello [nombre d’abonnements à une rubrique donnée](service-bus-quotas.md) too2, 000. Vous pouvez créer des abonnements supplémentaires en créant des rubriques de second niveau. Notez que même si vous ne sont pas liés par hello Service Bus limitation nombre hello d’abonnements, l’ajout d’un second niveau de rubriques peut améliorer hello débit global de votre rubrique.

![Scénario de transfert automatique][0]

Vous pouvez également utiliser des expéditeurs de messages toodecouple de transfert automatique à partir de récepteurs. Par exemple, considérez un système ERP qui se compose de trois modules : Traitement des commandes, Gestion des stocks et Gestion des relations client. Chacun de ces modules génère des messages qui sont placés en file d’attente dans une rubrique correspondante. Alice et Bob sont des représentants commerciaux intéressés par tous les messages qui se rapportent aux clients de tootheir. tooreceive ces messages, Alice et Bob créent une file d’attente personnel et un abonnement sur chacune des rubriques hello ERP qui transfèrent automatiquement tous les messages tootheir file d’attente.

![Scénario de transfert automatique][1]

Si Alice part en vacances, sa file d’attente personnelle, plutôt que rubrique ERP de hello, soit saturé. Dans ce scénario, car un représentant commercial n’a pas reçu les messages, aucun des rubriques ERP de hello n’atteignent jamais leur quota.

## <a name="auto-forwarding-considerations"></a>Considérations sur le transfert automatique

Si l’entité de destination hello accumule trop grand nombre de messages et dépasse le quota de hello ou entité de destination hello est désactivée, l’entité source hello ajoute hello messages tooits [file d’attente de lettres mortes](service-bus-dead-letter-queues.md) jusqu'à ce que l’espace dans la destination de hello (ou entité de hello est réactivée). Ces messages continue toolive dans la file d’attente de lettres mortes hello, vous devez donc explicitement de réception et les traiter à partir de la file d’attente de lettres mortes hello.

Lors du chaînage des rubriques individuelles tooobtain une rubrique composite avec de nombreux abonnements, il est recommandé d’avoir un nombre modéré d’abonnements sur la rubrique de premier niveau hello et un grand nombre de rubriques de second niveau hello. Par exemple, une rubrique de premier niveau possédant 20 abonnements, chacun d’eux chaînés tooa rubrique de second niveau possédant 200 abonnements, permet un débit plus élevé à une rubrique de premier niveau possédant 200 abonnements, chacun attaché tooa rubrique de second niveau possédant 20 abonnements .

Service Bus facture une opération pour chaque message transféré. Par exemple, envoi d’une rubrique de message de tooa possédant 20 abonnements, chacun d’eux configuré les messages avant de tooauto file d’attente tooanother ou une rubrique, est facturé 21 opérations si tous les abonnements de premier niveau reçoivent une copie du message de type hello.

toocreate un abonnement qui est la file d’attente tooanother chaînées ou une rubrique, le créateur de hello d’abonnement de hello doit avoir **gérer** autorisations sur la source de hello et entité de destination hello. Envoi de rubrique de messages toohello source nécessite uniquement **envoyer** autorisations sur la rubrique source de hello.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le transfert automatique, consultez hello rubriques de référence suivantes :

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn en savoir plus sur les améliorations des performances de Service Bus, consultez 

* [Meilleures pratiques relatives aux améliorations de performances à l’aide de la messagerie Service Bus](service-bus-performance-improvements.md)
* [Files d’attente et rubriques partitionnées][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
