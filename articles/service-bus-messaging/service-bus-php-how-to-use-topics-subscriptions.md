---
title: rubriques de Service Bus aaaHow toouse avec PHP | Documents Microsoft
description: "Découvrez comment toouse les rubriques de Service Bus avec PHP dans Azure."
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
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="611ca-103">Comment toouse Service Bus rubriques et les abonnements avec PHP</span><span class="sxs-lookup"><span data-stu-id="611ca-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="611ca-104">Cet article vous montre comment toouse Service Bus rubriques et abonnements.</span><span class="sxs-lookup"><span data-stu-id="611ca-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="611ca-105">exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="611ca-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="611ca-106">Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.</span><span class="sxs-lookup"><span data-stu-id="611ca-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="611ca-107">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="611ca-107">Create a PHP application</span></span>
<span data-ttu-id="611ca-108">Hello seule exigence pour la création d’une application PHP qui accède au service d’objets Blob Azure hello est classes tooreference Bonjour [Azure SDK pour PHP](../php-download-sdk.md) à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="611ca-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="611ca-109">Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, ou le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="611ca-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="611ca-110">Votre installation PHP doit également avoir hello [OpenSSL extension](http://php.net/openssl) installé et activé.</span><span class="sxs-lookup"><span data-stu-id="611ca-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="611ca-111">Cet article décrit comment les fonctions qui peuvent être appelées dans une application PHP localement ou dans le code en cours d’exécution au sein d’un rôle web Azure, le rôle de travail ou le site Web de service de toouse.</span><span class="sxs-lookup"><span data-stu-id="611ca-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="611ca-112">Obtenir les bibliothèques clientes Azure hello</span><span class="sxs-lookup"><span data-stu-id="611ca-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="611ca-113">Configurer votre toouse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="611ca-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="611ca-114">hello toouse API Service Bus :</span><span class="sxs-lookup"><span data-stu-id="611ca-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="611ca-115">Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require-once] instruction.</span><span class="sxs-lookup"><span data-stu-id="611ca-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="611ca-116">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="611ca-116">Reference any classes you might use.</span></span>

<span data-ttu-id="611ca-117">Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="611ca-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="611ca-118">Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur.</span><span class="sxs-lookup"><span data-stu-id="611ca-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="611ca-119">Si vous avez installé les bibliothèques hello manuellement ou en tant que package poire, vous devez référencer hello **WindowsAzure.php** fichier de chargeur automatique.</span><span class="sxs-lookup"><span data-stu-id="611ca-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="611ca-120">Bonjour exemple suivant, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.</span><span class="sxs-lookup"><span data-stu-id="611ca-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="611ca-121">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="611ca-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="611ca-122">tooinstantiate un client de Service Bus que vous devez d’abord avoir une chaîne de connexion valide au format suivant :</span><span class="sxs-lookup"><span data-stu-id="611ca-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="611ca-123">Où `Endpoint` est généralement hello format `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="611ca-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="611ca-124">toocreate n’importe quel client de service Azure que vous devez utiliser hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="611ca-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="611ca-125">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="611ca-125">You can:</span></span>

* <span data-ttu-id="611ca-126">Passer hello connexion chaîne directement tooit.</span><span class="sxs-lookup"><span data-stu-id="611ca-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="611ca-127">Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="611ca-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="611ca-128">par défaut une source externe est prise en charge : variables d'environnement.</span><span class="sxs-lookup"><span data-stu-id="611ca-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="611ca-129">Vous pouvez ajouter de nouvelles sources en étendant hello `ConnectionStringSource` classe.</span><span class="sxs-lookup"><span data-stu-id="611ca-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="611ca-130">Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello est passé directement.</span><span class="sxs-lookup"><span data-stu-id="611ca-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="611ca-131">Création d'une rubrique</span><span class="sxs-lookup"><span data-stu-id="611ca-131">Create a topic</span></span>
<span data-ttu-id="611ca-132">Vous pouvez effectuer les opérations de gestion pour les rubriques Service Bus via hello `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="611ca-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="611ca-133">A `ServiceBusRestProxy` objet est construit via hello `ServicesBuilder::createServiceBusService` méthode de fabrique avec une chaîne de connexion appropriée qui encapsule hello autorisations jeton toomanage il.</span><span class="sxs-lookup"><span data-stu-id="611ca-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="611ca-134">Hello suivant montre l’exemple de comment tooinstantiate un `ServiceBusRestProxy` et appelez `ServiceBusRestProxy->createTopic` toocreate une rubrique nommée `mytopic` dans un `MySBNamespace` espace de noms :</span><span class="sxs-lookup"><span data-stu-id="611ca-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="611ca-135">Vous pouvez utiliser hello `listTopics` méthode sur `ServiceBusRestProxy` objets toocheck si une rubrique portant le nom spécifié existe déjà dans un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="611ca-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="611ca-136">Création d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="611ca-136">Create a subscription</span></span>
<span data-ttu-id="611ca-137">Abonnements aux rubriques sont également créés par hello `ServiceBusRestProxy->createSubscription` (méthode).</span><span class="sxs-lookup"><span data-stu-id="611ca-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="611ca-138">Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble de hello de messages transmis de file d’attente virtuelle de l’abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="611ca-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="611ca-139">Créer un abonnement avec le filtre par défaut (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="611ca-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="611ca-140">Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="611ca-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="611ca-141">Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="611ca-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="611ca-142">Hello exemple suivant crée un abonnement nommé « mysubscription » et utilise hello par défaut **MatchAll** filtre.</span><span class="sxs-lookup"><span data-stu-id="611ca-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="611ca-143">Création d’abonnements avec des filtres</span><span class="sxs-lookup"><span data-stu-id="611ca-143">Create subscriptions with filters</span></span>
<span data-ttu-id="611ca-144">Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="611ca-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="611ca-145">type de filtre pris en charge par les abonnements plus souple Hello est hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), qui implémente un sous-ensemble de SQL92.</span><span class="sxs-lookup"><span data-stu-id="611ca-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="611ca-146">Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="611ca-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="611ca-147">Pour plus d'informations sur les filtres SQL, consultez la page [Propriété SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="611ca-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="611ca-148">Chaque règle sur un abonnement traite les messages entrants indépendamment, ajout de son abonnement toohello de messages de résultats.</span><span class="sxs-lookup"><span data-stu-id="611ca-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="611ca-149">En outre, chaque nouvel abonnement a une valeur par défaut **règle** objet avec un filtre qui ajoute tous les messages hello rubrique toohello abonnement.</span><span class="sxs-lookup"><span data-stu-id="611ca-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="611ca-150">tooreceive uniquement les messages correspondant à votre filtre, vous devez supprimer les règles par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="611ca-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="611ca-151">Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `ServiceBusRestProxy->deleteRule` (méthode).</span><span class="sxs-lookup"><span data-stu-id="611ca-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="611ca-152">Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `MessageNumber` propriété supérieure à 3.</span><span class="sxs-lookup"><span data-stu-id="611ca-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="611ca-153">Consultez [rubrique tooa de messages d’envoi](#send-messages-to-a-topic) pour plus d’informations sur l’ajout de propriétés personnalisées toomessages.</span><span class="sxs-lookup"><span data-stu-id="611ca-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="611ca-154">Notez que ce code nécessite utiliser hello un espace de noms supplémentaire : `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="611ca-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="611ca-155">De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un `SqlFilter` qui sélectionne uniquement les messages qui ont un `MessageNumber` propriété inférieur ou égal too3.</span><span class="sxs-lookup"><span data-stu-id="611ca-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="611ca-156">Désormais, lorsqu’un message est envoyé à toohello `mytopic` rubrique, il est toujours remis tooreceivers abonné toohello `mysubscription` abonnement et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` (des abonnements en fonction de contenu du message hello).</span><span class="sxs-lookup"><span data-stu-id="611ca-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="611ca-157">Rubrique tooa de messages d’envoi</span><span class="sxs-lookup"><span data-stu-id="611ca-157">Send messages tooa topic</span></span>
<span data-ttu-id="611ca-158">toosend une rubrique de Service Bus message tooa, votre application appelle hello `ServiceBusRestProxy->sendTopicMessage` (méthode).</span><span class="sxs-lookup"><span data-stu-id="611ca-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="611ca-159">Hello suivant de code montre comment toosend un toohello message `mytopic` rubrique créée précédemment dans le `MySBNamespace` espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="611ca-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="611ca-160">Les messages envoyés rubriques du Bus tooService sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="611ca-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="611ca-161">[BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de propriétés standard et les méthodes, ainsi que les propriétés qui peuvent être utilisés toohold des propriétés personnalisées spécifiques à l’application.</span><span class="sxs-lookup"><span data-stu-id="611ca-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="611ca-162">Hello suivant montre comment les messages de test de toosend 5 toohello `mytopic` rubrique créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="611ca-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="611ca-163">Hello `setProperty` méthode est utilisée tooadd une propriété personnalisée (`MessageNumber`) tooeach message.</span><span class="sxs-lookup"><span data-stu-id="611ca-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="611ca-164">Notez que hello `MessageNumber` valeur de propriété varie selon chaque message (vous pouvez utiliser cette toodetermine valeur les abonnements de réception, comme indiqué dans hello [créer un abonnement](#create-a-subscription) section) :</span><span class="sxs-lookup"><span data-stu-id="611ca-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="611ca-165">Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="611ca-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="611ca-166">en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="611ca-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="611ca-167">Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin.</span><span class="sxs-lookup"><span data-stu-id="611ca-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="611ca-168">La taille maximale de la rubrique est de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="611ca-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="611ca-169">Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="611ca-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="611ca-170">Réception des messages d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="611ca-170">Receive messages from a subscription</span></span>
<span data-ttu-id="611ca-171">messages Hello meilleure manière tooreceive à partir d’un abonnement est toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` (méthode).</span><span class="sxs-lookup"><span data-stu-id="611ca-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="611ca-172">Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete* et *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="611ca-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="611ca-173">**PeekLock** est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="611ca-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="611ca-174">Lors de l’utilisation de hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , le mode de réception est une opération de prise de vue unique ; autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans un abonnement, il marque le message de type hello comme ayant été consommé et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="611ca-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="611ca-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec.</span><span class="sxs-lookup"><span data-stu-id="611ca-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="611ca-176">toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter.</span><span class="sxs-lookup"><span data-stu-id="611ca-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="611ca-177">Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.</span><span class="sxs-lookup"><span data-stu-id="611ca-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="611ca-178">Dans la valeur par défaut hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, la réception d’un message devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants.</span><span class="sxs-lookup"><span data-stu-id="611ca-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="611ca-179">Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.</span><span class="sxs-lookup"><span data-stu-id="611ca-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="611ca-180">Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en passant le message de salutation reçu trop`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="611ca-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="611ca-181">Lorsque le Service Bus voit hello `deleteMessage` appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="611ca-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="611ca-182">Hello suivant montre l’exemple de comment tooreceive et traiter un message à l’aide de [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (mode par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="611ca-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="611ca-183">Gestion des blocages d’application et des messages illisibles</span><span class="sxs-lookup"><span data-stu-id="611ca-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="611ca-184">Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message.</span><span class="sxs-lookup"><span data-stu-id="611ca-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="611ca-185">Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le message de salutation reçu (au lieu de hello `deleteMessage` méthode).</span><span class="sxs-lookup"><span data-stu-id="611ca-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="611ca-186">Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.</span><span class="sxs-lookup"><span data-stu-id="611ca-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="611ca-187">Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.</span><span class="sxs-lookup"><span data-stu-id="611ca-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="611ca-188">Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage.</span><span class="sxs-lookup"><span data-stu-id="611ca-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="611ca-189">Cela est souvent appelé *au moins une fois* traitement ; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué.</span><span class="sxs-lookup"><span data-stu-id="611ca-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="611ca-190">Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter remise de messages en double de toohandle de tooapplications logique supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="611ca-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="611ca-191">Cela est souvent obtenue à l’aide de hello `getMessageId` méthode de message de type hello, qui reste constante entre les tentatives de remise.</span><span class="sxs-lookup"><span data-stu-id="611ca-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="611ca-192">Suppression de rubriques et d'abonnements</span><span class="sxs-lookup"><span data-stu-id="611ca-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="611ca-193">toodelete une rubrique ou un abonnement, utilisez hello `ServiceBusRestProxy->deleteTopic` ou hello `ServiceBusRestProxy->deleteSubscripton` méthodes, respectivement.</span><span class="sxs-lookup"><span data-stu-id="611ca-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="611ca-194">Notez que la suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="611ca-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="611ca-195">Hello suivant montre comment toodelete une rubrique nommée `mytopic` et ses abonnements enregistrés.</span><span class="sxs-lookup"><span data-stu-id="611ca-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="611ca-196">À l’aide de hello `deleteSubscription` (méthode), vous pouvez supprimer un abonnement de façon indépendante :</span><span class="sxs-lookup"><span data-stu-id="611ca-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="611ca-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="611ca-197">Next steps</span></span>
<span data-ttu-id="611ca-198">Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="611ca-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
