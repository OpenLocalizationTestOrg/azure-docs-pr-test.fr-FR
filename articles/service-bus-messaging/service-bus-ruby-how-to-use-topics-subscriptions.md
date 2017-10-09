---
title: rubriques de Service Bus toouse aaaHow (Ruby) | Documents Microsoft
description: "Découvrez comment toouse Service Bus rubriques et abonnements dans Azure. Les exemples de code sont écrits pour les applications Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Comment toouse Service Bus rubriques et abonnements Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Cet article décrit comment toouse Service Bus rubriques et abonnements à partir d’applications Ruby. Hello scénarios abordés incluent **création de rubriques et abonnements, création de filtres d’abonnement, envoi de messages** tooa rubrique, **réception de messages à partir d’un abonnement**, et  **suppression des rubriques et abonnements**. Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Création d'une rubrique
Hello **Azure::ServiceBusService** objet vous permet de toowork aux rubriques. Hello de code suivant crée un **Azure::ServiceBusService** objet. toocreate une rubrique, utilisez hello `create_topic()` (méthode). Bonjour à l’exemple suivant crée une rubrique ou imprime les erreurs hello le cas échéant.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Vous pouvez également passer un **Azure::ServiceBus::Topic** objet avec des options supplémentaires, qui permettent de paramètres de rubrique toooverride par défaut comme taille de file d’attente toolive ou une valeur maximale de temps de message. Hello exemple suivant illustre la définition de file d’attente maximale de hello too5 Go et d’heure too1 toolive minute :

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Création d’abonnements
Abonnements aux rubriques sont également créés par hello **Azure::ServiceBusService** objet. Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.

Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique associées, elles sont supprimées. Si votre application contient la logique toocreate un abonnement, il doit tout d’abord vérifier si hello abonnement existe déjà à l’aide de méthode de getSubscription hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Créer un abonnement avec le filtre par défaut (MatchAll) hello
Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement. Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello. Hello exemple suivant crée un abonnement nommé « tous les messages » et utilise hello par défaut **MatchAll** filtre.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Création d’abonnements avec des filtres
Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement spécifique.

type de filtre pris en charge par les abonnements plus souple Hello est hello **Azure::ServiceBus::SqlFilter**, qui implémente un sous-ensemble de SQL92. Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique. Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter](service-bus-messaging-sql-filter.md) syntaxe.

Vous pouvez ajouter des filtres tooa abonnement à l’aide de hello `create_rule()` méthode Hello **Azure::ServiceBusService** objet. Cette méthode vous permet d’abonnement existant tooadd nouveaux filtres tooan.

Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez tout d’abord supprimer le filtre par défaut de hello ou hello **MatchAll** remplace tous les autres filtres que vous pouvez spécifier. Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `delete_rule()` méthode sur hello **Azure::ServiceBusService** objet.

Hello exemple suivant crée un abonnement nommé « haute-messages » avec une **Azure::ServiceBus::SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `message_number` propriété supérieure à 3 :

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

De même, hello exemple suivant crée un abonnement nommé `low-messages` avec un **Azure::ServiceBus::SqlFilter** qui sélectionne uniquement les messages qui ont un `message_number` propriété inférieur ou égal too3 :

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Lorsqu’un message est envoyé maintenant trop`test-topic`, il est toujours remis tooreceivers abonné toohello `all-messages` abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello `high-messages` et `low-messages` (abonnements de rubrique en fonction de contenu du message hello).

## <a name="send-messages-tooa-topic"></a>Rubrique tooa de messages d’envoi
toosend une rubrique de Service Bus message tooa, votre application doit utiliser hello `send_topic_message()` méthode sur hello **Azure::ServiceBusService** objet. Les messages envoyés rubriques du Bus tooService sont des instances de hello **Azure::ServiceBus::BrokeredMessage** objets. **Azure::ServiceBus::BrokeredMessage** objets comportent un ensemble de propriétés standard (tels que `label` et `time_to_live`), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données de chaîne. Une application peut définir le corps de hello du message de type hello en passant un toohello de valeur de chaîne `send_topic_message()` (méthode) et tout requis propriétés standard seront remplies par les valeurs par défaut.

Hello exemple suivant montre comment le test de toosend cinq messages trop`test-topic`. Notez que hello `message_number` varie en fonction de valeur de propriété personnalisée de chaque message sur l’itération hello de boucle de hello (détermine quel abonnement reçoit) :

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin. Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.

## <a name="receive-messages-from-a-subscription"></a>Réception des messages d’un abonnement
Les messages sont reçus à partir d’un abonnement à l’aide de hello `receive_subscription_message()` méthode sur hello **Azure::ServiceBusService** objet. Par défaut, les messages sont read(peak) et verrouillé sans la supprimer de l’abonnement de hello. Vous pouvez lire et supprimer des message de type hello d’abonnement de hello en définissant un hello `peek_lock` option trop**false**.

comportement par défaut de Hello rend hello lors de la lecture et de suppression d’une opération de deux étapes, ce qui le rend également toosupport possible les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `delete_subscription_message()` (méthode) et en fournissant des toobe de message hello supprimé en tant que paramètre. Hello `delete_subscription_message()` méthode marquer le message de type hello comme ayant été consommé et le supprimer de l’abonnement de hello.

Si hello `:peek_lock` paramètre est défini trop**false**, la lecture et suppression d’un message de salutation devient le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement de hello un Échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receive_subscription_message()`. Hello exemple reçoit tout d’abord et supprime un message de salutation `low-messages` abonnement à l’aide de `:peek_lock` défini trop**false**, puis il reçoit un autre message hello `high-messages` et puis suppressions hello à l’aide du message `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlock_subscription_message()` méthode sur hello **Azure::ServiceBusService** objet. Cela entraîne hello toounlock de Service Bus de messages au sein de l’abonnement de hello et le rendre disponible toobe reçu, soit par Bonjour même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé au sein de l’abonnement de hello, et si l’application hello échoue le message de type hello tooprocess avant de délai d’attente de verrou hello expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `delete_subscription_message()` méthode est appelée, puis le message de type hello est redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois le traitement*; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cette logique est souvent réalisée à l’aide de hello `message_id` propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="delete-topics-and-subscriptions"></a>Suppression de rubriques et d'abonnements
Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme. exemple Hello ci-dessous montre comment la rubrique de hello toodelete nommé `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello. Les abonnements peuvent aussi être supprimés de manière indépendante. Hello de code suivant montre comment abonnement de hello toodelete nommé `high-messages` de hello `test-topic` rubrique :

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.

* Consultez [Files d’attente, rubriques et abonnements](service-bus-queues-topics-subscriptions.md).
* Référence d’API pour [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Visitez hello [Azure SDK pour Ruby](https://github.com/Azure/azure-sdk-for-ruby) référentiel sur GitHub.

[Azure portal]: https://portal.azure.com
