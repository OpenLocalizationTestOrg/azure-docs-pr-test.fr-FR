---
title: Utilisation des rubriques Service Bus (Ruby) | Microsoft Docs
description: "Découvrez comment utiliser les rubriques et abonnements Service Bus dans Azure. Les exemples de code sont écrits pour les applications Ruby."
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
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="6011b-104">Utilisation des rubriques et abonnements Service Bus avec Ruby</span><span class="sxs-lookup"><span data-stu-id="6011b-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="6011b-105">Cet article décrit l’utilisation des rubriques et des abonnements Service Bus depuis les applications Ruby.</span><span class="sxs-lookup"><span data-stu-id="6011b-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="6011b-106">Les scénarios couverts incluent la **création de rubriques et d’abonnements, la création de filtres d’abonnement, l’envoi de messages** à une rubrique, **la réception de messages en provenance d’un abonnement** et enfin **la suppression de rubriques et d’abonnements**.</span><span class="sxs-lookup"><span data-stu-id="6011b-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="6011b-107">Pour plus d’informations sur les rubriques et les abonnements, consultez la section [Étapes suivantes](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="6011b-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="6011b-108">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="6011b-108">Create a topic</span></span>
<span data-ttu-id="6011b-109">L’objet **Azure::ServiceBusService** permet d’utiliser des rubriques.</span><span class="sxs-lookup"><span data-stu-id="6011b-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="6011b-110">Le code suivant crée un objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-111">Pour créer une rubrique, utilisez la méthode `create_topic()`.</span><span class="sxs-lookup"><span data-stu-id="6011b-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="6011b-112">L’exemple suivant crée une rubrique ou imprime les erreurs s’il en existe.</span><span class="sxs-lookup"><span data-stu-id="6011b-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="6011b-113">Vous pouvez également transmettre un objet **Azure::ServiceBus::Topic** avec des options complémentaires, ce qui vous permet de remplacer les paramètres de rubrique par défaut comme la durée de vie de message ou la taille de file d’attente maximale.</span><span class="sxs-lookup"><span data-stu-id="6011b-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="6011b-114">L’exemple suivant montre comment définir la taille maximale de la file d’attente sur 5 Go et la durée de vie du message, sur 1 minute :</span><span class="sxs-lookup"><span data-stu-id="6011b-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="6011b-115">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="6011b-115">Create subscriptions</span></span>
<span data-ttu-id="6011b-116">Les abonnements de rubrique sont également créés à l’aide de l’objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-117">Les abonnements sont nommés et peuvent être assortis d'un filtre facultatif qui limite l'ensemble des messages transmis à la file d'attente virtuelle de l'abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="6011b-118">Les abonnements sont persistants et continuent à exister jusqu’à leur suppression ou celle de la rubrique à laquelle ils sont associés.</span><span class="sxs-lookup"><span data-stu-id="6011b-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="6011b-119">Si votre application contient une logique pour la création d’un abonnement, elle doit d’abord vérifier si l’abonnement existe déjà en utilisant la méthode getSubscription.</span><span class="sxs-lookup"><span data-stu-id="6011b-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="6011b-120">Création d’un abonnement avec le filtre par défaut (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="6011b-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="6011b-121">Le filtre **MatchAll** est le filtre utilisé par défaut si aucun filtre n’est spécifié lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="6011b-122">Lorsque le filtre **MatchAll** est utilisé, tous les messages publiés dans la rubrique sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="6011b-123">Dans l’exemple suivant, l’abonnement « all-messages » qui est créé utilise le filtre par défaut **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="6011b-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="6011b-124">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="6011b-124">Create subscriptions with filters</span></span>
<span data-ttu-id="6011b-125">Vous pouvez également définir des filtres pour spécifier quels sont les messages, parmi ceux envoyés à une rubrique, qui doivent apparaître dans un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="6011b-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="6011b-126">Parmi les types de filtres pris en charge par les abonnements, **Azure::ServiceBus::SqlFilter** est le plus flexible ; il implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="6011b-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="6011b-127">Les filtres SQL opèrent au niveau des propriétés des messages publiés dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="6011b-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="6011b-128">Pour plus de détails sur les expressions utilisables avec un filtre SQL, examinez la syntaxe [SqlFilter](service-bus-messaging-sql-filter.md).</span><span class="sxs-lookup"><span data-stu-id="6011b-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="6011b-129">Vous pouvez ajouter des filtres à un abonnement en utilisant la méthode `create_rule()` de l’objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-130">Cette méthode vous permet d’ajouter de nouveaux filtres à un abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="6011b-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="6011b-131">Étant donné que le filtre par défaut est appliqué automatiquement à tous les nouveaux abonnements, vous devez d’abord supprimer le filtre par défaut ou le filtre **MatchAll** remplacera tous les autres filtres spécifiés.</span><span class="sxs-lookup"><span data-stu-id="6011b-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="6011b-132">Vous pouvez supprimer la règle par défaut en utilisant la méthode `delete_rule()` sur l’objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="6011b-133">Dans l’exemple suivant, l’abonnement « high-messages » est créé avec un filtre **Azure::ServiceBus::SqlFilter** qui sélectionne uniquement les messages dont la propriété personnalisée `message_number` a une valeur supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="6011b-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="6011b-134">De même, l’exemple suivant crée l’abonnement `low-messages` avec un objet **Azure::ServiceBus::SqlFilter** qui ne sélectionne que les messages dont la propriété `message_number` a une valeur inférieure ou égale à 3 :</span><span class="sxs-lookup"><span data-stu-id="6011b-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

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

