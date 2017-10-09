---
title: "les files d’attente d’aaaHow toouse Azure Service Bus avec Java | Documents Microsoft"
description: "Découvrez comment toouse Service Bus de files d’attente dans Azure. Exemples de code écrits en Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="bffd3-104">Comment toouse Service Bus de files d’attente avec Java</span><span class="sxs-lookup"><span data-stu-id="bffd3-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="bffd3-105">Cet article décrit comment les files d’attente de toouse Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bffd3-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="bffd3-106">exemples de Hello sont écrits en Java et utiliser hello [SDK Azure pour Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="bffd3-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="bffd3-107">Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="bffd3-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="bffd3-108">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="bffd3-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="bffd3-109">Vérifiez que vous avez installé hello [SDK Azure pour Java] [ Azure SDK for Java] avant de générer cet exemple.</span><span class="sxs-lookup"><span data-stu-id="bffd3-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="bffd3-110">Si vous utilisez Eclipse, vous pouvez installer hello [boîte à outils Azure pour Eclipse] [ Azure Toolkit for Eclipse] incluant hello SDK Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="bffd3-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="bffd3-111">Vous pouvez ensuite ajouter hello **bibliothèques Microsoft Azure pour Java** tooyour projet :</span><span class="sxs-lookup"><span data-stu-id="bffd3-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="bffd3-112">Ajoutez hello suit `import` haut de toohello instructions hello du fichier de Java :</span><span class="sxs-lookup"><span data-stu-id="bffd3-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="bffd3-113">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="bffd3-113">Create a queue</span></span>
<span data-ttu-id="bffd3-114">Vous pouvez effectuer des opérations de gestion pour les files d’attente Service Bus via la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="bffd3-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="bffd3-115">A **ServiceBusContract** objet est construit avec une configuration appropriée qui encapsule le jeton SAS avec les autorisations toomanage et hello **ServiceBusContract** classe est point unique de hello de la communication avec Azure.</span><span class="sxs-lookup"><span data-stu-id="bffd3-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="bffd3-116">Hello **ServiceBusService** classe fournit des méthodes toocreate, énumérer et supprimer des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="bffd3-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="bffd3-117">Hello exemple ci-dessous montre comment un **ServiceBusService** objet peut être utilisé toocreate une file d’attente nommée `TestQueue`, avec un espace de noms `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="bffd3-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="bffd3-118">Il existe des méthodes sur `QueueInfo` qui autorisent des propriétés de toobe de file d’attente hello paramétrés (par exemple : tooset hello par défaut time-to-live (TTL) valeur toobe appliqué toomessages envoyé la file d’attente toohello).</span><span class="sxs-lookup"><span data-stu-id="bffd3-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="bffd3-119">Hello suivant montre comment toocreate une file d’attente nommée `TestQueue` avec une taille maximale de 5 Go :</span><span class="sxs-lookup"><span data-stu-id="bffd3-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="bffd3-120">Notez que vous pouvez utiliser hello `listQueues` méthode sur **ServiceBusContract** objets toocheck si une file d’attente portant le nom spécifié existe déjà dans un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="bffd3-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="bffd3-121">Envoyer la file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="bffd3-121">Send messages tooa queue</span></span>
<span data-ttu-id="bffd3-122">toosend une file d’attente Service Bus de messages tooa, votre application obtient un **ServiceBusContract** objet.</span><span class="sxs-lookup"><span data-stu-id="bffd3-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="bffd3-123">Hello suivant de code montre comment toosend un message pour hello `TestQueue` file d’attente créée précédemment Bonjour `HowToSample` espace de noms :</span><span class="sxs-lookup"><span data-stu-id="bffd3-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="bffd3-124">Les messages envoyés à et provenant du Service Bus files d’attente sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="bffd3-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="bffd3-125">[BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de propriétés standard (tels que [étiquette](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) et [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dictionnaire qui est utilisé toohold personnalisé les propriétés spécifiques à l’application et un corps de données d’application arbitraire.</span><span class="sxs-lookup"><span data-stu-id="bffd3-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="bffd3-126">Une application peut définir le corps de hello du message de type hello en passant tout objet sérialisable dans le constructeur hello Hello [BrokeredMessage][BrokeredMessage], et le sérialiseur approprié de hello sera ensuite utilisée objet de hello tooserialize.</span><span class="sxs-lookup"><span data-stu-id="bffd3-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="bffd3-127">Vous pouvez également fournir un objet **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="bffd3-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="bffd3-128">Hello exemple suivant montre comment les messages de test de toosend cinq toothe `TestQueue` **MessageSender** nous avons obtenu dans l’extrait de code précédent hello :</span><span class="sxs-lookup"><span data-stu-id="bffd3-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="bffd3-129">Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="bffd3-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="bffd3-130">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="bffd3-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="bffd3-131">Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="bffd3-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="bffd3-132">Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="bffd3-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="bffd3-133">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="bffd3-133">Receive messages from a queue</span></span>
<span data-ttu-id="bffd3-134">messages de tooreceive Hello moyen principal à partir d’une file d’attente est toouse un **ServiceBusContract** objet.</span><span class="sxs-lookup"><span data-stu-id="bffd3-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="bffd3-135">Ces messages reçus peuvent fonctionner dans deux modes différents : **ReceiveAndDelete** et **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="bffd3-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="bffd3-136">Lors de l’utilisation de hello **ReceiveAndDelete** , le mode de réception est une opération coup - autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans une file d’attente, il marque le message de type hello comme ayant été consommé et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="bffd3-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="bffd3-137">**ReceiveAndDelete** mode (mode par défaut de hello) est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="bffd3-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="bffd3-138">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="bffd3-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="bffd3-139">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="bffd3-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="bffd3-140">Dans **PeekLock** , le mode de réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="bffd3-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="bffd3-141">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="bffd3-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="bffd3-142">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant **supprimer** sur le message de salutation reçu.</span><span class="sxs-lookup"><span data-stu-id="bffd3-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="bffd3-143">Lorsque le Service Bus voit hello **supprimer** appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="bffd3-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="bffd3-144">Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de **PeekLock** mode (pas le mode hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="bffd3-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="bffd3-145">Hello exemple ci-dessous effectue une boucle infinie et traite les messages lorsqu’ils arrivent dans notre `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="bffd3-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="bffd3-146">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="bffd3-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="bffd3-147">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="bffd3-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="bffd3-148">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello **unlockMessage** méthode sur le message de salutation reçu (au lieu de hello **deleteMessage** méthode).</span><span class="sxs-lookup"><span data-stu-id="bffd3-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="bffd3-149">Cela entraîne hello toounlock de Service Bus de messages dans la file d’attente hello et le rendre disponible toobe reçu, soit par Bonjour même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="bffd3-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="bffd3-150">Il existe également un délai d’attente d’un message verrouillé dans la file d’attente, et si application hello échoue tooprocess hello message avant l’expiration du délai d’attente de verrou (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille le message de type hello automatiquement et rend disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="bffd3-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="bffd3-151">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello **deleteMessage** demande est émise, puis le message de type hello est redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="bffd3-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="bffd3-152">Cela est souvent appelé *au moins une fois le traitement*; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="bffd3-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="bffd3-153">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message.</span><span class="sxs-lookup"><span data-stu-id="bffd3-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="bffd3-154">Cela est souvent obtenue à l’aide de hello **getMessageId** méthode de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="bffd3-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bffd3-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bffd3-155">Next Steps</span></span>
<span data-ttu-id="bffd3-156">Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="bffd3-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="bffd3-157">Pour plus d’informations, consultez hello [centre de développement Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="bffd3-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
