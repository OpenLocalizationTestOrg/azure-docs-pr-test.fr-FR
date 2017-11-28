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
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="9a8b0-104">Comment toouse stockage de file d’attente à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="9a8b0-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9a8b0-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9a8b0-105">Overview</span></span>
<span data-ttu-id="9a8b0-106">Ce guide explique comment tooperform des scénarios courants à l’aide de hello service de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="9a8b0-107">exemples de Hello sont écrites via des classes hello SDK Windows pour PHP.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="9a8b0-108">Hello scénarios couverts sont insertion, lecture, mise en route et suppression des messages de la file d’attente, ainsi que la création et la suppression de files d’attente.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="9a8b0-109">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="9a8b0-109">Create a PHP application</span></span>
<span data-ttu-id="9a8b0-110">Hello seule exigence pour la création d’une application PHP qui accède au stockage de file d’attente Azure est hello faisant référence à des classes à partir de hello Azure SDK pour PHP à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="9a8b0-111">Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="9a8b0-112">Dans ce guide, vous allez utiliser des fonctionnalités du service de File d’attente qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="9a8b0-113">Obtenir les bibliothèques clientes Azure hello</span><span class="sxs-lookup"><span data-stu-id="9a8b0-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="9a8b0-114">Configurer votre stockage de file d’attente de tooaccess application</span><span class="sxs-lookup"><span data-stu-id="9a8b0-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="9a8b0-115">toouse hello API pour le stockage de la file d’attente Azure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="9a8b0-116">Fichier de chargeur automatique hello référence à l’aide de hello [require_once] instruction.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="9a8b0-117">référencer toutes les classes que vous êtes susceptible d’utiliser.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="9a8b0-118">Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="9a8b0-119">Cet exemple (et autres exemples de cet article) suppose que vous avez installé les bibliothèques clientes hello PHP pour Azure via le compositeur.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="9a8b0-120">Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello `WindowsAzure.php` fichier de chargeur automatique.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="9a8b0-121">Dans les exemples de hello ci-dessous, hello `require_once` instruction s’affiche toujours, mais seules les classes hello qui sont nécessaires pour hello exemple tooexecute seront référencés.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="9a8b0-122">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9a8b0-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="9a8b0-123">tooinstantiate un client de stockage de file d’attente Azure, vous devez avoir une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="9a8b0-124">format Hello pour la chaîne de connexion de service de file d’attente hello est comme suit.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="9a8b0-125">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="9a8b0-126">Pour accéder au stockage d’émulateur hello :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="9a8b0-127">toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="9a8b0-128">Vous pouvez utiliser de hello suivant techniques :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="9a8b0-129">Passer hello connexion chaîne directement tooit.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="9a8b0-130">Utilisez **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="9a8b0-131">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="9a8b0-132">Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="9a8b0-133">Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="9a8b0-134">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="9a8b0-134">Create a queue</span></span>
<span data-ttu-id="9a8b0-135">A **QueueRestProxy** objet vous permet de créer une file d’attente à l’aide de hello **createQueue** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="9a8b0-136">Lorsque vous créez une file d’attente, vous pouvez définir des options sur la file d’attente hello, mais cela n’est pas requis.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="9a8b0-137">(hello exemple ci-dessous montre comment les métadonnées tooset sur une file d’attente.)</span><span class="sxs-lookup"><span data-stu-id="9a8b0-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="9a8b0-138">Ne tenez pas compte de la différence entre majuscules et minuscules pour les clés de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="9a8b0-139">Toutes les clés sont lus à partir de service hello en minuscules.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="9a8b0-140">Ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="9a8b0-140">Add a message tooa queue</span></span>
<span data-ttu-id="9a8b0-141">tooadd une file d’attente de message tooa, utilisez **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="9a8b0-142">méthode Hello prend le nom de file d’attente de hello, texte du message hello et les options de message (qui sont facultatifs).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="9a8b0-143">Lire des message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="9a8b0-143">Peek at hello next message</span></span>
<span data-ttu-id="9a8b0-144">Lire un message (ou messages) à avant hello d’une file d’attente sans le supprimer de la file d’attente hello en appelant **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="9a8b0-145">Par défaut, hello **peekMessage** méthode retourne un seul message, mais vous pouvez modifier cette valeur à l’aide de hello **PeekMessagesOptions -> setNumberOfMessages** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="9a8b0-146">File d’attente message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="9a8b0-146">De-queue hello next message</span></span>
<span data-ttu-id="9a8b0-147">Votre code supprime un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="9a8b0-148">Tout d’abord, vous appelez **QueueRestProxy -> listMessages**, ce qui rend tooany invisible du message hello tout autre code qui lit à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="9a8b0-149">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="9a8b0-150">(Si le message de type hello n’est pas supprimé dans cette période, elle redevient visible sur la file d’attente hello.) toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez appeler **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="9a8b0-151">Ce processus en deux étapes de la suppression d’un message garantit que lorsque votre tooprocess échoue de code un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message et essayez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="9a8b0-152">Votre code appelle **deleteMessage** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="9a8b0-153">Modifier le contenu de hello d’un message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="9a8b0-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="9a8b0-154">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello en appelant **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="9a8b0-155">Si le message de type hello représente une tâche de travail, vous pouvez utiliser cet état de hello tooupdate la fonctionnalité de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="9a8b0-156">Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu, et il définit tooextend de délai d’attente de visibilité hello un autre 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="9a8b0-157">Cela enregistre l’état de hello de travail qui a associé à un message de type hello et il donne les client hello un autre toocontinue minute travaillant sur un message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="9a8b0-158">Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="9a8b0-159">En règle générale, vous conservez ainsi un nombre de tentatives, et si hello message est retentée plusieurs  *n*  fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="9a8b0-160">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="9a8b0-161">Options supplémentaires pour l'extraction de messages</span><span class="sxs-lookup"><span data-stu-id="9a8b0-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="9a8b0-162">Il existe deux façons de personnaliser la récupération des messages à partir d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="9a8b0-163">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="9a8b0-164">Ensuite, vous pouvez définir un délai d’attente de visibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="9a8b0-165">exemple de code suivant Hello utilise hello **getMessages** messages tooget 16 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="9a8b0-166">Ensuite, il traite chaque message à l’aide d’une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="9a8b0-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="9a8b0-167">Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="9a8b0-168">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="9a8b0-168">Get queue length</span></span>
<span data-ttu-id="9a8b0-169">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="9a8b0-170">Hello **QueueRestProxy -> getQueueMetadata** méthode demande hello file d’attente service tooreturn métadonnées sur la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="9a8b0-171">Appel hello **getApproximateMessageCount** méthode sur hello a retourné d’objet fournit un nombre du nombre de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="9a8b0-172">nombre de Hello uniquement est approximatif, car les messages peuvent être ajoutées ou supprimées une fois le service de file d’attente hello répond tooyour demande.</span><span class="sxs-lookup"><span data-stu-id="9a8b0-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="9a8b0-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="9a8b0-173">Delete a queue</span></span>
<span data-ttu-id="9a8b0-174">toodelete une file d’attente et tous les messages hello, appelez hello **QueueRestProxy -> deleteQueue** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9a8b0-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a8b0-175">Next steps</span></span>
<span data-ttu-id="9a8b0-176">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes :</span><span class="sxs-lookup"><span data-stu-id="9a8b0-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="9a8b0-177">Visitez hello [blog de l’équipe de stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="9a8b0-178">Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9a8b0-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

