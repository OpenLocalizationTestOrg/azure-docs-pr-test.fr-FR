---
title: "aaaGet main du stockage de file d’attente Azure à l’aide de .NET | Documents Microsoft"
description: "Les files d’attente Azure fournissent une messagerie asynchrone fiable entre les composants d’application. Le cloud permet de messagerie votre tooscale de composants d’application indépendamment."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="7f3a2-104">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="7f3a2-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="7f3a2-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7f3a2-105">Overview</span></span>
<span data-ttu-id="7f3a2-106">Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="7f3a2-107">Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="7f3a2-108">Stockage de file d’attente fournit une messagerie asynchrone pour la communication entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="7f3a2-109">Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="7f3a2-110">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="7f3a2-110">About this tutorial</span></span>
<span data-ttu-id="7f3a2-111">Ce didacticiel montre comment le code toowrite .NET pour les scénarios courants lors de l’utilisation du stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="7f3a2-112">Les scénarios traités sont les suivants : création et suppression de files d’attente, et ajout, lecture et suppression des messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="7f3a2-113">**Estimation du temps toocomplete :** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="7f3a2-114">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="7f3a2-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f3a2-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="7f3a2-116">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="7f3a2-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="7f3a2-117">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="7f3a2-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="7f3a2-118">Un [compte de stockage Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="7f3a2-119">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="7f3a2-119">Add using directives</span></span>
<span data-ttu-id="7f3a2-120">Ajoutez hello suivant `using` haut toohello de directives de hello `Program.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="7f3a2-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="7f3a2-121">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="7f3a2-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="7f3a2-122">Créer le client du service de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="7f3a2-122">Create hello Queue service client</span></span>
<span data-ttu-id="7f3a2-123">Hello **CloudQueueClient** classe permet de vous tooretrieve les files d’attente stockés dans le stockage de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="7f3a2-124">Voici un moyen toocreate hello service client :</span><span class="sxs-lookup"><span data-stu-id="7f3a2-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="7f3a2-125">Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooQueue.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="7f3a2-126">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="7f3a2-126">Create a queue</span></span>
<span data-ttu-id="7f3a2-127">Cet exemple montre comment toocreate une file d’attente si elle n’existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="7f3a2-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="7f3a2-128">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="7f3a2-128">Insert a message into a queue</span></span>
<span data-ttu-id="7f3a2-129">tooinsert un message dans une file d’attente existante, commencez par créer un **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="7f3a2-130">Ensuite, appelez hello **AddMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="7f3a2-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="7f3a2-131">Un **CloudQueueMessage** peut être créé à partir d’une chaîne (au format UTF-8) ou d’un tableau **d’octets**.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="7f3a2-132">Voici le code qui crée une file d’attente (s’il n’existe pas) et le message de type hello insertions « Hello, World » :</span><span class="sxs-lookup"><span data-stu-id="7f3a2-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="7f3a2-133">Lire des message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="7f3a2-133">Peek at hello next message</span></span>
<span data-ttu-id="7f3a2-134">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **PeekMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="7f3a2-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="7f3a2-135">Modifier le contenu de hello d’un message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="7f3a2-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="7f3a2-136">Vous pouvez modifier le contenu de hello d’un message en place dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="7f3a2-137">Si le message représente une tâche de travail, vous pouvez utiliser cette fonctionnalité de tooupdate l’état de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="7f3a2-138">Hello suivant code met à jour le message de file d’attente hello avec le nouveau contenu et jeux hello tooextend de délai d’attente de visibilité un autre 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="7f3a2-139">Cela enregistre l’état hello du travail associé au message de type hello, ainsi que les clients hello un autre toocontinue minute travaillant sur un message de type hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="7f3a2-140">Vous pouvez utiliser ce flux de travail à plusieurs étapes de tootrack technique sur les messages de la file d’attente, sans avoir toostart sur du début de hello si une étape de traitement échoue en raison de l’erreur toohardware ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="7f3a2-141">En règle générale, vous conservez ainsi un nombre de tentatives, et si hello message est retentée plusieurs  *n*  fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="7f3a2-142">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="7f3a2-143">File d’attente message de type hello suivant</span><span class="sxs-lookup"><span data-stu-id="7f3a2-143">De-queue hello next message</span></span>
<span data-ttu-id="7f3a2-144">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="7f3a2-145">Lorsque vous appelez **GetMessage**, vous obtenez un message de type hello suivante dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="7f3a2-146">Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="7f3a2-147">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="7f3a2-148">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="7f3a2-149">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="7f3a2-150">Votre code appelle **DeleteMessage** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="7f3a2-151">Utiliser le modèle Async-Await avec les API de stockage de files d’attente communes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="7f3a2-152">Cet exemple montre comment hello toouse Async-Await de modèle avec l’API de stockage de file d’attente commun.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="7f3a2-153">exemple Hello appelle la version asynchrone de hello de chacune des hello donné des méthodes, comme indiqué par hello *Async* suffixe de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="7f3a2-154">Lorsqu’une méthode async est utilisée, hello async-await modèle suspend l’exécution locale jusqu'à ce que la fin de l’appel hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="7f3a2-155">Ce comportement permet à toodo de thread actuel hello autre travail, ce qui permet d’éviter les goulots d’étranglement et améliore la réactivité globale de votre application de hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="7f3a2-156">Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET consultez [Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="7f3a2-157">Utilisation d’options supplémentaires pour l’enlèvement des messages</span><span class="sxs-lookup"><span data-stu-id="7f3a2-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="7f3a2-158">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="7f3a2-159">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="7f3a2-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="7f3a2-160">Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="7f3a2-161">code Hello suivant utilise le **GetMessages** messages tooget 20 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="7f3a2-162">Ensuite, il traite chaque message à l'aide d'une boucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="7f3a2-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="7f3a2-163">Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="7f3a2-164">Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**GetMessages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="7f3a2-165">Obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="7f3a2-165">Get hello queue length</span></span>
<span data-ttu-id="7f3a2-166">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="7f3a2-167">Le **FetchAttributes** méthode vous demande de service de file d’attente hello pour récupérer les attributs de file d’attente hello, y compris le nombre de messages hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="7f3a2-168">Hello **ApproximateMessageCount** propriété renvoie hello dernière valeur récupérée par le **FetchAttributes** (méthode), sans avoir à contacter le service de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="7f3a2-169">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="7f3a2-169">Delete a queue</span></span>
<span data-ttu-id="7f3a2-170">toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **supprimer** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="7f3a2-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-171">Next steps</span></span>
<span data-ttu-id="7f3a2-172">Maintenant que vous avez appris les notions de base de hello de stockage de la file d’attente, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="7f3a2-173">Afficher la documentation de référence de service de file d’attente hello pour plus d’informations sur les API disponibles :</span><span class="sxs-lookup"><span data-stu-id="7f3a2-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="7f3a2-174">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="7f3a2-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="7f3a2-175">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="7f3a2-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="7f3a2-176">En savoir plus toosimplify hello code que vous écrivez est comment toowork avec le stockage Azure à l’aide de hello [Kit de développement logiciel Azure WebJobs](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7f3a2-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="7f3a2-177">Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="7f3a2-178">[Prise en main le stockage de Table Azure à l’aide de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore des données structurées.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="7f3a2-179">[Prise en main le stockage Blob Azure à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore des données non structurées.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="7f3a2-180">[Se connecter tooSQL de base de données à l’aide de .NET (c#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore des données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
