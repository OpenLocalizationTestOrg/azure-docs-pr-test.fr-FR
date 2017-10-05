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
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="684a3-104">Utilisation du stockage de files d'attente à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="684a3-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="684a3-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="684a3-105">Overview</span></span>
<span data-ttu-id="684a3-106">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage des files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="684a3-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="684a3-107">Les exemples sont écrits au moyen de classes issues du Kit de développement logiciel (SDK) Windows pour PHP.</span><span class="sxs-lookup"><span data-stu-id="684a3-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="684a3-108">Les scénarios traités incluent l’insertion, la lecture furtive, la récupération et la suppression des messages de file d’attente, ainsi que la création et suppression des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="684a3-109">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="684a3-109">Create a PHP application</span></span>
<span data-ttu-id="684a3-110">Le référencement de classes issues du Kit de développement logiciel (SDK) Azure pour PHP dans votre code constitue la seule exigence pour créer une application PHP qui accède au service de File d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="684a3-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="684a3-111">Vous pouvez utiliser tous les outils de développement pour créer votre application, y compris Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="684a3-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="684a3-112">Dans ce guide, vous allez utiliser des fonctionnalités du service de File d’attente qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="684a3-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="684a3-113">Obtention des bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="684a3-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="684a3-114">Configuration de votre application pour accéder au stockage de files d’attente</span><span class="sxs-lookup"><span data-stu-id="684a3-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="684a3-115">Pour utiliser les API du stockage de files d’attente Azure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="684a3-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="684a3-116">référencer le fichier de chargeur automatique à l’aide de l’instruction [require_once] ;</span><span class="sxs-lookup"><span data-stu-id="684a3-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="684a3-117">référencer toutes les classes que vous êtes susceptible d’utiliser.</span><span class="sxs-lookup"><span data-stu-id="684a3-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="684a3-118">L'exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="684a3-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="684a3-119">Cet exemple et d’autres exemples dans cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="684a3-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="684a3-120">Si vous avez installé les bibliothèques manuellement, vous devrez référencer le fichier de chargeur automatique `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="684a3-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="684a3-121">Dans les exemples ci-dessous, l’instruction `require_once` s’affiche toujours, mais seules les classes nécessaires à l’exécution de l’exemple sont référencées.</span><span class="sxs-lookup"><span data-stu-id="684a3-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="684a3-122">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="684a3-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="684a3-123">Pour instancier un client de stockage de files d’attente Azure, vous devez disposer d’une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="684a3-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="684a3-124">Le format de la chaîne de connexion du service de File d’attente est le suivant :</span><span class="sxs-lookup"><span data-stu-id="684a3-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="684a3-125">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="684a3-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="684a3-126">Pour accéder au stockage de l’émulateur :</span><span class="sxs-lookup"><span data-stu-id="684a3-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="684a3-127">Pour créer un client de service Azure, vous devez utiliser la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="684a3-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="684a3-128">Vous pouvez utiliser une des techniques suivantes :</span><span class="sxs-lookup"><span data-stu-id="684a3-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="684a3-129">Lui passer directement la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="684a3-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="684a3-130">Utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="684a3-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="684a3-131">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="684a3-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="684a3-132">Vous pouvez ajouter de nouvelles sources via une extension de la classe **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="684a3-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="684a3-133">Dans les exemples ci-dessous, la chaîne de connexion est passée directement.</span><span class="sxs-lookup"><span data-stu-id="684a3-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="684a3-134">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="684a3-134">Create a queue</span></span>
<span data-ttu-id="684a3-135">Un objet **QueueRestProxy** vous permet de créer une file d’attente avec la méthode **createQueue**.</span><span class="sxs-lookup"><span data-stu-id="684a3-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="684a3-136">Lors de la création d'une file d'attente, vous pouvez définir des options sur cette dernière, mais vous n'y êtes pas obligé.</span><span class="sxs-lookup"><span data-stu-id="684a3-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="684a3-137">L'exemple ci-dessous illustre comment définir des métadonnées dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="684a3-138">Ne tenez pas compte de la différence entre majuscules et minuscules pour les clés de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="684a3-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="684a3-139">Toutes les clés sont lues en minuscules sur le service.</span><span class="sxs-lookup"><span data-stu-id="684a3-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="684a3-140">Ajout d'un message à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="684a3-140">Add a message to a queue</span></span>
<span data-ttu-id="684a3-141">Pour ajouter un message à une file d’attente, utilisez **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="684a3-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="684a3-142">La méthode prend le nom de la file d'attente, le texte du message et les options du message (qui sont facultatives).</span><span class="sxs-lookup"><span data-stu-id="684a3-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="684a3-143">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="684a3-143">Peek at the next message</span></span>
<span data-ttu-id="684a3-144">Vous pouvez lire furtivement un ou plusieurs messages au début d’une file d’attente sans les supprimer de la file d’attente en appelant la méthode **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="684a3-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="684a3-145">Par défaut, la méthode **peekMessage** renvoie un seul message, mais vous pouvez modifier cette valeur à l’aide de la méthode **PeekMessagesOptions->setNumberOfMessages**.</span><span class="sxs-lookup"><span data-stu-id="684a3-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="684a3-146">Enlèvement du message suivant de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="684a3-146">De-queue the next message</span></span>
<span data-ttu-id="684a3-147">Votre code supprime un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="684a3-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="684a3-148">Tout d’abord, vous appelez **QueueRestProxy->listMessages**, ce qui rend le message invisible à tout autre code lu à partir de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="684a3-149">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="684a3-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="684a3-150">(Si le message n’est pas supprimé pendant cette période, il redevient visible dans la file d’attente). Pour finaliser la suppression du message de la file d’attente, vous devez appeler **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="684a3-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="684a3-151">Ce processus de suppression d’un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="684a3-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="684a3-152">Votre code appelle **deleteMessage** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="684a3-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="684a3-153">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="684a3-153">Change the contents of a queued message</span></span>
<span data-ttu-id="684a3-154">Vous pouvez modifier le contenu d’un message placé dans la file d’attente en appelant **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="684a3-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="684a3-155">Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="684a3-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="684a3-156">Le code suivant met à jour le message de la file d’attente avec un nouveau contenu et ajoute 60 secondes au délai d’expiration de la visibilité.</span><span class="sxs-lookup"><span data-stu-id="684a3-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="684a3-157">Cette opération enregistre l’état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message.</span><span class="sxs-lookup"><span data-stu-id="684a3-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="684a3-158">Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="684a3-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="684a3-159">Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de *n* fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="684a3-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="684a3-160">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="684a3-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="684a3-161">Options supplémentaires pour l'extraction de messages</span><span class="sxs-lookup"><span data-stu-id="684a3-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="684a3-162">Il existe deux façons de personnaliser la récupération des messages à partir d’une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="684a3-163">Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="684a3-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="684a3-164">Deuxièmement, vous pouvez définir un délai d'expiration de la visibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="684a3-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="684a3-165">L'exemple de code suivant utilise la méthode **getMessages** pour obtenir 16 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="684a3-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="684a3-166">Ensuite, il traite chaque message à l’aide d’une boucle **for** .</span><span class="sxs-lookup"><span data-stu-id="684a3-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="684a3-167">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="684a3-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="684a3-168">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="684a3-168">Get queue length</span></span>
<span data-ttu-id="684a3-169">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="684a3-170">La méthode **QueueRestProxy->getQueueMetadata** demande au service de file d’attente de renvoyer les métadonnées relatives à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="684a3-171">Appeler la méthode **getApproximateMessageCount** sur l'objet renvoyé permet d'obtenir le nombre de messages figurant dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="684a3-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="684a3-172">Ce nombre est approximatif étant donné que des messages peuvent être ajoutés ou supprimés une fois que le service de File d'attente a répondu à votre demande.</span><span class="sxs-lookup"><span data-stu-id="684a3-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="684a3-173">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="684a3-173">Delete a queue</span></span>
<span data-ttu-id="684a3-174">Pour supprimer une file d’attente et tous les messages qu’elle contient, appelez la méthode **QueueRestProxy->deleteQueue**.</span><span class="sxs-lookup"><span data-stu-id="684a3-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="684a3-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="684a3-175">Next steps</span></span>
<span data-ttu-id="684a3-176">Maintenant que vous connaissez les bases du stockage des files d’attente Azure, consultez les liens suivants pour apprendre à effectuer des tâches de stockage plus complexes :</span><span class="sxs-lookup"><span data-stu-id="684a3-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="684a3-177">Consultez le [blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="684a3-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="684a3-178">Pour plus d’informations, consultez également le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="684a3-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

