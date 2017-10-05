---
title: "Prendre en main Stockage File d’attente et les services connectés de Visual Studio (services cloud) | Microsoft Docs"
description: "Comment prendre en main le stockage de files d’attente Azure dans un projet service cloud dans Visual Studio après s’être connecté à un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 7a6e58a62b4cfbf99641559363dd0c860cdf8af2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="18c10-103">Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets services cloud)</span><span class="sxs-lookup"><span data-stu-id="18c10-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="18c10-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="18c10-104">Overview</span></span>
<span data-ttu-id="18c10-105">Cet article décrit comment prendre en main Stockage File d’attente Azure dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet de services cloud via la boîte de dialogue **Ajouter des services connectés** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18c10-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="18c10-106">Nous allons vous montrer comment créer une file d’attente dans le code.</span><span class="sxs-lookup"><span data-stu-id="18c10-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="18c10-107">Nous vous indiquerons aussi comment effectuer des opérations de base sur les files d’attente, comme l’ajout, la modification, la lecture et la suppression des messages des files d’attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="18c10-108">Les exemples sont écrits en code C# et utilisent la [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="18c10-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="18c10-109">L’opération **Ajouter des services connectés** installe les packages NuGet appropriés pour accéder au stockage Azure de votre projet et ajoute la chaîne de connexion pour le compte de stockage aux fichiers de configuration de votre projet.</span><span class="sxs-lookup"><span data-stu-id="18c10-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="18c10-110">Pour plus d’informations sur l’utilisation de files d’attente dans le code, consultez [Prise en main du stockage de files d’attente Azure à l’aide de .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="18c10-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="18c10-111">Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="18c10-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="18c10-112">Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .</span><span class="sxs-lookup"><span data-stu-id="18c10-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="18c10-113">Pour plus d’informations sur la programmation d’applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .</span><span class="sxs-lookup"><span data-stu-id="18c10-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="18c10-114">Les files d’attente de stockage Azure sont un service permettant de stocker un grand nombre de messages accessibles depuis n’importe où dans le monde via des appels authentifiés avec HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="18c10-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="18c10-115">Un simple message de file d’attente peut avoir une taille de 64 Ko et une file d’attente peut contenir des millions de messages, jusqu’à la limite de capacité totale d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18c10-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="18c10-116">Accéder à des files d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="18c10-116">Access queues in code</span></span>
<span data-ttu-id="18c10-117">Pour accéder à des files d’attente dans les projets Visual Studio Cloud Services, vous devez inclure les éléments suivants dans les fichiers sources C# qui accèdent au stockage de files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="18c10-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="18c10-118">Vérifiez que les déclarations d’espace de noms figurant au début du fichier C# incluent ces instructions **using** .</span><span class="sxs-lookup"><span data-stu-id="18c10-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="18c10-119">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18c10-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="18c10-120">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure.</span><span class="sxs-lookup"><span data-stu-id="18c10-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="18c10-121">Obtenez un objet **CloudQueueClient** pour référencer les objets de file d’attente de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18c10-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="18c10-122">Obtenez un objet **CloudQueue** pour référencer une file d’attente spécifique.</span><span class="sxs-lookup"><span data-stu-id="18c10-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="18c10-123">**REMARQUE :** placez tout le code ci-dessus avant celui des exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="18c10-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="18c10-124">Créer une file d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="18c10-124">Create a queue in code</span></span>
<span data-ttu-id="18c10-125">Pour créer la file d’attente dans le code, ajoutez simplement un appel à **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="18c10-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="18c10-126">Ajout d'un message à une file d'attente</span><span class="sxs-lookup"><span data-stu-id="18c10-126">Add a message to a queue</span></span>
<span data-ttu-id="18c10-127">Pour insérer un message dans une file d’attente existante, créez un objet **CloudQueueMessage**, puis appelez la méthode **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="18c10-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="18c10-128">Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="18c10-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="18c10-129">Voici un exemple qui insère le message « Hello, World ».</span><span class="sxs-lookup"><span data-stu-id="18c10-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="18c10-130">Lire un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="18c10-130">Read a message in a queue</span></span>
<span data-ttu-id="18c10-131">Vous pouvez lire furtivement le message au début de la file d'attente sans l'enlever de la file d'attente en appelant la méthode **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="18c10-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="18c10-132">Lire et supprimer un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="18c10-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="18c10-133">Votre code permet de supprimer (retirer) un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="18c10-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="18c10-134">Lorsque vous appelez **GetMessage** , vous obtenez le message suivant au sein de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="18c10-135">Un message renvoyé par **GetMessage** devient invisible par les autres codes lisant les messages de cette file d'attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="18c10-136">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="18c10-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="18c10-137">Pour finaliser la suppression du message de la file d’attente, vous devez appeler **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="18c10-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="18c10-138">Ce processus de suppression d'un message en deux étapes garantit que, si votre code ne parvient pas à traiter un message à cause d'une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et réessayer.</span><span class="sxs-lookup"><span data-stu-id="18c10-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="18c10-139">Le code suivant appelle **DeleteMessage** juste après le traitement du message.</span><span class="sxs-lookup"><span data-stu-id="18c10-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="18c10-140">Utiliser des options supplémentaires pour traiter et supprimer des messages de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="18c10-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="18c10-141">Il existe deux façons de personnaliser la récupération des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="18c10-142">Vous pouvez obtenir un lot de messages (jusqu'à 32).</span><span class="sxs-lookup"><span data-stu-id="18c10-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="18c10-143">Vous pouvez définir un délai d'expiration de l'invisibilité plus long ou plus court afin d'accorder à votre code plus ou moins de temps pour traiter complètement chaque message.</span><span class="sxs-lookup"><span data-stu-id="18c10-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="18c10-144">L'exemple de code suivant utilise la méthode **GetMessages** pour obtenir 20 messages en un appel.</span><span class="sxs-lookup"><span data-stu-id="18c10-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="18c10-145">Ensuite, il traite chaque message à l'aide d'une boucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="18c10-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="18c10-146">Il définit également le délai d'expiration de l'invisibilité sur cinq minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="18c10-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="18c10-147">Notez que le délai de 5 minutes démarre en même temps pour tous les messages, donc une fois les 5 minutes écoulées après l'appel de **GetMessages**, tous les messages n'ayant pas été supprimés redeviennent visibles.</span><span class="sxs-lookup"><span data-stu-id="18c10-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="18c10-148">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="18c10-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="18c10-149">Obtention de la longueur de la file d'attente</span><span class="sxs-lookup"><span data-stu-id="18c10-149">Get the queue length</span></span>
<span data-ttu-id="18c10-150">Vous pouvez obtenir une estimation du nombre de messages dans une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="18c10-151">La méthode **FetchAttributes** demande au service de files d'attente d'extraire les attributs de la file d'attente, y compris le nombre de messages.</span><span class="sxs-lookup"><span data-stu-id="18c10-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="18c10-152">La propriété **ApproximateMethodCount** renvoie la dernière valeur extraite par la méthode **FetchAttributes**, sans appeler le service de File d’attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="18c10-153">Utiliser le modèle Async-Await avec les API de file d’attente commune Azure</span><span class="sxs-lookup"><span data-stu-id="18c10-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="18c10-154">Cet exemple décrit comment utiliser le modèle Async-Await avec les API de file d’attente commune Azure.</span><span class="sxs-lookup"><span data-stu-id="18c10-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="18c10-155">L’exemple appelle la version asynchrone de chacune des méthodes spécifiées, comme indiqué par le suffixe **Async** de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="18c10-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="18c10-156">Quand une méthode asynchrone est utilisée, le modèle Async-Await suspend l’exécution locale jusqu’à la fin de l’appel.</span><span class="sxs-lookup"><span data-stu-id="18c10-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="18c10-157">Ce comportement permet au thread actuel d’effectuer d'autres tâches afin d’éviter les goulots d’étranglement au niveau des performances et d’améliorer la réactivité globale de votre application.</span><span class="sxs-lookup"><span data-stu-id="18c10-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="18c10-158">Pour plus d’informations sur l’utilisation du modèle Async-Await dans .NET, consultez l’article [Programmation asynchrone avec Async et Await (C# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="18c10-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="18c10-159">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="18c10-159">Delete a queue</span></span>
<span data-ttu-id="18c10-160">Pour supprimer une file d'attente et tous les messages qu'elle contient, appelez la méthode **Delete** sur l'objet file d'attente.</span><span class="sxs-lookup"><span data-stu-id="18c10-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="18c10-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18c10-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

