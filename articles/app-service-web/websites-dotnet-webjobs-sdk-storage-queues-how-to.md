---
title: "Utilisation du stockage de file d’attente Microsoft Azure avec le Kit de développement logiciel (SDK) de WebJobs"
description: "Découvrez comment utiliser le stockage de file d’attente Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs. Créez et supprimez des files d’attente ; insérez, lisez, recevez et supprimez les messages de la file d’attente et bien plus encore."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="d9377-104">Utilisation du stockage de file d’attente Microsoft Azure avec le Kit de développement logiciel (SDK) de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d9377-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="d9377-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d9377-105">Overview</span></span>
<span data-ttu-id="d9377-106">Ce guide fournit des exemples de code C# qui indiquent comment utiliser la version 1.x du Kit de développement logiciel (SDK) WebJobs de Microsoft Azure avec le service de stockage de file d’attente Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9377-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="d9377-107">Ce guide suppose que vous savez [comment créer un projet WebJob dans Visual Studio avec des chaînes de connexion qui pointent vers votre compte de stockage](websites-dotnet-webjobs-sdk-get-started.md) ou [plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="d9377-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="d9377-108">La plupart des extraits de code présentent uniquement les fonctions, et non le code chargé de créer l’objet `JobHost` comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d9377-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="d9377-109">Ce guide comprend les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9377-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="d9377-110">Comment déclencher une fonction lors de la réception d’un message de file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="d9377-111">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d9377-111">String queue messages</span></span>
  * <span data-ttu-id="d9377-112">Messages de file d’attente POCO</span><span class="sxs-lookup"><span data-stu-id="d9377-112">POCO queue messages</span></span>
  * <span data-ttu-id="d9377-113">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d9377-113">Async functions</span></span>
  * <span data-ttu-id="d9377-114">Types gérés par l’attribut QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="d9377-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="d9377-115">Algorithme d’interrogation</span><span class="sxs-lookup"><span data-stu-id="d9377-115">Polling algorithm</span></span>
  * <span data-ttu-id="d9377-116">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="d9377-116">Multiple instances</span></span>
  * <span data-ttu-id="d9377-117">Exécution en parallèle</span><span class="sxs-lookup"><span data-stu-id="d9377-117">Parallel execution</span></span>
  * <span data-ttu-id="d9377-118">Obtention des métadonnées de file d'attente ou de message de file d'attente</span><span class="sxs-lookup"><span data-stu-id="d9377-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="d9377-119">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="d9377-119">Graceful shutdown</span></span>
