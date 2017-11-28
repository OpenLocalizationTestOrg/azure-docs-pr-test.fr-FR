---
title: "Prise en main du stockage de files d’attente Azure à l’aide de .NET | Microsoft Docs"
description: "Les files d’attente Azure fournissent une messagerie asynchrone fiable entre les composants d’application. La messagerie cloud permet de mettre à l’échelle vos composants d’application indépendamment."
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
ms.openlocfilehash: 7f88aa9c50e669d1be7248346c7b1176bce61249
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="37380-104">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="37380-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="37380-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="37380-105">Overview</span></span>
<span data-ttu-id="37380-106">Le stockage de files d’attente Azure fournit une messagerie cloud entre les composants d’application.</span><span class="sxs-lookup"><span data-stu-id="37380-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="37380-107">Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment.</span><span class="sxs-lookup"><span data-stu-id="37380-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="37380-108">Le stockage de files d’attente offre une messagerie asynchrone pour la communication entre les composants d’application, qu’ils soient exécutés dans le cloud, sur le bureau, sur un serveur local ou sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="37380-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="37380-109">Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.</span><span class="sxs-lookup"><span data-stu-id="37380-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="37380-110">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="37380-110">About this tutorial</span></span>
<span data-ttu-id="37380-111">Ce didacticiel montre comment écrire du code .NET pour des scénarios courants d’utilisation du stockage de files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="37380-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="37380-112">Les scénarios traités sont les suivants : création et suppression de files d’attente, et ajout, lecture et suppression des messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="37380-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="37380-113">**Durée estimée :** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="37380-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="37380-114">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="37380-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="37380-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37380-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="37380-116">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="37380-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="37380-117">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="37380-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="37380-118">Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="37380-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="37380-119">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="37380-119">Add using directives</span></span>
<span data-ttu-id="37380-120">Ajoutez les directives `using` suivantes au fichier `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="37380-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="37380-121">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="37380-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="37380-122">Création du client du service Queue</span><span class="sxs-lookup"><span data-stu-id="37380-122">Create the Queue service client</span></span>
<span data-ttu-id="37380-123">La classe **CloudQueueClient** vous permet de récupérer des files d’attente stockées dans Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="37380-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="37380-124">Voici un moyen de créer le client du service :</span><span class="sxs-lookup"><span data-stu-id="37380-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="37380-125">Vous êtes maintenant prêt à écrire du code qui lit et écrit des données dans le Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="37380-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="37380-126">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="37380-126">Create a queue</span></span>
<span data-ttu-id="37380-127">Cet exemple montre comment créer une file d’attente, si elle n’existe pas encore :</span><span class="sxs-lookup"><span data-stu-id="37380-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="37380-128">Insertion d'un message dans une file d'attente</span><span class="sxs-lookup"><span data-stu-id="37380-128">Insert a message into a queue</span></span>
<span data-ttu-id="37380-129">Pour insérer un message dans une file d'attente existante, commencez par créer un **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="37380-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="37380-130">Appelez ensuite la méthode **AddMessage** .</span><span class="sxs-lookup"><span data-stu-id="37380-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="37380-131">Un **CloudQueueMessage** peut être créé à partir d’une chaîne (au format UTF-8) ou d’un tableau **d’octets**.</span><span class="sxs-lookup"><span data-stu-id="37380-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="37380-132">Voici le code qui crée une file d'attente (si elle n'existe pas) et insère le message « Hello, World » :</span><span class="sxs-lookup"><span data-stu-id="37380-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="37380-133">Lecture furtive du message suivant</span><span class="sxs-lookup"><span data-stu-id="37380-133">Peek at the next message</span></span>
<span data-ttu-id="37380-134">Vous pouvez lire furtivement le message au début de la file d'attente sans l'enlever de la file d'attente en appelant la méthode **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="37380-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="37380-135">Modification du contenu d'un message en file d'attente</span><span class="sxs-lookup"><span data-stu-id="37380-135">Change the contents of a queued message</span></span>
<span data-ttu-id="37380-136">Vous pouvez modifier le contenu d'un message placé dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="37380-137">Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour l'état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="37380-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="37380-138">Le code suivant met à jour le message de la file d'attente avec un nouveau contenu et ajoute 60 secondes au délai d'expiration de la visibilité.</span><span class="sxs-lookup"><span data-stu-id="37380-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="37380-139">Cette opération enregistre l'état de la tâche associée au message et accorde une minute supplémentaire au client pour traiter le message.</span><span class="sxs-lookup"><span data-stu-id="37380-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="37380-140">Vous pouvez utiliser cette technique pour suivre des flux de travail à plusieurs étapes sur les messages de file d'attente, sans devoir reprendre du début si une étape du traitement échoue à cause d'une défaillance matérielle ou logicielle.</span><span class="sxs-lookup"><span data-stu-id="37380-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="37380-141">Normalement, vous conservez aussi un nombre de nouvelles tentatives et si le message est retenté plus de *n* fois, vous le supprimez.</span><span class="sxs-lookup"><span data-stu-id="37380-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="37380-142">Cela protège du déclenchement d'une erreur d'application par un message chaque fois qu'il est traité.</span><span class="sxs-lookup"><span data-stu-id="37380-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="37380-143">Enlèvement du message suivant de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="37380-143">De-queue the next message</span></span>
<span data-ttu-id="37380-144">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="37380-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="37380-145">Lorsque vous appelez **GetMessage**, vous obtenez le message suivant dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="37380-146">Un message renvoyé par **GetMessage** devient invisible par les autres codes lisant les messages de cette file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="37380-147">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="37380-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="37380-148">Pour finaliser la suppression du message de la file d'attente, vous devez aussi appeler **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="37380-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="37380-149">Ce processus de suppression d'un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d'une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="37380-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="37380-150">Votre code appelle **DeleteMessage** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="37380-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="37380-151">Utiliser le modèle Async-Await avec les API de stockage de files d’attente communes</span><span class="sxs-lookup"><span data-stu-id="37380-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="37380-152">Cet exemple décrit comment utiliser le modèle Async-Await avec les API de stockage de files d’attente communes.</span><span class="sxs-lookup"><span data-stu-id="37380-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="37380-153">L’exemple appelle la version asynchrone de chacune des méthodes spécifiées, comme l’indique le suffixe *Async* de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="37380-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="37380-154">Quand une méthode asynchrone est utilisée, le modèle Async-Await suspend l’exécution locale jusqu’à la fin de l’appel.</span><span class="sxs-lookup"><span data-stu-id="37380-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="37380-155">Ce comportement permet au thread actuel d’effectuer d’autres tâches afin d’éviter les goulots d’étranglement au niveau des performances et d’améliorer la réactivité globale de votre application.</span><span class="sxs-lookup"><span data-stu-id="37380-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="37380-156">Pour plus d’informations sur l’utilisation du modèle Async-Await dans .NET, consultez l’article [Programmation asynchrone avec Async et Await (C# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="37380-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="37380-157">Utilisation d’options supplémentaires pour l’enlèvement des messages</span><span class="sxs-lookup"><span data-stu-id="37380-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="37380-158">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="37380-159">Premièrement, vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="37380-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="37380-160">Deuxièmement, vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="37380-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="37380-161">L'exemple de code suivant utilise la méthode **GetMessages** pour obtenir 20 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="37380-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="37380-162">Ensuite, il traite chaque message à l'aide d'une boucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="37380-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="37380-163">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="37380-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="37380-164">Notez que le délai de 5 minutes démarre en même temps pour tous les messages, donc une fois les 5 minutes écoulées après l'appel de **GetMessages**, tous les messages n'ayant pas été supprimés redeviennent visibles.</span><span class="sxs-lookup"><span data-stu-id="37380-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="37380-165">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="37380-165">Get the queue length</span></span>
<span data-ttu-id="37380-166">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="37380-167">La méthode **FetchAttributes** demande au service de files d'attente d'extraire les attributs de la file d'attente, y compris le nombre de messages.</span><span class="sxs-lookup"><span data-stu-id="37380-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="37380-168">La propriété **ApproximateMessageCount** renvoie la dernière valeur extraite par la méthode **FetchAttributes**, sans appeler le service de files d’attente.</span><span class="sxs-lookup"><span data-stu-id="37380-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="37380-169">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="37380-169">Delete a queue</span></span>
<span data-ttu-id="37380-170">Pour supprimer une file d'attente et tous les messages qu'elle contient, appelez la méthode **Delete** sur l'objet file d'attente.</span><span class="sxs-lookup"><span data-stu-id="37380-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="37380-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37380-171">Next steps</span></span>
<span data-ttu-id="37380-172">Maintenant que vous connaissez les bases du stockage des files d'attente, consultez les liens suivants pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="37380-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="37380-173">Pour plus d'informations sur les API disponibles, consultez la documentation de référence des services de files d'attente :</span><span class="sxs-lookup"><span data-stu-id="37380-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="37380-174">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="37380-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="37380-175">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="37380-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="37380-176">Découvrez comment simplifier le code que vous écrivez avec Azure Storage, à l’aide du [Kit de développement logiciel (SDK) Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="37380-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="37380-177">Pour plus d’informations sur les autres options de stockage de données dans Azure, consultez d’autres guides de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="37380-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="37380-178">[Prise en main du stockage de tables Azure à l’aide de .NET](storage-dotnet-how-to-use-tables.md) pour le stockage de données structurées.</span><span class="sxs-lookup"><span data-stu-id="37380-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="37380-179">[Prise en main d’Azure Blob Storage à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) pour le stockage de données non structurées.</span><span class="sxs-lookup"><span data-stu-id="37380-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="37380-180">[Connexion à SQL Database à l’aide de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) pour stocker des données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="37380-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
