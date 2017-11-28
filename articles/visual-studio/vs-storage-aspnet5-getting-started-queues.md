---
title: "aaaGet en main de Visual Studio et de stockage de la file d’attente des services connectés (ASP.NET Core) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage de file d’attente Azure dans un projet ASP.NET Core dans Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="cc0c0-103">Bien démarrer avec Stockage File d’attente et les services connectés de Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="cc0c0-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="cc0c0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cc0c0-104">Overview</span></span>
<span data-ttu-id="cc0c0-105">Cet article décrit comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans Visual Studio après avoir créé ou référencé un compte de stockage Azure dans un projet ASP.NET Core à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="cc0c0-106">Hello **ajouter des Services connectés** opération installe hello approprié NuGet packages tooaccess stockage Azure dans votre projet et ajoute la chaîne de connexion hello pour hello du compte de stockage tooyour les fichiers de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="cc0c0-107">Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="cc0c0-108">Un message de la file d’attente unique peut être de taille too64 kilo-octets (Ko), et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="cc0c0-109">tooget démarré, vous devez toocreate une file d’attente Azure dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="cc0c0-110">Nous allons vous montrer comment toocreate une file d’attente dans le code.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="cc0c0-111">Nous allons également vous montrer comment tooperform basic file d’attente des opérations, telles que l’ajout, modification, lecture et suppression des messages de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="cc0c0-112">exemples de Hello sont écrits en C\# de code et d’utiliser hello bibliothèque cliente de stockage Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="cc0c0-113">Pour plus d’informations sur ASP.NET, voir le site [ASP.NET](http://www.asp.net)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="cc0c0-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="cc0c0-114">**Remarque :** certaines hello API qui effectuent des appels tooAzure stockage dans ASP.NET Core sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="cc0c0-115">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="cc0c0-116">code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="cc0c0-117">Pour plus d’informations sur la manipulation des files d’attente par programme, consultez la page [Prise en main du stockage de files d’attente Azure à l’aide de .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-117">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="cc0c0-118">Pour des informations générales sur Azure Storage, consultez la [documentation relative au stockage](https://azure.microsoft.com/documentation/services/storage/) .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="cc0c0-119">Pour des informations générales sur les services cloud Azure, consultez la [documentation des services cloud](https://azure.microsoft.com/documentation/services/cloud-services/) .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="cc0c0-120">Pour plus d’informations sur la programmation des applications ASP.NET, consultez la page [ASP.NET](http://www.asp.net) .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="cc0c0-121">Accéder à des files d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="cc0c0-121">Access queues in code</span></span>
<span data-ttu-id="cc0c0-122">tooaccess files d’attente dans les projets ASP.NET Core, vous devez suivant de hello tooinclude les fichiers source des éléments tooany c# qui accède au stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="cc0c0-123">Assurez-vous que les déclarations d’espace de noms hello haut hello du fichier de hello c# incluent ces **à l’aide de** instructions.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="cc0c0-124">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cc0c0-125">Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="cc0c0-126">Obtenir un **CloudQueueClient** tooreference objets de file d’attente hello dans votre compte de stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="cc0c0-127">Obtenir un **CloudQueue** tooreference une file d’attente spécifique de l’objet.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="cc0c0-128">**Remarque :** utilisent les hello ci-dessus code devant les code hello dans hello suivant des exemples.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="cc0c0-129">Créer une file d’attente dans le code</span><span class="sxs-lookup"><span data-stu-id="cc0c0-129">Create a queue in code</span></span>
<span data-ttu-id="cc0c0-130">toocreate hello file d’attente Azure dans le code, ajoutez simplement un appel trop**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="cc0c0-131">Ajouter une file d’attente de messages tooa</span><span class="sxs-lookup"><span data-stu-id="cc0c0-131">Add a message tooa queue</span></span>
<span data-ttu-id="cc0c0-132">tooinsert un message dans une file d’attente existante, créer un nouveau **CloudQueueMessage** objet, puis appel hello **AddMessageAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="cc0c0-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="cc0c0-133">Un objet **CloudQueueMessage** peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="cc0c0-134">Voici un exemple qui insère des message de type hello « Hello, World ».</span><span class="sxs-lookup"><span data-stu-id="cc0c0-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="cc0c0-135">Lire un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="cc0c0-135">Read a message in a queue</span></span>
<span data-ttu-id="cc0c0-136">Vous pouvez lire de message hello devant hello une file d’attente sans le supprimer de la file d’attente hello en appelant hello **PeekMessageAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="cc0c0-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="cc0c0-137">Lire et supprimer un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="cc0c0-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="cc0c0-138">Votre code permet de supprimer (retirer) un message d’une file d’attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="cc0c0-139">Appelez **GetMessageAsync** tooget message suivant dans une file d’attente de type hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="cc0c0-140">Un message retourné à partir de **GetMessageAsync** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="cc0c0-141">Par défaut, ce message reste invisible pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="cc0c0-142">toofinish suppression de message de type hello à partir de la file d’attente hello, appelez **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="cc0c0-143">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="cc0c0-144">code Hello suivant appelle **DeleteMessageAsync** avec le bouton droit une fois le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="cc0c0-145">des options supplémentaires pour l'enlèvement des messages</span><span class="sxs-lookup"><span data-stu-id="cc0c0-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="cc0c0-146">Il existe deux façons de personnaliser l'extraction des messages à partir d'une file d'attente.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="cc0c0-147">Tout d’abord, vous pouvez obtenir un lot de messages (haut too32).</span><span class="sxs-lookup"><span data-stu-id="cc0c0-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="cc0c0-148">Ensuite, vous pouvez définir un délai d’attente de l’invisibilité plus ou moins longtemps, ce qui permet de votre code plus ou moins toofully temps traitent chaque message.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="cc0c0-149">code Hello suivant utilise le **GetMessages** messages tooget 20 de méthode dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="cc0c0-150">Ensuite, il traite chaque message à l'aide d'une boucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="cc0c0-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="cc0c0-151">Il définit également hello invisibilité délai d’expiration too5 minutes pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="cc0c0-152">Remarque que début de 5 minutes hello pour tous les messages à hello même temps, après 5 minutes après l’appel de hello trop**GetMessages**, tous les messages qui n’ont pas été supprimés devient visibles.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="cc0c0-153">Obtenir la longueur de file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="cc0c0-153">Get hello queue length</span></span>
<span data-ttu-id="cc0c0-154">Vous pouvez obtenir une estimation du nombre de hello de messages dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="cc0c0-155">Le **FetchAttributes** méthode vous demande de service de file d’attente hello pour récupérer les attributs de file d’attente hello, y compris le nombre de messages hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="cc0c0-156">Hello **ApproximateMethodCount** propriété renvoie hello dernière valeur récupérée par le **FetchAttributes** (méthode), sans avoir à contacter le service de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="cc0c0-157">Utiliser le modèle de hello Async-Await avec l’API de file d’attente commune</span><span class="sxs-lookup"><span data-stu-id="cc0c0-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="cc0c0-158">Cet exemple montre comment toouse hello Async-Await de modèle avec l’API de file d’attente commune.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="cc0c0-159">Hello exemple appels hello async version de chacun de hello donné de méthodes.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="cc0c0-160">Ceci peut être observé par POST-correctif de hello asynchrone de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="cc0c0-161">Lorsqu’une méthode async est utilisée, modèle de hello Async-Await suspend l’exécution locale avant la fin de l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="cc0c0-162">Ce comportement permet à toodo de thread actuel hello autre travail qui permet d’éviter les goulots d’étranglement et améliore la réactivité globale de votre application de hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="cc0c0-163">Pour plus d’informations sur l’utilisation de hello modèle Async-Await dans .NET, consultez [Async et Await (c# et Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="cc0c0-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="cc0c0-164">Suppression d'une file d'attente</span><span class="sxs-lookup"><span data-stu-id="cc0c0-164">Delete a queue</span></span>
<span data-ttu-id="cc0c0-165">toodelete une file d’attente et tous les messages hello qu’il contient, appelez le **supprimer** méthode sur un objet de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="cc0c0-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="cc0c0-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc0c0-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

