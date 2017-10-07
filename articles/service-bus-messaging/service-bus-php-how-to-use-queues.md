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
# <a name="how-toouse-service-bus-queues-with-php"></a>Comment toouse Service Bus de files d’attente avec PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Ce guide vous montre comment les files d’attente de toouse Service Bus. exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP](../php-download-sdk.md). Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Hello uniquement requis pour la création d’une application PHP qui accède au service d’objets Blob Azure hello est hello faisant référence à des classes de hello [Azure SDK pour PHP](../php-download-sdk.md) à partir de votre code. Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, ou le bloc-notes.

> [!NOTE]
> Votre installation PHP doit également avoir hello [OpenSSL extension](http://php.net/openssl) installé et activé.
> 
> 

Dans ce guide, vous allez utiliser les fonctionnalités du service qui peuvent être appelées dans une application PHP en local, ou dans le code s'exécutant dans un rôle web, un rôle de travail ou un site web Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
file d’attente de Service Bus toouse hello API, hello suivant :

1. Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] [ require_once] instruction.
2. référencer toute classe que vous êtes susceptible d'utiliser.

Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique `ServicesBuilder` classe.

> [!NOTE]
> Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur. Si vous avez installé les bibliothèques hello manuellement ou en tant que package poire, vous devez référencer hello **WindowsAzure.php** fichier de chargeur automatique.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Dans les exemples de hello ci-dessous, hello `require_once` instruction est toujours affichée, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.

## <a name="set-up-a-service-bus-connection"></a>Configuration d’une connexion Service Bus
tooinstantiate un client Service Bus, vous devez avoir une chaîne de connexion valide au format suivant :

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Où `Endpoint` est généralement hello format `[yourNamespace].servicebus.windows.net`.

toocreate n’importe quel client de service Azure que vous devez utiliser hello `ServicesBuilder` classe. Vous pouvez :

* Passer hello connexion chaîne directement tooit.
* Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :
  * par défaut une source externe est prise en charge : variables d'environnement
  * Vous pouvez ajouter de nouvelles sources en étendant hello `ConnectionStringSource` classe

Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello est passé directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Création d’une file d’attente
Vous pouvez effectuer les opérations de gestion des files d’attente Service Bus via hello `ServiceBusRestProxy` classe. A `ServiceBusRestProxy` objet est construit via hello `ServicesBuilder::createServiceBusService` méthode de fabrique avec une chaîne de connexion appropriée qui encapsule hello autorisations jeton toomanage il.

Hello suivant montre l’exemple de comment tooinstantiate un `ServiceBusRestProxy` et appelez `ServiceBusRestProxy->createQueue` toocreate une file d’attente nommée `myqueue` dans un `MySBNamespace` espace de noms de service :

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
> Vous pouvez utiliser hello `listQueues` méthode sur `ServiceBusRestProxy` objets toocheck si une file d’attente portant le nom spécifié existe déjà dans un espace de noms.
> 
> 

## <a name="send-messages-tooa-queue"></a>Envoyer la file d’attente de messages tooa
toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `ServiceBusRestProxy->sendQueueMessage` (méthode). Hello suivant de code montre comment toosend un toohello message `myqueue` file d’attente créée précédemment dans le `MySBNamespace` espace de noms de service.

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

Messages trop envoyées (et reçues à partir de) les files d’attente Service Bus sont des instances de hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objets comportent un ensemble de méthodes et propriétés qui sont utilisées toohold des propriétés personnalisées spécifiques à l’application et un corps de données d’application arbitraire standard.

Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin. La taille maximale de la file d'attente est de 5 Go.

## <a name="receive-messages-from-a-queue"></a>Réception des messages d'une file d'attente

messages Hello meilleure manière tooreceive à partir d’une file d’attente est toouse un `ServiceBusRestProxy->receiveQueueMessage` (méthode). Les messages peuvent être reçus dans deux modes : [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) et [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** est la valeur par défaut hello.

Lorsque vous utilisez [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , le mode de réception est une opération de prise de vue unique ; autrement dit, lorsque le Service Bus reçoit une demande de lecture d’un message dans une file d’attente, il marque le message de type hello comme ayant été consommé et le retourne toohello application. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Dans la valeur par défaut hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, la réception d’un message devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe est utilisé, il verrouille tooprevent autres consommateurs de le recevoir, puis retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en passant le message de salutation reçu trop`ServiceBusRestProxy->deleteMessage`. Lorsque le Service Bus voit hello `deleteMessage` appel, il marque le message de type hello comme ayant été consommé et supprimez-le de la file d’attente hello.

Hello suivant montre l’exemple de comment tooreceive et traiter un message à l’aide de [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (mode par défaut de hello).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles

Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le message de salutation reçu (au lieu de hello `deleteMessage` méthode). Cette opération provoquent le message de type hello toounlock Service Bus au sein de la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille un message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` demande est émise, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois* traitement ; autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne tolère pas le traitement dupliqué, puis ajouter des remise de messages en double logique tooapplications toohandle est recommandé. Cela est souvent obtenue à l’aide de hello `getMessageId` méthode de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de files d’attente Service Bus, consultez [les files d’attente, rubriques et abonnements] [ Queues, topics, and subscriptions] pour plus d’informations.

Pour plus d’informations, reportez-vous également au hello [centre de développement PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


