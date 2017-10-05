---
title: Utilisation des rubriques Service Bus avec PHP | Microsoft Docs
description: "Découvrez comment utiliser les rubriques Service Bus avec PHP dans Azure."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="62ce8-103">Utilisation des rubriques et abonnements Service Bus avec PHP</span><span class="sxs-lookup"><span data-stu-id="62ce8-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="62ce8-104">Cet article vous montre comment utiliser les rubriques et les abonnements Service Bus.</span><span class="sxs-lookup"><span data-stu-id="62ce8-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="62ce8-105">Les exemples sont écrits en PHP et utilisent le [Kit de développement logiciel (SDK) Azure pour PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="62ce8-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="62ce8-106">Les scénarios couverts incluent la **création de rubriques et d’abonnements**, la **création de filtres d’abonnement**, **l’envoi de messages à une rubrique**, la **réception de messages en provenance d’un abonnement** et enfin la **suppression de rubriques et d’abonnements**.</span><span class="sxs-lookup"><span data-stu-id="62ce8-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="62ce8-107">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="62ce8-107">Create a PHP application</span></span>
<span data-ttu-id="62ce8-108">Le référencement de classes issues du [Kit de développement logiciel (SDK) Azure pour PHP](../php-download-sdk.md) dans votre code constitue la seule exigence pour créer une application PHP qui accède au service blob Azure.</span><span class="sxs-lookup"><span data-stu-id="62ce8-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="62ce8-109">Vous pouvez utiliser tous les outils de développement pour créer votre application, ou Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="62ce8-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="62ce8-110">[L’extension OpenSSL](http://php.net/openssl) doit également être installée et activée dans votre installation PHP.</span><span class="sxs-lookup"><span data-stu-id="62ce8-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="62ce8-111">Cet article décrit comment utiliser des fonctionnalités de service qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="62ce8-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="62ce8-112">Obtention des bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="62ce8-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="62ce8-113">Configuration de votre application pour l’utilisation de Service Bus</span><span class="sxs-lookup"><span data-stu-id="62ce8-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="62ce8-114">Utilisation des API Service Bus :</span><span class="sxs-lookup"><span data-stu-id="62ce8-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="62ce8-115">Référencez le fichier de chargeur automatique à l’aide de l’instruction [require_once][require-once].</span><span class="sxs-lookup"><span data-stu-id="62ce8-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="62ce8-116">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="62ce8-116">Reference any classes you might use.</span></span>

<span data-ttu-id="62ce8-117">L’exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="62ce8-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="62ce8-118">Cet exemple et d'autres exemples de cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="62ce8-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="62ce8-119">Si vous avez installé les bibliothèques manuellement ou en tant que package PEAR, vous devez référencer le fichier de chargeur automatique **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="62ce8-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="62ce8-120">Dans les exemples suivants, l'instruction `require_once` s'affichera toujours, mais seules les classes nécessaires aux besoins de l'exemple à exécuter sont référencées.</span><span class="sxs-lookup"><span data-stu-id="62ce8-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="62ce8-121">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="62ce8-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="62ce8-122">Pour instancier un client Service Bus, vous devez disposer au préalable d'une chaîne de connexion valide au format suivant :</span><span class="sxs-lookup"><span data-stu-id="62ce8-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="62ce8-123">où `Endpoint` est généralement au format `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="62ce8-124">Pour créer un client de service Azure, vous devez utiliser la classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="62ce8-125">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="62ce8-125">You can:</span></span>

* <span data-ttu-id="62ce8-126">Lui passer directement la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="62ce8-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="62ce8-127">utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="62ce8-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="62ce8-128">par défaut une source externe est prise en charge : variables d'environnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="62ce8-129">Vous pouvez ajouter de nouvelles sources en étendant la classe `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="62ce8-130">Dans les exemples ci-dessous, la chaîne de connexion est passée directement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="62ce8-131">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="62ce8-131">Create a topic</span></span>
<span data-ttu-id="62ce8-132">Vous pouvez effectuer des opérations de gestion pour les rubriques Service Bus avec la classe `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="62ce8-133">Un objet `ServiceBusRestProxy` est construit par la méthode d’usine `ServicesBuilder::createServiceBusService` avec une chaîne de connexion appropriée qui encapsule les autorisations de jeton pour le gérer.</span><span class="sxs-lookup"><span data-stu-id="62ce8-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="62ce8-134">L’exemple suivant montre comment instancier un `ServiceBusRestProxy` et appeler `ServiceBusRestProxy->createTopic` pour créer une rubrique nommée `mytopic` dans un espace de noms `MySBNamespace` :</span><span class="sxs-lookup"><span data-stu-id="62ce8-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> <span data-ttu-id="62ce8-135">vous pouvez utiliser la méthode `listTopics` sur les objets `ServiceBusRestProxy` pour vérifier s’il existe déjà une rubrique d’un nom déterminé dans un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="62ce8-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="62ce8-136">Création d'un abonnement</span><span class="sxs-lookup"><span data-stu-id="62ce8-136">Create a subscription</span></span>
<span data-ttu-id="62ce8-137">La méthode `ServiceBusRestProxy->createSubscription` permet également de créer des abonnements à une rubrique.</span><span class="sxs-lookup"><span data-stu-id="62ce8-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="62ce8-138">Les abonnements sont nommés et peuvent être assortis d'un filtre facultatif qui limite l'ensemble des messages transmis à la file d'attente virtuelle de l'abonnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="62ce8-139">Création d’un abonnement avec le filtre par défaut (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="62ce8-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="62ce8-140">Le filtre **MatchAll** est le filtre utilisé par défaut si aucun filtre n’est spécifié lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="62ce8-141">Lorsque le filtre **MatchAll** est utilisé, tous les messages publiés dans la rubrique sont placés dans la file d’attente virtuelle de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="62ce8-142">Dans l’exemple suivant, l’abonnement « mysubscription » qui est créé utilise le filtre par défaut **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="62ce8-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="62ce8-143">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="62ce8-143">Create subscriptions with filters</span></span>
<span data-ttu-id="62ce8-144">Vous pouvez également configurer des filtres pour spécifier quels sont les messages, parmi ceux envoyés à une rubrique, qui doivent apparaître dans un abonnement de rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="62ce8-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="62ce8-145">Parmi les types de filtre pris en charge par les abonnements, [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) est le plus flexible. Il implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="62ce8-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="62ce8-146">Les filtres SQL opèrent au niveau des propriétés des messages publiés dans la rubrique.</span><span class="sxs-lookup"><span data-stu-id="62ce8-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="62ce8-147">Pour plus d'informations sur les filtres SQL, consultez la page [Propriété SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="62ce8-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="62ce8-148">Chaque règle d’un abonnement traite les messages entrants de façon indépendante, ajoutant leurs messages de résultat à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="62ce8-149">En outre, chaque nouvel abonnement dispose d’un objet **Rule** par défaut avec un filtre qui ajoute tous les messages de la rubrique à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="62ce8-150">Pour recevoir uniquement les messages correspondant à votre filtre, vous devez supprimer la règle par défaut.</span><span class="sxs-lookup"><span data-stu-id="62ce8-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="62ce8-151">Vous pouvez supprimer la règle par défaut à l'aide de la méthode `ServiceBusRestProxy->deleteRule`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="62ce8-152">L’exemple suivant crée l’abonnement `HighMessages` avec un objet **SqlFilter** qui ne sélectionne que les messages dont la propriété personnalisée `MessageNumber` a une valeur supérieure à 3.</span><span class="sxs-lookup"><span data-stu-id="62ce8-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="62ce8-153">Pour plus d’informations sur l’ajout de propriétés personnalisées à des messages, consultez [Envoyer des messages à une rubrique](#send-messages-to-a-topic).</span><span class="sxs-lookup"><span data-stu-id="62ce8-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="62ce8-154">Notez que ce code requiert l'utilisation d'un espace de noms supplémentaire : `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="62ce8-155">De même, l’exemple suivant crée l’abonnement `LowMessages` avec un objet `SqlFilter` qui ne sélectionne que les messages dont la propriété `MessageNumber` a une valeur inférieure ou égale à 3.</span><span class="sxs-lookup"><span data-stu-id="62ce8-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="62ce8-156">À présent, dès lors qu’un message est envoyé vers la rubrique `mytopic`, il est toujours remis aux destinataires abonnés à l’abonnement `mysubscription` et est remis de manière sélective aux destinataires abonnés aux abonnements `HighMessages` et `LowMessages` (en fonction du contenu du message).</span><span class="sxs-lookup"><span data-stu-id="62ce8-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="62ce8-157">Envoi de messages à une rubrique</span><span class="sxs-lookup"><span data-stu-id="62ce8-157">Send messages to a topic</span></span>
<span data-ttu-id="62ce8-158">Pour envoyer un message à une rubrique Service Bus, votre application appelle la méthode `ServiceBusRestProxy->sendTopicMessage`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="62ce8-159">Le code suivant montre comment envoyer un message à la rubrique `mytopic` créée plus haut dans l’espace de noms de service `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

<span data-ttu-id="62ce8-160">Les messages envoyés aux rubriques Service Bus sont des instances de la classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="62ce8-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="62ce8-161">Les objets [BrokeredMessage][BrokeredMessage] possèdent un ensemble de propriétés et de méthodes standard, ainsi que des propriétés permettant de conserver les propriétés personnalisées propres à une application.</span><span class="sxs-lookup"><span data-stu-id="62ce8-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="62ce8-162">L’exemple suivant montre comment envoyer 5 messages test à la rubrique `mytopic` créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="62ce8-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="62ce8-163">La méthode `setProperty` sert à ajouter une propriété personnalisée (`MessageNumber`) à chaque message.</span><span class="sxs-lookup"><span data-stu-id="62ce8-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="62ce8-164">Notez que la valeur de la propriété `MessageNumber` varie pour chaque message (cela peut être utilisé pour déterminer les abonnements qui le reçoivent, comme indiqué dans la section [Création d’un abonnement](#create-a-subscription)) :</span><span class="sxs-lookup"><span data-stu-id="62ce8-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="62ce8-165">Les rubriques Service Bus prennent en charge une taille de message maximale de 256 Ko dans le [niveau Standard](service-bus-premium-messaging.md) et de 1 Mo dans le [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="62ce8-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="62ce8-166">L’en-tête, qui comprend les propriétés d’application standard et personnalisées, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="62ce8-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="62ce8-167">Si une rubrique n'est pas limitée par le nombre de messages qu'elle peut contenir, elle l'est en revanche par la taille totale des messages qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="62ce8-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="62ce8-168">La taille maximale de la rubrique est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="62ce8-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="62ce8-169">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="62ce8-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="62ce8-170">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="62ce8-170">Receive messages from a subscription</span></span>
<span data-ttu-id="62ce8-171">Le meilleur moyen pour recevoir les messages d’un abonnement est d’utiliser une méthode `ServiceBusRestProxy->receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="62ce8-172">Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete* et *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="62ce8-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="62ce8-173">Le mode par défaut est **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="62ce8-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="62ce8-174">Lorsque le mode [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) est utilisé, la réception est une opération unique : lorsque Service Bus reçoit une demande de lecture pour un message figurant dans un abonnement, il marque le message comme étant consommé et le renvoie à l’application.</span><span class="sxs-lookup"><span data-stu-id="62ce8-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="62ce8-175">Le mode [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) est le modèle le plus simple et le mieux adapté aux scénarios dans lesquels une application peut tolérer le non-traitement d’un message en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="62ce8-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="62ce8-176">Pour mieux comprendre, imaginez un scénario dans lequel le consommateur émet la demande de réception et subit un incident avant de la traiter.</span><span class="sxs-lookup"><span data-stu-id="62ce8-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="62ce8-177">Comme Service Bus a marqué le message comme étant consommé, lorsque l’application redémarre et recommence à consommer des messages, elle manque le message consommé avant l’incident.</span><span class="sxs-lookup"><span data-stu-id="62ce8-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="62ce8-178">En mode [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) par défaut, la réception d’un message s’effectue en deux temps, ce qui permet de prendre en charge les applications qui ne tolèrent pas les messages manquants.</span><span class="sxs-lookup"><span data-stu-id="62ce8-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="62ce8-179">Lorsque Service Bus reçoit une demande, il recherche le prochain message à consommer, le verrouille pour empêcher d'autres consommateurs de le recevoir, puis le renvoie à l'application.</span><span class="sxs-lookup"><span data-stu-id="62ce8-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="62ce8-180">Dès que l’application a terminé de traiter le message (ou qu’elle l’a stocké de manière sûre en vue d’un traitement ultérieur), elle effectue la deuxième étape du processus de réception en transmettant le message reçu à `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="62ce8-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="62ce8-181">Lorsque Service Bus voit l’appel `deleteMessage`, il marque le message comme consommé et le supprime de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="62ce8-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="62ce8-182">L’exemple ci-dessous montre comment recevoir et traiter un message avec le mode [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (mode par défaut).</span><span class="sxs-lookup"><span data-stu-id="62ce8-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="62ce8-183">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="62ce8-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="62ce8-184">Service Bus intègre des fonctionnalités destinées à faciliter la récupération à la suite d’erreurs survenues dans votre application ou de difficultés à traiter un message.</span><span class="sxs-lookup"><span data-stu-id="62ce8-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="62ce8-185">Si une application de réception ne parvient pas à traiter le message pour une raison quelconque, elle peut appeler la méthode `unlockMessage` sur le message reçu (au lieu de la méthode `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="62ce8-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="62ce8-186">Service Bus déverrouille alors le message dans la file d’attente et le rend à nouveau disponible en réception, pour la même application consommatrice ou pour une autre.</span><span class="sxs-lookup"><span data-stu-id="62ce8-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="62ce8-187">De même, il faut savoir qu'un message verrouillé dans une file d'attente est assorti d'un délai d'expiration et que si l'application ne parvient pas à traiter le message dans le temps imparti (par exemple, si l'application subit un incident), Service Bus déverrouille le message automatiquement et le rend à nouveau disponible en réception.</span><span class="sxs-lookup"><span data-stu-id="62ce8-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="62ce8-188">Si l’application se bloque après le traitement du message mais avant l’émission de la demande `deleteMessage`, le message est à nouveau transmis à l’application lorsqu’elle redémarre.</span><span class="sxs-lookup"><span data-stu-id="62ce8-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="62ce8-189">Cette opération est souvent appelée *Au moins une fois*. Chaque message est traité au moins une fois. Toutefois, dans certaines circonstances, un même message peut être remis une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="62ce8-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="62ce8-190">Si le scénario ne peut pas tolérer le traitement en double, les développeurs d'application doivent ajouter une logique supplémentaire aux applications pour traiter la remise de messages en double,</span><span class="sxs-lookup"><span data-stu-id="62ce8-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="62ce8-191">Ceci, grâce à la méthode `getMessageId` du message, qui reste constante entre les tentatives de transmission.</span><span class="sxs-lookup"><span data-stu-id="62ce8-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="62ce8-192">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="62ce8-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="62ce8-193">Pour supprimer une rubrique ou un abonnement, utilisez les méthodes `ServiceBusRestProxy->deleteTopic` ou `ServiceBusRestProxy->deleteSubscripton` respectivement.</span><span class="sxs-lookup"><span data-stu-id="62ce8-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="62ce8-194">Notez que la suppression d’une rubrique a également pour effet de supprimer les abonnements inscrits au niveau de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="62ce8-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="62ce8-195">L’exemple suivant montre comment supprimer une rubrique nommée `mytopic` et ses abonnements inscrits.</span><span class="sxs-lookup"><span data-stu-id="62ce8-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

<span data-ttu-id="62ce8-196">La méthode `deleteSubscription` permet de supprimer un abonnement de façon indépendante :</span><span class="sxs-lookup"><span data-stu-id="62ce8-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="62ce8-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62ce8-197">Next steps</span></span>
<span data-ttu-id="62ce8-198">Maintenant que vous connaissez les principes de base des files d’attente Service Bus, consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="62ce8-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
