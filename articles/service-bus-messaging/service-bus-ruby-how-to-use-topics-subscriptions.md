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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="576f5-104">Comment toouse Service Bus rubriques et abonnements Ruby</span><span class="sxs-lookup"><span data-stu-id="576f5-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="576f5-105">Cet article décrit comment toouse Service Bus rubriques et abonnements à partir d’applications Ruby.</span><span class="sxs-lookup"><span data-stu-id="576f5-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="576f5-106">Hello scénarios abordés incluent **création de rubriques et abonnements, création de filtres d’abonnement, envoi de messages** tooa rubrique, **réception de messages à partir d’un abonnement**, et  **suppression des rubriques et abonnements**.</span><span class="sxs-lookup"><span data-stu-id="576f5-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="576f5-107">Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="576f5-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="576f5-108">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="576f5-108">Create a topic</span></span>
<span data-ttu-id="576f5-109">Hello **Azure::ServiceBusService** objet vous permet de toowork aux rubriques.</span><span class="sxs-lookup"><span data-stu-id="576f5-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="576f5-110">Hello de code suivant crée un **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-111">toocreate une rubrique, utilisez hello `create_topic()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="576f5-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="576f5-112">Bonjour à l’exemple suivant crée une rubrique ou imprime les erreurs hello le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="576f5-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="576f5-113">Vous pouvez également passer un **Azure::ServiceBus::Topic** objet avec des options supplémentaires, qui permettent de paramètres de rubrique toooverride par défaut comme taille de file d’attente toolive ou une valeur maximale de temps de message.</span><span class="sxs-lookup"><span data-stu-id="576f5-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="576f5-114">Hello exemple suivant illustre la définition de file d’attente maximale de hello too5 Go et d’heure too1 toolive minute :</span><span class="sxs-lookup"><span data-stu-id="576f5-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="576f5-115">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="576f5-115">Create subscriptions</span></span>
<span data-ttu-id="576f5-116">Abonnements aux rubriques sont également créés par hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-117">Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="576f5-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="576f5-118">Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique associées, elles sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="576f5-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="576f5-119">Si votre application contient la logique toocreate un abonnement, il doit tout d’abord vérifier si hello abonnement existe déjà à l’aide de méthode de getSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="576f5-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="576f5-120">Créer un abonnement avec le filtre par défaut (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="576f5-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="576f5-121">Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="576f5-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="576f5-122">Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="576f5-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="576f5-123">Hello exemple suivant crée un abonnement nommé « tous les messages » et utilise hello par défaut **MatchAll** filtre.</span><span class="sxs-lookup"><span data-stu-id="576f5-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="576f5-124">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="576f5-124">Create subscriptions with filters</span></span>
<span data-ttu-id="576f5-125">Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="576f5-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="576f5-126">type de filtre pris en charge par les abonnements plus souple Hello est hello **Azure::ServiceBus::SqlFilter**, qui implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="576f5-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="576f5-127">Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="576f5-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="576f5-128">Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter](service-bus-messaging-sql-filter.md) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="576f5-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="576f5-129">Vous pouvez ajouter des filtres tooa abonnement à l’aide de hello `create_rule()` méthode Hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-130">Cette méthode vous permet d’abonnement existant tooadd nouveaux filtres tooan.</span><span class="sxs-lookup"><span data-stu-id="576f5-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="576f5-131">Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez tout d’abord supprimer le filtre par défaut de hello ou hello **MatchAll** remplace tous les autres filtres que vous pouvez spécifier.</span><span class="sxs-lookup"><span data-stu-id="576f5-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="576f5-132">Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `delete_rule()` méthode sur hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="576f5-133">Hello exemple suivant crée un abonnement nommé « haute-messages » avec une **Azure::ServiceBus::SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `message_number` propriété supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="576f5-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="576f5-134">De même, hello exemple suivant crée un abonnement nommé `low-messages` avec un **Azure::ServiceBus::SqlFilter** qui sélectionne uniquement les messages qui ont un `message_number` propriété inférieur ou égal too3 :</span><span class="sxs-lookup"><span data-stu-id="576f5-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="576f5-135">Lorsqu’un message est envoyé maintenant trop`test-topic`, il est toujours remis tooreceivers abonné toohello `all-messages` abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello `high-messages` et `low-messages` (abonnements de rubrique en fonction de contenu du message hello).</span><span class="sxs-lookup"><span data-stu-id="576f5-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="576f5-136">Rubrique tooa de messages d’envoi</span><span class="sxs-lookup"><span data-stu-id="576f5-136">Send messages tooa topic</span></span>
<span data-ttu-id="576f5-137">toosend une rubrique de Service Bus message tooa, votre application doit utiliser hello `send_topic_message()` méthode sur hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-138">Les messages envoyés rubriques du Bus tooService sont des instances de hello **Azure::ServiceBus::BrokeredMessage** objets.</span><span class="sxs-lookup"><span data-stu-id="576f5-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="576f5-139">**Azure::ServiceBus::BrokeredMessage** objets comportent un ensemble de propriétés standard (tels que `label` et `time_to_live`), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données de chaîne.</span><span class="sxs-lookup"><span data-stu-id="576f5-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="576f5-140">Une application peut définir le corps de hello du message de type hello en passant un toohello de valeur de chaîne `send_topic_message()` (méthode) et tout requis propriétés standard seront remplies par les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="576f5-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="576f5-141">Hello exemple suivant montre comment le test de toosend cinq messages trop`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="576f5-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="576f5-142">Notez que hello `message_number` varie en fonction de valeur de propriété personnalisée de chaque message sur l’itération hello de boucle de hello (détermine quel abonnement reçoit) :</span><span class="sxs-lookup"><span data-stu-id="576f5-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="576f5-143">Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="576f5-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="576f5-144">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="576f5-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="576f5-145">Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="576f5-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="576f5-146">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="576f5-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="576f5-147">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="576f5-147">Receive messages from a subscription</span></span>
<span data-ttu-id="576f5-148">Les messages sont reçus à partir d’un abonnement à l’aide de hello `receive_subscription_message()` méthode sur hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-149">Par défaut, les messages sont read(peak) et verrouillé sans la supprimer de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="576f5-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="576f5-150">Vous pouvez lire et supprimer des message de type hello d’abonnement de hello en définissant un hello `peek_lock` option trop**false**.</span><span class="sxs-lookup"><span data-stu-id="576f5-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="576f5-151">comportement par défaut de Hello rend hello lors de la lecture et de suppression d’une opération de deux étapes, ce qui le rend également toosupport possible les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="576f5-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="576f5-152">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="576f5-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="576f5-153">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `delete_subscription_message()` (méthode) et en fournissant des toobe de message hello supprimé en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="576f5-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="576f5-154">Hello `delete_subscription_message()` méthode marquer le message de type hello comme ayant été consommé et le supprimer de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="576f5-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="576f5-155">Si hello `:peek_lock` paramètre est défini trop**false**, la lecture et suppression d’un message de salutation devient le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement de hello un Échec.</span><span class="sxs-lookup"><span data-stu-id="576f5-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="576f5-156">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="576f5-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="576f5-157">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="576f5-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="576f5-158">Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="576f5-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="576f5-159">Hello exemple reçoit tout d’abord et supprime un message de salutation `low-messages` abonnement à l’aide de `:peek_lock` défini trop**false**, puis il reçoit un autre message hello `high-messages` et puis suppressions hello à l’aide du message `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="576f5-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="576f5-160">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="576f5-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="576f5-161">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="576f5-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="576f5-162">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlock_subscription_message()` méthode sur hello **Azure::ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="576f5-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="576f5-163">Cela entraîne hello toounlock de Service Bus de messages au sein de l’abonnement de hello et le rendre disponible toobe reçu, soit par Bonjour même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="576f5-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="576f5-164">Il existe également un délai d’attente d’un message verrouillé au sein de l’abonnement de hello, et si l’application hello échoue le message de type hello tooprocess avant de délai d’attente de verrou hello expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="576f5-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="576f5-165">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `delete_subscription_message()` méthode est appelée, puis le message de type hello est redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="576f5-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="576f5-166">Cela est souvent appelé *au moins une fois le traitement*; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="576f5-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="576f5-167">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="576f5-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="576f5-168">Cette logique est souvent réalisée à l’aide de hello `message_id` propriété de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="576f5-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="576f5-169">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="576f5-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="576f5-170">Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="576f5-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="576f5-171">exemple Hello ci-dessous montre comment la rubrique de hello toodelete nommé `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="576f5-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="576f5-172">Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="576f5-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="576f5-173">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="576f5-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="576f5-174">Hello de code suivant montre comment abonnement de hello toodelete nommé `high-messages` de hello `test-topic` rubrique :</span><span class="sxs-lookup"><span data-stu-id="576f5-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="576f5-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="576f5-175">Next steps</span></span>
<span data-ttu-id="576f5-176">Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="576f5-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="576f5-177">Consultez [Files d’attente, rubriques et abonnements](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="576f5-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="576f5-178">Référence d’API pour [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="576f5-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="576f5-179">Visitez hello [Azure SDK pour Ruby](https://github.com/Azure/azure-sdk-for-ruby) référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="576f5-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
