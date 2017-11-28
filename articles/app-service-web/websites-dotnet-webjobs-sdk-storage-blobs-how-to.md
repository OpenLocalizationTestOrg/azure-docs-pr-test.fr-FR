---
title: "aaaHow toouse stockage d’objets blob Azure avec hello WebJobs SDK"
description: "Découvrez comment toouse Azure stockage d’objets blob par hello WebJobs SDK. Déclenchez un processus lorsqu’un nouvel objet blob apparaît dans un conteneur et gérez les « objets blob incohérents »."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="f4c11-104">Comment toouse Azure stockage d’objets blob par hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="f4c11-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="f4c11-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f4c11-105">Overview</span></span>
<span data-ttu-id="f4c11-106">Ce guide fournit des c# des exemples de code qui montrent comment tootrigger un processus lorsqu’un objet blob Azure est créé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f4c11-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="f4c11-107">utilisation des exemples de code de Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="f4c11-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="f4c11-108">Pour obtenir des exemples de code qui montrent comment toocreate les objets BLOB, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f4c11-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="f4c11-109">guide de Hello suppose que vous connaissez [comment toocreate un projet de la tâche Web dans Visual Studio avec connexion chaînes ce compte de stockage point tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou trop[plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f4c11-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="f4c11-110"><a id="trigger"></a>Comment tootrigger une fonction lorsqu’un objet blob est créé ou mis à jour</span><span class="sxs-lookup"><span data-stu-id="f4c11-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="f4c11-111">Cette section montre comment toouse hello `BlobTrigger` attribut.</span><span class="sxs-lookup"><span data-stu-id="f4c11-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4c11-112">Hello toowatch de fichiers WebJobs SDK analyses de journal pour les objets BLOB nouveau ou modifié.</span><span class="sxs-lookup"><span data-stu-id="f4c11-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="f4c11-113">Ce processus n’est pas en temps réel ; une fonction ne peut-être pas déclenchée jusqu'à ce que quelques minutes ou plus après que l’objet blob de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="f4c11-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="f4c11-114">En outre, des [journaux de stockage sont créés sur la base du « meilleur effort »](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; il n’est pas garanti que tous les événements soient capturés.</span><span class="sxs-lookup"><span data-stu-id="f4c11-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="f4c11-115">Dans certaines conditions, des journaux peuvent être omis.</span><span class="sxs-lookup"><span data-stu-id="f4c11-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="f4c11-116">Si hello les limitations de vitesse et la fiabilité des déclencheurs de l’objet blob ne sont pas acceptables pour votre application, hello recommandé consiste toocreate un message de la file d’attente lorsque vous créez les blob hello et que vous utilisez hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) au lieu de Hello `BlobTrigger` attribut sur la fonction hello qui traite l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="f4c11-117">Espace réservé unique pour le nom d’objet blob avec extension</span><span class="sxs-lookup"><span data-stu-id="f4c11-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="f4c11-118">Hello exemple de code suivant copie les objets BLOB de texte qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur :</span><span class="sxs-lookup"><span data-stu-id="f4c11-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="f4c11-119">constructeur d’attribut Hello prend un paramètre de chaîne qui spécifie le nom du conteneur hello et un espace réservé pour le nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="f4c11-120">Dans cet exemple, si un objet blob nommé *Blob1.txt* est créé dans hello *d’entrée* conteneur, la fonction hello crée un objet blob nommé *Blob1.txt* Bonjour *sortie*  conteneur.</span><span class="sxs-lookup"><span data-stu-id="f4c11-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="f4c11-121">Vous pouvez spécifier un modèle de nom avec un espace réservé au nom hello blob, comme indiqué dans hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="f4c11-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="f4c11-122">Ce code copie uniquement les objets blob dont le nom commence par "original-".</span><span class="sxs-lookup"><span data-stu-id="f4c11-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="f4c11-123">Par exemple, *d’origine-Blob1.txt* Bonjour *d’entrée* conteneur est copié trop*copie-Blob1.txt* Bonjour *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="f4c11-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="f4c11-124">Si vous avez besoin de toospecify un modèle de nom pour les noms d’objet blob qui ont des accolades dans le nom de hello, deux accolades hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="f4c11-125">Par exemple, si vous souhaitez que les objets BLOB toofind hello *images* conteneur qui ont des noms comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4c11-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="f4c11-126">utilisez ce qui suit pour votre modèle :</span><span class="sxs-lookup"><span data-stu-id="f4c11-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="f4c11-127">Dans l’exemple de hello, hello *nom* valeur d’espace réservé serait *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="f4c11-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="f4c11-128">Séparation des espaces réservés d’extension et des noms d’objet blob</span><span class="sxs-lookup"><span data-stu-id="f4c11-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="f4c11-129">Hello modifications suivantes au code exemple hello extension de fichier pendant la copie des objets BLOB qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="f4c11-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="f4c11-130">code de Hello consigne extension hello Hello *d’entrée* d’objets blob et définit l’extension hello Hello *sortie* trop d’objets blob*.txt*.</span><span class="sxs-lookup"><span data-stu-id="f4c11-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="f4c11-131"><a id="types"></a>Types que vous pouvez lier tooblobs</span><span class="sxs-lookup"><span data-stu-id="f4c11-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="f4c11-132">Vous pouvez utiliser hello `BlobTrigger` attribut sur hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="f4c11-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="f4c11-133">Autres types de désérialisation par [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="f4c11-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="f4c11-134">Si vous souhaitez toowork directement avec hello compte de stockage Azure, vous pouvez également ajouter un `CloudStorageAccount` la signature de méthode toohello paramètre.</span><span class="sxs-lookup"><span data-stu-id="f4c11-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="f4c11-135">Pour obtenir des exemples, consultez hello [code de liaison dans le référentiel du Kit sdk azure webjobs hello sur GitHub.com d’objets blob](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f4c11-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="f4c11-136"><a id="string"></a>Mise en route du contenu d’objet blob de texte par liaison toostring</span><span class="sxs-lookup"><span data-stu-id="f4c11-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="f4c11-137">Si les objets BLOB de texte est attendus, `BlobTrigger` peuvent être appliqué tooa `string` paramètre.</span><span class="sxs-lookup"><span data-stu-id="f4c11-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="f4c11-138">exemple de code suivant Hello lie un tooa d’objets blob de texte `string` paramètre nommé `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="f4c11-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="f4c11-139">fonction Hello utilise ce contenu de hello paramètre toowrite de hello blob toohello du tableau de bord WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="f4c11-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="f4c11-140"><a id="icbsb"></a> Obtention de contenu d’objet blob sérialisé via ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="f4c11-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="f4c11-141">Hello exemple de code suivant utilise une classe qui implémente `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind un toohello de l’objet blob d’attribut `WebImage` type.</span><span class="sxs-lookup"><span data-stu-id="f4c11-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="f4c11-142">Hello `WebImage` code de liaison est fournie dans un `WebImageBinder` classe qui dérive de `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="f4c11-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="f4c11-143">Mise en route de chemin d’accès des blob hello pour hello déclenchant des objets blob</span><span class="sxs-lookup"><span data-stu-id="f4c11-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="f4c11-144">nom du conteneur tooget hello et nom d’objet blob d’objet blob hello qui a déclenché fonction hello, incluent un `blobTrigger` paramètre dans la signature de fonction hello de chaîne.</span><span class="sxs-lookup"><span data-stu-id="f4c11-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="f4c11-145"><a id="poison"></a>Comment les objets BLOB toohandle incohérents</span><span class="sxs-lookup"><span data-stu-id="f4c11-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="f4c11-146">Lorsqu’un `BlobTrigger` fonction échoue, hello SDK appelle à nouveau, en cas d’échec de hello a été provoquée par une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="f4c11-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="f4c11-147">Si l’erreur de hello est provoquée par le contenu de l’objet blob de hello hello, fonction hello échoue à chaque fois qu’il essaie d’objet blob de tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="f4c11-148">Par défaut, hello SDK appelle une fonction des heures de too5 pour un objet blob donné.</span><span class="sxs-lookup"><span data-stu-id="f4c11-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="f4c11-149">Si vous essayez de cinquième hello échoue, hello Kit de développement logiciel ajoute une file d’attente de tooa message nommé *webjobs-blobtrigger-incohérents*.</span><span class="sxs-lookup"><span data-stu-id="f4c11-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="f4c11-150">Hello le nombre maximal de tentatives est configurable.</span><span class="sxs-lookup"><span data-stu-id="f4c11-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="f4c11-151">Hello même [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) paramètre est utilisé pour la gestion des objets blob incohérent et la gestion des messages de file d’attente de messages incohérents.</span><span class="sxs-lookup"><span data-stu-id="f4c11-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="f4c11-152">message de file d’attente Hello pour les objets BLOB incohérent est un objet JSON qui contient les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="f4c11-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="f4c11-153">ID de fonction (au format de hello *{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*, par exemple : WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="f4c11-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="f4c11-154">BlobType (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="f4c11-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f4c11-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="f4c11-155">ContainerName</span></span>
* <span data-ttu-id="f4c11-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="f4c11-156">BlobName</span></span>
* <span data-ttu-id="f4c11-157">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="f4c11-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="f4c11-158">Dans hello code suivant exemple hello `CopyBlob` fonction comporte du code qui provoque son toofail chaque fois qu’elle est appelée.</span><span class="sxs-lookup"><span data-stu-id="f4c11-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="f4c11-159">Une fois hello SDK appelle pour le nombre maximal de hello de nouvelles tentatives, un message est créé sur la file d’attente de messages incohérents blob hello et ce message est traité par hello `LogPoisonBlob` (fonction).</span><span class="sxs-lookup"><span data-stu-id="f4c11-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="f4c11-160">Hello SDK désérialise automatiquement un message JSON hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="f4c11-161">Voici hello `PoisonBlobMessage` classe :</span><span class="sxs-lookup"><span data-stu-id="f4c11-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="f4c11-162"><a id="polling"></a> Algorithme d’interrogation des objets blob</span><span class="sxs-lookup"><span data-stu-id="f4c11-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="f4c11-163">Hello WebJobs SDK analyse tous les conteneurs spécifiés par `BlobTrigger` attributs au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="f4c11-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="f4c11-164">Dans un compte de stockage volumineux, cette analyse peut prendre du temps. Il se peut que les nouveaux objets blob ne soient pas tout de suite détectés et que les fonctions `BlobTrigger` ne soient pas exécutées avant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="f4c11-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="f4c11-165">toodetect BLOB nouvelles ou modifiées après le démarrage de l’application, hello que SDK lit périodiquement à partir du stockage d’objets blob hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="f4c11-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="f4c11-166">Hello blob journaux sont en mémoire tampon et sont écrites uniquement physiquement de toutes les 10 minutes ou, par conséquent, il peut y avoir un délai important après un objet blob est créé ou mis à jour avant hello correspondant `BlobTrigger` fonction s’exécute.</span><span class="sxs-lookup"><span data-stu-id="f4c11-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="f4c11-167">Il existe une exception pour les objets BLOB que vous créez à l’aide de hello `Blob` attribut.</span><span class="sxs-lookup"><span data-stu-id="f4c11-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="f4c11-168">Lorsque hello WebJobs SDK crée un nouvel objet blob, il passe immédiatement hello un nouvel objet blob tooany correspondance `BlobTrigger` fonctions.</span><span class="sxs-lookup"><span data-stu-id="f4c11-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="f4c11-169">Par conséquent, si vous avez une chaîne d’objets blob entrées et sorties, hello SDK peut les traiter efficacement.</span><span class="sxs-lookup"><span data-stu-id="f4c11-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="f4c11-170">Mais si vous voulez bénéficier d’une faible latence lors de l’exécution des fonctions de traitement des objets blob créés ou mis à jour par d’autres moyens, nous vous recommandons d’utiliser l’élément `QueueTrigger` plutôt que l’élément `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="f4c11-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="f4c11-171"><a id="receipts"></a> Reçus d’objets blob</span><span class="sxs-lookup"><span data-stu-id="f4c11-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="f4c11-172">Hello WebJobs SDK vous assurer qu’aucune `BlobTrigger` fonction est appelée plusieurs fois pour hello même nouveaux ou mis à jour des objets blob.</span><span class="sxs-lookup"><span data-stu-id="f4c11-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="f4c11-173">Pour ce faire, il en conservant *accusés de réception d’objets blob* dans l’ordre toodetermine si une version de l’objet blob donné a été traitée.</span><span class="sxs-lookup"><span data-stu-id="f4c11-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="f4c11-174">Accusés de réception BLOB sont stockées dans un conteneur nommé *hôtes de tâches Web azure* dans le compte de stockage Azure hello spécifié par la chaîne de connexion AzureWebJobsStorage de hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="f4c11-175">Un accusé de réception d’objet blob a hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4c11-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="f4c11-176">fonction qui a été appelée pour l’objet blob de hello de Hello («*{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*», par exemple : « WebJob1.Functions.CopyBlob »)</span><span class="sxs-lookup"><span data-stu-id="f4c11-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="f4c11-177">nom du conteneur Hello</span><span class="sxs-lookup"><span data-stu-id="f4c11-177">hello container name</span></span>
* <span data-ttu-id="f4c11-178">type d’objet blob Hello (« BlockBlob » ou « Un PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="f4c11-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f4c11-179">nom d’objet blob Hello</span><span class="sxs-lookup"><span data-stu-id="f4c11-179">hello blob name</span></span>
* <span data-ttu-id="f4c11-180">Hello ETag (un identificateur de version des objets blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="f4c11-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="f4c11-181">Si vous souhaitez tooforce retraitement d’un objet blob, vous pouvez supprimer manuellement le reçu de blob hello pour cet objet blob à partir de hello *hôtes de tâches Web azure* conteneur.</span><span class="sxs-lookup"><span data-stu-id="f4c11-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="f4c11-182"><a id="queues"></a>Rubriques connexes couvertes par l’article de files d’attente hello</span><span class="sxs-lookup"><span data-stu-id="f4c11-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="f4c11-183">Pour plus d’informations sur la façon dont le traitement des objets blob toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas tooblob spécifique du traitement, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f4c11-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="f4c11-184">Rubriques connexes dans cet article hello suivants :</span><span class="sxs-lookup"><span data-stu-id="f4c11-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="f4c11-185">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="f4c11-185">Async functions</span></span>
* <span data-ttu-id="f4c11-186">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="f4c11-186">Multiple instances</span></span>
* <span data-ttu-id="f4c11-187">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="f4c11-187">Graceful shutdown</span></span>
* <span data-ttu-id="f4c11-188">Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello</span><span class="sxs-lookup"><span data-stu-id="f4c11-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="f4c11-189">Définir des chaînes de connexion du Kit de développement logiciel hello dans le code.</span><span class="sxs-lookup"><span data-stu-id="f4c11-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="f4c11-190">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="f4c11-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="f4c11-191">Configuration de l’élément `MaxDequeueCount` pour la gestion des objets blob incohérents.</span><span class="sxs-lookup"><span data-stu-id="f4c11-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="f4c11-192">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="f4c11-192">Trigger a function manually</span></span>
* <span data-ttu-id="f4c11-193">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="f4c11-193">Write logs</span></span>

## <span data-ttu-id="f4c11-194"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4c11-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="f4c11-195">Ce guide a fourni des exemples de code qui montrent comment les objets BLOB toohandle des scénarios courants d’utilisation de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4c11-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="f4c11-196">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f4c11-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

