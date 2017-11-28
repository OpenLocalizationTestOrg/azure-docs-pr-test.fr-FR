---
title: "les files d’attente d’aaaHow toouse Azure Service Bus avec Python | Documents Microsoft"
description: "Découvrez comment toouse Azure Service Bus de files d’attente à partir de Python."
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="5cf52-103">Comment toouse Service Bus de files d’attente avec Python</span><span class="sxs-lookup"><span data-stu-id="5cf52-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="5cf52-104">Cet article décrit comment les files d’attente de toouse Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5cf52-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="5cf52-105">exemples de Hello sont écrites dans Python et utiliser hello [package Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="5cf52-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="5cf52-106">Hello scénarios abordés incluent **création de files d’attente, envoyer et recevoir des messages**, et **la suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="5cf52-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="5cf52-107">tooinstall Python ou hello [package Python Azure Service Bus][Python Azure Service Bus package], consultez hello [Guide d’Installation de Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="5cf52-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="5cf52-108">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="5cf52-108">Create a queue</span></span>
<span data-ttu-id="5cf52-109">Hello **ServiceBusService** objet vous permet de toowork avec les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="5cf52-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="5cf52-110">Ajoutez hello suivant code haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès Service Bus :</span><span class="sxs-lookup"><span data-stu-id="5cf52-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="5cf52-111">Hello de code suivant crée un **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="5cf52-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="5cf52-112">Remplacez `mynamespace`, `sharedaccesskeyname` et `sharedaccesskey` par votre espace de noms, le nom et la valeur de clé de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="5cf52-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="5cf52-113">Hello valeurs pour le nom de la clé SAS hello et valeur sont accessibles dans hello [portail Azure] [ Azure portal] informations de connexion, ou dans Visual Studio de hello **propriétés** volet lors de la sélection Bonjour espace de noms Service Bus dans l’Explorateur de serveurs (comme indiqué dans la section précédente de hello).</span><span class="sxs-lookup"><span data-stu-id="5cf52-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="5cf52-114">Hello `create_queue` méthode prend également en charge des options supplémentaires, qui vous permettent de paramètres de file d’attente par défaut toooverride telles que message toolive TTL (time) ou taille maximale de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5cf52-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="5cf52-115">Hello exemple suivant définit hello file d’attente maximale taille too5 Go et à la minute de too1 de valeur de durée de vie hello :</span><span class="sxs-lookup"><span data-stu-id="5cf52-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="5cf52-116">Envoyer la file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="5cf52-116">Send messages tooa queue</span></span>
<span data-ttu-id="5cf52-117">toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `send_queue_message` méthode sur hello **ServiceBusService** objet.</span><span class="sxs-lookup"><span data-stu-id="5cf52-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="5cf52-118">Hello exemple suivant montre comment toosend une file d’attente toohello test nommé `taskqueue` à l’aide de `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="5cf52-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="5cf52-119">Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5cf52-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5cf52-120">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="5cf52-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5cf52-121">Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="5cf52-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="5cf52-122">Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="5cf52-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="5cf52-123">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="5cf52-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="5cf52-124">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="5cf52-124">Receive messages from a queue</span></span>
<span data-ttu-id="5cf52-125">Les messages sont reçus à partir d’une file d’attente à l’aide de hello `receive_queue_message` méthode sur hello **ServiceBusService** objet :</span><span class="sxs-lookup"><span data-stu-id="5cf52-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="5cf52-126">Les messages sont supprimés de la file d’attente hello lorsqu’elles sont lues lorsque hello paramètre `peek_lock` est défini trop**False**.</span><span class="sxs-lookup"><span data-stu-id="5cf52-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="5cf52-127">Vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre hello `peek_lock` trop**True**.</span><span class="sxs-lookup"><span data-stu-id="5cf52-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="5cf52-128">Hello le comportement de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="5cf52-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5cf52-129">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="5cf52-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5cf52-130">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="5cf52-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5cf52-131">Si hello `peek_lock` paramètre est défini trop**True**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="5cf52-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5cf52-132">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="5cf52-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5cf52-133">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant hello **supprimer** méthode sur hello **Message** objet.</span><span class="sxs-lookup"><span data-stu-id="5cf52-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="5cf52-134">Hello **supprimer** méthode marquer le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="5cf52-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5cf52-135">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="5cf52-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="5cf52-136">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="5cf52-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5cf52-137">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **déverrouiller** méthode sur hello **Message** objet.</span><span class="sxs-lookup"><span data-stu-id="5cf52-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="5cf52-138">Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="5cf52-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5cf52-139">Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello, et si l’échec de l’application hello tooprocess hello message avant hello délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="5cf52-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5cf52-140">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **supprimer** méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="5cf52-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5cf52-141">Cela est souvent appelé **au moins une fois le traitement**, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="5cf52-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5cf52-142">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="5cf52-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="5cf52-143">Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="5cf52-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cf52-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5cf52-144">Next steps</span></span>
<span data-ttu-id="5cf52-145">Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez ces articles de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="5cf52-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="5cf52-146">[Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="5cf52-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

