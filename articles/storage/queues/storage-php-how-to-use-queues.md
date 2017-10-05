---
title: "Utilisation du stockage de files d’attente à partir de PHP | Microsoft Docs"
description: "Découvrez comment utiliser le service de stockage de files d’attente Azure pour créer et supprimer des files d’attente, ainsi que pour insérer, récupérer et supprimer des messages. Les exemples sont écrits en PHP."
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
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a>Utilisation du stockage de files d'attente à partir de PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage des files d’attente Azure. Les exemples sont écrits au moyen de classes issues du Kit de développement logiciel (SDK) Windows pour PHP. Les scénarios traités incluent l’insertion, la lecture furtive, la récupération et la suppression des messages de file d’attente, ainsi que la création et suppression des files d’attente.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Le référencement de classes issues du Kit de développement logiciel (SDK) Azure pour PHP dans votre code constitue la seule exigence pour créer une application PHP qui accède au service de File d’attente Azure. Vous pouvez utiliser tous les outils de développement pour créer votre application, y compris Bloc-notes.

Dans ce guide, vous allez utiliser des fonctionnalités du service de File d’attente qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.

## <a name="get-the-azure-client-libraries"></a>Obtention des bibliothèques clientes Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a>Configuration de votre application pour accéder au stockage de files d’attente
Pour utiliser les API du stockage de files d’attente Azure, vous devez :

1. référencer le fichier de chargeur automatique à l’aide de l’instruction [require_once] ;
2. référencer toutes les classes que vous êtes susceptible d’utiliser.

L'exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe **ServicesBuilder** .

> [!NOTE]
> Cet exemple et d’autres exemples dans cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer. Si vous avez installé les bibliothèques manuellement, vous devrez référencer le fichier de chargeur automatique `WindowsAzure.php` .
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Dans les exemples ci-dessous, l’instruction `require_once` s’affiche toujours, mais seules les classes nécessaires à l’exécution de l’exemple sont référencées.

## <a name="set-up-an-azure-storage-connection"></a>Configuration d’une connexion de stockage Azure
Pour instancier un client de stockage de files d’attente Azure, vous devez disposer d’une chaîne de connexion valide. Le format de la chaîne de connexion du service de File d’attente est le suivant :

Pour accéder à un service en ligne :

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Pour accéder au stockage de l’émulateur :

```php
UseDevelopmentStorage=true
```

Pour créer un client de service Azure, vous devez utiliser la classe **ServicesBuilder** . Vous pouvez utiliser une des techniques suivantes :

* Lui passer directement la chaîne de connexion.
* Utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :
  * Par défaut, il prend en charge une source externe : les variables d’environnement.
  * Vous pouvez ajouter de nouvelles sources via une extension de la classe **ConnectionStringSource** .

Dans les exemples ci-dessous, la chaîne de connexion est passée directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Création d’une file d’attente
Un objet **QueueRestProxy** vous permet de créer une file d’attente avec la méthode **createQueue**. Lors de la création d'une file d'attente, vous pouvez définir des options sur cette dernière, mais vous n'y êtes pas obligé. L'exemple ci-dessous illustre comment définir des métadonnées dans une file d'attente.

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
> Ne tenez pas compte de la différence entre majuscules et minuscules pour les clés de métadonnées. Toutes les clés sont lues en minuscules sur le service.
> 
> 

## <a name="add-a-message-to-a-queue"></a>Ajout d'un message à une file d'attente
Pour ajouter un message à une file d’attente, utilisez **QueueRestProxy->createMessage**. La méthode prend le nom de la file d'attente, le texte du message et les options du message (qui sont facultatives).

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

## <a name="peek-at-the-next-message"></a>Lecture furtive du message suivant
Vous pouvez lire furtivement un ou plusieurs messages au début d’une file d’attente sans les supprimer de la file d’attente en appelant la méthode **QueueRestProxy->peekMessages**. Par défaut, la méthode **peekMessage** renvoie un seul message, mais vous pouvez modifier cette valeur à l’aide de la méthode **PeekMessagesOptions->setNumberOfMessages**.

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

## <a name="de-queue-the-next-message"></a>Enlèvement du message suivant de la file d'attente
Votre code supprime un message d'une file d'attente en deux étapes. Tout d’abord, vous appelez **QueueRestProxy->listMessages**, ce qui rend le message invisible à tout autre code lu à partir de la file d’attente. Par défaut, ce message reste invisible pendant 30 secondes. (Si le message n’est pas supprimé pendant cette période, il redevient visible dans la file d’attente). Pour finaliser la suppression du message de la file d’attente, vous devez appeler **QueueRestProxy->deleteMessage**. Ce processus de suppression d’un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer. Votre code appelle **deleteMessage** juste après le traitement du message.

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

## <a name="change-the-contents-of-a-queued-message"></a>Modification du contenu d'un message en file d'attente
Vous pouvez modifier le contenu d’un message placé dans la file d’attente en appelant **QueueRestProxy->updateMessage**. Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche. Le code suivant met à jour le message de la file d’attente avec un nouveau contenu et ajoute 60 secondes au délai d’expiration de la visibilité. Cette opération enregistre l’état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message. Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle. Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de *n* fois, vous le supprimez. Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.

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
Il existe deux façons de personnaliser la récupération des messages à partir d’une file d’attente. Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32). Deuxièmement, vous pouvez définir un délai d'expiration de la visibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message. L'exemple de code suivant utilise la méthode **getMessages** pour obtenir 16 messages en un appel. Ensuite, il traite chaque message à l’aide d’une boucle **for** . Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.

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
Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente. La méthode **QueueRestProxy->getQueueMetadata** demande au service de file d’attente de renvoyer les métadonnées relatives à la file d’attente. Appeler la méthode **getApproximateMessageCount** sur l'objet renvoyé permet d'obtenir le nombre de messages figurant dans une file d'attente. Ce nombre est approximatif étant donné que des messages peuvent être ajoutés ou supprimés une fois que le service de File d'attente a répondu à votre demande.

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
Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **QueueRestProxy->deleteQueue**.

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
Maintenant que vous connaissez les bases du stockage des files d’attente Azure, consultez les liens suivants pour apprendre à effectuer des tâches de stockage plus complexes :

* Consultez le [blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/).

Pour plus d’informations, consultez également le [Centre pour développeurs PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

