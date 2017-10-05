---
title: "Utilisation des files d’attente Azure Service Bus avec Python | Microsoft Docs"
description: "Découvrez comment utiliser les files d'attente Service Bus Azure depuis Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="dcd59-103">Utilisation des files d’attente Service Bus avec Python</span><span class="sxs-lookup"><span data-stu-id="dcd59-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="dcd59-104">Cet article décrit l’utilisation des files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dcd59-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="dcd59-105">Les exemples sont écrits en Python et utilisent le [package Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="dcd59-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="dcd59-106">Les scénarios couverts dans ce guide sont les suivants : **création de files d’attente, envoi et réception de messages** et **suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="dcd59-107">Pour installer Python ou le [package Python Azure Service Bus][Python Azure Service Bus package], consultez le [Python Installation Guide (Guide d’installation de Python)](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="dcd59-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="dcd59-108">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="dcd59-108">Create a queue</span></span>
<span data-ttu-id="dcd59-109">L’objet **ServiceBusService** permet d’utiliser des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="dcd59-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="dcd59-110">Ajoutez le code suivant au début de chaque fichier Python dans lequel vous souhaitez accéder à Service Bus par programme :</span><span class="sxs-lookup"><span data-stu-id="dcd59-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="dcd59-111">Le code suivant crée un objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="dcd59-112">Remplacez `mynamespace`, `sharedaccesskeyname` et `sharedaccesskey` par votre espace de noms, le nom et la valeur de clé de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="dcd59-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="dcd59-113">Le nom et la valeur de la clé de signature d’accès partagé se trouvent dans les informations de connexion du [portail Azure][Azure portal] ou dans le volet **Propriétés** de Visual Studio quand vous sélectionnez l’espace de noms Service Bus dans l’Explorateur de serveurs (comme indiqué dans la section précédente).</span><span class="sxs-lookup"><span data-stu-id="dcd59-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="dcd59-114">La méthode `create_queue` prend également en charge des options supplémentaires, qui vous permettent de remplacer les paramètres de file d’attente par défaut comme la durée de vie (TTL) du message ou la taille maximale de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="dcd59-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="dcd59-115">L’exemple suivant définit la taille maximale de la file d’attente sur 5 Go et la durée de vie de message sur 1 minute :</span><span class="sxs-lookup"><span data-stu-id="dcd59-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="dcd59-116">Envoi de messages à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="dcd59-116">Send messages to a queue</span></span>
<span data-ttu-id="dcd59-117">Pour envoyer un message à une file d’attente Service Bus, votre application appelle la méthode `send_queue_message` sur l’objet **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="dcd59-118">L’exemple suivant indique comment envoyer un message test à la file d’attente nommée `taskqueue` au moyen de la méthode `send_queue_message` :</span><span class="sxs-lookup"><span data-stu-id="dcd59-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="dcd59-119">Les files d’attente Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et d’1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="dcd59-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="dcd59-120">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="dcd59-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="dcd59-121">Si une file d'attente n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="dcd59-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="dcd59-122">Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="dcd59-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="dcd59-123">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="dcd59-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="dcd59-124">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="dcd59-124">Receive messages from a queue</span></span>
<span data-ttu-id="dcd59-125">La méthode `receive_queue_message` de l’objet **ServiceBusService** permet de recevoir les messages d’une file d’attente :</span><span class="sxs-lookup"><span data-stu-id="dcd59-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="dcd59-126">Les messages sont supprimés de la file d’attente au fur et à mesure de leur lecture, si le paramètre `peek_lock` est défini sur **False**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="dcd59-127">Vous pouvez lire (afficher un aperçu) et verrouiller le message sans le supprimer de la file d’attente en définissant le paramètre `peek_lock` sur **True**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="dcd59-128">Le comportement de lecture et de suppression du message dans le cadre de l'opération de réception est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application est capable de tolérer le non-traitement d'un message en cas d'échec.</span><span class="sxs-lookup"><span data-stu-id="dcd59-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="dcd59-129">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="dcd59-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="dcd59-130">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="dcd59-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="dcd59-131">Si le paramètre `peek_lock` est défini sur **True**, la réception devient une opération en deux étapes, qui autorise une prise en charge des applications qui ne peuvent pas tolérer de messages manquants.</span><span class="sxs-lookup"><span data-stu-id="dcd59-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="dcd59-132">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="dcd59-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="dcd59-133">Dès lors que l’application a terminé le traitement du message (ou qu’elle l’a stocké de manière fiable pour un traitement ultérieur), elle accomplit la deuxième étape du processus de réception en appelant la méthode **delete** sur l’objet **Message**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="dcd59-134">La méthode **delete** marque le message comme étant consommé et le supprime de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="dcd59-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="dcd59-135">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="dcd59-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="dcd59-136">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="dcd59-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="dcd59-137">Si une application réceptrice ne parvient pas à traiter le message pour une raison quelconque, elle appelle la méthode **unlock** pour l’objet **Message**.</span><span class="sxs-lookup"><span data-stu-id="dcd59-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="dcd59-138">Service Bus déverrouille alors le message dans la file d’attente et le rend à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="dcd59-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="dcd59-139">De même, il faut savoir qu’un message verrouillé dans une file d’attente est assorti d’un délai d’expiration et que si l’application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l’application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="dcd59-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="dcd59-140">Si l’application subit un incident après le traitement du message, mais avant l’appel de la méthode **delete**, le message est à nouveau remis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="dcd59-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="dcd59-141">Lors de cette opération souvent appelée **Au moins une fois**, chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="dcd59-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="dcd59-142">Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="dcd59-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="dcd59-143">Pour ce faire, il suffit souvent d’utiliser la propriété **MessageId** du message, qui reste constante pendant les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="dcd59-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcd59-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcd59-144">Next steps</span></span>
<span data-ttu-id="dcd59-145">Maintenant que vous avez appris les principes de base des files d'attente Service Bus, consultez ces liens pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="dcd59-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="dcd59-146">[Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="dcd59-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

