---
title: "aaaHow toouse stockage de file d’attente à partir de PHP | Documents Microsoft"
description: "Découvrez comment toouse hello file d’attente Azure storage service toocreate et les files d’attente de suppression, insertion, obtenir et supprimer les messages. Les exemples sont écrits en PHP."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Comment toouse stockage de file d’attente à partir de PHP
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide explique comment tooperform des scénarios courants à l’aide de hello service de stockage de file d’attente Azure. exemples de Hello sont écrites via des classes hello SDK Windows pour PHP. Hello scénarios couverts sont insertion, lecture, mise en route et suppression des messages de la file d’attente, ainsi que la création et la suppression de files d’attente.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Hello seule exigence pour la création d’une application PHP qui accède au stockage de file d’attente Azure est hello faisant référence à des classes à partir de hello Azure SDK pour PHP à partir de votre code. Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.

Dans ce guide, vous allez utiliser des fonctionnalités du service de File d’attente qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurer votre stockage de file d’attente de tooaccess application
toouse hello API pour le stockage de la file d’attente Azure, vous devez :

1. Fichier de chargeur automatique hello référence à l’aide de hello [require_once] instruction.
2. référencer toutes les classes que vous êtes susceptible d’utiliser.

Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.

> [!NOTE]
> Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur. Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello `WindowsAzure.php` fichier de chargeur automatique.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Dans les exemples de hello ci-dessous, hello `require_once` instruction s’affiche toujours, mais seules les classes hello qui sont nécessaires pour hello exemple tooexecute seront référencés.

## <a name="set-up-an-azure-storage-connection"></a>Configuration d’une connexion de stockage Azure
tooinstantiate un client de stockage de file d’attente Azure, vous devez avoir une chaîne de connexion valide. format Hello pour la chaîne de connexion de service de file d’attente hello est comme suit.

Pour accéder à un service en ligne :

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Pour accéder au stockage d’émulateur hello :

```php
UseDevelopmentStorage=true
```

toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe. Vous pouvez utiliser de hello suivant techniques :

* Passer hello connexion chaîne directement tooit.
* Utilisez **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :
  * Par défaut, il prend en charge une source externe : les variables d’environnement.
  * Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe.

Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Création d’une file d’attente
A **QueueRestProxy** objet vous permet de créer une file d’attente à l’aide de hello **createQueue** (méthode). Lorsque vous créez une file d’attente, vous pouvez définir des options sur la file d’attente hello, mais cela n’est pas requis. (hello exemple ci-dessous montre comment les métadonnées tooset sur une file d’attente.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Ne tenez pas compte de la différence entre majuscules et minuscules pour les clés de métadonnées. Toutes les clés sont lus à partir de service hello en minuscules.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Ajouter une file d’attente de messages tooa
tooadd une file d’attente de message tooa, utilisez **QueueRestProxy -> createMessage**. méthode Hello prend le nom de file d’attente de hello, texte du message hello et les options de message (qui sont facultatifs).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Lire des message de type hello suivant
Lire un message (ou messages) à avant hello d’une file d’attente sans le supprimer de la file d’attente hello en appelant **QueueRestProxy -> peekMessages**. Par défaut, hello **peekMessage** méthode retourne un seul message, mais vous pouvez modifier cette valeur à l’aide de hello **PeekMessagesOptions -> setNumberOfMessages** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>File d’attente message de type hello suivant
Votre code supprime un message d'une file d'attente en deux étapes. Tout d’abord, vous appelez **QueueRestProxy -> listMessages**, ce qui rend tooany invisible du message hello tout autre code qui lit à partir de la file d’attente hello. Par défaut, ce message reste invisible pendant 30 secondes. (Si le message de type hello n’est pas supprimé dans cette période, elle redevient visible sur la file d’attente hello.) toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez appeler **QueueRestProxy -> deleteMessage**. Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre tooprocess échoue de code un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message et essayez à nouveau. Votre code appelle **deleteMessage** juste après le message de salutation a été traité.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Modifier le contenu de hello d’un message en file d’attente
Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello en appelant **QueueRestProxy -> updateMessage**. Si le message de type hello représente une tâche de travail, vous pouvez utiliser cet état de hello tooupdate la fonctionnalité de tâche hello. Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu, et il définit tooextend de délai d’attente de visibilité hello un autre 60 secondes. Cela enregistre l’état de hello de travail qui a associé à un message de type hello et il donne les client hello un autre toocontinue minute travaillant sur un message de type hello. Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle. En règle générale, vous conservez ainsi un nombre de tentatives, et si hello message est retentée plusieurs  *n*  fois, vous le supprimez. Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Options supplémentaires pour l'extraction de messages
Il existe deux façons de personnaliser la récupération des messages à partir d’une file d’attente. Tout d’abord, vous pouvez obtenir un lot de messages (haut too32). Ensuite, vous pouvez définir un délai d’attente de visibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message. exemple de code suivant Hello utilise hello **getMessages** messages tooget 16 de méthode dans un seul appel. Ensuite, il traite chaque message à l’aide d’une boucle **for** . Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Obtention de la longueur de la file d'attente
Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente. Hello **QueueRestProxy -> getQueueMetadata** méthode demande hello file d’attente service tooreturn métadonnées sur la file d’attente hello. Appel hello **getApproximateMessageCount** méthode sur hello a retourné d’objet fournit un nombre du nombre de messages dans une file d’attente. nombre de Hello uniquement est approximatif, car les messages peuvent être ajoutées ou supprimées une fois le service de file d’attente hello répond tooyour demande.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Suppression d'une file d'attente
toodelete une file d’attente et tous les messages hello, appelez hello **QueueRestProxy -> deleteQueue** (méthode).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes :

* Visitez hello [blog de l’équipe de stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

