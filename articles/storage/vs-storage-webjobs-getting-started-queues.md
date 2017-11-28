---
title: "aaaGetting en main de Visual Studio et de stockage de la file d’attente des services connectés (projets de la tâche Web) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans un projet de la tâche Web une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="9fc00-103">Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets WebJob)</span><span class="sxs-lookup"><span data-stu-id="9fc00-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9fc00-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9fc00-104">Overview</span></span>
<span data-ttu-id="9fc00-105">Cet article décrit comment obtenir démarré à l’aide de la file d’attente Azure storage dans un projet de la tâche Web de Visual Studio Azure une fois que vous avez créé ou référencé d’un compte de stockage Azure à l’aide de hello Visual Studio **ajouter des Services connectés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9fc00-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="9fc00-106">Lorsque vous ajoutez un projet de tâche Web tooa compte stockage à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue, les packages NuGet de stockage Azure appropriés hello sont installées, les références .NET appropriées hello sont toohello ajouté projet et les chaînes de connexion pour le compte de stockage hello sont mis à jour dans le fichier App.config hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="9fc00-107">Cet article fournit des exemples de code c# qui montrent comment toouse hello Azure WebJobs SDK version 1.x avec hello service de stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc00-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="9fc00-108">Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9fc00-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="9fc00-109">Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9fc00-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="9fc00-110">Pour plus d’informations, consultez la section [Prise en main d’Azure Queue Storage à l’aide de .NET](storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="9fc00-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="9fc00-111">Pour plus d’informations sur ASP.NET, voir le site [ASP.NET](http://www.asp.net)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="9fc00-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="9fc00-112">Comment tootrigger une fonction lors de la réception d’un message de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="9fc00-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="9fc00-113">toowrite une fonction qui hello WebJobs SDK appelle lors de la réception d’un message de la file d’attente, utilisez hello **QueueTrigger** attribut.</span><span class="sxs-lookup"><span data-stu-id="9fc00-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="9fc00-114">constructeur d’attribut Hello prend un paramètre de chaîne qui spécifie le nom hello de toopoll de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="9fc00-115">toosee comment tooset hello le nom de la file d’attente dynamique, consultez [comment tooset les Options de Configuration](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="9fc00-116">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="9fc00-116">String queue messages</span></span>
<span data-ttu-id="9fc00-117">Dans l’exemple suivant de hello, file d’attente hello contient un message de type chaîne, donc **QueueTrigger** est le paramètre de chaîne tooa appliqué nommé **logMessage** qui contient le contenu du message de file d’attente hello hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="9fc00-118">Hello fonction [écrit un toohello de message du journal du tableau de bord](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="9fc00-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="9fc00-119">En outre **chaîne**, paramètre hello peut être un tableau d’octets, un **CloudQueueMessage** objet ou un POCO que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="9fc00-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="9fc00-120">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="9fc00-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9fc00-121">Dans l’exemple suivant de hello, message de file d’attente hello contient des données JSON pour un **BlobInformation** objet qui inclut un **BlobName** propriété.</span><span class="sxs-lookup"><span data-stu-id="9fc00-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="9fc00-122">Hello SDK désérialise automatiquement l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="9fc00-123">Hello SDK utilise hello [package Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="9fc00-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="9fc00-124">Si vous créez des messages de la file d’attente dans un programme qui n’utilise pas hello WebJobs SDK, vous pouvez écrire du code comme hello suivant exemple toocreate un message de la file d’attente POCO qui hello que SDK peut analyser.</span><span class="sxs-lookup"><span data-stu-id="9fc00-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="9fc00-125">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="9fc00-125">Async functions</span></span>
<span data-ttu-id="9fc00-126">Hello suivant fonction async [écrit un tableau de bord de toohello journal](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="9fc00-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="9fc00-127">Fonctions Async peuvent prendre un [jeton d’annulation](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), comme indiqué dans hello qui copie un objet blob de l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="9fc00-128">(Pour obtenir une explication de hello **queueTrigger** espace réservé, consultez hello [BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span><span class="sxs-lookup"><span data-stu-id="9fc00-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="9fc00-129">Attribut de types hello QueueTrigger fonctionne avec</span><span class="sxs-lookup"><span data-stu-id="9fc00-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="9fc00-130">Vous pouvez utiliser **QueueTrigger** avec hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="9fc00-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="9fc00-131">**string**</span><span class="sxs-lookup"><span data-stu-id="9fc00-131">**string**</span></span>
* <span data-ttu-id="9fc00-132">Type d’objet POCO sérialisé au format JSON</span><span class="sxs-lookup"><span data-stu-id="9fc00-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="9fc00-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="9fc00-133">**byte[]**</span></span>
* <span data-ttu-id="9fc00-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="9fc00-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="9fc00-135">Algorithme d’interrogation</span><span class="sxs-lookup"><span data-stu-id="9fc00-135">Polling algorithm</span></span>
<span data-ttu-id="9fc00-136">Hello SDK implémente un effet de hello tooreduce aléatoire exponentielle algorithme de temporisation d’inactivité-file d’attente sur les coûts de stockage.</span><span class="sxs-lookup"><span data-stu-id="9fc00-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="9fc00-137">Lorsqu’un message est détecté, hello SDK attend deux secondes, puis vérifie un autre message ; Lorsque aucun message n’est trouvé, il attend environ quatre secondes avant de réessayer.</span><span class="sxs-lookup"><span data-stu-id="9fc00-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="9fc00-138">Après les tentatives ayant échoué tooget un message de la file d’attente, temps d’attente hello continue tooincrease jusqu'à ce qu’il atteigne le délai d’attente maximal hello, les minutes tooone de valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="9fc00-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="9fc00-139">[Hello délai d’attente maximal est configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="9fc00-140">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="9fc00-140">Multiple instances</span></span>
<span data-ttu-id="9fc00-141">Si votre application web s’exécute sur plusieurs instances, une tâche Web continue s’exécute sur chaque ordinateur, et chaque ordinateur va attendre que les déclencheurs et essayer de fonctions de toorun.</span><span class="sxs-lookup"><span data-stu-id="9fc00-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="9fc00-142">Dans certains scénarios, que cela peut entraîner toosome les fonctions de traitement hello à deux reprises, les mêmes données fonctions ne doivent donc être idempotentes (écrite afin que les appeler à plusieurs reprises avec les mêmes données d’entrée ne génère pas de hello dupliquer les résultats).</span><span class="sxs-lookup"><span data-stu-id="9fc00-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="9fc00-143">Exécution en parallèle</span><span class="sxs-lookup"><span data-stu-id="9fc00-143">Parallel execution</span></span>
<span data-ttu-id="9fc00-144">Si vous avez plusieurs fonctions à l’écoute sur différentes files d’attente, hello SDK appellera les en parallèle lorsque les messages sont reçus simultanément.</span><span class="sxs-lookup"><span data-stu-id="9fc00-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="9fc00-145">Hello est de même lorsque plusieurs messages sont reçus d’une file d’attente unique.</span><span class="sxs-lookup"><span data-stu-id="9fc00-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="9fc00-146">Par défaut, hello SDK Obtient un lot de messages de file d’attente 16 à la fois et exécute la fonction hello qui les traite en parallèle.</span><span class="sxs-lookup"><span data-stu-id="9fc00-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="9fc00-147">[taille de lot Hello est configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="9fc00-148">Lorsqu’il obtient nombre hello en cours de traitement vers le bas toohalf hello taille de lot, hello SDK Obtient un autre lot et commence à traiter les messages.</span><span class="sxs-lookup"><span data-stu-id="9fc00-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="9fc00-149">Par conséquent nombre maximal de hello de messages simultanés en cours de traitement par la fonction est la taille du lot une fois et demie hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="9fc00-150">Cette limite s’applique séparément les fonction tooeach qui a un **QueueTrigger** attribut.</span><span class="sxs-lookup"><span data-stu-id="9fc00-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="9fc00-151">Si vous ne souhaitez pas l’exécution en parallèle pour les messages reçus sur une file d’attente, définissez too1 de taille de lot hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="9fc00-152">Obtention des métadonnées de file d'attente ou de message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="9fc00-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="9fc00-153">Vous pouvez obtenir hello suivant des propriétés de message en ajoutant la signature de méthode toohello paramètres :</span><span class="sxs-lookup"><span data-stu-id="9fc00-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="9fc00-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="9fc00-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="9fc00-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="9fc00-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="9fc00-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="9fc00-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="9fc00-157">**string** queueTrigger (contient le texte du message)</span><span class="sxs-lookup"><span data-stu-id="9fc00-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="9fc00-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="9fc00-158">**string** id</span></span>
* <span data-ttu-id="9fc00-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="9fc00-159">**string** popReceipt</span></span>
* <span data-ttu-id="9fc00-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="9fc00-160">**int** dequeueCount</span></span>

<span data-ttu-id="9fc00-161">Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez également ajouter un **CloudStorageAccount** paramètre.</span><span class="sxs-lookup"><span data-stu-id="9fc00-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="9fc00-162">Hello exemple suivant écrit tous ce métadonnées tooan informations journal d’application.</span><span class="sxs-lookup"><span data-stu-id="9fc00-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="9fc00-163">Dans l’exemple de hello, logMessage et queueTrigger contiennent le contenu du message de file d’attente hello hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="9fc00-164">Voici un exemple de journal écrit par l’exemple de code hello :</span><span class="sxs-lookup"><span data-stu-id="9fc00-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="9fc00-165">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="9fc00-165">Graceful shutdown</span></span>
<span data-ttu-id="9fc00-166">Une fonction qui s’exécute dans une tâche Web continue peut accepter un **CancellationToken** paramètre qui permet la fonction hello toonotify hello de système d’exploitation lorsque hello la tâche Web est sur toobe terminée.</span><span class="sxs-lookup"><span data-stu-id="9fc00-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="9fc00-167">Vous pouvez utiliser cette toomake de notification que la fonction hello n’arrêt inattendu d’une manière qui laisse les données dans un état incohérent.</span><span class="sxs-lookup"><span data-stu-id="9fc00-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="9fc00-168">Hello suivant montre l’exemple de comment toocheck à l’arrêt de la tâche Web imminente dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="9fc00-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="9fc00-169">**Remarque :** hello du tableau de bord ne peut pas afficher correctement état de hello et la sortie de fonctions qui ont été arrêtés.</span><span class="sxs-lookup"><span data-stu-id="9fc00-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="9fc00-170">Pour plus d’informations, consultez [Arrêt correct de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="9fc00-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="9fc00-171">Comment toocreate une file d’attente de message lors du traitement d’un message de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="9fc00-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="9fc00-172">toowrite une fonction qui crée un nouveau message de file d’attente, utilisez hello **file d’attente** attribut.</span><span class="sxs-lookup"><span data-stu-id="9fc00-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="9fc00-173">Comme **QueueTrigger**, vous passez dans un nom de file d’attente hello sous forme de chaîne, ou vous pouvez [définir le nom de file d’attente hello dynamiquement](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="9fc00-174">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="9fc00-174">String queue messages</span></span>
<span data-ttu-id="9fc00-175">Hello suivant l’exemple de code non-async crée un nouveau message de file d’attente dans la file d’attente hello nommé « outputqueue » avec hello même contenu en tant que message de file d’attente de salutation reçu dans la file d’attente hello nommé « inputqueue ».</span><span class="sxs-lookup"><span data-stu-id="9fc00-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="9fc00-176">(Dans le cas de fonctions asynchrones, utilisez l'élément **IAsyncCollector<T>** , comme indiqué plus loin dans la présente section.)</span><span class="sxs-lookup"><span data-stu-id="9fc00-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="9fc00-177">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="9fc00-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9fc00-178">type d’un message de la file d’attente qui contient un POCO plutôt que d’une chaîne, passez hello POCO toocreate comme un toohello de paramètre de sortie **file d’attente** constructeur d’attribut.</span><span class="sxs-lookup"><span data-stu-id="9fc00-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="9fc00-179">Kit de développement logiciel de Hello sérialise automatiquement hello objet tooJSON.</span><span class="sxs-lookup"><span data-stu-id="9fc00-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="9fc00-180">Un message de la file d’attente est toujours créé, même si l’objet hello est null.</span><span class="sxs-lookup"><span data-stu-id="9fc00-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="9fc00-181">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="9fc00-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="9fc00-182">toocreate plusieurs messages, vérifiez le type de paramètre hello pour la file d’attente de sortie hello **ICollector<T>**  ou **IAsyncCollector<T>**, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="9fc00-183">Chaque message de la file d’attente est créée immédiatement lorsque hello **ajouter** méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="9fc00-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="9fc00-184">Types de cet attribut de la file d’attente hello fonctionne avec</span><span class="sxs-lookup"><span data-stu-id="9fc00-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="9fc00-185">Vous pouvez utiliser hello **file d’attente** attribut sur hello les types de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="9fc00-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="9fc00-186">**chaîne** (crée le message de la file d’attente si la valeur du paramètre est non null lors de la fin de la fonction hello)</span><span class="sxs-lookup"><span data-stu-id="9fc00-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="9fc00-187">**out byte[]** (fonctionne comme **string**)</span><span class="sxs-lookup"><span data-stu-id="9fc00-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="9fc00-188">**out CloudQueueMessage** (fonctionne comme **string**)</span><span class="sxs-lookup"><span data-stu-id="9fc00-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="9fc00-189">**out POCO** (un type sérialisable, crée un message avec un objet null si hello paramètre est null lors de la fin de la fonction hello)</span><span class="sxs-lookup"><span data-stu-id="9fc00-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="9fc00-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="9fc00-190">**ICollector**</span></span>
* <span data-ttu-id="9fc00-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="9fc00-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="9fc00-192">**CloudQueue** (pour la création de messages manuellement à l’aide de hello API de stockage Azure directement)</span><span class="sxs-lookup"><span data-stu-id="9fc00-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="9fc00-193">Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello</span><span class="sxs-lookup"><span data-stu-id="9fc00-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="9fc00-194">Si vous avez besoin de toodo certains fonctionnent dans votre fonction avant d’utiliser un attribut WebJobs SDK comme **file d’attente**, **Blob**, ou **Table**, vous pouvez utiliser hello **IBinder** interface.</span><span class="sxs-lookup"><span data-stu-id="9fc00-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="9fc00-195">Hello, l’exemple suivant prend un message de la file d’attente d’entrée et crée un nouveau message avec hello même contenu dans une file d’attente de sortie.</span><span class="sxs-lookup"><span data-stu-id="9fc00-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="9fc00-196">nom de file d’attente de sortie Hello est définie par le code dans le corps de hello de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="9fc00-197">Hello **IBinder** interface peut également être utilisée avec hello **Table** et **Blob** attributs.</span><span class="sxs-lookup"><span data-stu-id="9fc00-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="9fc00-198">Comment tooread et l’écriture d’objets BLOB et les tables lors du traitement d’un message de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="9fc00-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="9fc00-199">Hello **Blob** et **Table** attributs vous tooread et écrire des objets BLOB et tables.</span><span class="sxs-lookup"><span data-stu-id="9fc00-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="9fc00-200">exemples de Hello dans cette section s’appliquent tooblobs.</span><span class="sxs-lookup"><span data-stu-id="9fc00-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="9fc00-201">Pour obtenir des exemples de code qui montrent comment tootrigger traite lorsque les objets BLOB est créés ou mis à jour, consultez [comment toouse Azure stockage d’objets blob par hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)et pour obtenir des exemples de code qui lisent et écrivent des tables, consultez [comment toouse table Azure stockage avec hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9fc00-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="9fc00-202">Messages en file d’attente de chaîne déclenchant des opérations d’objet blob</span><span class="sxs-lookup"><span data-stu-id="9fc00-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="9fc00-203">Pour un message de la file d’attente qui contient une chaîne, **queueTrigger** est un espace réservé que vous pouvez utiliser Bonjour **Blob** l’attribut **blobPath** paramètre qui contient le contenu de hello de message de type Hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="9fc00-204">Hello exemple suivant utilise **flux** objets blobs tooread et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="9fc00-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="9fc00-205">message de file d’attente Hello est nom hello d’un objet blob situé dans le conteneur de textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="9fc00-206">Une copie de l’objet blob de hello avec «-nouveau » ajouté toohello nom est créé dans hello même conteneur.</span><span class="sxs-lookup"><span data-stu-id="9fc00-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="9fc00-207">Hello **Blob** attribut constructeur prend un **blobPath** paramètre qui spécifie le conteneur de hello et nom d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="9fc00-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="9fc00-208">Pour plus d’informations sur cet espace réservé, consultez [comment toouse Azure stockage d’objets blob par hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9fc00-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="9fc00-209">Lorsque les attributs hello décore un **flux** de l’objet, un autre paramètre de constructeur spécifie hello **FileAccess** mode en lecture, écriture ou en lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="9fc00-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="9fc00-210">Hello exemple suivant utilise un **CloudBlockBlob** toodelete un objet blob de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9fc00-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="9fc00-211">message de file d’attente Hello est nom hello d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="9fc00-212">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="9fc00-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9fc00-213">Pour un POCO stockée en tant que JSON dans le message de file d’attente d’appel, vous pouvez utiliser des espaces réservés qui nommer les propriétés d’objet de hello en hello **file d’attente** l’attribut **blobPath** paramètre.</span><span class="sxs-lookup"><span data-stu-id="9fc00-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="9fc00-214">Vous pouvez également utiliser des noms de propriété de métadonnées de file d'attente comme espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="9fc00-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="9fc00-215">Consultez la section [Obtention des métadonnées de file d’attente ou de message de file d’attente](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="9fc00-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="9fc00-216">Hello exemple suivant copie un objet blob tooa nouvel objet blob avec une autre extension.</span><span class="sxs-lookup"><span data-stu-id="9fc00-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="9fc00-217">message de file d’attente Hello est un **BlobInformation** objet inclut **BlobName** et **BlobNameWithoutExtension** propriétés.</span><span class="sxs-lookup"><span data-stu-id="9fc00-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="9fc00-218">les noms de propriété Hello sont utilisés comme espaces réservés dans le chemin d’accès des blob hello pour hello **Blob** attributs.</span><span class="sxs-lookup"><span data-stu-id="9fc00-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="9fc00-219">Hello SDK utilise hello [package Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="9fc00-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="9fc00-220">Si vous créez des messages de la file d’attente dans un programme qui n’utilise pas hello WebJobs SDK, vous pouvez écrire du code comme hello suivant exemple toocreate un message de la file d’attente POCO qui hello que SDK peut analyser.</span><span class="sxs-lookup"><span data-stu-id="9fc00-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="9fc00-221">Si vous devez toodo certains fonctionnent dans votre fonction avant de lier un objet tooan d’objets blob, vous pouvez utiliser attribut hello dans les corps de hello de fonction hello, comme indiqué dans [attributs utiliser le SDK WebJobs dans le corps d’une fonction de hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="9fc00-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="9fc00-222">Vous pouvez utiliser hello des types d’objets Blob attribut avec</span><span class="sxs-lookup"><span data-stu-id="9fc00-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="9fc00-223">Hello **Blob** attribut peut être utilisé avec les types suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="9fc00-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="9fc00-224">**Flux** (lecture ou écriture, spécifiée à l’aide du paramètre de constructeur FileAccess hello)</span><span class="sxs-lookup"><span data-stu-id="9fc00-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="9fc00-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="9fc00-225">**TextReader**</span></span>
* <span data-ttu-id="9fc00-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="9fc00-226">**TextWriter**</span></span>
* <span data-ttu-id="9fc00-227">**string** (lecture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-227">**string** (read)</span></span>
* <span data-ttu-id="9fc00-228">**chaîne** (écriture ; crée un objet blob uniquement si le paramètre de chaîne hello est non null lors de la fonction hello retourne)</span><span class="sxs-lookup"><span data-stu-id="9fc00-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="9fc00-229">POCO (lecture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-229">POCO (read)</span></span>
* <span data-ttu-id="9fc00-230">out POCO (écrire ; toujours crée un objet blob, crée en tant qu’objet null si POCO paramètre est null lors de la fonction hello retourne)</span><span class="sxs-lookup"><span data-stu-id="9fc00-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="9fc00-231">**CloudBlobStream** (écriture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="9fc00-232">**ICloudBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="9fc00-233">**CloudBlockBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="9fc00-234">**CloudPageBlob** (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="9fc00-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="9fc00-235">Comment toohandle des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="9fc00-235">How toohandle poison messages</span></span>
<span data-ttu-id="9fc00-236">Les messages dont le contenu provoque une toofail de fonction sont appelées *messages incohérents*.</span><span class="sxs-lookup"><span data-stu-id="9fc00-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="9fc00-237">En cas d’échec de la fonction hello, message de file d’attente hello n’est pas supprimé et finalement est de nouveau récupéré, entraînant toobe de cycle de hello répétée.</span><span class="sxs-lookup"><span data-stu-id="9fc00-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="9fc00-238">Hello SDK peut interrompre automatiquement hello cycle après un nombre limité d’itérations, ou vous pouvez le faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="9fc00-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="9fc00-239">Gestion automatique des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="9fc00-239">Automatic poison message handling</span></span>
<span data-ttu-id="9fc00-240">Kit de développement logiciel de Hello appelle une fonction des too5 tooprocess de fois où un message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="9fc00-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="9fc00-241">Si vous essayez de cinquième hello échoue, le message de type hello est file d’attente de messages incohérents tooa déplacé.</span><span class="sxs-lookup"><span data-stu-id="9fc00-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="9fc00-242">Vous pouvez voir comment tooconfigure hello nombre maximal de tentatives dans [comment les options de configuration tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="9fc00-243">file d’attente de messages incohérents Hello est nommé *{originalqueuename}*-incohérents.</span><span class="sxs-lookup"><span data-stu-id="9fc00-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="9fc00-244">Vous pouvez écrire une fonction tooprocess messages de file d’attente de messages incohérents hello par les enregistrer ou de l’envoi d’une notification qu’attention manuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9fc00-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="9fc00-245">Bonjour suivant hello d’exemple **CopyBlob** ne fonctionnera pas si un message de la file d’attente contient nom hello d’un objet blob qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="9fc00-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="9fc00-246">Lorsque cela se produit, message de type hello est déplacé à partir de la file d’attente de file d’attente toohello copyblobqueue-incohérents hello copyblobqueue.</span><span class="sxs-lookup"><span data-stu-id="9fc00-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="9fc00-247">Hello **ProcessPoisonMessage** puis journaux hello message incohérent.</span><span class="sxs-lookup"><span data-stu-id="9fc00-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="9fc00-248">Hello suivant montre l’illustration sortie de console à partir de ces fonctions lorsqu’un message incohérent est traité.</span><span class="sxs-lookup"><span data-stu-id="9fc00-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Sortie de la console pour la gestion des messages incohérents](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="9fc00-250">Gestion manuelle des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="9fc00-250">Manual poison message handling</span></span>
<span data-ttu-id="9fc00-251">Vous pouvez obtenir le nombre de hello de fois où un message n’a été sélectionné pour le traitement en ajoutant une **int** paramètre nommé **dequeueCount** tooyour (fonction).</span><span class="sxs-lookup"><span data-stu-id="9fc00-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="9fc00-252">Vous pouvez ensuite cocher hello dequeue nombre dans le code de fonction et effectuer votre propre gestion de message incohérent lorsque le nombre de hello dépasse un seuil, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="9fc00-253">Comment les options de configuration tooset</span><span class="sxs-lookup"><span data-stu-id="9fc00-253">How tooset configuration options</span></span>
<span data-ttu-id="9fc00-254">Vous pouvez utiliser hello **JobHostConfiguration** hello tooset de type des options de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="9fc00-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="9fc00-255">Définir des chaînes de connexion du Kit de développement logiciel hello dans le code.</span><span class="sxs-lookup"><span data-stu-id="9fc00-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="9fc00-256">Configuration des paramètres **QueueTrigger** tels que le nombre de retraits maximal.</span><span class="sxs-lookup"><span data-stu-id="9fc00-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="9fc00-257">Obtention des noms de file d’attente de la configuration.</span><span class="sxs-lookup"><span data-stu-id="9fc00-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="9fc00-258">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code</span><span class="sxs-lookup"><span data-stu-id="9fc00-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="9fc00-259">Définition des chaînes de connexion du Kit de développement logiciel hello dans le code permet vous toouse vos propres noms de chaîne de connexion dans les fichiers de configuration ou des variables d’environnement, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="9fc00-260">Configuration des paramètres QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="9fc00-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="9fc00-261">Vous pouvez configurer hello suivant les paramètres qui s’appliquent le traitement des messages toohello file d’attente :</span><span class="sxs-lookup"><span data-stu-id="9fc00-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="9fc00-262">Hello nombre maximal de messages de file d’attente sont appliquées simultanément les toobe exécuté en parallèle (valeur par défaut est 16).</span><span class="sxs-lookup"><span data-stu-id="9fc00-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="9fc00-263">Hello nombre maximal de tentatives avant que la file d’attente de messages incohérents tooa envoi d’un message de la file d’attente (valeur par défaut est 5).</span><span class="sxs-lookup"><span data-stu-id="9fc00-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="9fc00-264">délai d’attente maximal Hello avant d’interroger à nouveau lorsqu’une file d’attente est vide (valeur par défaut est 1 minute).</span><span class="sxs-lookup"><span data-stu-id="9fc00-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="9fc00-265">Hello suivant montre l’exemple de comment tooconfigure ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="9fc00-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="9fc00-266">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="9fc00-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="9fc00-267">Parfois vous toospecify un nom de file d’attente, un nom d’objet blob ou un conteneur ou nom de la table dans le code au lieu de coder en dur il.</span><span class="sxs-lookup"><span data-stu-id="9fc00-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="9fc00-268">Par exemple, vous pourriez le nom de file d’attente toospecify hello pour **QueueTrigger** dans une variable d’environnement ou le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="9fc00-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="9fc00-269">C’est également en passant un **NameResolver** objet toohello **JobHostConfiguration** type.</span><span class="sxs-lookup"><span data-stu-id="9fc00-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="9fc00-270">Vous incluez des espaces réservés spéciales, délimitées par des signes de pourcentage (%) dans les paramètres de constructeur d’attribut WebJobs SDK et votre **NameResolver** code spécifie hello toobe de valeurs réelles utilisée à la place de ces espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="9fc00-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="9fc00-271">Par exemple, supposons que vous vouliez toouse une file d’attente nommée logqueuetest dans l’environnement de test hello et un logqueueprod nommée en production.</span><span class="sxs-lookup"><span data-stu-id="9fc00-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="9fc00-272">Au lieu d’un nom codé en dur la file d’attente, vous souhaitez nom hello de toospecify d’une entrée dans hello **appSettings** collection qui aurait le nom de file d’attente réel hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="9fc00-273">Si hello **appSettings** la clé est logqueue, votre fonction pourrait ressembler à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="9fc00-274">Votre **NameResolver** classe pu obtenir ensuite le nom de file d’attente de hello de **appSettings** comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9fc00-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="9fc00-275">Vous passez hello **NameResolver** classe dans toohello **JobHost** de l’objet comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="9fc00-276">**Remarque :** file d’attente, de table et noms d’objets blob ne sont pas résolus chaque fois une fonction est appelée, mais les noms de conteneur d’objets blob sont résolues uniquement au démarrage d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="9fc00-277">Vous ne pouvez pas modifier le nom de conteneur pendant l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="9fc00-278">Comment tootrigger une fonction manuellement</span><span class="sxs-lookup"><span data-stu-id="9fc00-278">How tootrigger a function manually</span></span>
<span data-ttu-id="9fc00-279">une fonction de tootrigger utiliser manuellement, hello **appeler** ou **CallAsync** méthode sur hello **JobHost** objet et hello **NoAutomaticTrigger** attribut sur la fonction hello, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9fc00-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="9fc00-280">Mode de journalisation des toowrite</span><span class="sxs-lookup"><span data-stu-id="9fc00-280">How toowrite logs</span></span>
<span data-ttu-id="9fc00-281">Hello du tableau de bord affiche les journaux à deux emplacements : page hello pourquoi la tâche Web et page hello pour un appel de la tâche Web particulier.</span><span class="sxs-lookup"><span data-stu-id="9fc00-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Journaux affichés dans la page relative aux tâches web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="9fc00-284">Sortie des méthodes de Console que vous appelez une fonction ou Bonjour **Main()** méthode s’affiche dans la page de tableau de bord hello pourquoi la tâche Web, et non dans la page hello pour un appel de méthode particulier.</span><span class="sxs-lookup"><span data-stu-id="9fc00-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="9fc00-285">Sortie à partir de l’objet TextWriter hello que vous obtenez à partir d’un paramètre dans la signature de méthode s’affiche dans la page de tableau de bord hello pour un appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="9fc00-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="9fc00-286">La sortie de console ne peut pas être appel de méthode particulière tooa lié étant hello Console monothread, tandis que de nombreuses fonctions de travail peuvent s’exécuter à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="9fc00-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="9fc00-287">C’est pourquoi hello SDK fournit à chaque appel de fonction avec son propre objet d’enregistreur de journal unique.</span><span class="sxs-lookup"><span data-stu-id="9fc00-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="9fc00-288">toowrite [journaux de suivi d’application](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilisez **Console.Out** (crée des journaux marquées comme INFO) et **Console.Error** (crée des journaux marquées comme erreur).</span><span class="sxs-lookup"><span data-stu-id="9fc00-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="9fc00-289">Une autre solution consiste à toouse [Trace ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), qui fournit des commentaires, avertissement, et des niveaux critique dans tooInfo d’ajout et d’erreur.</span><span class="sxs-lookup"><span data-stu-id="9fc00-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="9fc00-290">Journaux de suivi d’application s’affichent dans les fichiers de journaux hello web app, les tables Azure, ou les objets BLOB Azure en fonction de la façon dont vous configurez votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc00-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="9fc00-291">Qu’est remplie de toutes les sorties de la Console, derniers journaux d’application 100 hello apparaissent également dans la page de tableau de bord hello pourquoi la tâche Web, page de hello pas pour un appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="9fc00-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="9fc00-292">La sortie de console s’affiche dans hello du tableau de bord uniquement si le programme de hello est en cours d’exécution dans une tâche Web Azure, pas si le programme de hello s’exécute localement ou dans tout autre environnement.</span><span class="sxs-lookup"><span data-stu-id="9fc00-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="9fc00-293">Vous pouvez désactiver la journalisation en définissant toonull de chaîne de connexion de tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="9fc00-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="9fc00-294">Pour plus d’informations, consultez [comment tooset les Options de Configuration](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="9fc00-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="9fc00-295">Hello suivant montre plusieurs façons toowrite journaux :</span><span class="sxs-lookup"><span data-stu-id="9fc00-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="9fc00-296">Bonjour le tableau de bord WebJobs SDK, hello sortie de hello **TextWriter** de l’objet s’affiche lorsque vous ouvrez la page toohello pour un particulier appel de fonction et sélectionnez **bascule sortie**:</span><span class="sxs-lookup"><span data-stu-id="9fc00-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Lien d’appel](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="9fc00-299">Bonjour le tableau de bord WebJobs SDK, lignes hello 100 la plus récente de la Console de sortie afficher des lorsque vous accédez page toohello pourquoi la tâche Web (et non de l’appel de la fonction hello) et sélectionnez **bascule sortie**.</span><span class="sxs-lookup"><span data-stu-id="9fc00-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Activer/désactiver la sortie](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="9fc00-301">Dans une tâche Web continue, journaux des applications s’affichent dans/données/tâches/continu/*{webjobname}*/job_log.txt hello web application système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9fc00-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="9fc00-302">Dans une application de hello d’objets blob Azure des journaux ressembler à ceci : 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world !, 2014-09-26T21:01:13, erreur, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world !, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world !,</span><span class="sxs-lookup"><span data-stu-id="9fc00-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="9fc00-303">Et un Bonjour Azure table **Console.Out** et **Console.Error** journaux ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="9fc00-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Journal d’informations dans la table](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Journal d’erreurs dans la table](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="9fc00-306">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fc00-306">Next steps</span></span>
<span data-ttu-id="9fc00-307">Cet article a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc00-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="9fc00-308">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="9fc00-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

