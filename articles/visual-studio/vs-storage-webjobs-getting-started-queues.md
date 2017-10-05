---
title: "Prise en main du stockage File d’attente et des services connectés Visual Studio (projets WebJob) | Microsoft Docs"
description: "Comment commencer à utiliser le stockage de files d'attente Azure dans un projet WebJob après la connexion à un compte Azure Storage à l'aide des services connectés Visual Studio."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ef40db782114bfdaa02dafeabcfc6da6c41423e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="54280-103">Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets WebJob)</span><span class="sxs-lookup"><span data-stu-id="54280-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="54280-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="54280-104">Overview</span></span>
<span data-ttu-id="54280-105">Cet article explique comment prendre en main Stockage File d’attente Azure dans un projet WebJob Visual Studio Azure après avoir créé ou référencé un compte de stockage Azure à l’aide de la boîte de dialogue **Ajouter des services connectés** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54280-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="54280-106">Quand vous ajoutez un compte de stockage à un projet de tâche web à l’aide de la boîte de dialogue **Ajouter des services connectés** de Visual Studio, le package NuGet d’Azure Storage approprié est installé, les références .NET appropriées sont ajoutées au projet et les chaînes de connexion pour le compte de stockage sont mises à jour dans le fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="54280-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="54280-107">Cet article fournit des exemples de code C# qui indiquent comment utiliser la version 1.x du Kit de développement logiciel (SDK) WebJobs Azure avec le service de stockage de files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="54280-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="54280-108">Les files d’attente de stockage Azure sont un service permettant de stocker un grand nombre de messages accessibles depuis n’importe où dans le monde via des appels authentifiés avec HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54280-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="54280-109">Un simple message de file d’attente peut avoir une taille de 64 Ko et une file d’attente peut contenir des millions de messages, jusqu’à la limite de capacité totale d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54280-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="54280-110">Pour plus d’informations, consultez la section [Prise en main d’Azure Queue Storage à l’aide de .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="54280-110">See [Get started with Azure Queue Storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="54280-111">Pour plus d’informations sur ASP.NET, voir le site [ASP.NET](http://www.asp.net)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="54280-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="54280-112">Déclenchement d'une fonction à la réception d'un message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="54280-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="54280-113">Pour écrire une fonction que le Kit de développement logiciel (SDK) WebJobs appelle durant la réception d'un message en file d'attente, utilisez l'attribut **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="54280-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="54280-114">Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom de la file d’attente à interroger.</span><span class="sxs-lookup"><span data-stu-id="54280-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="54280-115">Pour découvrir comment définir de manière dynamique le nom de la file d’attente, consultez la section [Définition des options de configuration](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="54280-116">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="54280-116">String queue messages</span></span>
<span data-ttu-id="54280-117">Dans l’exemple suivant, la file d’attente contient un message de chaîne, ainsi **QueueTrigger** est appliqué à un paramètre de chaîne nommé **logMessage** qui renferme le contenu du message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54280-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="54280-118">La fonction [écrit un message de journal dans le tableau de bord](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="54280-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="54280-119">Outre **string**, le paramètre peut être un tableau d’octets, un objet **CloudQueueMessage** ou un objet POCO que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="54280-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="54280-120">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="54280-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="54280-121">Dans l’exemple suivant, le message de file d’attente contient JSON pour un objet **BlobInformation** qui inclut une propriété **BlobName**.</span><span class="sxs-lookup"><span data-stu-id="54280-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="54280-122">Le Kit de développement logiciel (SDK) désérialise automatiquement l’objet.</span><span class="sxs-lookup"><span data-stu-id="54280-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="54280-123">Le Kit de développement logiciel (SDK) utilise le package [NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) pour sérialiser et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="54280-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="54280-124">Si vous créez des messages en file d’attente dans un programme qui n’utilise pas le Kit de développement logiciel (SDK) WebJobs, vous pouvez écrire le code comme dans l’exemple suivant, afin de créer un message en file d’attente POCO que le Kit de développement logiciel (SDK) peut analyser.</span><span class="sxs-lookup"><span data-stu-id="54280-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="54280-125">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="54280-125">Async functions</span></span>
<span data-ttu-id="54280-126">La fonction asynchrone suivante [écrit un journal dans le tableau de bord](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="54280-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="54280-127">Les fonctions asynchrones peuvent prendre un [jeton d’annulation](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), comme illustré dans l’exemple suivant, qui copie un objet blob.</span><span class="sxs-lookup"><span data-stu-id="54280-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="54280-128">(Pour obtenir une explication de l'espace réservé **queueTrigger** , consultez la section [Objets blob](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) ).</span><span class="sxs-lookup"><span data-stu-id="54280-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="54280-129">Types gérés par l’attribut QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="54280-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="54280-130">Vous pouvez utiliser l'attribut **QueueTrigger** avec les types suivants :</span><span class="sxs-lookup"><span data-stu-id="54280-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="54280-131">**string**</span><span class="sxs-lookup"><span data-stu-id="54280-131">**string**</span></span>
* <span data-ttu-id="54280-132">Type d’objet POCO sérialisé au format JSON</span><span class="sxs-lookup"><span data-stu-id="54280-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="54280-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="54280-133">**byte[]**</span></span>
* <span data-ttu-id="54280-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="54280-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="54280-135">Algorithme d’interrogation</span><span class="sxs-lookup"><span data-stu-id="54280-135">Polling algorithm</span></span>
<span data-ttu-id="54280-136">Le Kit de développement logiciel (SDK) implémente un algorithme d’interruption exponentiel et aléatoire pour réduire l’effet de l’interrogation de file d’attente inactive sur les coûts de transactions de stockage.</span><span class="sxs-lookup"><span data-stu-id="54280-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="54280-137">Quand un message est détecté, le Kit de développement logiciel (SDK) attend deux secondes, puis vérifie s’il existe un autre message ; quand aucun message n’est détecté, il attend environ quatre secondes avant de réessayer.</span><span class="sxs-lookup"><span data-stu-id="54280-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="54280-138">Après plusieurs échecs de tentatives d’obtention d’un message de file d’attente, le temps d’attente continue à augmenter jusqu’à ce qu’il atteigne le délai d’attente maximal par défaut (une minute).</span><span class="sxs-lookup"><span data-stu-id="54280-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="54280-139">[Le délai d’attente maximal est configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="54280-140">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="54280-140">Multiple instances</span></span>
<span data-ttu-id="54280-141">Si votre application web s’exécute sur plusieurs instances, une tâche web continue se lance sur chaque machine, qui attend des déclencheurs et essaie d’exécuter les fonctions.</span><span class="sxs-lookup"><span data-stu-id="54280-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="54280-142">Dans certains scénarios, cela peut entraîner que certaines fonctions traitent deux fois les mêmes données ; ces fonctions doivent donc être idempotentes (écrites de façon que, si elles sont appelées de manière répétitive avec les mêmes données d’entrée, elles ne produisent pas des résultats en double).</span><span class="sxs-lookup"><span data-stu-id="54280-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="54280-143">Exécution en parallèle</span><span class="sxs-lookup"><span data-stu-id="54280-143">Parallel execution</span></span>
<span data-ttu-id="54280-144">Si vous avez plusieurs fonctions à l’écoute sur différentes files d’attente, le Kit de développement logiciel (SDK) les appelle en parallèle en cas de réception de messages simultanés.</span><span class="sxs-lookup"><span data-stu-id="54280-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="54280-145">Il en est de même quand plusieurs messages sont reçus en provenance d’une file d’attente unique.</span><span class="sxs-lookup"><span data-stu-id="54280-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="54280-146">Par défaut, le Kit de développement logiciel (SDK) obtient un lot de 16 messages de file d’attente à la fois et exécute la fonction qui les traite en parallèle.</span><span class="sxs-lookup"><span data-stu-id="54280-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="54280-147">[La taille de lot est configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="54280-148">Quand le nombre de messages en cours de traitement tombe sous la moitié de la taille de lot, le Kit de développement logiciel (SDK) obtient un autre lot et commence à traiter ces messages.</span><span class="sxs-lookup"><span data-stu-id="54280-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="54280-149">Par conséquent, le nombre maximal de messages traités simultanément par la fonction est une fois et demie la taille de lot.</span><span class="sxs-lookup"><span data-stu-id="54280-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="54280-150">Cette limite s'applique séparément à chaque fonction qui a un attribut **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="54280-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="54280-151">Si vous ne souhaitez pas d’exécution en parallèle pour les messages reçus sur une file d’attente, affectez la valeur 1 à la taille de lot.</span><span class="sxs-lookup"><span data-stu-id="54280-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="54280-152">Obtention des métadonnées de file d'attente ou de message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="54280-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="54280-153">Vous pouvez obtenir les propriétés de messages suivantes en ajoutant des paramètres à la signature de méthode :</span><span class="sxs-lookup"><span data-stu-id="54280-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="54280-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="54280-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="54280-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="54280-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="54280-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="54280-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="54280-157">**string** queueTrigger (contient le texte du message)</span><span class="sxs-lookup"><span data-stu-id="54280-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="54280-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="54280-158">**string** id</span></span>
* <span data-ttu-id="54280-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="54280-159">**string** popReceipt</span></span>
* <span data-ttu-id="54280-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="54280-160">**int** dequeueCount</span></span>

<span data-ttu-id="54280-161">Si vous souhaitez travailler directement avec l'API de stockage Azure, vous pouvez également ajouter un paramètre **CloudStorageAccount** .</span><span class="sxs-lookup"><span data-stu-id="54280-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="54280-162">L’exemple suivant écrit toutes ces métadonnées dans un journal d’application INFO.</span><span class="sxs-lookup"><span data-stu-id="54280-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="54280-163">Dans l’exemple, logMessage et queueTrigger contiennent le contenu du message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54280-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="54280-164">Voici un exemple de journal écrit par l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="54280-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="54280-165">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="54280-165">Graceful shutdown</span></span>
<span data-ttu-id="54280-166">Une fonction qui s'exécute dans une tâche web WebJob continue peut accepter un paramètre **CancellationToken** qui permet au système d'exploitation de notifier la fonction quand la tâche web est sur le point de se terminer.</span><span class="sxs-lookup"><span data-stu-id="54280-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="54280-167">Vous pouvez utiliser cette notification pour vous assurer que la fonction ne s’arrête pas de manière inattendue et laisse les données dans un état incohérent.</span><span class="sxs-lookup"><span data-stu-id="54280-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="54280-168">L’exemple suivant montre comment vérifier l’arrêt imminent d’une tâche web dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="54280-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="54280-169">**Remarque :** le tableau de bord peut ne pas afficher correctement l’état et la sortie des fonctions qui ont été arrêtées.</span><span class="sxs-lookup"><span data-stu-id="54280-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="54280-170">Pour plus d’informations, consultez [Arrêt correct de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="54280-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="54280-171">Création d'un message de file d'attente pendant le traitement d'un message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="54280-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="54280-172">Pour écrire une fonction qui crée un message en file d'attente, utilisez l'attribut **Queue** .</span><span class="sxs-lookup"><span data-stu-id="54280-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="54280-173">Comme **QueueTrigger**, vous transmettez le nom de la file d'attente sous forme de chaîne, ou vous pouvez [définir le nom de la file d'attente de manière dynamique](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="54280-174">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="54280-174">String queue messages</span></span>
<span data-ttu-id="54280-175">L’exemple de code non asynchrone suivant crée un message en file d’attente dans la file d’attente nommée « outputqueue », avec le même contenu que le message de file d’attente reçu dans la file d’attente « inputqueue ».</span><span class="sxs-lookup"><span data-stu-id="54280-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="54280-176">(Dans le cas de fonctions asynchrones, utilisez l'élément **IAsyncCollector<T>** , comme indiqué plus loin dans la présente section.)</span><span class="sxs-lookup"><span data-stu-id="54280-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="54280-177">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="54280-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="54280-178">Pour créer un message de file d'attente qui contient un objet POCO plutôt qu'une chaîne, passez le type POCO en tant que paramètre de sortie au constructeur d'attribut **Queue** .</span><span class="sxs-lookup"><span data-stu-id="54280-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="54280-179">Le Kit de développement logiciel (SDK) sérialise automatiquement l’objet au format JSON.</span><span class="sxs-lookup"><span data-stu-id="54280-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="54280-180">Un message de file d’attente est toujours créé, même si l’objet est null.</span><span class="sxs-lookup"><span data-stu-id="54280-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="54280-181">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="54280-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="54280-182">Pour créer plusieurs messages, affectez **ICollector<T>** ou **IAsyncCollector<T>**, comme type de paramètre pour la file d’attente de sortie, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="54280-183">Chaque message de file d'attente est créé immédiatement quand la méthode **Add** est appelée.</span><span class="sxs-lookup"><span data-stu-id="54280-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="54280-184">Types gérés par l’attribut Queue</span><span class="sxs-lookup"><span data-stu-id="54280-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="54280-185">Vous pouvez utiliser l'attribut **Queue** sur les types de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="54280-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="54280-186">**out string** (crée le message en file d'attente si la valeur du paramètre n'est pas null lorsque la fonction se termine)</span><span class="sxs-lookup"><span data-stu-id="54280-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="54280-187">**out byte[]** (fonctionne comme **string**)</span><span class="sxs-lookup"><span data-stu-id="54280-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="54280-188">**out CloudQueueMessage** (fonctionne comme **string**)</span><span class="sxs-lookup"><span data-stu-id="54280-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="54280-189">**out POCO** (type sérialisable, qui crée un message avec un objet null si le paramètre est null lorsque la fonction se termine)</span><span class="sxs-lookup"><span data-stu-id="54280-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="54280-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="54280-190">**ICollector**</span></span>
* <span data-ttu-id="54280-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="54280-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="54280-192">**CloudQueue** (dédié à la création manuelle de messages via l'utilisation directe de l'API Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="54280-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="54280-193">Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="54280-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="54280-194">Si vous avez besoin d’effectuer une tâche dans votre fonction avant d’utiliser un attribut de Kit de développement logiciel (SDK) WebJobs comme **Queue**, **Blob** ou **Table**, vous pouvez utiliser l’interface **IBinder**.</span><span class="sxs-lookup"><span data-stu-id="54280-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="54280-195">L’exemple suivant prend un message en file d’attente d’entrée et crée un message avec le même contenu dans une file d’attente de sortie.</span><span class="sxs-lookup"><span data-stu-id="54280-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="54280-196">Le nom de file d’attente de sortie est défini par le code dans le corps de la fonction.</span><span class="sxs-lookup"><span data-stu-id="54280-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="54280-197">L’interface **IBinder** peut également être utilisée avec les attributs **Table** et **Blob**.</span><span class="sxs-lookup"><span data-stu-id="54280-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="54280-198">Lecture et écriture d'objets blob et de tables pendant le traitement d'un message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="54280-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="54280-199">Les attributs **Blob** et **Table** vous permettent de lire et d’écrire des objets blob et des tables.</span><span class="sxs-lookup"><span data-stu-id="54280-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="54280-200">Les exemples de cette section s’appliquent aux objets blob.</span><span class="sxs-lookup"><span data-stu-id="54280-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="54280-201">Pour obtenir des exemples de code qui lisent et écrivent des tables, voir [Utilisation du stockage de tables Azure avec le Kit de développement logiciel (SDK) WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md). Pour obtenir des exemples de code qui indiquent comment déclencher des processus lors de la création ou de la mise à jour d’objets blob, voir [Utilisation du Stockage Blob Azure avec le Kit de développement logiciel (SDK) WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="54280-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="54280-202">Messages en file d’attente de chaîne déclenchant des opérations d’objet blob</span><span class="sxs-lookup"><span data-stu-id="54280-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="54280-203">Pour un message de file d’attente qui contient une chaîne, **queueTrigger** est un espace réservé que vous pouvez utiliser dans le paramètre **blobPath** de l’attribut **Blob** qui contient le contenu du message.</span><span class="sxs-lookup"><span data-stu-id="54280-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="54280-204">L'exemple suivant utilise des objets **Stream** pour lire et écrire des objets blob.</span><span class="sxs-lookup"><span data-stu-id="54280-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="54280-205">Le message de file d’attente correspond au nom d’un objet blob situé dans le conteneur textblobs.</span><span class="sxs-lookup"><span data-stu-id="54280-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="54280-206">Une copie de l’objet blob, la chaîne « -new » étant ajoutée au nom, est créée dans le même conteneur.</span><span class="sxs-lookup"><span data-stu-id="54280-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="54280-207">Le constructeur d’attribut **Blob** prend un paramètre **blobPath** qui indique le nom de l’objet blob et du conteneur.</span><span class="sxs-lookup"><span data-stu-id="54280-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="54280-208">Pour en savoir plus sur cet espace réservé, consultez la section [Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="54280-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="54280-209">Lorsque l’attribut décore un objet **Stream**, un autre paramètre de constructeur spécifie le mode **FileAccess** (lecture, écriture ou lecture/écriture).</span><span class="sxs-lookup"><span data-stu-id="54280-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="54280-210">L'exemple suivant utilise un objet **CloudBlockBlob** pour supprimer un objet blob.</span><span class="sxs-lookup"><span data-stu-id="54280-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="54280-211">Le message de la file d’attente correspond au nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="54280-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="54280-212">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="54280-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="54280-213">Pour un objet POCO stocké au format JSON dans le message de file d’attente, vous pouvez utiliser des espaces réservés qui nomment les propriétés de nom de l’objet dans le paramètre **blobPath** de l’attribut **Queue**.</span><span class="sxs-lookup"><span data-stu-id="54280-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="54280-214">Vous pouvez également utiliser des noms de propriété de métadonnées de file d'attente comme espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="54280-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="54280-215">Consultez la section [Obtention des métadonnées de file d’attente ou de message de file d’attente](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="54280-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="54280-216">L’exemple suivant copie un objet blob dans un nouvel objet blob, avec une autre extension.</span><span class="sxs-lookup"><span data-stu-id="54280-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="54280-217">Le message de la file d’attente est un objet **BlobInformation** qui inclut les propriétés **BlobName** et **BlobNameWithoutExtension**.</span><span class="sxs-lookup"><span data-stu-id="54280-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="54280-218">Les noms de propriété sont utilisés en tant qu'espaces réservés dans le chemin de l'objet blob pour les attributs **blob** .</span><span class="sxs-lookup"><span data-stu-id="54280-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="54280-219">Le Kit de développement logiciel (SDK) utilise le package [NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) pour sérialiser et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="54280-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="54280-220">Si vous créez des messages en file d’attente dans un programme qui n’utilise pas le Kit de développement logiciel (SDK) WebJobs, vous pouvez écrire le code comme dans l’exemple suivant, afin de créer un message en file d’attente POCO que le Kit de développement logiciel (SDK) peut analyser.</span><span class="sxs-lookup"><span data-stu-id="54280-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="54280-221">Si vous devez effectuer un travail dans votre fonction avant de lier un objet blob à un objet, vous pouvez utiliser l’attribut dans le corps de la fonction comme indiqué dans [Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="54280-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="54280-222">Types avec lesquels vous pouvez utiliser l’attribut Blob</span><span class="sxs-lookup"><span data-stu-id="54280-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="54280-223">L'attribut **blob** peut être utilisé avec les types suivants :</span><span class="sxs-lookup"><span data-stu-id="54280-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="54280-224">**Stream** (lecture ou écriture ; spécifié à l'aide du paramètre de constructeur FileAccess)</span><span class="sxs-lookup"><span data-stu-id="54280-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="54280-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="54280-225">**TextReader**</span></span>
* <span data-ttu-id="54280-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="54280-226">**TextWriter**</span></span>
* <span data-ttu-id="54280-227">**string** (lecture)</span><span class="sxs-lookup"><span data-stu-id="54280-227">**string** (read)</span></span>
* <span data-ttu-id="54280-228">**out string** (écriture ; crée un objet blob uniquement si le paramètre de chaîne n'est pas null lorsque la fonction renvoie des résultats)</span><span class="sxs-lookup"><span data-stu-id="54280-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="54280-229">POCO (lecture)</span><span class="sxs-lookup"><span data-stu-id="54280-229">POCO (read)</span></span>
* <span data-ttu-id="54280-230">out POCO (écriture ; crée systématiquement un objet blob, créé en tant qu’objet null si le paramètre POCO est null lorsque la fonction renvoie des résultats)</span><span class="sxs-lookup"><span data-stu-id="54280-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="54280-231">**CloudBlobStream** (écriture)</span><span class="sxs-lookup"><span data-stu-id="54280-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="54280-232">**ICloudBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="54280-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="54280-233">**CloudBlockBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="54280-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="54280-234">**CloudPageBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="54280-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="54280-235">Gestion de messages incohérents</span><span class="sxs-lookup"><span data-stu-id="54280-235">How to handle poison messages</span></span>
<span data-ttu-id="54280-236">Les messages dont le contenu provoque l'échec d'une fonction sont appelés *messages incohérents*.</span><span class="sxs-lookup"><span data-stu-id="54280-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="54280-237">Lorsque la fonction échoue, le message en file d’attente n’est pas supprimé, mais finalement récupéré à nouveau, provoquant la répétition du cycle.</span><span class="sxs-lookup"><span data-stu-id="54280-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="54280-238">Le Kit de développement logiciel (SDK) peut interrompre automatiquement le cycle après un nombre limité d’itérations, ou vous pouvez le faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="54280-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="54280-239">Gestion automatique des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="54280-239">Automatic poison message handling</span></span>
<span data-ttu-id="54280-240">Le Kit de développement logiciel (SDK) appelle une fonction jusqu’à cinq fois pour traiter un message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54280-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="54280-241">Si la cinquième tentative échoue, le message est déplacé vers une file d’attente de messages incohérents.</span><span class="sxs-lookup"><span data-stu-id="54280-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="54280-242">Vous pouvez voir comment configurer le nombre maximal de nouvelles tentatives dans [Définition des options de configuration](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="54280-243">La file d'attente de messages incohérents se nomme *{nom_file_d'attente_d'origine}*-poison.</span><span class="sxs-lookup"><span data-stu-id="54280-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="54280-244">Vous pouvez écrire une fonction pour traiter les messages de la file d’attente de messages incohérents en les consignant dans un journal ou en envoyant une notification signalant qu’une attention manuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="54280-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="54280-245">Dans l'exemple suivant, la fonction **CopyBlob** ne fonctionnera pas si un message de file d'attente contient le nom d'un objet blob qui n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="54280-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="54280-246">Quand cela se produit, le message est déplacé de la file d’attente copyblobqueue vers la file d’attente copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="54280-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="54280-247">Le **ProcessPoisonMessage** enregistre ensuite le message incohérent.</span><span class="sxs-lookup"><span data-stu-id="54280-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="54280-248">L’illustration suivante montre la sortie de console de ces fonctions pendant le traitement d’un message incohérent.</span><span class="sxs-lookup"><span data-stu-id="54280-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Sortie de la console pour la gestion des messages incohérents](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="54280-250">Gestion manuelle des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="54280-250">Manual poison message handling</span></span>
<span data-ttu-id="54280-251">Vous pouvez obtenir le nombre de fois qu’un message a été récupéré en vue de son traitement en ajoutant un paramètre **int** nommé **dequeueCount** à votre fonction.</span><span class="sxs-lookup"><span data-stu-id="54280-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="54280-252">Vous pouvez ensuite vérifier le nombre d’enlèvements de la file d’attente dans le code de fonction et effectuer votre propre gestion des messages incohérents quand le nombre dépasse un seuil, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="54280-253">Définition des options de configuration</span><span class="sxs-lookup"><span data-stu-id="54280-253">How to set configuration options</span></span>
<span data-ttu-id="54280-254">Vous pouvez utiliser le type **JobHostConfiguration** pour définir les options de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="54280-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="54280-255">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code.</span><span class="sxs-lookup"><span data-stu-id="54280-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="54280-256">Configuration des paramètres **QueueTrigger** tels que le nombre de retraits maximal.</span><span class="sxs-lookup"><span data-stu-id="54280-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="54280-257">Obtention des noms de file d’attente de la configuration.</span><span class="sxs-lookup"><span data-stu-id="54280-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="54280-258">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code</span><span class="sxs-lookup"><span data-stu-id="54280-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="54280-259">La définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code vous permet d’utiliser vos propres noms de chaînes de connexion dans les fichiers de configuration ou les variables d’environnement, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="54280-260">Configuration des paramètres QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="54280-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="54280-261">Vous pouvez configurer les paramètres suivants, qui s’appliquent au traitement des messages en file d’attente :</span><span class="sxs-lookup"><span data-stu-id="54280-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="54280-262">nombre maximal de messages de file d'attente prélevés simultanément pour être exécutés en parallèle (la valeur par défaut est 16) ;</span><span class="sxs-lookup"><span data-stu-id="54280-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="54280-263">nombre maximal de tentatives avant l'envoi d'un message de file d'attente à une file d'attente de messages incohérents (la valeur par défaut est 5) ;</span><span class="sxs-lookup"><span data-stu-id="54280-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="54280-264">durée d'attente maximale avant la nouvelle interrogation quand une file d'attente est vide (la valeur par défaut est 1 minute).</span><span class="sxs-lookup"><span data-stu-id="54280-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="54280-265">L’exemple suivant montre comment configurer ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="54280-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="54280-266">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="54280-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="54280-267">Dans certains cas, vous souhaitez spécifier dans le code un nom de file d’attente, un nom d’objet blob ou un conteneur, ou encore un nom de table, plutôt que de les coder en dur.</span><span class="sxs-lookup"><span data-stu-id="54280-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="54280-268">Par exemple, vous pouvez souhaiter spécifier le nom de la file d'attente de **QueueTrigger** dans une variable d'environnement ou un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="54280-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="54280-269">Vous pouvez le faire en transmettant un objet **NameResolver** au type **JobHostConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="54280-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="54280-270">Incluez des espaces réservés spéciaux, entourés par des signes de pourcentage (%) dans les paramètres de constructeur d'attribut de Kit de développement logiciel (SDK) pour que votre code **NameResolver** spécifie les valeurs réelles à utiliser à la place de ces espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="54280-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="54280-271">Par exemple, supposons que vous souhaitez utiliser une file d’attente nommée logqueuetest dans l’environnement de test et une autre nommée logqueueprod en production.</span><span class="sxs-lookup"><span data-stu-id="54280-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="54280-272">Au lieu d'un nom de file d'attente codé en dur, vous voulez spécifier le nom d'une entrée dans la collection **appSettings** ayant le nom de la file d'attente réelle.</span><span class="sxs-lookup"><span data-stu-id="54280-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="54280-273">Si la clé **appSettings** est logqueue, votre fonction peut ressembler à l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="54280-274">Votre classe **NameResolver** peut alors obtenir le nom de la file d’attente à partir d’**appSettings** comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="54280-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="54280-275">Vous transmettez la classe **NameResolver** à l’objet **JobHost** comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="54280-276">**Remarque :** les noms d’objet blob, de table et de file d’attente sont résolus chaque fois qu’une fonction est appelée, mais les noms de conteneur d’objet blob sont uniquement résolus au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="54280-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="54280-277">Vous ne pouvez pas modifier le nom d’un conteneur d’objet blob lorsque la tâche s’exécute.</span><span class="sxs-lookup"><span data-stu-id="54280-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="54280-278">Déclenchement manuel d'une fonction</span><span class="sxs-lookup"><span data-stu-id="54280-278">How to trigger a function manually</span></span>
<span data-ttu-id="54280-279">Pour déclencher manuellement une fonction, utilisez la méthode **Call** ou **CallAsync** sur l’objet **JobHost** et l’attribut **NoAutomaticTrigger** sur la fonction, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="54280-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-to-write-logs"></a><span data-ttu-id="54280-280">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="54280-280">How to write logs</span></span>
<span data-ttu-id="54280-281">Le tableau de bord affiche des journaux à deux emplacements : la page relative aux tâches web et la page portant sur l’appel d’une tâche web spécifique.</span><span class="sxs-lookup"><span data-stu-id="54280-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Journaux affichés dans la page relative aux tâches web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="54280-284">La sortie des méthodes de console que vous appelez dans une fonction ou dans la méthode **Main()** s'affiche dans la page Tableau de bord de la tâche web, et non dans la page relative à l'appel d'une méthode particulière.</span><span class="sxs-lookup"><span data-stu-id="54280-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="54280-285">La sortie de l’objet TextWriter que vous obtenez à partir d’un paramètre dans la signature de méthode s’affiche dans la page Tableau de bord relative à l’appel d’une méthode.</span><span class="sxs-lookup"><span data-stu-id="54280-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="54280-286">La sortie de la console ne peut pas être liée à un appel de méthode particulier, car la console présente un thread unique, tandis que de nombreuses fonctions de tâche peuvent s’exécuter en même temps.</span><span class="sxs-lookup"><span data-stu-id="54280-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="54280-287">C’est pourquoi le Kit de développement logiciel (SDK) fournit à chaque appel de fonction son propre objet d’enregistreur de journal unique.</span><span class="sxs-lookup"><span data-stu-id="54280-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="54280-288">Pour écrire des [journaux de suivi d’application](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilisez **Console.Out** (crée des journaux marqués INFO) et **Console.Error** (crée des journaux marqués ERROR).</span><span class="sxs-lookup"><span data-stu-id="54280-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="54280-289">Vous pouvez aussi utiliser des éléments [Trace ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), qui fournissent des niveaux supplémentaires (En clair, Avertissement et Critique).</span><span class="sxs-lookup"><span data-stu-id="54280-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="54280-290">Les journaux de suivi d’application s’affichent dans les fichiers de journaux d’application web, les tables Microsoft Azure, ou les objets blob Microsoft Azure, selon la configuration de votre application web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54280-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="54280-291">Comme pour toutes les autres sorties de console, les 100 journaux d’application les plus récents s’affichent également dans la page Tableau de bord de la tâche web, et non dans la page d’appel d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="54280-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="54280-292">La sortie de console s’affiche dans le tableau de bord uniquement si le programme s’exécute dans une tâche web Microsoft Azure, et non lorsque le programme est exécuté localement ou dans un autre environnement.</span><span class="sxs-lookup"><span data-stu-id="54280-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="54280-293">Vous pouvez désactiver la journalisation en définissant la chaîne de connexion du tableau de bord sur null.</span><span class="sxs-lookup"><span data-stu-id="54280-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="54280-294">Pour plus d’informations, consultez la section [Définition des options de configuration](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="54280-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="54280-295">L’exemple suivant montre plusieurs manières d’écrire des journaux :</span><span class="sxs-lookup"><span data-stu-id="54280-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="54280-296">Dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs, la sortie de l’objet **TextWriter** apparaît quand vous accédez à la page d’un appel de fonction spécifique et sélectionnez **Activer/désactiver la sortie** :</span><span class="sxs-lookup"><span data-stu-id="54280-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Lien d’appel](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="54280-299">Dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs, les 100 lignes les plus récentes de la sortie de console apparaissent lorsque vous accédez à la page de la tâche web (et non à celle de l’appel de fonction) et que vous sélectionnez **Activer/désactiver la sortie**.</span><span class="sxs-lookup"><span data-stu-id="54280-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Activer/désactiver la sortie](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="54280-301">Dans une tâche web continue, les journaux des applications apparaissent dans /data/jobs/continuous/*{nom_tâche_web*/job_log.txt dans le système de fichiers du site web.</span><span class="sxs-lookup"><span data-stu-id="54280-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="54280-302">Dans un objet blob Azure, les journaux d’application ressemblent à ceci : 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="54280-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="54280-303">Dans une table Azure, les journaux **Console.Out** et **Console.Error** ressemblent à ceci :</span><span class="sxs-lookup"><span data-stu-id="54280-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Journal d’informations dans la table](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Journal d’erreurs dans la table](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="54280-306">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54280-306">Next steps</span></span>
<span data-ttu-id="54280-307">Cet article fournit des exemples de code qui montrent comment gérer des scénarios courants pour l’utilisation des files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="54280-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="54280-308">Pour plus d’informations sur l’utilisation d’Azure WebJobs et du Kit de développement logiciel (SDK) WebJobs, consultez la section [Ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="54280-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

