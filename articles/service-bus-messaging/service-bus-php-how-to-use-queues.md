---
title: "les files d’attente d’aaaHow toouse Service Bus avec PHP | Documents Microsoft"
description: "Découvrez comment toouse Service Bus de files d’attente dans Azure. Exemples de code écrits en PHP."
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="95b98-104">Comment toouse Service Bus de files d’attente avec PHP</span><span class="sxs-lookup"><span data-stu-id="95b98-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="95b98-105">Ce guide vous montre comment les files d’attente de toouse Service Bus.</span><span class="sxs-lookup"><span data-stu-id="95b98-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="95b98-106">exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="95b98-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="95b98-107">Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="95b98-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="95b98-108">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="95b98-108">Create a PHP application</span></span>
<span data-ttu-id="95b98-109">Hello uniquement requis pour la création d’une application PHP qui accède au service d’objets Blob Azure hello est hello faisant référence à des classes de hello [Azure SDK pour PHP](../php-download-sdk.md) à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="95b98-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="95b98-110">Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, ou le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="95b98-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="95b98-111">Votre installation PHP doit également avoir hello [OpenSSL extension](http://php.net/openssl) installé et activé.</span><span class="sxs-lookup"><span data-stu-id="95b98-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="95b98-112">Dans ce guide, vous allez utiliser les fonctionnalités du service qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="95b98-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="95b98-113">Obtenir les bibliothèques clientes Azure hello</span><span class="sxs-lookup"><span data-stu-id="95b98-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="95b98-114">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="95b98-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="95b98-115">file d’attente de Service Bus toouse hello API, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="95b98-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="95b98-116">Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require_once] instruction.</span><span class="sxs-lookup"><span data-stu-id="95b98-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="95b98-117">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="95b98-117">Reference any classes you might use.</span></span>

<span data-ttu-id="95b98-118">Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="95b98-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="95b98-119">Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur.</span><span class="sxs-lookup"><span data-stu-id="95b98-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="95b98-120">Si vous avez installé les bibliothèques hello manuellement ou en tant que package poire, vous devez référencer hello **WindowsAzure.php** fichier de chargeur automatique.</span><span class="sxs-lookup"><span data-stu-id="95b98-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="95b98-121">Dans les exemples de hello ci-dessous, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.</span><span class="sxs-lookup"><span data-stu-id="95b98-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="95b98-122">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="95b98-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="95b98-123">tooinstantiate un client Service Bus, vous devez avoir une chaîne de connexion valide au format suivant :</span><span class="sxs-lookup"><span data-stu-id="95b98-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="95b98-124">Où `Endpoint` est généralement hello format `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="95b98-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="95b98-125">toocreate n’importe quel client de service Azure que vous devez utiliser hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="95b98-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="95b98-126">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="95b98-126">You can:</span></span>

* <span data-ttu-id="95b98-127">Passer hello connexion chaîne directement tooit.</span><span class="sxs-lookup"><span data-stu-id="95b98-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="95b98-128">Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="95b98-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="95b98-129">par défaut une source externe est prise en charge : variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="95b98-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="95b98-130">Vous pouvez ajouter de nouvelles sources en étendant hello `ConnectionStringSource` classe</span><span class="sxs-lookup"><span data-stu-id="95b98-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="95b98-131">Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello est passé directement.</span><span class="sxs-lookup"><span data-stu-id="95b98-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="95b98-132">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="95b98-132">Create a queue</span></span>
<span data-ttu-id="95b98-133">Vous pouvez effectuer les opérations de gestion des files d’attente Service Bus via hello `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="95b98-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="95b98-134">A `ServiceBusRestProxy` objet est construit via hello `ServicesBuilder::createServiceBusService` méthode de fabrique avec une chaîne de connexion appropriée qui encapsule hello autorisations jeton toomanage il.</span><span class="sxs-lookup"><span data-stu-id="95b98-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="95b98-135">Hello suivant montre l’exemple de comment tooinstantiate un `ServiceBusRestProxy` et appelez `ServiceBusRestProxy->createQueue` toocreate une file d’attente nommée `myqueue` dans un `MySBNamespace` espace de noms de service :</span><span class="sxs-lookup"><span data-stu-id="95b98-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="95b98-136">Vous pouvez utiliser hello `listQueues` méthode sur `ServiceBusRestProxy` objets toocheck si une file d’attente portant le nom spécifié existe déjà dans un espace de noms.</span><span class="sxs-lookup"><span data-stu-id="95b98-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="95b98-137">Envoyer la file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="95b98-137">Send messages tooa queue</span></span>
<span data-ttu-id="95b98-138">toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `ServiceBusRestProxy->sendQueueMessage` (méthode).</span><span class="sxs-lookup"><span data-stu-id="95b98-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="95b98-139">Hello suivant de code montre comment toosend un toohello message `myqueue` file d’attente créée précédemment dans le `MySBNamespace` espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="95b98-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="95b98-140">Messages trop envoyées (et reçues à partir de) les files d’attente Service Bus sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="95b98-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="95b98-141">[BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de méthodes et propriétés qui sont utilisées toohold des propriétés personnalisées spécifiques à l’application et un corps de données d’application arbitraire standard.</span><span class="sxs-lookup"><span data-stu-id="95b98-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="95b98-142">Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="95b98-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="95b98-143">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="95b98-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="95b98-144">Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="95b98-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="95b98-145">La taille maximale de la file d'attente est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="95b98-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="95b98-146">Réception des messages d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="95b98-146">Receive messages from a queue</span></span>

<span data-ttu-id="95b98-147">messages Hello meilleure manière tooreceive à partir d’une file d’attente est toouse un `ServiceBusRestProxy->receiveQueueMessage` (méthode).</span><span class="sxs-lookup"><span data-stu-id="95b98-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="95b98-148">Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) et [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="95b98-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="95b98-149">**PeekLock** est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="95b98-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="95b98-150">Lorsque vous utilisez [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , le mode de réception est une opération de prise de vue unique ; autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans une file d’attente, il marque le message de type hello comme ayant été consommé et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="95b98-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="95b98-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="95b98-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="95b98-152">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="95b98-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="95b98-153">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="95b98-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="95b98-154">Dans la valeur par défaut hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, la réception d’un message devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="95b98-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="95b98-155">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe est utilisé, il verrouille tooprevent autres consommateurs de le recevoir, puis retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="95b98-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="95b98-156">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en passant le message de salutation reçu trop`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="95b98-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="95b98-157">Lorsque le Service Bus voit hello `deleteMessage` appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="95b98-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="95b98-158">Hello suivant montre l’exemple de comment tooreceive et traiter un message à l’aide de [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (mode par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="95b98-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="95b98-159">Comment toohandle application tombe en panne et messages illisibles</span><span class="sxs-lookup"><span data-stu-id="95b98-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="95b98-160">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="95b98-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="95b98-161">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le message de salutation reçu (au lieu de hello `deleteMessage` méthode).</span><span class="sxs-lookup"><span data-stu-id="95b98-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="95b98-162">Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="95b98-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="95b98-163">Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="95b98-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="95b98-164">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="95b98-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="95b98-165">Cela est souvent appelé *au moins une fois* traitement ; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="95b98-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="95b98-166">Si le scénario de hello ne tolère pas le traitement dupliqué, puis ajouter des remise de messages en double logique tooapplications toohandle est recommandé.</span><span class="sxs-lookup"><span data-stu-id="95b98-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="95b98-167">Cela est souvent obtenue à l’aide de hello `getMessageId` méthode de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="95b98-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95b98-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95b98-168">Next steps</span></span>
<span data-ttu-id="95b98-169">Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="95b98-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="95b98-170">Pour plus d’informations, reportez-vous également au hello [centre de développement PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="95b98-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


