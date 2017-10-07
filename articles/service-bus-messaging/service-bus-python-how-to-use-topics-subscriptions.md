---
title: rubriques de Azure Service Bus aaaHow toouse avec Python | Documents Microsoft
description: "Découvrez comment toouse Azure Service Bus rubriques et abonnements à partir de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="6749c-103">Comment toouse Service Bus rubriques et les abonnements avec Python</span><span class="sxs-lookup"><span data-stu-id="6749c-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="6749c-104">Cet article décrit comment toouse Service Bus rubriques et abonnements.</span><span class="sxs-lookup"><span data-stu-id="6749c-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="6749c-105">exemples de Hello sont écrites dans Python et utiliser hello [package SDK de Python Azure][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="6749c-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="6749c-106">Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.</span><span class="sxs-lookup"><span data-stu-id="6749c-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="6749c-107">Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="6749c-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="6749c-108">Si vous avez besoin tooinstall Python ou hello [package Azure Python][Azure Python package], consultez hello [Guide d’Installation de Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="6749c-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="6749c-109">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="6749c-109">Create a topic</span></span>
<span data-ttu-id="6749c-110">Hello **ServiceBusService** objet vous permet de toowork aux rubriques.</span><span class="sxs-lookup"><span data-stu-id="6749c-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="6749c-111">Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Service Bus :</span><span class="sxs-lookup"><span data-stu-id="6749c-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="6749c-112">Hello de code suivant crée un **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="6749c-113">Remplacez `mynamespace`, `sharedaccesskeyname` et `sharedaccesskey` par un espace de noms, un nom et une valeur de clé de signature d’accès partagé (SAP) réels.</span><span class="sxs-lookup"><span data-stu-id="6749c-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="6749c-114">Vous pouvez obtenir les valeurs hello pour le nom de la clé SAS hello et la valeur à partir de hello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6749c-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="6749c-115">Hello `create_topic` méthode prend également en charge des options supplémentaires, qui permettent de paramètres de rubrique toooverride par défaut comme taille de rubrique toolive ou maximale de temps de message.</span><span class="sxs-lookup"><span data-stu-id="6749c-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="6749c-116">Hello exemple suivant définit hello rubrique maximale taille too5 Go et heure toolive (TTL) de 1 minute :</span><span class="sxs-lookup"><span data-stu-id="6749c-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="6749c-117">Création d’abonnements</span><span class="sxs-lookup"><span data-stu-id="6749c-117">Create subscriptions</span></span>
<span data-ttu-id="6749c-118">Abonnements tootopics sont également créés par hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="6749c-119">Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="6749c-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="6749c-120">Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique toowhich êtes abonné, elles sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="6749c-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="6749c-121">Créer un abonnement avec le filtre par défaut (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="6749c-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="6749c-122">Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="6749c-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="6749c-123">Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="6749c-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="6749c-124">Hello exemple suivant crée un abonnement nommé `AllMessages` et utilise hello par défaut **MatchAll** filtre.</span><span class="sxs-lookup"><span data-stu-id="6749c-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="6749c-125">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="6749c-125">Create subscriptions with filters</span></span>
<span data-ttu-id="6749c-126">Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="6749c-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="6749c-127">Bonjour type de filtre pris en charge par les abonnements plus souple est un **SqlFilter**, qui implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="6749c-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="6749c-128">Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="6749c-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="6749c-129">Pour plus d’informations sur les expressions hello qui peut être utilisé avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.</span><span class="sxs-lookup"><span data-stu-id="6749c-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="6749c-130">Vous pouvez ajouter des filtres tooa abonnement à l’aide de hello **créer\_règle** méthode Hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="6749c-131">Cette méthode vous permet d’abonnement existant tooadd nouveaux filtres tooan.</span><span class="sxs-lookup"><span data-stu-id="6749c-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6749c-132">Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez d’abord supprimer filtre par défaut de hello ou hello **MatchAll** remplace tous les autres filtres que vous pouvez spécifier.</span><span class="sxs-lookup"><span data-stu-id="6749c-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="6749c-133">Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `delete_rule` méthode Hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="6749c-134">Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `messagenumber` propriété supérieure à 3 :</span><span class="sxs-lookup"><span data-stu-id="6749c-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="6749c-135">De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont un `messagenumber` propriété inférieur ou égal too3 :</span><span class="sxs-lookup"><span data-stu-id="6749c-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="6749c-136">Désormais, lorsqu’un message est envoyé trop`mytopic` qu’il est toujours remis tooreceivers abonné toohello **AllMessages** abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello **HighMessages**  et **LowMessages** abonnements à la rubrique (selon le contenu du message hello).</span><span class="sxs-lookup"><span data-stu-id="6749c-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="6749c-137">Rubrique tooa de messages d’envoi</span><span class="sxs-lookup"><span data-stu-id="6749c-137">Send messages tooa topic</span></span>
<span data-ttu-id="6749c-138">toosend une rubrique de Service Bus message tooa, votre application doit utiliser hello `send_topic_message` méthode Hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="6749c-139">Hello exemple suivant montre comment le test de toosend cinq messages trop`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="6749c-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="6749c-140">Notez que hello `messagenumber` varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (détermine les abonnements reçoivent) :</span><span class="sxs-lookup"><span data-stu-id="6749c-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="6749c-141">Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6749c-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="6749c-142">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="6749c-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="6749c-143">Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="6749c-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="6749c-144">Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="6749c-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="6749c-145">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="6749c-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="6749c-146">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="6749c-146">Receive messages from a subscription</span></span>
<span data-ttu-id="6749c-147">Les messages sont reçus à partir d’un abonnement à l’aide de hello `receive_subscription_message` méthode sur hello **ServiceBusService** objet :</span><span class="sxs-lookup"><span data-stu-id="6749c-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="6749c-148">Les messages sont supprimés de l’abonnement de hello lorsqu’elles sont lues lorsque hello paramètre `peek_lock` est défini trop**False**.</span><span class="sxs-lookup"><span data-stu-id="6749c-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="6749c-149">Vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre hello `peek_lock` trop**True**.</span><span class="sxs-lookup"><span data-stu-id="6749c-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="6749c-150">Hello le comportement de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="6749c-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="6749c-151">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="6749c-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="6749c-152">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="6749c-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="6749c-153">Si hello `peek_lock` paramètre est défini trop**True**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="6749c-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="6749c-154">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="6749c-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="6749c-155">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `delete` méthode sur hello **Message** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="6749c-156">Hello `delete` méthode marque le message de type hello comme ayant été consommé et le supprime de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="6749c-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="6749c-157">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="6749c-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="6749c-158">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="6749c-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="6749c-159">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlock` méthode sur hello **Message** objet.</span><span class="sxs-lookup"><span data-stu-id="6749c-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="6749c-160">Cette opération provoquent le message de type hello toounlock Service Bus au sein de l’abonnement de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="6749c-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="6749c-161">Il existe également un délai d’attente d’un message verrouillé au sein de l’abonnement de hello, et si l’application hello échoue le message de type hello tooprocess avant de délai d’attente de verrou hello expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille le message de type hello automatiquement et le rend disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="6749c-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="6749c-162">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `delete` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="6749c-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="6749c-163">Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="6749c-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="6749c-164">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="6749c-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="6749c-165">Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="6749c-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="6749c-166">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="6749c-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="6749c-167">Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme.</span><span class="sxs-lookup"><span data-stu-id="6749c-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="6749c-168">Hello suivant montre comment la rubrique de hello toodelete nommé `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="6749c-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="6749c-169">Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="6749c-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="6749c-170">Les abonnements peuvent aussi être supprimés de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="6749c-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="6749c-171">Hello de code suivant montre comment toodelete un abonnement nommé `HighMessages` de hello `mytopic` rubrique :</span><span class="sxs-lookup"><span data-stu-id="6749c-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="6749c-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6749c-172">Next steps</span></span>
<span data-ttu-id="6749c-173">Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="6749c-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="6749c-174">Consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="6749c-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="6749c-175">Référence pour [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="6749c-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
