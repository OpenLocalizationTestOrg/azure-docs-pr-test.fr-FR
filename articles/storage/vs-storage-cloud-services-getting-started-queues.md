---
title: "aaaGet démarré avec Visual Studio et le stockage de file d’attente des services connectés (services de cloud computing) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans un projet de service cloud dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="6fe7c-103">Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets services cloud)</span><span class="sxs-lookup"><span data-stu-id="6fe7c-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6fe7c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6fe7c-104">Overview</span></span>
<span data-ttu-id="6fe7c-105">Cet article décrit comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet de services cloud à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="6fe7c-106">Nous allons vous montrer comment toocreate une file d’attente dans le code.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="6fe7c-107">Nous allons également vous montrer comment tooperform basic file d’attente des opérations, telles que l’ajout, modification, lecture et suppression des messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="6fe7c-108">les exemples de Hello sont écrits en code c# et utilisez hello [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fe7c-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="6fe7c-109">Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="6fe7c-110">Pour plus d’informations sur l’utilisation de files d’attente dans le code, consultez [Prise en main du stockage de files d’attente Azure à l’aide de .NET](storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="6fe7c-111">Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="6fe7c-112">Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="6fe7c-113">Pour plus d’informations sur la programmation des applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="6fe7c-114">Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="6fe7c-115">Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="6fe7c-116">Accéder à des files d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="6fe7c-116">Access queues in code</span></span>
<span data-ttu-id="6fe7c-117">tooaccess files d’attente dans les projets Visual Studio Cloud Services, vous devez suivant de hello tooinclude fichier source tooany c# éléments accéder au stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="6fe7c-118">Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="6fe7c-119">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6fe7c-120">Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="6fe7c-121">Obtenir un **CloudQueueClient** tooreference objets de file d’attente hello dans votre compte de stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="6fe7c-122">Obtenir un **CloudQueue** tooreference une file d’attente spécifique de l’objet.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="6fe7c-123">**Remarque :** utilisent les hello ci-dessus code devant les code hello dans hello suivant des exemples.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="6fe7c-124">Créer une file d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="6fe7c-124">Create a queue in code</span></span>
<span data-ttu-id="6fe7c-125">file d’attente de hello toocreate dans le code, ajoutez simplement un appel trop**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="6fe7c-126">Ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="6fe7c-126">Add a message tooa queue</span></span>
<span data-ttu-id="6fe7c-127">tooinsert un message dans une file d’attente existante, créer un nouveau **CloudQueueMessage** objet, puis appel hello **AddMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6fe7c-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="6fe7c-128">Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="6fe7c-129">Voici un exemple qui insère des message de type hello « Hello, World ».</span><span class="sxs-lookup"><span data-stu-id="6fe7c-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="6fe7c-130">Lire un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="6fe7c-130">Read a message in a queue</span></span>
<span data-ttu-id="6fe7c-131">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **PeekMessage** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6fe7c-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="6fe7c-132">Lire et supprimer un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="6fe7c-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="6fe7c-133">Votre code permet de supprimer (retirer) un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="6fe7c-134">Appelez **GetMessage** tooget message suivant dans une file d’attente de type hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="6fe7c-135">Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="6fe7c-136">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="6fe7c-137">toofinish suppression de message de type hello à partir de la file d’attente hello, appelez **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="6fe7c-138">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="6fe7c-139">code Hello suivant appelle **DeleteMessage** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="6fe7c-140">Utilisez les options supplémentaires tooprocess et supprimer les messages de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="6fe7c-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="6fe7c-141">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="6fe7c-142">Vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="6fe7c-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="6fe7c-143">Vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="6fe7c-144">code Hello suivant utilise le **GetMessages** messages tooget 20 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="6fe7c-145">Ensuite, il traite chaque message à l'aide d'une boucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="6fe7c-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="6fe7c-146">Il définit également hello invisibilité délai d’expiration toofive minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="6fe7c-147">Notez que hello 5 minutes démarre pour tous les messages à hello même moment, après que les 5 minutes se sont écoulées depuis l’appel de hello trop**GetMessages**, tous les messages qui n’ont pas été supprimés devient visibles à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="6fe7c-148">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="6fe7c-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="6fe7c-149">Obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="6fe7c-149">Get hello queue length</span></span>
<span data-ttu-id="6fe7c-150">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="6fe7c-151">Le **FetchAttributes** méthode vous demande de service de file d’attente hello pour récupérer les attributs de file d’attente hello, y compris le nombre de messages hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="6fe7c-152">Hello **ApproximateMethodCount** propriété renvoie hello dernière valeur récupérée par le **FetchAttributes** (méthode), sans avoir à contacter le service de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="6fe7c-153">Utilisez hello Async-Await un modèle avec l’API de file d’attente Azure courantes</span><span class="sxs-lookup"><span data-stu-id="6fe7c-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="6fe7c-154">Cet exemple montre comment hello toouse Async-Await de modèle avec l’API de file d’attente Azure courantes.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="6fe7c-155">exemple Hello appelle la version asynchrone de hello de chacune des hello donné des méthodes, ceci peut être observé par hello **Async** après correction de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="6fe7c-156">Quand une méthode async est utilisé hello async-await modèle suspend l’exécution locale jusqu'à ce que la fin de l’appel hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="6fe7c-157">Ce comportement permet à toodo de thread actuel hello autre travail qui permet d’éviter les goulots d’étranglement et améliore la réactivité globale de votre application de hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="6fe7c-158">Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET consultez [Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="6fe7c-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="6fe7c-159">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="6fe7c-159">Delete a queue</span></span>
<span data-ttu-id="6fe7c-160">toodelete une file d’attente et tous les messages hello qu’il contient, appel hello **supprimer** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="6fe7c-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="6fe7c-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fe7c-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

