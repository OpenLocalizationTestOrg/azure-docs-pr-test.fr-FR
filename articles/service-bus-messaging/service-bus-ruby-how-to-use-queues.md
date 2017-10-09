---
title: "les files d’attente d’aaaHow toouse Azure Service Bus Ruby | Documents Microsoft"
description: "Découvrez comment toouse Service Bus de files d’attente dans Azure. Exemples de code écrits en Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Comment toouse Service Bus de files d’attente Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Ce guide décrit comment les files d’attente de toouse Service Bus. exemples de Hello sont écrits en Ruby et utilisent hello marque Azure. Hello scénarios abordés incluent **création de files d’attente, envoyer et recevoir des messages**, et **la suppression de files d’attente**. Pour plus d’informations sur les files d’attente Service Bus, consultez hello [étapes](#next-steps) section.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Comment toocreate une file d’attente
Hello **Azure::ServiceBusService** objet vous permet de toowork avec les files d’attente. toocreate une file d’attente, utilisez hello `create_queue()` (méthode). Hello exemple suivant crée une file d’attente ou imprime les erreurs.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

Vous pouvez également passer un **Azure::ServiceBus::Queue** de l’objet avec des options supplémentaires, qui vous permet de paramètres file d’attente par défaut toooverride hello, telles que la taille de file d’attente toolive ou maximale message temps. Bonjour à l’exemple suivant montre comment les tooset hello too5 de taille de file d’attente maximale Go et too1 toolive minutes de temps :

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Comment la file d’attente de tooa de messages toosend
toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `send_queue_message()` méthode sur hello **Azure::ServiceBusService** objet. Trop envoyée (et reçues à partir de) Service Bus sont des files d’attente de messages **Azure::ServiceBus::BrokeredMessage** , et qu’un ensemble de propriétés standard (tels que `label` et `time_to_live`), un dictionnaire qui est utilisé toohold les propriétés spécifiques à l’application personnalisées et un corps de données d’application arbitraire. Une application peut définir le corps de hello du message de type hello en passant une valeur de chaîne en tant que message de type hello et les propriétés standards sont remplies avec les valeurs par défaut.

Hello exemple suivant montre comment toosend une file d’attente toohello test nommé `test-queue` à l’aide de `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin. Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.

## <a name="how-tooreceive-messages-from-a-queue"></a>Comment tooreceive les messages à partir d’une file d’attente
Les messages sont reçus à partir d’une file d’attente à l’aide de hello `receive_queue_message()` méthode sur hello **Azure::ServiceBusService** objet. Par défaut, les messages sont lus et verrouillés sans les supprimer de la file d’attente hello. Toutefois, vous pouvez supprimer des messages à partir de la file d’attente hello lorsqu’elles sont lues par la définition de hello `:peek_lock` option trop**false**.

comportement par défaut de Hello rend hello lors de la lecture et de suppression d’une opération de deux étapes, ce qui le rend également toosupport possible les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `delete_queue_message()` (méthode) et en fournissant des toobe de message hello supprimé en tant que paramètre. Hello `delete_queue_message()` méthode marquer le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.

Si hello `:peek_lock` paramètre est défini trop**false**, la lecture et suppression d’un message de salutation devient le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement de hello un Échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Étant donné que le Service Bus a marqué le message de type hello comme ayant été consommé, quand l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Hello exemple suivant montre comment tooreceive et processus de messages à l’aide de `receive_queue_message()`. tout d’abord, Hello exemple reçoit et supprime un message à l’aide de `:peek_lock` défini trop**false**, il reçoit un autre message, puis puis suppressions hello à l’aide du message `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlock_queue_message()` méthode sur hello **Azure::ServiceBusService** objet. Cela entraîne appel hello toounlock de Service Bus de messages dans la file d’attente hello et le rendre disponible toobe reçu, soit par Bonjour même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille le message de type hello automatiquement et le rend disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `delete_queue_message()` méthode est appelée, puis le message de type hello est redistribué toohello application lors de son redémarrage. Ce processus est souvent appelé *au moins une fois le traitement*; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello `message_id` propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, suivez ces liens de toolearn plus.

* Vue d’ensemble des [files d’attente, rubriques et abonnements](service-bus-queues-topics-subscriptions.md).
* Visitez hello [Azure SDK pour Ruby](https://github.com/Azure/azure-sdk-for-ruby) référentiel sur GitHub.

Pour obtenir une comparaison entre les files d’attente Azure Service Bus hello abordés dans cet article et des files d’attente Azure présentés dans hello [comment toouse stockage de file d’attente à partir de Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) l’article, consultez [Azure files d’attente et Azure Service Bus - comparées et différences](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

