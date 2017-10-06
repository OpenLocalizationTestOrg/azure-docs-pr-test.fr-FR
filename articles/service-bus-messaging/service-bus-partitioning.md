---
title: "aaaCreate les files d’attente Azure Service Bus et les rubriques partitionnés | Documents Microsoft"
description: "Décrit comment les files d’attente de toopartition Service Bus et des rubriques à l’aide de plusieurs messages fournit."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Files d’attente et rubriques partitionnées
Azure Service Bus utilise plusieurs messages de tooprocess courtiers et messagerie plusieurs stocke les messages de toostore. Une file d’attente ou une rubrique classique est gérée par un seul courtier de messages et stockée dans une seule banque de messagerie. Service Bus *partitions* activer les files d’attente et rubriques, ou *des entités de messagerie*, toobe partitionnée entre plusieurs brokers et banques de messages. Cela signifie que hello le débit global d’une entité partitionnée n’est plus limitée par des performances d’un seul broker ou de la banque de messages hello. En outre, la panne temporaire d’une banque de messagerie ne rend pas une rubrique ou une file d’attente partitionnée indisponible. Les rubriques et les files d’attente partitionnées peuvent contenir toutes les fonctionnalités avancées de Service Bus, comme la prise en charge des transactions et des sessions.

Pour plus d’informations sur les mécanismes internes de Service Bus, consultez hello [architecture de Service Bus] [ Service Bus architecture] l’article.

Le partitionnement est activé par défaut lors de la création d’entités sur toutes les files d’attente et rubriques à la fois dans la messagerie Standard et Premium. Vous pouvez créer des entités de niveau de messagerie Standard sans partitionnement, mais les files d’attente et les rubriques dans un espace de noms Premium sont toujours partitionnées ; cette option ne peut pas être désactivée. 

Il n’est pas possible de toochange hello option sur une file d’attente existante ou une rubrique dans les niveaux Standard ou Premium de partitionnement, vous pouvez uniquement définir hello option lorsque vous créez des entités de hello.

## <a name="how-it-works"></a>Fonctionnement

Chaque file d’attente ou rubrique partitionnée est constituée de plusieurs fragments. Chaque fragment est stocké dans une banque de messagerie différente et géré par un courtier de messages différent. Lorsqu’un message est envoyé tooa la file d’attente partitionnée ou une rubrique, Service Bus assigne tooone de message hello de fragments de hello. sélection de Hello est effectuée de façon aléatoire par Service Bus ou à l’aide d’une clé de partition qui hello expéditeur peut spécifier.

Quand un client veut tooreceive un message à partir d’une file d’attente partitionnée ou à partir d’une rubrique partitionnée tooa d’abonnement, Service Bus interroge tous les fragments de messages, puis retourne hello premier message qui est obtenue à partir des hello magasins toohello destinataire de messagerie. Les caches de service Bus hello autres messages et les retourne les lorsqu’il reçoit plus les demandes de réception. Un client récepteur n’est pas informé de hello partitionnement ; Hello le comportement des clients d’une file d’attente partitionnée ou une rubrique (par exemple, lire, exécuter, différez, de lettres mortes, la prérécupération) est le comportement toohello identiques d’une entité normale.

Il n’existe aucun coût supplémentaire lors de l’envoi d’un message à, ou lors de la réception d’un message depuis, une file d’attente ou une rubrique partitionnée.

## <a name="enable-partitioning"></a>Activation du partitionnement

toouse partitionné les files d’attente et rubriques avec Azure Service Bus, utilisez hello Azure SDK version 2.2 ou version ultérieure, ou spécifiez `api-version=2013-10` dans vos requêtes HTTP.

### <a name="standard"></a>Standard

Dans la couche de messagerie Standard hello, vous pouvez créer des files d’attente Service Bus et les rubriques de tailles de 1, 2, 3, 4 ou 5 Go (valeur par défaut hello est 1 Go). Avec le partitionnement est activé, Service Bus crée 16 copies (16 partitions) de l’entité de hello pour chaque Go que vous spécifiez. Par conséquent, si vous créez une file d’attente est de 5 Go de taille, avec 16 partitions taille de file d’attente maximale hello devient (5 \* 16) = 80 Go. Vous pouvez voir la taille maximale de hello de votre file d’attente partitionnée ou une rubrique en examinant son entrée sur hello [portail Azure][Azure portal], Bonjour **vue d’ensemble** panneau pour cette entité.

