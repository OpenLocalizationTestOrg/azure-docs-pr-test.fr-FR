---
title: "Utilisation des files d’attente Service Bus avec PHP | Microsoft Docs"
description: "Découvrez comment utiliser les files d'attente Service Bus dans Azure. Exemples de code écrits en PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="deea6-104">Utilisation des files d’attente Service Bus avec PHP</span><span class="sxs-lookup"><span data-stu-id="deea6-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="deea6-105">Ce guide vous montre comment utiliser les files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="deea6-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="deea6-106">Les exemples sont écrits en PHP et utilisent le [Kit de développement logiciel (SDK) Azure pour PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="deea6-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="deea6-107">Les scénarios couverts dans ce guide sont les suivants : **création de files d’attente**, **envoi et réception de messages** et **suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="deea6-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="deea6-108">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="deea6-108">Create a PHP application</span></span>
<span data-ttu-id="deea6-109">Le référencement de classes issues du [Kit de développement logiciel (SDK) Azure pour PHP](../php-download-sdk.md) dans votre code constitue la seule exigence pour créer une application PHP qui accède au service blob Azure.</span><span class="sxs-lookup"><span data-stu-id="deea6-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="deea6-110">Vous pouvez utiliser tous les outils de développement pour créer votre application, ou Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="deea6-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="deea6-111">L’[extension OpenSSL](http://php.net/openssl) doit également être installée et activée dans votre installation PHP.</span><span class="sxs-lookup"><span data-stu-id="deea6-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="deea6-112">Dans ce guide, vous allez utiliser les fonctionnalités du service qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="deea6-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="deea6-113">Obtention des bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="deea6-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="deea6-114">Configuration de votre application pour l’utilisation de Service Bus</span><span class="sxs-lookup"><span data-stu-id="deea6-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="deea6-115">Pour utiliser des API de file d'attente Service Bus, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="deea6-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="deea6-116">Référencez le fichier de chargeur automatique à l’aide de l’instruction [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="deea6-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="deea6-117">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="deea6-117">Reference any classes you might use.</span></span>

<span data-ttu-id="deea6-118">L’exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="deea6-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="deea6-119">Cet exemple et d'autres exemples de cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="deea6-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="deea6-120">Si vous avez installé les bibliothèques manuellement ou en tant que package PEAR, vous devez référencer le fichier de chargeur automatique **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="deea6-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="deea6-121">Dans les exemples ci-dessous, l'instruction `require_once` s'affichera toujours, mais seules les classes nécessaires aux besoins de l'exemple à exécuter sont référencées.</span><span class="sxs-lookup"><span data-stu-id="deea6-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="deea6-122">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="deea6-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="deea6-123">Pour instancier un client Service Bus, vous devez disposer au préalable d'une chaîne de connexion valide au format suivant :</span><span class="sxs-lookup"><span data-stu-id="deea6-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="deea6-124">où `Endpoint` est généralement au format `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="deea6-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="deea6-125">Pour créer un client de service Azure, vous devez utiliser la classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="deea6-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="deea6-126">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="deea6-126">You can:</span></span>

* <span data-ttu-id="deea6-127">Lui passer directement la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="deea6-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="deea6-128">utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="deea6-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="deea6-129">par défaut une source externe est prise en charge : variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="deea6-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="deea6-130">Vous pouvez ajouter de nouvelles sources en étendant la classe `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="deea6-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="deea6-131">Dans les exemples ci-dessous, la chaîne de connexion est passée directement.</span><span class="sxs-lookup"><span data-stu-id="deea6-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="deea6-132">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="deea6-132">Create a queue</span></span>
<span data-ttu-id="deea6-133">Vous pouvez effectuer des opérations de gestion pour les files d’attente Service Bus en utilisant la classe `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="deea6-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="deea6-134">Un objet `ServiceBusRestProxy` est construit via la méthode d’usine `ServicesBuilder::createServiceBusService` avec une chaîne de connexion appropriée qui encapsule les autorisations de jeton pour le gérer.</span><span class="sxs-lookup"><span data-stu-id="deea6-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="deea6-135">L’exemple suivant montre comment instancier un `ServiceBusRestProxy` et appeler `ServiceBusRestProxy->createQueue` pour créer une file d’attente nommée `myqueue` dans un espace de noms de service `MySBNamespace` :</span><span class="sxs-lookup"><span data-stu-id="deea6-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="deea6-136">vous pouvez utiliser la méthode `listQueues` sur les objets `ServiceBusRestProxy` pour vérifier s’il existe déjà une file d’attente d’un nom déterminé dans un espace de noms.</span><span class="sxs-lookup"><span data-stu-id="deea6-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="deea6-137">Envoi de messages à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="deea6-137">Send messages to a queue</span></span>
<span data-ttu-id="deea6-138">Pour envoyer un message à une file d’attente Service Bus, votre application appelle la méthode `ServiceBusRestProxy->sendQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="deea6-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="deea6-139">Le code suivant montre comment envoyer un message à la file d’attente `myqueue` créée plus haut dans l’espace de noms de service `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="deea6-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="deea6-140">Les messages envoyés aux files d’attente Service Bus (et reçus de celles-ci) sont des instances de la classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="deea6-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="deea6-141">Les objets [BrokeredMessage][BrokeredMessage] possèdent un ensemble de propriétés standard qui stockent des propriétés personnalisées propres à une application, ainsi qu’un corps de données d’application arbitraires.</span><span class="sxs-lookup"><span data-stu-id="deea6-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="deea6-142">Les files d’attente Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et d’1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="deea6-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="deea6-143">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="deea6-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="deea6-144">Si une file d'attente n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="deea6-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="deea6-145">La taille maximale de la file d'attente est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="deea6-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="deea6-146">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="deea6-146">Receive messages from a queue</span></span>

<span data-ttu-id="deea6-147">Le moyen le plus simple de recevoir les messages d’une file d’attente est d’utiliser une méthode `ServiceBusRestProxy->receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="deea6-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="deea6-148">Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) et [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="deea6-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="deea6-149">**PeekLock** est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="deea6-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="deea6-150">Lorsque le mode [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) est utilisé, la réception est une opération unique : quand Service Bus reçoit une demande de lecture d’un message figurant dans une file d’attente, il marque le message comme consommé et le renvoie à l’application.</span><span class="sxs-lookup"><span data-stu-id="deea6-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="deea6-151">Le mode [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application est capable de tolérer le non-traitement d’un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="deea6-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="deea6-152">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="deea6-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="deea6-153">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="deea6-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="deea6-154">En mode [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) par défaut), la réception d’un message devient une opération en deux étapes, ce qui permet de prendre en charge les applications qui ne tolèrent pas les messages manquants.</span><span class="sxs-lookup"><span data-stu-id="deea6-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="deea6-155">Lorsque Service Bus reçoit une demande, il recherche le message suivant à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="deea6-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="deea6-156">Dès que l’application a terminé de traiter le message (ou qu’elle l’a stocké de manière sûre en vue d’un traitement ultérieur), elle effectue la deuxième étape du processus de réception en transmettant le message reçu à `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="deea6-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="deea6-157">Lorsque Service Bus voit l’appel `deleteMessage`, il marque le message comme consommé et le supprime de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="deea6-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="deea6-158">L’exemple ci-dessous montre comment recevoir et traiter un message avec le mode [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (mode par défaut).</span><span class="sxs-lookup"><span data-stu-id="deea6-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="deea6-159">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="deea6-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="deea6-160">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="deea6-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="deea6-161">Si une application de réception ne parvient pas à traiter le message pour une raison quelconque, elle peut appeler la méthode `unlockMessage` sur le message reçu (au lieu de la méthode `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="deea6-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="deea6-162">Service Bus déverrouille alors le message dans la file d’attente et le rend à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="deea6-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="deea6-163">De même, il faut savoir qu'un message verrouillé dans une file d'attente est assorti d'un délai d'expiration et que si l'application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l'application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="deea6-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="deea6-164">Si l’application se bloque après le traitement du message mais avant l’émission de la demande `deleteMessage`, le message est à nouveau transmis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="deea6-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="deea6-165">Ce traitement est souvent appelé *Au moins une fois*. Chaque message est traité au moins une fois, mais dans certaines circonstances, un même message peut être transmis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="deea6-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="deea6-166">Si le scénario ne peut pas tolérer le traitement en double,l'ajout d'une logique supplémentaire à vos applications pour traiter la remise de messages en double est recommandé.</span><span class="sxs-lookup"><span data-stu-id="deea6-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="deea6-167">Ceci, grâce à la méthode `getMessageId` du message, qui reste constante entre les tentatives de transmission.</span><span class="sxs-lookup"><span data-stu-id="deea6-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="deea6-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="deea6-168">Next steps</span></span>
<span data-ttu-id="deea6-169">Maintenant que vous connaissez les principes de base des files d’attente Service Bus, consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="deea6-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="deea6-170">Pour plus d’informations, visitez aussi le [Centre pour développeurs PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="deea6-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


