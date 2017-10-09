---
title: "les files d’attente aaaService mortes Bus | Documents Microsoft"
description: "Vue d’ensemble des files d’attente de lettres mortes Azure Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Vue d’ensemble des files d’attente de lettres mortes Service Bus

Les files d’attente Service Bus et les abonnements aux rubriques fournissent une sous-file d’attente secondaire, appelée *file d’attente de lettres mortes*. file d’attente de lettres mortes Hello n’a pas besoin toobe explicitement créé et ne peut pas être supprimée ou indépendants gérés de l’entité principale de hello.

Cet article traite des files d’attente de lettres mortes dans Azure Service Bus. Une grande partie de la discussion de hello est illustrée par hello [exemple de files d’attente de lettres mortes](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) sur GitHub.
 
## <a name="hello-dead-letter-queue"></a>file d’attente de lettres mortes Hello

Hello de file d’attente de lettres mortes hello vise toohold les messages qui ne peut pas être remis tooany récepteur ou des messages qui n’a pas pu être traitées.. Les messages pouvant être supprimés de hello DLQ et inspectés. Une application peut, à l’aide d’un opérateur, corriger les problèmes et soumettez à nouveau le message de type hello, fait hello qu’une erreur s’est produite et prendre des mesures correctives. 

Une API et le protocole du point de vue, hello DLQ est principalement similaire tooany autre file d’attente, à ceci près que les messages ne peuvent être envoyées via des mouvements de lettres mortes hello de l’entité parente de hello. En outre, la durée de vie n’est pas observée, et vous ne pouvez pas supprimer un message d’une file d’attente de lettres mortes. file d’attente de lettres mortes Hello prend entièrement en charge la remise de verrou de lecture et d’opérations transactionnelles.

Notez qu’il n’y a aucun nettoyage automatique de hello DLQ. Les messages demeurent dans hello DLQ jusqu'à ce que vous les récupérer à partir de hello DLQ et appelez [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) sur les messages de lettres mortes hello.

## <a name="moving-messages-toohello-dlq"></a>Déplacement des messages toohello DLQ

Il existe plusieurs activités dans Service Bus qui provoquent tooget messages envoyée toohello DLQ à partir de hello moteur de messagerie. Une application peut également explicitement déplacer des messages toohello DLQ. 

Comme le message de type hello est déplacé par service broker de hello, deux propriétés sont ajoutées toohello message comme service broker de hello appelle sa version interne de hello [lettres mortes](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) méthode sur le message de type hello : `DeadLetterReason` et `DeadLetterErrorDescription`.

Les applications peuvent définir leurs propres codes de hello `DeadLetterReason` propriété mais hello système jeux hello valeurs suivantes.

| Condition | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Toujours |HeaderSizeExceeded |le quota de taille Hello pour ce flux a été dépassé. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing et SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |message de type Hello expiré et a été d morts. |
| SubscriptionDescription.RequiresSession |L’ID de session a la valeur null. |L’entité activée dans la session n’autorise pas les messages dont l’identificateur de session a la valeur null. |
| !dead letter queue |MaxTransferHopCountExceeded |Null |
| Mise en file d’attente de lettres mortes explicite par l’application |Spécifié par l’application |Spécifié par l’application |

## <a name="exceeding-maxdeliverycount"></a>Dépassement de MaxDeliveryCount
Les files d’attente et les abonnements ont un [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) et [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) propriété respectivement ; hello valeur par défaut est 10. Chaque fois qu’un message a été remis sous un verrou ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), mais a été explicitement abandonné ou un verrou hello a expiré, du message de type hello [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) est incrémenté. Lorsque [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) dépasse [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), message de type hello est déplacé toohello DLQ, en spécifiant hello `MaxDeliveryCountExceeded` code motif.

Ce comportement ne peut pas être désactivé, mais vous pouvez définir [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa très grand nombre.

## <a name="exceeding-timetolive"></a>Dépassement de TimeToLive
Hello lorsque [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) ou [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) propriété a la valeur trop**lavaleurtrue** (valeur par défaut hello est **false**), tous les messages arrivant à expiration sont déplacé toohello DLQ, en spécifiant hello `TTLExpiredException` code motif.

Notez que les messages arrivés à expiration sont purgés uniquement et par conséquent déplacé toohello DLQ lorsqu’il existe au moins un destinataire active tirant sur la file d’attente principale de hello ou un abonnement ; Ce comportement est normal.

## <a name="errors-while-processing-subscription-rules"></a>Erreurs pendant le traitement des règles d’abonnement
Hello lorsque [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) propriété est activée pour un abonnement, toutes les erreurs qui se produisent pendant l’exécution de la règle de filtre d’un abonnement SQL sont capturées dans hello DLQ en même temps que hello incriminée du message.

## <a name="application-level-dead-lettering"></a>Mise en file d’attente de lettres mortes au niveau de l’application
Dans Ajout toohello fournie par le système lettres mortes à des fonctionnalités, les applications peuvent utiliser hello DLQ tooexplicitly rejeter inacceptable les messages. Cela peut inclure des messages qui ne peut pas être traités correctement en raison de tri tooany de problème système, les messages qui contiennent des charges utiles mal formés ou des messages que l’authentification échoueront lorsque certains modèle de sécurité de niveau message est utilisé.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Mise en file d’attente de lettres mortes dans des scénarios ForwardTo ou SendVia

Les messages seront file d’attente de lettres mortes de transfert toohello envoyé sous hello conditions suivantes :

- Un message passe par plus de 3 files d’attente ou rubriques [enchaînées](service-bus-auto-forwarding.md).
- file d’attente de destination Hello ou une rubrique est désactivé ou supprimé.
- file d’attente de destination Hello ou une rubrique dépasse la taille d’entité maximale hello.

tooretrieve ces messages représentées par des lettres mortes, vous pouvez créer un récepteur à l’aide de hello [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) méthode utilitaire.

## <a name="example"></a>Exemple
Hello suivant extrait de code crée un récepteur de message. Bonjour, recevoir une boucle pour la file d’attente principale de hello, code de hello récupère le message de type hello avec [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), qui vous demande tooinstantly de broker hello retour tout message prête ou tooreturn aucun résultat. Si le code de hello reçoit un message, il immédiatement abandonne, qui incrémente hello `DeliveryCount`. Une fois que le système de hello déplace hello message toohello DLQ, file d’attente principale de hello est vide et hello issues de la boucle, comme [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) retourne **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des articles pour plus d’informations sur les files d’attente Service Bus :

* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Comparaison des files d’attente Azure et Service Bus](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