### <a name="premium"></a>Premium

Dans un espace de noms de niveau Premium, vous pouvez créer des files d’attente Service Bus et les rubriques de tailles de 1, 2, 3, 4, 5, 10, 20, 40 ou 80 Go (valeur par défaut hello est 1 Go). Avec le partitionnement activé par défaut, Service Bus crée deux partitions par entité. Vous pouvez voir la taille maximale de hello de votre file d’attente partitionnée ou une rubrique en examinant son entrée sur hello [portail Azure][Azure portal], Bonjour **vue d’ensemble** panneau pour cette entité.

Pour plus d’informations sur le partitionnement dans la couche de messagerie hello Premium, consultez [Premium de Bus de Service et les niveaux de messagerie Standard](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Créer une entité partitionnée

Il existe plusieurs façons toocreate une file d’attente partitionnée ou une rubrique. Lorsque vous créez une file d’attente hello ou une rubrique à partir de votre application, vous pouvez activer le partitionnement de la file d’attente hello ou une rubrique en hello de paramètre respectivement [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] ou [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] propriété trop**true**. Ces propriétés doivent être définies à hello délai hello file d’attente ou rubrique est créée. Comme indiqué précédemment, il est impossible toochange ces propriétés sur une file d’attente existante ou une rubrique. Par exemple :

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Vous pouvez également créer une file d’attente partitionnée ou une rubrique Bonjour [portail Azure] [ Azure portal] ou dans Visual Studio. Lorsque vous créez une file d’attente ou une rubrique dans le portail de hello, hello **activer leur partitionnement** option dans la file d’attente hello ou une rubrique **créer** lame est activée par défaut. Vous pouvez uniquement désactiver cette option dans une entité de niveau Standard ; Bonjour partitionnement de niveau Premium est toujours activé. Dans Visual Studio, cliquez sur hello **activer le partitionnement** case à cocher Bonjour **nouvelle file d’attente** ou **nouvelle rubrique** boîte de dialogue.

## <a name="use-of-partition-keys"></a>Utilisation de clés de partition
Lorsqu’un message est envoyé vers une file d’attente partitionnée ou une rubrique, Service Bus vérifie présence hello d’une clé de partition. S’il en trouve, il sélectionne le fragment de hello basé sur cette clé. S’il ne trouve pas une clé de partition, il sélectionne le fragment hello selon un algorithme interne.

### <a name="using-a-partition-key"></a>Utilisation d’une clé de partition
Certains scénarios, tels que les sessions ou les transactions, nécessitent toobe messages stocké dans un fragment spécifique. Tous ces scénarios requièrent l’utilisation hello d’une clé de partition. Tous les messages que hello utilisez même clé de partition sont affectés toohello même fragment. Si le fragment de hello est temporairement indisponible, Service Bus renvoie une erreur.

Selon le scénario de hello, les propriétés de message différents sont utilisées comme clé de partition :

**SessionId**: si un message hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriété définie, puis le Service Bus utilise cette propriété en tant que clé de partition hello. De cette manière, tous les messages appartenant toohello même session sont gérés par hello même service broker de message. Ainsi, le message de tooguarantee Service Bus classement, ainsi que la cohérence de hello des États de session.

**PartitionKey**: si un message hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriété mais pas hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriété définie, puis Service Bus utilise hello [PartitionKey] [ PartitionKey] propriété en tant que clé de partition hello. Si le message de salutation a deux hello [SessionId] [ SessionId] et hello [PartitionKey] [ PartitionKey] jeu de propriétés, les deux propriétés doivent être identiques. Si hello [PartitionKey] [ PartitionKey] propriété a une valeur différente tooa hello [SessionId] [ SessionId] propriété, Service Bus retourne non valide exception de l’opération. Hello [PartitionKey] [ PartitionKey] propriété doit être utilisée si un expéditeur envoie des messages transactionnelles prenant en charge de session non. Hello clé de partition garantit que tous les messages sont envoyés dans une transaction sont gérés par hello que même broker de messagerie.

**MessageId**: si la file d’attente de hello ou une rubrique a hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriété trop**true** et hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] ou [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriétés ne sont pas définies, puis hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] propriété sert de clé de partition hello. (Notez que les bibliothèques Microsoft .NET et AMQP hello attribuer automatiquement un ID de message n’est pas le cas de l’application d’expédition hello). Dans ce cas, toutes les copies de hello même message sont gérées par Bonjour même service broker de message. Cela permet à Service Bus toodetect et éliminer les messages en double. Si hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriété n’est pas définie trop**true**, Service Bus ne tient pas compte hello [MessageId] [ MessageId] propriété comme clé de partition.