* [<span data-ttu-id="d9377-120">Comment créer un message de file d’attente lors du traitement d’un message de file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="d9377-121">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d9377-121">String queue messages</span></span>
  * <span data-ttu-id="d9377-122">Messages de file d’attente POCO</span><span class="sxs-lookup"><span data-stu-id="d9377-122">POCO queue messages</span></span>
  * <span data-ttu-id="d9377-123">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d9377-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="d9377-124">Types gérés par l’attribut Queue</span><span class="sxs-lookup"><span data-stu-id="d9377-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="d9377-125">Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d9377-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="d9377-126">Comment lire et écrire des objets blob lors du traitement d’un message de file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="d9377-127">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d9377-127">String queue messages</span></span>
  * <span data-ttu-id="d9377-128">Messages de file d’attente POCO</span><span class="sxs-lookup"><span data-stu-id="d9377-128">POCO queue messages</span></span>
  * <span data-ttu-id="d9377-129">Types gérés par l’attribut Blob</span><span class="sxs-lookup"><span data-stu-id="d9377-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="d9377-130">Gestion des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="d9377-131">Gestion automatique des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="d9377-132">Gestion manuelle des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-132">Manual poison message handling</span></span>
* [<span data-ttu-id="d9377-133">Définition des options de configuration</span><span class="sxs-lookup"><span data-stu-id="d9377-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="d9377-134">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code</span><span class="sxs-lookup"><span data-stu-id="d9377-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="d9377-135">Configuration des paramètres QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="d9377-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="d9377-136">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="d9377-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="d9377-137">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d9377-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="d9377-138">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="d9377-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="d9377-139">Gestion des erreurs et configuration des délais d'attente</span><span class="sxs-lookup"><span data-stu-id="d9377-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="d9377-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9377-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="d9377-141"><a id="trigger"></a> Comment déclencher une fonction lors de la réception d’un message de file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="d9377-142">Pour écrire une fonction que le Kit de développement logiciel (SDK) WebJobs appelle durant la réception d’un message en file d’attente, utilisez l’attribut `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="d9377-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="d9377-143">Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom de la file d’attente à interroger.</span><span class="sxs-lookup"><span data-stu-id="d9377-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="d9377-144">Vous pouvez également [définir de manière dynamique le nom de la file d’attente](#config).</span><span class="sxs-lookup"><span data-stu-id="d9377-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d9377-145">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d9377-145">String queue messages</span></span>
<span data-ttu-id="d9377-146">Dans l’exemple suivant, la file d’attente contient un message de chaîne ; ainsi, `QueueTrigger` est appliqué à un paramètre de chaîne nommé `logMessage`, qui inclut le contenu du message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d9377-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="d9377-147">La fonction [écrit un message de journal dans le tableau de bord](#logs).</span><span class="sxs-lookup"><span data-stu-id="d9377-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="d9377-148">En plus de `string`, le paramètre peut correspondre à un tableau d’octets, à un objet `CloudQueueMessage` ou à un objet POCO que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="d9377-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d9377-149">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="d9377-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d9377-150">Dans l’exemple suivant, le message en file d’attente contient JSON pour un objet `BlobInformation` qui inclut une propriété `BlobName`.</span><span class="sxs-lookup"><span data-stu-id="d9377-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="d9377-151">Le Kit de développement logiciel (SDK) désérialise automatiquement l’objet.</span><span class="sxs-lookup"><span data-stu-id="d9377-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="d9377-152">Le Kit de développement logiciel (SDK) utilise le package [NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) pour sérialiser et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="d9377-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="d9377-153">Si vous créez des messages en file d’attente dans un programme qui n’utilise pas le Kit de développement logiciel (SDK) WebJobs, vous pouvez écrire le code comme dans l’exemple suivant, afin de créer un message en file d’attente POCO que le Kit de développement logiciel (SDK) peut analyser.</span><span class="sxs-lookup"><span data-stu-id="d9377-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="d9377-154">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d9377-154">Async functions</span></span>
<span data-ttu-id="d9377-155">La fonction asynchrone suivante [écrit un journal dans le tableau de bord](#logs).</span><span class="sxs-lookup"><span data-stu-id="d9377-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="d9377-156">Les fonctions asynchrones peuvent prendre un [jeton d’annulation](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), comme illustré dans l’exemple suivant, qui copie un objet blob.</span><span class="sxs-lookup"><span data-stu-id="d9377-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="d9377-157">(Pour obtenir une explication sur l’espace réservé `queueTrigger` , consultez la section [Objets blob](#blobs) .)</span><span class="sxs-lookup"><span data-stu-id="d9377-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="d9377-158"><a id="qtattributetypes"></a> Types gérés par l’attribut QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="d9377-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="d9377-159">Vous pouvez utiliser l’attribut `QueueTrigger` avec les types suivants :</span><span class="sxs-lookup"><span data-stu-id="d9377-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="d9377-160">Type d’objet POCO sérialisé au format JSON</span><span class="sxs-lookup"><span data-stu-id="d9377-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="d9377-161"><a id="polling"></a> Algorithme d’interrogation</span><span class="sxs-lookup"><span data-stu-id="d9377-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="d9377-162">Le Kit de développement logiciel (SDK) implémente un algorithme d’interruption exponentiel et aléatoire pour réduire l’effet de l’interrogation de file d’attente inactive sur les coûts de transactions de stockage.</span><span class="sxs-lookup"><span data-stu-id="d9377-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="d9377-163">Quand un message est détecté, le Kit de développement logiciel (SDK) attend deux secondes, puis vérifie s’il existe un autre message ; quand aucun message n’est détecté, il attend environ quatre secondes avant de réessayer.</span><span class="sxs-lookup"><span data-stu-id="d9377-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="d9377-164">Après plusieurs échecs de tentatives d’obtention d’un message de file d’attente, le temps d’attente continue à augmenter jusqu’à ce qu’il atteigne le délai d’attente maximal par défaut (une minute).</span><span class="sxs-lookup"><span data-stu-id="d9377-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="d9377-165">[Le délai d’attente maximal est configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="d9377-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="d9377-166"><a id="instances"></a> Instances multiples</span><span class="sxs-lookup"><span data-stu-id="d9377-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="d9377-167">Si votre application web s'exécute sur plusieurs instances, une tâche web continue se lance sur chaque machine, qui attend des déclencheurs et essaie d'exécuter les fonctions.</span><span class="sxs-lookup"><span data-stu-id="d9377-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="d9377-168">Le déclencheur de la file d'attente SDK WebJobs empêche automatiquement une fonction de traiter un message de file d'attente plusieurs fois ; les fonctions ne doivent pas nécessairement être écrites pour être idempotent.</span><span class="sxs-lookup"><span data-stu-id="d9377-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="d9377-169">Toutefois, si vous souhaitez vous assurer qu'une seule instance d'une fonction s'exécute même lorsqu'il existe plusieurs instances de l'application web hôte, vous pouvez utiliser l'attribut `Singleton` .</span><span class="sxs-lookup"><span data-stu-id="d9377-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="d9377-170"><a id="parallel"></a> Exécution en parallèle</span><span class="sxs-lookup"><span data-stu-id="d9377-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="d9377-171">Si vous avez plusieurs fonctions à l’écoute sur différentes files d’attente, le Kit de développement logiciel (SDK) les appelle en parallèle en cas de réception de messages simultanés.</span><span class="sxs-lookup"><span data-stu-id="d9377-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="d9377-172">Il en est de même quand plusieurs messages sont reçus en provenance d’une file d’attente unique.</span><span class="sxs-lookup"><span data-stu-id="d9377-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="d9377-173">Par défaut, le Kit de développement logiciel (SDK) obtient un lot de 16 messages de file d’attente à la fois et exécute la fonction qui les traite en parallèle.</span><span class="sxs-lookup"><span data-stu-id="d9377-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="d9377-174">[La taille de lot est configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="d9377-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="d9377-175">Quand le nombre de messages en cours de traitement tombe sous la moitié de la taille de lot, le Kit de développement logiciel (SDK) obtient un autre lot et commence à traiter ces messages.</span><span class="sxs-lookup"><span data-stu-id="d9377-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="d9377-176">Par conséquent, le nombre maximal de messages traités simultanément par la fonction est une fois et demie la taille de lot.</span><span class="sxs-lookup"><span data-stu-id="d9377-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="d9377-177">Cette limite s’applique séparément à chaque fonction qui présente un attribut `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="d9377-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="d9377-178">Si vous ne souhaitez pas d'exécution en parallèle pour les messages reçus sur une file d'attente, vous pouvez affecter la valeur 1 à la taille de lot.</span><span class="sxs-lookup"><span data-stu-id="d9377-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="d9377-179">Voir aussi **Davantage de contrôle sur le traitement de la file d'attente** dans [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="d9377-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="d9377-180"><a id="queuemetadata"></a>Obtenir des métadonnées de file d’attente ou de message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="d9377-181">Vous pouvez obtenir les propriétés de messages suivantes en ajoutant des paramètres à la signature de méthode :</span><span class="sxs-lookup"><span data-stu-id="d9377-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="d9377-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="d9377-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="d9377-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="d9377-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="d9377-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="d9377-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="d9377-185">`string` queueTrigger (contient le texte du message)</span><span class="sxs-lookup"><span data-stu-id="d9377-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="d9377-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="d9377-186">`string` id</span></span>
* <span data-ttu-id="d9377-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="d9377-187">`string` popReceipt</span></span>
* <span data-ttu-id="d9377-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="d9377-188">`int` dequeueCount</span></span>

<span data-ttu-id="d9377-189">Si vous souhaitez travailler directement avec l’API Azure Storage, vous pouvez également ajouter un paramètre `CloudStorageAccount` .</span><span class="sxs-lookup"><span data-stu-id="d9377-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="d9377-190">L’exemple suivant écrit toutes ces métadonnées dans un journal d’application INFO.</span><span class="sxs-lookup"><span data-stu-id="d9377-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="d9377-191">Dans l’exemple, logMessage et queueTrigger contiennent le contenu du message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d9377-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="d9377-192">Voici un exemple de journal écrit par l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="d9377-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="d9377-193"><a id="graceful"></a>Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="d9377-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="d9377-194">Une fonction qui s’exécute dans une tâche web continue peut accepter un paramètre `CancellationToken` , qui permet au système d’exploitation de notifier la fonction lorsque la tâche web est sur le point de se terminer.</span><span class="sxs-lookup"><span data-stu-id="d9377-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="d9377-195">Vous pouvez utiliser cette notification pour vous assurer que la fonction ne s’arrête pas de manière inattendue et laisse les données dans un état incohérent.</span><span class="sxs-lookup"><span data-stu-id="d9377-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="d9377-196">L’exemple suivant montre comment vérifier l’arrêt imminent d’une tâche web dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="d9377-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="d9377-197">**Remarque :** le tableau de bord peut ne pas afficher correctement l’état et la sortie des fonctions qui ont été arrêtées.</span><span class="sxs-lookup"><span data-stu-id="d9377-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="d9377-198">Pour plus d’informations, consultez [Arrêt correct de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="d9377-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="d9377-199"><a id="createqueue"></a> Comment créer un message de file d’attente lors du traitement d’un message de file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="d9377-200">Pour écrire une fonction qui crée un message en file d’attente, utilisez l’attribut `Queue` .</span><span class="sxs-lookup"><span data-stu-id="d9377-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="d9377-201">Comme l’élément `QueueTrigger`, vous passez le nom de la file d’attente sous forme de chaîne ou vous pouvez [définir de manière dynamique le nom de la file d’attente](#config).</span><span class="sxs-lookup"><span data-stu-id="d9377-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d9377-202">Messages de file d’attente de chaîne</span><span class="sxs-lookup"><span data-stu-id="d9377-202">String queue messages</span></span>
<span data-ttu-id="d9377-203">L’exemple de code non asynchrone suivant crée un message en file d’attente dans la file d’attente nommée « outputqueue », avec le même contenu que le message de file d’attente reçu dans la file d’attente « inputqueue ».</span><span class="sxs-lookup"><span data-stu-id="d9377-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="d9377-204">(Dans le cas de fonctions asynchrones, utilisez l’élément `IAsyncCollector<T>` , comme indiqué plus loin dans la présente section.)</span><span class="sxs-lookup"><span data-stu-id="d9377-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d9377-205">Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="d9377-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d9377-206">Pour créer un message de file d’attente qui contient un objet POCO plutôt qu’une chaîne, passez le type POCO en tant que paramètre de sortie au constructeur d’attribut `Queue` .</span><span class="sxs-lookup"><span data-stu-id="d9377-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="d9377-207">Le Kit de développement logiciel (SDK) sérialise automatiquement l’objet au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d9377-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="d9377-208">Un message de file d’attente est toujours créé, même si l’objet est null.</span><span class="sxs-lookup"><span data-stu-id="d9377-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="d9377-209">Création de plusieurs messages de file d’attente dans des fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="d9377-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="d9377-210">Pour créer plusieurs messages, choisissez le type de paramètre pour la file d’attente de sortie `ICollector<T>` ou `IAsyncCollector<T>`, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="d9377-211">Chaque message de file d’attente est créé immédiatement après l’appel de la méthode `Add` .</span><span class="sxs-lookup"><span data-stu-id="d9377-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="d9377-212">Types gérés par l’attribut Queue</span><span class="sxs-lookup"><span data-stu-id="d9377-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="d9377-213">Vous pouvez utiliser l’attribut `Queue` sur les types de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="d9377-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="d9377-214">`out string` (crée le message en file d’attente si la valeur du paramètre n’est pas null lorsque la fonction se termine)</span><span class="sxs-lookup"><span data-stu-id="d9377-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="d9377-215">`out byte[]` (fonctionne comme `string`)</span><span class="sxs-lookup"><span data-stu-id="d9377-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="d9377-216">`out CloudQueueMessage` (fonctionne comme `string`)</span><span class="sxs-lookup"><span data-stu-id="d9377-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="d9377-217">`out POCO` (type sérialisable, qui crée un message avec un objet null si le paramètre est null lorsque la fonction se termine)</span><span class="sxs-lookup"><span data-stu-id="d9377-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="d9377-218">`CloudQueue` (dédié à la création manuelle de messages via l’utilisation directe de l’API Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="d9377-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="d9377-219"><a id="ibinder"></a>Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d9377-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="d9377-220">Si vous avez besoin d’effectuer une tâche dans votre fonction avant d’utiliser un attribut de Kit de développement logiciel (SDK) WebJobs comme `Queue`, `Blob`, ou `Table`, vous pouvez utiliser l’interface `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="d9377-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="d9377-221">L’exemple suivant prend un message en file d’attente d’entrée et crée un message avec le même contenu dans une file d’attente de sortie.</span><span class="sxs-lookup"><span data-stu-id="d9377-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="d9377-222">Le nom de file d’attente de sortie est défini par le code dans le corps de la fonction.</span><span class="sxs-lookup"><span data-stu-id="d9377-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="d9377-223">L’interface `IBinder` peut également être utilisée avec les attributs `Table` et `Blob`.</span><span class="sxs-lookup"><span data-stu-id="d9377-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="d9377-224"><a id="blobs"></a> Comment lire et écrire des objets blob et des tables lors du traitement d’un message en file d’attente</span><span class="sxs-lookup"><span data-stu-id="d9377-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="d9377-225">Les attributs `Blob` et `Table` permettent de lire et d’écrire des objets blob et des tables.</span><span class="sxs-lookup"><span data-stu-id="d9377-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="d9377-226">Les exemples de cette section s’appliquent aux objets blob.</span><span class="sxs-lookup"><span data-stu-id="d9377-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="d9377-227">Pour obtenir des exemples de code qui lisent et écrivent des tables, voir [Utilisation du stockage de tables Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md). Pour obtenir des exemples de code qui indiquent comment déclencher des processus lors de la création ou de la mise à jour d’objets blob, voir [Utilisation du Stockage Blob Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="d9377-228">Messages en file d’attente de chaîne déclenchant des opérations d’objet blob</span><span class="sxs-lookup"><span data-stu-id="d9377-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="d9377-229">Pour un message de file d’attente qui contient une chaîne, l’élément `queueTrigger` est un espace réservé que vous pouvez utiliser dans le paramètre `blobPath` de l’attribut `Blob`qui inclut le contenu du message.</span><span class="sxs-lookup"><span data-stu-id="d9377-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="d9377-230">L’exemple suivant utilise des objets `Stream` pour lire et écrire des objets blob.</span><span class="sxs-lookup"><span data-stu-id="d9377-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="d9377-231">Le message de file d’attente correspond au nom d’un objet blob situé dans le conteneur textblobs.</span><span class="sxs-lookup"><span data-stu-id="d9377-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="d9377-232">Une copie de l’objet blob, la chaîne « -new » étant ajoutée au nom, est créée dans le même conteneur.</span><span class="sxs-lookup"><span data-stu-id="d9377-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d9377-233">Le constructeur d’attribut `Blob` prend un paramètre `blobPath` qui indique le nom de l’objet blob et du conteneur.</span><span class="sxs-lookup"><span data-stu-id="d9377-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="d9377-234">Pour en savoir plus sur cet espace réservé, voir [Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="d9377-235">Lorsque l’attribut décore un objet `Stream`, un autre paramètre de constructeur spécifie le mode `FileAccess` (lecture, écriture ou lecture/écriture).</span><span class="sxs-lookup"><span data-stu-id="d9377-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="d9377-236">L’exemple suivant utilise un objet `CloudBlockBlob` pour supprimer un objet blob.</span><span class="sxs-lookup"><span data-stu-id="d9377-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="d9377-237">Le message de la file d’attente correspond au nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="d9377-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="d9377-238"><a id="pocoblobs"></a> Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="d9377-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d9377-239">Pour un objet POCO stocké au format JSON dans le message en file d’attente, vous pouvez utiliser des espaces réservés qui nomment les propriétés de l’objet dans le paramètre `blobPath` de l’attribut `Queue`.</span><span class="sxs-lookup"><span data-stu-id="d9377-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="d9377-240">Vous pouvez également utiliser des [noms de propriété de métadonnées de file d’attente](#queuemetadata) comme espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="d9377-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="d9377-241">L’exemple suivant copie un objet blob dans un nouvel objet blob, avec une autre extension.</span><span class="sxs-lookup"><span data-stu-id="d9377-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="d9377-242">Le message en file d’attente est un objet `BlobInformation` qui inclut les propriétés `BlobName` et `BlobNameWithoutExtension`.</span><span class="sxs-lookup"><span data-stu-id="d9377-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="d9377-243">Les noms de propriété sont utilisés en tant qu’espaces réservés dans le chemin de l’objet blob pour les attributs `Blob` .</span><span class="sxs-lookup"><span data-stu-id="d9377-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d9377-244">Le Kit de développement logiciel (SDK) utilise le package [NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) pour sérialiser et désérialiser les messages.</span><span class="sxs-lookup"><span data-stu-id="d9377-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="d9377-245">Si vous créez des messages en file d’attente dans un programme qui n’utilise pas le Kit de développement logiciel (SDK) WebJobs, vous pouvez écrire le code comme dans l’exemple suivant, afin de créer un message en file d’attente POCO que le Kit de développement logiciel (SDK) peut analyser.</span><span class="sxs-lookup"><span data-stu-id="d9377-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="d9377-246">Si vous devez effectuer un travail dans votre fonction avant de lier un objet blob à un objet, vous pouvez utiliser l’attribut dans le corps de la fonction [comme indiqué plus haut pour l’attribut Queue](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="d9377-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="d9377-247"><a id="blobattributetypes"></a> Types avec lesquels vous pouvez utiliser l’attribut blob</span><span class="sxs-lookup"><span data-stu-id="d9377-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="d9377-248">L’attribut `Blob` peut être utilisé avec les types suivants :</span><span class="sxs-lookup"><span data-stu-id="d9377-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="d9377-249">`Stream` (lecture ou écriture ; spécifié à l’aide du paramètre de constructeur FileAccess)</span><span class="sxs-lookup"><span data-stu-id="d9377-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="d9377-250">`string` (lecture)</span><span class="sxs-lookup"><span data-stu-id="d9377-250">`string` (read)</span></span>
* <span data-ttu-id="d9377-251">`out string` (écriture ; crée un objet blob uniquement si le paramètre de chaîne n’est pas null lorsque la fonction renvoie des résultats)</span><span class="sxs-lookup"><span data-stu-id="d9377-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="d9377-252">POCO (lecture)</span><span class="sxs-lookup"><span data-stu-id="d9377-252">POCO (read)</span></span>
* <span data-ttu-id="d9377-253">out POCO (écriture ; crée systématiquement un objet blob, créé en tant qu’objet null si le paramètre POCO est null lorsque la fonction renvoie des résultats)</span><span class="sxs-lookup"><span data-stu-id="d9377-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="d9377-254">`CloudBlobStream` (écriture)</span><span class="sxs-lookup"><span data-stu-id="d9377-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="d9377-255">`ICloudBlob` (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="d9377-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="d9377-256">`CloudBlockBlob` (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="d9377-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="d9377-257">`CloudPageBlob` (lecture ou écriture)</span><span class="sxs-lookup"><span data-stu-id="d9377-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="d9377-258"><a id="poison"></a> Gestion des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="d9377-259">Les messages dont le contenu provoque l'échec d'une fonction sont appelés *messages incohérents*.</span><span class="sxs-lookup"><span data-stu-id="d9377-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="d9377-260">Lorsque la fonction échoue, le message en file d’attente n’est pas supprimé, mais finalement récupéré à nouveau, provoquant la répétition du cycle.</span><span class="sxs-lookup"><span data-stu-id="d9377-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="d9377-261">Le Kit de développement logiciel (SDK) peut interrompre automatiquement le cycle après un nombre limité d’itérations, ou vous pouvez le faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="d9377-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="d9377-262">Gestion automatique des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-262">Automatic poison message handling</span></span>
<span data-ttu-id="d9377-263">Le Kit de développement logiciel (SDK) appelle une fonction jusqu’à cinq fois pour traiter un message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d9377-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="d9377-264">Si la cinquième tentative échoue, le message est déplacé vers une file d’attente de messages incohérents.</span><span class="sxs-lookup"><span data-stu-id="d9377-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="d9377-265">[Vous pouvez configurer le nombre maximal de tentatives](#config).</span><span class="sxs-lookup"><span data-stu-id="d9377-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="d9377-266">La file d'attente de messages incohérents se nomme *{nom_file_d'attente_d'origine}*-poison.</span><span class="sxs-lookup"><span data-stu-id="d9377-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="d9377-267">Vous pouvez écrire une fonction pour traiter les messages de la file d’attente de messages incohérents en les consignant dans un journal ou en envoyant une notification signalant qu’une attention manuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d9377-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="d9377-268">Dans l’exemple suivant, la fonction `CopyBlob` échoue lorsqu’un message en file d’attente contient le nom d’un objet blob qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="d9377-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="d9377-269">Quand cela se produit, le message est déplacé de la file d’attente copyblobqueue vers la file d’attente copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="d9377-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="d9377-270">L’élément `ProcessPoisonMessage` consigne ensuite le message incohérent.</span><span class="sxs-lookup"><span data-stu-id="d9377-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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

<span data-ttu-id="d9377-271">L’illustration suivante montre la sortie de console de ces fonctions pendant le traitement d’un message incohérent.</span><span class="sxs-lookup"><span data-stu-id="d9377-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Sortie de la console pour la gestion des messages incohérents](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="d9377-273">Gestion manuelle des messages incohérents</span><span class="sxs-lookup"><span data-stu-id="d9377-273">Manual poison message handling</span></span>
<span data-ttu-id="d9377-274">Vous pouvez obtenir le nombre de fois qu’un message a été récupéré pour le traitement en ajoutant un paramètre `int` nommé `dequeueCount` à votre fonction.</span><span class="sxs-lookup"><span data-stu-id="d9377-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="d9377-275">Vous pouvez ensuite vérifier le nombre d’enlèvements de la file d’attente dans le code de fonction et effectuer votre propre gestion des messages incohérents quand le nombre dépasse un seuil, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <span data-ttu-id="d9377-276"><a id="config"></a> Définition des options de configuration</span><span class="sxs-lookup"><span data-stu-id="d9377-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="d9377-277">Vous pouvez utiliser le type `JobHostConfiguration` pour définir les options de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9377-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="d9377-278">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code.</span><span class="sxs-lookup"><span data-stu-id="d9377-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="d9377-279">Configuration des paramètres `QueueTrigger` tels que le nombre maximal d’enlèvements de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d9377-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="d9377-280">Obtention des noms de file d’attente de la configuration.</span><span class="sxs-lookup"><span data-stu-id="d9377-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="d9377-281"><a id="setconnstr"></a>Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code</span><span class="sxs-lookup"><span data-stu-id="d9377-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="d9377-282">La définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code vous permet d’utiliser vos propres noms de chaînes de connexion dans les fichiers de configuration ou les variables d’environnement, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="d9377-283"><a id="configqueue"></a>Configuration des paramètres QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="d9377-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="d9377-284">Vous pouvez configurer les paramètres suivants, qui s’appliquent au traitement des messages en file d’attente :</span><span class="sxs-lookup"><span data-stu-id="d9377-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="d9377-285">nombre maximal de messages de file d'attente prélevés simultanément pour être exécutés en parallèle (la valeur par défaut est 16) ;</span><span class="sxs-lookup"><span data-stu-id="d9377-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="d9377-286">nombre maximal de tentatives avant l'envoi d'un message de file d'attente à une file d'attente de messages incohérents (la valeur par défaut est 5) ;</span><span class="sxs-lookup"><span data-stu-id="d9377-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="d9377-287">durée d'attente maximale avant la nouvelle interrogation quand une file d'attente est vide (la valeur par défaut est 1 minute).</span><span class="sxs-lookup"><span data-stu-id="d9377-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="d9377-288">L’exemple suivant montre comment configurer ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="d9377-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="d9377-289"><a id="setnamesincode"></a>Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="d9377-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="d9377-290">Dans certains cas, vous souhaitez spécifier dans le code un nom de file d’attente, un nom d’objet blob ou un conteneur, ou encore un nom de table, plutôt que de les coder en dur.</span><span class="sxs-lookup"><span data-stu-id="d9377-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="d9377-291">Par exemple, vous pouvez souhaiter spécifier le nom de la file d’attente de `QueueTrigger` dans une variable d’environnement ou un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="d9377-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="d9377-292">Pour cela, passez un objet `NameResolver` au type `JobHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="d9377-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="d9377-293">Incluez des espaces réservés spéciaux, entourés par des signes de pourcentage (%) dans les paramètres de constructeur d’attribut de Kit de développement logiciel (SDK) pour que votre code `NameResolver` spécifie les valeurs réelles à utiliser à la place de ces espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="d9377-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="d9377-294">Par exemple, supposons que vous souhaitez utiliser une file d’attente nommée logqueuetest dans l’environnement de test et une autre nommée logqueueprod en production.</span><span class="sxs-lookup"><span data-stu-id="d9377-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="d9377-295">Au lieu d’un nom de file d’attente codé en dur, vous souhaitez spécifier le nom d’une entrée dans la collection `appSettings` ayant le nom de la file d’attente réelle.</span><span class="sxs-lookup"><span data-stu-id="d9377-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="d9377-296">Si la clé est `appSettings` , votre fonction pourrait ressembler à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="d9377-297">Votre classe `NameResolver` peut alors obtenir le nom de la file d'attente à partir de `appSettings`, comme indiqué dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d9377-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="d9377-298">Vous passez la classe `NameResolver` à l’objet `JobHost`, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="d9377-299">**Remarque :** les noms d’objet blob, de table et de file d’attente sont résolus chaque fois qu’une fonction est appelée, mais les noms de conteneur d’objet blob sont uniquement résolus au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="d9377-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="d9377-300">Vous ne pouvez pas modifier le nom d’un conteneur d’objet blob lorsque la tâche s’exécute.</span><span class="sxs-lookup"><span data-stu-id="d9377-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="d9377-301"><a id="manual"></a>Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d9377-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="d9377-302">Pour déclencher une fonction manuellement, utilisez la méthode `Call` ou `CallAsync` sur l’objet `JobHost` et l’attribut `NoAutomaticTrigger` sur la fonction, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="d9377-303"><a id="logs"></a>Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="d9377-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="d9377-304">Le tableau de bord affiche des journaux à deux emplacements : la page relative aux tâches web et la page portant sur l’appel d’une tâche web spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9377-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Journaux affichés dans la page relative aux tâches web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Journaux affichés dans la page d’appel de fonctions](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="d9377-307">La sortie des méthodes de console que vous appelez dans une fonction ou dans la méthode `Main()` s’affiche dans la page Tableau de bord de la tâche web, et non dans la page relative à l’appel d’une méthode particulière.</span><span class="sxs-lookup"><span data-stu-id="d9377-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="d9377-308">La sortie de l’objet TextWriter que vous obtenez à partir d’un paramètre dans la signature de méthode s’affiche dans la page Tableau de bord relative à l’appel d’une méthode.</span><span class="sxs-lookup"><span data-stu-id="d9377-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="d9377-309">La sortie de la console ne peut pas être liée à un appel de méthode particulier, car la console présente un thread unique, tandis que de nombreuses fonctions de tâche peuvent s’exécuter en même temps.</span><span class="sxs-lookup"><span data-stu-id="d9377-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="d9377-310">C’est pourquoi le Kit de développement logiciel (SDK) fournit à chaque appel de fonction son propre objet d’enregistreur de journal unique.</span><span class="sxs-lookup"><span data-stu-id="d9377-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="d9377-311">Pour écrire des [journaux de suivi d’application](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilisez `Console.Out` (crée des journaux marqués INFO) et `Console.Error` (crée des journaux marqués ERROR).</span><span class="sxs-lookup"><span data-stu-id="d9377-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="d9377-312">Vous pouvez aussi utiliser des éléments [Trace ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), qui fournissent des niveaux supplémentaires (En clair, Avertissement et Critique).</span><span class="sxs-lookup"><span data-stu-id="d9377-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="d9377-313">Les journaux de suivi d’application s’affichent dans les fichiers de journaux d’application web, les tables Microsoft Azure, ou les objets blob Microsoft Azure, selon la configuration de votre application web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9377-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="d9377-314">Comme pour toutes les autres sorties de console, les 100 journaux d’application les plus récents s’affichent également dans la page Tableau de bord de la tâche web, et non dans la page d’appel d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="d9377-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="d9377-315">La sortie de console s’affiche dans le tableau de bord uniquement si le programme s’exécute dans une tâche web Microsoft Azure, et non lorsque le programme est exécuté localement ou dans un autre environnement.</span><span class="sxs-lookup"><span data-stu-id="d9377-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="d9377-316">Désactivez la journalisation du tableau de bord pour les scénarios à débit élevé.</span><span class="sxs-lookup"><span data-stu-id="d9377-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="d9377-317">Par défaut, le Kit de développement logiciel (SDK) écrit des journaux de stockage, et cette activité peut dégrader les performances lorsque vous traitez un grand nombre de messages.</span><span class="sxs-lookup"><span data-stu-id="d9377-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="d9377-318">Pour désactiver la journalisation, attribuez à la chaîne de connexion du tableau de bord la valeur null comme indiqué dans l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d9377-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="d9377-319">L’exemple suivant montre plusieurs manières d’écrire des journaux :</span><span class="sxs-lookup"><span data-stu-id="d9377-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="d9377-320">Dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs, la sortie de l’objet `TextWriter` apparaît lorsque vous accédez à la page relative à l’appel d’une fonction particulière et que vous cliquez sur **Activer/désactiver la sortie**:</span><span class="sxs-lookup"><span data-stu-id="d9377-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Cliquez sur le lien d’appel de fonction](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Journaux affichés dans la page d’appel de fonctions](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="d9377-323">Dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs, les 100 lignes les plus récentes de la sortie de console apparaissent lorsque vous accédez à la page de la tâche web (et non à celle de l’appel de fonction) et que vous cliquez sur **Activer/désactiver la sortie**.</span><span class="sxs-lookup"><span data-stu-id="d9377-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Cliquez sur Activer/désactiver la sortie](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="d9377-325">Dans une tâche web continue, les journaux des applications apparaissent dans /data/jobs/continuous/*{nom_tâche_web*/job_log.txt dans le système de fichiers du site web.</span><span class="sxs-lookup"><span data-stu-id="d9377-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="d9377-326">Dans un objet blob Azure, les journaux d’application ressemblent à ceci : 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="d9377-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="d9377-327">Dans une table Azure, les journaux `Console.Out` et `Console.Error` ressemblent quant à eux à ceci :</span><span class="sxs-lookup"><span data-stu-id="d9377-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Journal d’informations dans la table](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Journal d’erreurs dans la table](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="d9377-330">Si vous souhaitez incorporer dans votre propre journal, consultez [cet exemple](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="d9377-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="d9377-331"><a id="errors"></a>Gestion des erreurs et configuration des délais d'attente</span><span class="sxs-lookup"><span data-stu-id="d9377-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="d9377-332">Le SDK WebJobs inclut également un attribut [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) que vous pouvez utiliser pour qu'une fonction soit annulée si elle ne se termine pas dans un laps de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="d9377-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="d9377-333">Et si vous souhaitez déclencher une alerte lorsque trop d'erreurs se produisent pendant une période de temps spécifiée, vous pouvez utiliser l'attribut `ErrorTrigger` .</span><span class="sxs-lookup"><span data-stu-id="d9377-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="d9377-334">Voici un [exemple ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="d9377-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="d9377-335">Vous pouvez également désactiver et activer dynamiquement des fonctions pour contrôler si elles peuvent être déclenchées, en utilisant un commutateur de configuration qui peut être un paramètre d'application ou le nom de variable d'environnement.</span><span class="sxs-lookup"><span data-stu-id="d9377-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="d9377-336">Pour l'exemple de code, consultez l'attribut `Disable` dans le [référentiel des exemples du Kit de développement logiciel (SDK) WebJobs](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="d9377-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="d9377-337"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9377-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="d9377-338">Ce guide fournit des exemples de code qui indiquent comment gérer des scénarios courants pour l’utilisation des files d’attente Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9377-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="d9377-339">Pour plus d’informations sur l’utilisation d’Azure Webjobs et du Kit de développement logiciel (SDK) WebJobs Azure, consultez la rubrique [Azure Webjobs - Ressources recommandées](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d9377-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