<span data-ttu-id="6011b-135">Lorsqu’un message est envoyé à `test-topic`, il est toujours remis aux destinataires abonnés à l’abonnement de rubrique `all-messages`, et est remis de manière sélective aux destinataires abonnés aux abonnements de rubrique `high-messages` et `low-messages` (en fonction du contenu du message).</span><span class="sxs-lookup"><span data-stu-id="6011b-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="6011b-136">Envoi de messages à une rubrique</span><span class="sxs-lookup"><span data-stu-id="6011b-136">Send messages to a topic</span></span>
<span data-ttu-id="6011b-137">Pour envoyer un message à une rubrique Service Bus, votre application doit utiliser la méthode `send_topic_message()` sur l’objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-138">Les messages envoyés aux rubriques Service Bus sont des instances des objets **Azure::ServiceBus::BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="6011b-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="6011b-139">Les objets **Azure::ServiceBus::BrokeredMessage** possèdent un ensemble de propriétés standard (telles que `label` et `time_to_live`), un dictionnaire servant à conserver les propriétés personnalisées propres à une application, ainsi qu’un corps de données de chaîne.</span><span class="sxs-lookup"><span data-stu-id="6011b-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="6011b-140">Une application peut définir le corps du message en transmettant une valeur de chaîne à la méthode `send_topic_message()` pour remplir toutes les propriétés standard requises avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="6011b-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="6011b-141">L’exemple suivant montre comment envoyer cinq messages de test à `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="6011b-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="6011b-142">Notez que la valeur de la propriété personnalisée `message_number` de chaque message varie au niveau de l’itération de la boucle (cela détermine l’abonnement qui le reçoit) :</span><span class="sxs-lookup"><span data-stu-id="6011b-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="6011b-143">Les rubriques Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et de 1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6011b-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="6011b-144">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="6011b-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="6011b-145">Si une rubrique n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="6011b-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="6011b-146">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="6011b-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="6011b-147">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="6011b-147">Receive messages from a subscription</span></span>
<span data-ttu-id="6011b-148">La méthode `receive_subscription_message()` de l’objet **Azure::ServiceBusService** permet de recevoir les messages associés à un abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-149">Par défaut, les messages sont lus et verrouillés sans être supprimés de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="6011b-150">Il est possible de lire et de supprimer le message de l’abonnement en définissant l’option `peek_lock` sur **false**.</span><span class="sxs-lookup"><span data-stu-id="6011b-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="6011b-151">Avec le comportement par défaut, la lecture et la suppression sont une opération en deux étapes, ce qui permet également de prendre en charge des applications ne pouvant pas fonctionner avec des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="6011b-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="6011b-152">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="6011b-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="6011b-153">Dès lors que l’application a terminé le traitement du message (ou qu’elle l’a stocké de manière fiable pour un traitement ultérieur), elle accomplit la deuxième étape du processus de réception en appelant la méthode `delete_subscription_message()` et en fournissant le message à supprimer sous la forme d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="6011b-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="6011b-154">La méthode `delete_subscription_message()` marque le message comme étant consommé et le supprime de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6011b-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="6011b-155">Si le paramètre `:peek_lock` est défini sur **false**, le modèle le plus simple correspond à la lecture et à la suppression du message. Ce modèle fonctionne mieux pour les scénarios dans lesquels une application peut accepter de ne pas traiter un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="6011b-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="6011b-156">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="6011b-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="6011b-157">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="6011b-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="6011b-158">L’exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="6011b-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="6011b-159">Dans l’exemple, un message est d’abord reçu, puis supprimé par le biais de l’abonnement `low-messages`, le paramètre `:peek_lock` étant défini sur **false**, puis `high-messages` envoie un autre message, qui est supprimé via `delete_subscription_message()` :</span><span class="sxs-lookup"><span data-stu-id="6011b-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="6011b-160">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="6011b-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="6011b-161">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="6011b-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="6011b-162">Si une application réceptrice ne parvient pas à traiter le message pour une raison quelconque, elle appelle la méthode `unlock_subscription_message()` pour l’objet **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="6011b-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="6011b-163">Cela amène Service Bus à déverrouiller le message dans l’abonnement et à le rendre à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="6011b-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="6011b-164">De même, il faut savoir qu’un message verrouillé dans un abonnement est assorti d’un délai d’expiration et que si l’application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l’application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="6011b-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="6011b-165">Si l’application subit un incident après le traitement du message, mais avant l’appel de la méthode `delete_subscription_message()`, le message est à nouveau remis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="6011b-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="6011b-166">Dans ce type de traitement, souvent appelé *Au moins une fois*, chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="6011b-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="6011b-167">Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="6011b-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="6011b-168">Cette logique est souvent obtenue grâce à la propriété `message_id` du message, qui reste constante pendant les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="6011b-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="6011b-169">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="6011b-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="6011b-170">Les rubriques et les abonnements sont persistants et doivent être supprimés de façon explicite par le biais du [portail Azure][Azure portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="6011b-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="6011b-171">L’exemple suivant montre comme supprimer la rubrique intitulée `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="6011b-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="6011b-172">La suppression d’une rubrique a également pour effet de supprimer les abonnements inscrits dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="6011b-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="6011b-173">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="6011b-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="6011b-174">Le code suivant montre comment supprimer l’abonnement `high-messages` de la rubrique `test-topic` :</span><span class="sxs-lookup"><span data-stu-id="6011b-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="6011b-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6011b-175">Next steps</span></span>
<span data-ttu-id="6011b-176">Maintenant que vous avez appris les principes de base des rubriques Service Bus, consultez ces liens pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="6011b-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="6011b-177">Consultez [Files d’attente, rubriques et abonnements](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="6011b-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="6011b-178">Référence d’API pour [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="6011b-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="6011b-179">Accédez au référentiel du [Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/Azure/azure-sdk-for-ruby) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="6011b-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
