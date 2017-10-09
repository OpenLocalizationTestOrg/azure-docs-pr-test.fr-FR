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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Comment toouse Service Bus rubriques et les abonnements avec PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Cet article vous montre comment toouse Service Bus rubriques et abonnements. exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP](../php-download-sdk.md). Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi rubrique tooa de messages**, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Hello seule exigence pour la création d’une application PHP qui accède au service d’objets Blob Azure hello est classes tooreference Bonjour [Azure SDK pour PHP](../php-download-sdk.md) à partir de votre code. Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, ou le bloc-notes.

> [!NOTE]
> Votre installation PHP doit également avoir hello [OpenSSL extension](http://php.net/openssl) installé et activé.
> 
> 

Cet article décrit comment les fonctions qui peuvent être appelées dans une application PHP localement ou dans le code en cours d’exécution au sein d’un rôle web Azure, le rôle de travail ou le site Web de service de toouse.

## <a name="get-hello-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
hello toouse API Service Bus :

1. Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require-once] instruction.
2. référencer toute classe que vous êtes susceptible d'utiliser.

Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServiceBusService** classe.

> [!NOTE]
> Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur. Si vous avez installé les bibliothèques hello manuellement ou en tant que package poire, vous devez référencer hello **WindowsAzure.php** fichier de chargeur automatique.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Bonjour exemple suivant, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.

## <a name="set-up-a-service-bus-connection"></a>Configuration d’une connexion Service Bus
tooinstantiate un client de Service Bus que vous devez d’abord avoir une chaîne de connexion valide au format suivant :

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Où `Endpoint` est généralement hello format `https://[yourNamespace].servicebus.windows.net`.

toocreate n’importe quel client de service Azure que vous devez utiliser hello `ServicesBuilder` classe. Vous pouvez :

* Passer hello connexion chaîne directement tooit.
* Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :
  * par défaut une source externe est prise en charge : variables d'environnement.
  * Vous pouvez ajouter de nouvelles sources en étendant hello `ConnectionStringSource` classe.

Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello est passé directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Création d'une rubrique
Vous pouvez effectuer les opérations de gestion pour les rubriques Service Bus via hello `ServiceBusRestProxy` classe. A `ServiceBusRestProxy` objet est construit via hello `ServicesBuilder::createServiceBusService` méthode de fabrique avec une chaîne de connexion appropriée qui encapsule hello autorisations jeton toomanage il.

Hello suivant montre l’exemple de comment tooinstantiate un `ServiceBusRestProxy` et appelez `ServiceBusRestProxy->createTopic` toocreate une rubrique nommée `mytopic` dans un `MySBNamespace` espace de noms :

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
> Vous pouvez utiliser hello `listTopics` méthode sur `ServiceBusRestProxy` objets toocheck si une rubrique portant le nom spécifié existe déjà dans un espace de noms de service.
> 
> 

## <a name="create-a-subscription"></a>Création d’un abonnement
Abonnements aux rubriques sont également créés par hello `ServiceBusRestProxy->createSubscription` (méthode). Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble de hello de messages transmis de file d’attente virtuelle de l’abonnement toohello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Créer un abonnement avec le filtre par défaut (MatchAll) hello
Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement. Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement hello. Hello exemple suivant crée un abonnement nommé « mysubscription » et utilise hello par défaut **MatchAll** filtre.

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

### <a name="create-subscriptions-with-filters"></a>Création d’abonnements avec des filtres
Vous pouvez également définir des filtres qui vous permettent de toospecify lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique. type de filtre pris en charge par les abonnements plus souple Hello est hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), qui implémente un sous-ensemble de SQL92. Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique. Pour plus d'informations sur les filtres SQL, consultez la page [Propriété SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Chaque règle sur un abonnement traite les messages entrants indépendamment, ajout de son abonnement toohello de messages de résultats. En outre, chaque nouvel abonnement a une valeur par défaut **règle** objet avec un filtre qui ajoute tous les messages hello rubrique toohello abonnement. tooreceive uniquement les messages correspondant à votre filtre, vous devez supprimer les règles par défaut de hello. Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `ServiceBusRestProxy->deleteRule` (méthode).
> 
> 

Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `MessageNumber` propriété supérieure à 3. Consultez [rubrique tooa de messages d’envoi](#send-messages-to-a-topic) pour plus d’informations sur l’ajout de propriétés personnalisées toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Notez que ce code nécessite utiliser hello un espace de noms supplémentaire : `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un `SqlFilter` qui sélectionne uniquement les messages qui ont un `MessageNumber` propriété inférieur ou égal too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Désormais, lorsqu’un message est envoyé à toohello `mytopic` rubrique, il est toujours remis tooreceivers abonné toohello `mysubscription` abonnement et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` (des abonnements en fonction de contenu du message hello).

## <a name="send-messages-tooa-topic"></a>Rubrique tooa de messages d’envoi
toosend une rubrique de Service Bus message tooa, votre application appelle hello `ServiceBusRestProxy->sendTopicMessage` (méthode). Hello suivant de code montre comment toosend un toohello message `mytopic` rubrique créée précédemment dans le `MySBNamespace` espace de noms de service.

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

Les messages envoyés rubriques du Bus tooService sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de propriétés standard et les méthodes, ainsi que les propriétés qui peuvent être utilisés toohold des propriétés personnalisées spécifiques à l’application. Hello suivant montre comment les messages de test de toosend 5 toohello `mytopic` rubrique créée précédemment. Hello `setProperty` méthode est utilisée tooadd une propriété personnalisée (`MessageNumber`) tooeach message. Notez que hello `MessageNumber` valeur de propriété varie selon chaque message (vous pouvez utiliser cette toodetermine valeur les abonnements de réception, comme indiqué dans hello [créer un abonnement](#create-a-subscription) section) :

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

Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin. La taille maximale de la rubrique est de 5 Go. Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Réception des messages d’un abonnement
messages Hello meilleure manière tooreceive à partir d’un abonnement est toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` (méthode). Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete* et *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** est la valeur par défaut hello.

Lors de l’utilisation de hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , le mode de réception est une opération de prise de vue unique ; autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans un abonnement, il marque le message de type hello comme ayant été consommé et le retourne toohello application. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Dans la valeur par défaut hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, la réception d’un message devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en passant le message de salutation reçu trop`ServiceBusRestProxy->deleteMessage`. Lorsque le Service Bus voit hello `deleteMessage` appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.

Hello suivant montre l’exemple de comment tooreceive et traiter un message à l’aide de [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (mode par défaut de hello). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Gestion des blocages d’application et des messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le message de salutation reçu (au lieu de hello `deleteMessage` méthode). Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois* traitement ; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter remise de messages en double de toohandle de tooapplications logique supplémentaire. Cela est souvent obtenue à l’aide de hello `getMessageId` méthode de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="delete-topics-and-subscriptions"></a>Suppression de rubriques et d'abonnements
toodelete une rubrique ou un abonnement, utilisez hello `ServiceBusRestProxy->deleteTopic` ou hello `ServiceBusRestProxy->deleteSubscripton` méthodes, respectivement. Notez que la suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello.

Hello suivant montre comment toodelete une rubrique nommée `mytopic` et ses abonnements enregistrés.

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

À l’aide de hello `deleteSubscription` (méthode), vous pouvez supprimer un abonnement de façon indépendante :

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