### <a name="not-using-a-partition-key"></a>Non utilisation d'une clé de partition
En absence de hello d’une clé de partition, Service Bus distribue les messages dans un tourniquet tooall hello des fragments de file d’attente partitionnée de hello ou une rubrique. Si le fragment de hello choisi n’est pas disponible, Service Bus affecte autre fragment hello message tooa. De cette manière, opération d’envoi hello réussit en dépit de l’indisponibilité temporaire d’une banque de messages hello. Toutefois, vous n’obtiendrez pas hello classement qu’une clé de partition fournit garanti.

Pour obtenir une explication plus approfondie des compromis hello entre la disponibilité (aucune clé de partition) et la cohérence (à l’aide d’une clé de partition), consultez [cet article](../event-hubs/event-hubs-availability-and-consistency.md). Ces informations s’appliquent également les entités de Service Bus toopartitioned et les partitions de concentrateurs d’événements.

toogive Service Bus suffisamment message de type hello tooenqueue temps dans un fragment différent, hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] valeur spécifiée par le client hello qui envoie le message de type hello doit être supérieure à 15 secondes. Il est recommandé de définir hello [OperationTimeout] [ OperationTimeout] propriété toohello par défaut de 60 secondes.

Notez qu’une clé de partition « épingle » un fragment spécifique tooa de message. Si la banque de messages hello qui détient ce fragment n’est pas disponible, Service Bus renvoie une erreur. En absence de hello d’une clé de partition, Service Bus peut choisir un autre fragment et hello réussit. Par conséquent, il est recommandé de ne pas fournir de clé de partition, sauf si elle est requise.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Rubriques avancées : utiliser des transactions avec des entités partitionnées
Les messages envoyés dans le cadre d’une transaction doivent spécifier une clé de partition. Cela peut être une des propriétés suivantes de hello : [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], ou [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Tous les messages sont envoyés dans le cadre de hello même transaction doive spécifier hello la même clé de partition. Si vous essayez de toosend un message sans clé de partition dans une transaction, Service Bus renvoie une exception d’opération non valide. Si vous essayez de toosend plusieurs messages dans hello même transaction qui ont différentes clés de partition, Service Bus renvoie une exception d’opération non valide. Par exemple :

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Si une des propriétés hello servir de clé de partition sont définie, codes confidentiels de Service Bus hello fragments de message tooa spécifique. Ce comportement se produit qu'une transaction soit utilisée ou non. Il est recommandé de ne pas spécifier de clé de partition si elle n'est pas nécessaire.

## <a name="using-sessions-with-partitioned-entities"></a>Utilisation de sessions avec les entités partitionnées
toosend une rubrique en charge la session de message transactionnel tooa ou file d’attente, message de salutation doit avoir hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] jeu de propriétés. Si hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriété est également spécifiée, elle doit être identique toohello [SessionId] [ SessionId] propriété. Si ces propriétés diffèrent, Service Bus renvoie une exception d’opération non valide.

Contrairement à standards (non partitionnée) les files d’attente ou rubriques, il n’est pas possible toouse un toosend transaction unique plusieurs sessions de toodifferent de messages. En cas de tentative, Service Bus renvoie une exception d’opération non valide. Par exemple :

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Transfert automatique des messages avec des entités partitionnées
Service Bus prend en charge le transfert automatique des messages à partir de, vers ou entre les entités partitionnées. tooenable transfert automatique de messages, définissez hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] propriété sur la file d’attente de la source hello ou un abonnement. Si le message de type hello spécifie une clé de partition ([SessionId][SessionId], [PartitionKey][PartitionKey], ou [MessageId] [ MessageId]), cette clé de partition est utilisée pour l’entité de destination hello.

