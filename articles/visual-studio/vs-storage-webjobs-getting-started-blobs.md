---
title: "aaaGet a démarré avec le stockage d’objets blob et de Visual Studio (projets de la tâche Web) de services connectés | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage d’objets Blob dans un projet de la tâche Web après la connexion tooan stockage Azure à l’aide de Visual Studio de services connectés."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="cb774-103">Prise en main du stockage d’objets blob Azure et des services connectés Visual Studio (projets WebJob)</span><span class="sxs-lookup"><span data-stu-id="cb774-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="cb774-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cb774-104">Overview</span></span>
<span data-ttu-id="cb774-105">Cet article fournit c# des exemples de code qui montrent comment tootrigger un processus lorsqu’un objet blob Azure est créé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="cb774-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="cb774-106">exemples de code Hello utilisent hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="cb774-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="cb774-107">Lorsque vous ajoutez un projet de tâche Web tooa compte stockage à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue, package NuGet de stockage Azure approprié de hello est installé, les références .NET appropriées hello sont toohello ajouté projet et les chaînes de connexion pour le compte de stockage hello sont mis à jour dans le fichier App.config hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="cb774-108">Comment tootrigger une fonction lorsqu’un objet blob est créé ou mis à jour</span><span class="sxs-lookup"><span data-stu-id="cb774-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="cb774-109">Cette section montre comment toouse hello **BlobTrigger** attribut.</span><span class="sxs-lookup"><span data-stu-id="cb774-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="cb774-110">**Remarque :** hello toowatch de fichiers WebJobs SDK analyses de journal pour les objets BLOB nouveau ou modifié.</span><span class="sxs-lookup"><span data-stu-id="cb774-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="cb774-111">Ce processus est lent ; une fonction ne peut-être pas déclenchée jusqu'à ce que quelques minutes ou plus après que l’objet blob de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="cb774-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="cb774-112">Si votre application doit immédiatement les objets BLOB de tooprocess, hello recommandé consiste toocreate un message de la file d’attente lorsque vous créez les blob hello et que vous utilisez hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribut au lieu de hello **BlobTrigger** attribut sur la fonction hello qui traite l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="cb774-113">Espace réservé unique pour le nom d’objet blob avec extension</span><span class="sxs-lookup"><span data-stu-id="cb774-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="cb774-114">Hello exemple de code suivant copie les objets BLOB de texte qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur :</span><span class="sxs-lookup"><span data-stu-id="cb774-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="cb774-115">constructeur d’attribut Hello prend un paramètre de chaîne qui spécifie le nom du conteneur hello et un espace réservé pour le nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="cb774-116">Dans cet exemple, si un objet blob nommé *Blob1.txt* est créé dans hello *d’entrée* conteneur, la fonction hello crée un objet blob nommé *Blob1.txt* Bonjour *sortie*  conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb774-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="cb774-117">Vous pouvez spécifier un modèle de nom avec un espace réservé au nom hello blob, comme indiqué dans hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="cb774-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="cb774-118">Ce code copie uniquement les objets blob dont le nom commence par "original-".</span><span class="sxs-lookup"><span data-stu-id="cb774-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="cb774-119">Par exemple, *d’origine-Blob1.txt* Bonjour *d’entrée* conteneur est copié trop*copie-Blob1.txt* Bonjour *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb774-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="cb774-120">Si vous avez besoin de toospecify un modèle de nom pour les noms d’objet blob qui ont des accolades dans le nom de hello, deux accolades hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="cb774-121">Par exemple, si vous souhaitez que les objets BLOB toofind hello *images* conteneur qui ont des noms comme suit :</span><span class="sxs-lookup"><span data-stu-id="cb774-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="cb774-122">utilisez ce qui suit pour votre modèle :</span><span class="sxs-lookup"><span data-stu-id="cb774-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="cb774-123">Dans l’exemple de hello, hello *nom* valeur d’espace réservé serait *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="cb774-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="cb774-124">Séparation des espaces réservés d’extension et des noms d’objet blob</span><span class="sxs-lookup"><span data-stu-id="cb774-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="cb774-125">Hello modifications suivantes au code exemple hello extension de fichier pendant la copie des objets BLOB qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb774-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="cb774-126">code de Hello consigne extension hello Hello *d’entrée* d’objets blob et définit l’extension hello Hello *sortie* trop d’objets blob*.txt*.</span><span class="sxs-lookup"><span data-stu-id="cb774-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="cb774-127">Types que vous pouvez lier tooblobs</span><span class="sxs-lookup"><span data-stu-id="cb774-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="cb774-128">Vous pouvez utiliser hello **BlobTrigger** attribut sur hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="cb774-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="cb774-129">**string**</span><span class="sxs-lookup"><span data-stu-id="cb774-129">**string**</span></span>
* <span data-ttu-id="cb774-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="cb774-130">**TextReader**</span></span>
* <span data-ttu-id="cb774-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="cb774-131">**Stream**</span></span>
* <span data-ttu-id="cb774-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="cb774-132">**ICloudBlob**</span></span>
* <span data-ttu-id="cb774-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="cb774-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="cb774-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="cb774-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="cb774-135">Autres types de désérialisation par [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="cb774-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="cb774-136">Si vous souhaitez toowork directement avec hello compte de stockage Azure, vous pouvez également ajouter un **CloudStorageAccount** signature de méthode toohello de paramètre.</span><span class="sxs-lookup"><span data-stu-id="cb774-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="cb774-137">Mise en route du contenu d’objet blob de texte par liaison toostring</span><span class="sxs-lookup"><span data-stu-id="cb774-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="cb774-138">Si les objets BLOB de texte est attendus, **BlobTrigger** peuvent être appliqué tooa **chaîne** paramètre.</span><span class="sxs-lookup"><span data-stu-id="cb774-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="cb774-139">exemple de code suivant Hello lie un tooa d’objets blob de texte **chaîne** paramètre nommé **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="cb774-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="cb774-140">fonction Hello utilise ce contenu de hello paramètre toowrite de hello blob toohello du tableau de bord WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="cb774-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="cb774-141">Obtention de contenu d’objet blob sérialisé via ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="cb774-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="cb774-142">Hello exemple de code suivant utilise une classe qui implémente **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind un toohello de l’objet blob d’attribut **webimage pour** type.</span><span class="sxs-lookup"><span data-stu-id="cb774-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="cb774-143">Hello **webimage pour** code de liaison est fournie dans un **WebImageBinder** classe qui dérive de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="cb774-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="cb774-144">Comment les objets BLOB toohandle incohérents</span><span class="sxs-lookup"><span data-stu-id="cb774-144">How toohandle poison blobs</span></span>
<span data-ttu-id="cb774-145">Lorsqu’un **BlobTrigger** fonction échoue, hello SDK appelle à nouveau, en cas d’échec de hello a été provoquée par une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="cb774-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="cb774-146">Si l’erreur de hello est provoquée par le contenu de l’objet blob de hello hello, fonction hello échoue à chaque fois qu’il essaie d’objet blob de tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="cb774-147">Par défaut, hello SDK appelle une fonction des heures de too5 pour un objet blob donné.</span><span class="sxs-lookup"><span data-stu-id="cb774-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="cb774-148">Si vous essayez de cinquième hello échoue, hello Kit de développement logiciel ajoute une file d’attente de tooa message nommé *webjobs-blobtrigger-incohérents*.</span><span class="sxs-lookup"><span data-stu-id="cb774-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="cb774-149">Hello le nombre maximal de tentatives est configurable.</span><span class="sxs-lookup"><span data-stu-id="cb774-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="cb774-150">Hello même [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) paramètre est utilisé pour la gestion des objets blob incohérent et la gestion des messages de file d’attente de messages incohérents.</span><span class="sxs-lookup"><span data-stu-id="cb774-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="cb774-151">message de file d’attente Hello pour les objets BLOB incohérent est un objet JSON qui contient les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="cb774-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="cb774-152">ID de fonction (au format de hello *{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*, par exemple : WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="cb774-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="cb774-153">BlobType (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="cb774-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="cb774-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="cb774-154">ContainerName</span></span>
* <span data-ttu-id="cb774-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="cb774-155">BlobName</span></span>
* <span data-ttu-id="cb774-156">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="cb774-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="cb774-157">Dans hello code suivant exemple hello **CopyBlob** fonction comporte du code qui provoque son toofail chaque fois qu’elle est appelée.</span><span class="sxs-lookup"><span data-stu-id="cb774-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="cb774-158">Une fois hello SDK appelle pour le nombre maximal de hello de nouvelles tentatives, un message est créé sur la file d’attente de messages incohérents blob hello et ce message est traité par hello **LogPoisonBlob** (fonction).</span><span class="sxs-lookup"><span data-stu-id="cb774-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="cb774-159">Hello SDK désérialise automatiquement un message JSON hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="cb774-160">Voici hello **PoisonBlobMessage** classe :</span><span class="sxs-lookup"><span data-stu-id="cb774-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="cb774-161">Algorithme d’interrogation des objets blob</span><span class="sxs-lookup"><span data-stu-id="cb774-161">Blob polling algorithm</span></span>
<span data-ttu-id="cb774-162">Hello WebJobs SDK analyse tous les conteneurs spécifiés par **BlobTrigger** attributs au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="cb774-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="cb774-163">Dans un compte de stockage volumineux, cette analyse peut prendre du temps. Il se peut que les nouveaux objets blob ne soient pas tout de suite détectés et que les fonctions **BlobTrigger** ne soient pas exécutées avant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="cb774-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="cb774-164">toodetect BLOB nouvelles ou modifiées après le démarrage de l’application, hello que SDK lit périodiquement à partir du stockage d’objets blob hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="cb774-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="cb774-165">Hello blob journaux sont en mémoire tampon et sont écrites uniquement physiquement de toutes les 10 minutes ou, par conséquent, il peut y avoir un délai important après un objet blob est créé ou mis à jour avant hello correspondant **BlobTrigger** fonction s’exécute.</span><span class="sxs-lookup"><span data-stu-id="cb774-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="cb774-166">Il existe une exception pour les objets BLOB que vous créez à l’aide de hello **Blob** attribut.</span><span class="sxs-lookup"><span data-stu-id="cb774-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="cb774-167">Lorsque hello WebJobs SDK crée un nouvel objet blob, il passe immédiatement hello un nouvel objet blob correspondant à tooany **BlobTrigger** fonctions.</span><span class="sxs-lookup"><span data-stu-id="cb774-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="cb774-168">Par conséquent, si vous avez une chaîne d’objets blob entrées et sorties, hello SDK peut les traiter efficacement.</span><span class="sxs-lookup"><span data-stu-id="cb774-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="cb774-169">Mais si vous voulez bénéficier d’une faible latence lors de l’exécution des fonctions de traitement des objets blob créés ou mis à jour par d’autres moyens, nous vous recommandons d’utiliser l’élément **QueueTrigger** plutôt que l’élément **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="cb774-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="cb774-170">Reçus d’objets blob</span><span class="sxs-lookup"><span data-stu-id="cb774-170">Blob receipts</span></span>
<span data-ttu-id="cb774-171">Hello WebJobs SDK vous assurer qu’aucune **BlobTrigger** fonction est appelée plusieurs fois pour hello même nouveaux ou mis à jour des objets blob.</span><span class="sxs-lookup"><span data-stu-id="cb774-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="cb774-172">Pour ce faire, il en conservant *accusés de réception d’objets blob* dans l’ordre toodetermine si une version de l’objet blob donné a été traitée.</span><span class="sxs-lookup"><span data-stu-id="cb774-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="cb774-173">Accusés de réception BLOB sont stockées dans un conteneur nommé *hôtes de tâches Web azure* dans le compte de stockage Azure hello spécifié par la chaîne de connexion AzureWebJobsStorage de hello.</span><span class="sxs-lookup"><span data-stu-id="cb774-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="cb774-174">Un accusé de réception d’objet blob a hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb774-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="cb774-175">fonction qui a été appelée pour l’objet blob de hello de Hello («*{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*», par exemple : « WebJob1.Functions.CopyBlob »)</span><span class="sxs-lookup"><span data-stu-id="cb774-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="cb774-176">nom du conteneur Hello</span><span class="sxs-lookup"><span data-stu-id="cb774-176">hello container name</span></span>
* <span data-ttu-id="cb774-177">type d’objet blob Hello (« BlockBlob » ou « Un PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="cb774-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="cb774-178">nom d’objet blob Hello</span><span class="sxs-lookup"><span data-stu-id="cb774-178">hello blob name</span></span>
* <span data-ttu-id="cb774-179">Hello ETag (un identificateur de version des objets blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="cb774-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="cb774-180">Si vous souhaitez tooforce retraitement d’un objet blob, vous pouvez supprimer manuellement le reçu de blob hello pour cet objet blob à partir de hello *hôtes de tâches Web azure* conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb774-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="cb774-181">Rubriques connexes couvertes par l’article de files d’attente hello</span><span class="sxs-lookup"><span data-stu-id="cb774-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="cb774-182">Pour plus d’informations sur la façon dont le traitement des objets blob toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas tooblob spécifique du traitement, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="cb774-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="cb774-183">Rubriques connexes dans cet article hello suivants :</span><span class="sxs-lookup"><span data-stu-id="cb774-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="cb774-184">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="cb774-184">Async functions</span></span>
* <span data-ttu-id="cb774-185">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="cb774-185">Multiple instances</span></span>
* <span data-ttu-id="cb774-186">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="cb774-186">Graceful shutdown</span></span>
* <span data-ttu-id="cb774-187">Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello</span><span class="sxs-lookup"><span data-stu-id="cb774-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="cb774-188">Définir des chaînes de connexion du Kit de développement logiciel hello dans le code.</span><span class="sxs-lookup"><span data-stu-id="cb774-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="cb774-189">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="cb774-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="cb774-190">Configuration de **MaxDequeueCount** pour la gestion des objets blob incohérents.</span><span class="sxs-lookup"><span data-stu-id="cb774-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="cb774-191">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="cb774-191">Trigger a function manually</span></span>
* <span data-ttu-id="cb774-192">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="cb774-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb774-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb774-193">Next steps</span></span>
<span data-ttu-id="cb774-194">Cet article a fourni des exemples de code qui montrent comment les objets BLOB toohandle des scénarios courants d’utilisation de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb774-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="cb774-195">Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="cb774-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