## <a name="considerations-and-guidelines"></a>Considérations et recommandations
* **Fonctionnalités de cohérence haute**: si une entité utilise des fonctionnalités telles que des sessions, détection des doublons ou un contrôle explicite de la clé de partitionnement, les opérations de messagerie hello sont toujours toospecific routé fragments. Si un des fragments de hello rencontrer un trafic élevé ou le magasin sous-jacent hello est défectueux, ces opérations échouent et la disponibilité est réduite. En général, la cohérence de hello est bien plue importante que les entités non partitionnée ; uniquement un sous-ensemble du trafic rencontre des problèmes, comme le trafic de hello tooall exécutée. Pour plus d’informations, consultez cette [discussion sur la disponibilité et la cohérence](../event-hubs/event-hubs-availability-and-consistency.md).
* **Gestion**: opérations telles que Create, Update et Delete doivent être exécutées sur tous les fragments de hello d’entité de hello. Si un fragment est défectueux, cela peut entraîner l’échec de ces opérations. Pour une opération d’obtention de hello, des informations telles que des nombres de messages doivent être agrégées à partir de tous les fragments. Si un fragment est défectueux, état de disponibilité d’entité hello est signalée comme limitée.
* **Scénarios de message de volume à faible**: dans ce cas, surtout lorsque vous utilisez le protocole de hello HTTP, vous avez peut-être tooperform plusieurs opérations de réception dans l’ordre tooobtain tous les messages de type hello. Pour les demandes de réception, serveur frontal hello effectue une opération de réception sur tous les fragments hello et met en cache toutes les réponses hello reçues. Une demande de réception suivantes sur la même connexion serait tirer parti de cette mise en cache et recevoir des latences de hello sera inférieure. Toutefois, si vous disposez de plusieurs connexions ou si vous utilisez HTTP, une nouvelle connexion est établie pour chaque demande. Par conséquent, il n’existe aucune garantie qu’il serait arriver sur hello même nœud. Si tous les messages existants sont verrouillés et mis en cache dans un autre serveur frontal, hello retourne de l’opération de réception **null**. Les messages peuvent arriver à expiration et vous pouvez les recevoir à nouveau. La persistance du protocole HTTP est recommandée.
* **Parcourir/Peek messages**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) ne retourne pas toujours le nombre de hello de messages spécifiés dans hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) propriété. Il existe deux raisons courantes à cela. L’une des raisons sont que hello agrégées de collection hello de messages dépasse hello maximale de 256 Ko. Une autre raison est que si la file d’attente de hello ou une rubrique a hello [EnablePartitioning propriété](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) défini trop**true**, une partition ne peut pas avoir suffisamment de messages toocomplete hello a demandé le nombre de messages. En règle générale, si une application veut tooreceive un certain nombre de messages, il doit appeler [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) à plusieurs reprises jusqu'à ce qu’il obtient le nombre de messages, ou il n’y aucun toopeek plus de messages. Pour plus d’informations, y compris pour obtenir des exemples de code, consultez [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) ou [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Dernières fonctionnalités ajoutées
* L’ajout ou la suppression de règles est désormais pris en charge avec les entités partitionnées. À la différence des entités non partitionnée, ces opérations ne sont pas prises en charge dans le cadre des transactions. 
* AMQP est désormais pris en charge pour envoyer et recevoir des messages tooand d’une entité partitionnée.
* AMQP est désormais pris en charge pour hello opérations suivantes : [envoyer de lot](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [lot recevoir](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [réception par numéro de séquence](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [aperçu](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Renouveler le verrou](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [planifier Message](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [Annuler Message planifiée](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [ajouter une règle](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [supprimer la règle](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Verrou de renouvellement de session](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [définir l’état de Session](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [obtenir l’état de Session](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), et [énumérer les Sessions](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Limites des entités partitionnées
Actuellement, Service Bus impose hello limites suivantes sur les rubriques et files d’attente partitionnées :

* Celles-ci ne gèrent pas d’envoi de messages appartenant toodifferent sessions dans une transaction unique.
* Service Bus permet actuellement too100 partitionné les files d’attente ou rubriques par espace de noms. Chaque file d’attente partitionnée ou une rubrique compte dans le quota de hello de 10 000 entités par espace de noms (ne s’applique pas tooPremium couche).

## <a name="next-steps"></a>Étapes suivantes
Consultez la discussion hello de [prise en charge d’AMQP 1.0 pour Service Bus partitionnée files d’attente et rubriques] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn plus d’informations sur le partitionnement des entités de messagerie. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
