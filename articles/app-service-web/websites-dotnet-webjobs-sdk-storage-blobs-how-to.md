---
title: "Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs"
description: "Découvrez comment utiliser le stockage d’objets blob Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs. Déclenchez un processus lorsqu’un nouvel objet blob apparaît dans un conteneur et gérez les « objets blob incohérents »."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="a4c3b-104">Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="a4c3b-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="a4c3b-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="a4c3b-105">Overview</span></span>
<span data-ttu-id="a4c3b-106">Ce guide fournit des exemples de code c# qui montrent comment déclencher un processus pendant la création ou la mise à jour d’un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="a4c3b-107">Les exemples de code utilisent le [Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk.md) version 1.x.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="a4c3b-108">Pour obtenir des exemples de code vous indiquant comment créer des objets blob, consultez la rubrique [Utilisation du stockage de file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a4c3b-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="a4c3b-109">Ce guide suppose que vous savez [comment créer un projet WebJob dans Visual Studio avec des chaînes de connexion qui pointent vers votre compte de stockage](websites-dotnet-webjobs-sdk-get-started.md) ou [plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="a4c3b-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="a4c3b-110"><a id="trigger"></a> Déclenchement d’une fonction lors de la création ou de la mise à jour d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="a4c3b-111">Cette section vous indique comment utiliser l’attribut `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="a4c3b-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4c3b-112">Le kit de développement logiciel (SDK) WebJobs analyse les fichiers journaux pour surveiller les objets blob qui ont été créés ou modifiés.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="a4c3b-113">Ce processus ne se déroule pas en temps réel ; il se peut qu’une fonction ne se déclenche que quelques minutes ou plus après la création de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="a4c3b-114">En outre, des [journaux de stockage sont créés sur la base du « meilleur effort »](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; il n’est pas garanti que tous les événements soient capturés.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="a4c3b-115">Dans certaines conditions, des journaux peuvent être omis.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="a4c3b-116">Si les limitations relatives à la vitesse et à la fiabilité des déclenchements d’objets blob ne sont pas acceptables pour votre application, il est conseillé d’utiliser la méthode de création d’un message de file d’attente lorsque vous créez l’objet blob et l’attribut [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) à la place de l’attribut `BlobTrigger` sur la fonction qui traite l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="a4c3b-117">Espace réservé unique pour le nom d’objet blob avec extension</span><span class="sxs-lookup"><span data-stu-id="a4c3b-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="a4c3b-118">L’exemple de code suivant copie les objets blob de texte qui apparaissent dans le conteneur *input* vers le conteneur *output* :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a4c3b-119">Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom du conteneur ainsi qu’un espace réservé pour le nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="a4c3b-120">Dans cet exemple, si un objet blob nommé *Blob1.txt* est créé dans le conteneur *input*, la fonction crée un objet blob appelé *Blob1.txt* dans le conteneur *output*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="a4c3b-121">Vous pouvez spécifier un modèle de nom avec l’espace réservé de nom d’objet blob, comme indiqué dans l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a4c3b-122">Ce code copie uniquement les objets blob dont le nom commence par "original-".</span><span class="sxs-lookup"><span data-stu-id="a4c3b-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="a4c3b-123">Par exemple, *original-Blob1.txt* dans le conteneur *input* est copié vers *copy-Blob1.txt* dans le conteneur *output*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="a4c3b-124">Si vous devez spécifier un modèle de nom pour les noms d’objet blob qui présentent des accolades, doublez ces dernières.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="a4c3b-125">Par exemple, si vous souhaitez rechercher des objets blob, dans le conteneur *images* , qui présentent des noms comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="a4c3b-126">utilisez ce qui suit pour votre modèle :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="a4c3b-127">Dans cet exemple, la valeur de l’espace réservé *name* correspond à *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="a4c3b-128">Séparation des espaces réservés d’extension et des noms d’objet blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="a4c3b-129">L’exemple de code suivant remplace l’extension de fichier pendant la copie des objets blob qui s’affichent dans le conteneur *input*, vers le conteneur *output*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="a4c3b-130">Le code enregistre l’extension de l’objet blob *input* et définit l’extension de l’objet blob *output* sur *.txt*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="a4c3b-131"><a id="types"></a> Types que vous pouvez lier aux objets blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="a4c3b-132">Vous pouvez utiliser l’attribut `BlobTrigger` sur les types de paramètre suivants :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="a4c3b-133">Autres types de désérialisation par [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="a4c3b-134">Si vous souhaitez utiliser directement le compte Microsoft Azure Storage, vous pouvez ajouter un paramètre `CloudStorageAccount` à la signature de méthode.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="a4c3b-135">Pour obtenir des exemples, consultez le [code de liaison d’objets blob dans le référentiel azure-webjobs-sdk sur GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="a4c3b-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="a4c3b-136"><a id="string"></a> Obtention du contenu de l’objet blob de texte via la liaison à une chaîne</span><span class="sxs-lookup"><span data-stu-id="a4c3b-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="a4c3b-137">Si vous attendez des objets de texte blob, vous pouvez appliquer l’élément `BlobTrigger` à un paramètre `string`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="a4c3b-138">L’exemple de code suivant lie un objet blob de texte à un paramètre `string` nommé `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="a4c3b-139">La fonction utilise ce paramètre pour écrire le contenu de l’objet blob dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="a4c3b-140"><a id="icbsb"></a> Obtention de contenu d’objet blob sérialisé via ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="a4c3b-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="a4c3b-141">L’exemple de code suivant utilise une classe qui implémente l’élément `ICloudBlobStreamBinder` pour activer l’attribut `BlobTrigger`, afin de lier un objet blob au type `WebImage`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="a4c3b-142">Le code de liaison du type `WebImage` est fourni dans une classe `WebImageBinder` dérivée de la classe `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="a4c3b-143">Obtenir le chemin d'accès aux objets blob pour l'objet blob de déclenchement</span><span class="sxs-lookup"><span data-stu-id="a4c3b-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="a4c3b-144">Pour obtenir le nom du conteneur et le nom blob de l'objet blob qui a déclenché la fonction, incluez un paramètre de chaîne `blobTrigger` dans la signature de la fonction.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="a4c3b-145"><a id="poison"></a> Gestion des objets blob incohérents</span><span class="sxs-lookup"><span data-stu-id="a4c3b-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="a4c3b-146">Lorsqu’une fonction `BlobTrigger` échoue, le Kit de développement logiciel (SDK) l’appelle à nouveau, au cas où l’échec aurait été provoqué par une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="a4c3b-147">Si le problème est occasionné par le contenu de l’objet blob, la fonction échoue chaque fois qu’elle tente de traiter cet objet.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="a4c3b-148">Par défaut, le Kit de développement logiciel (SDK) appelle une fonction jusqu’à 5 fois pour un objet blob donné.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="a4c3b-149">En cas d’échec après la cinquième tentative, le Kit de développement logiciel (SDK) ajoute un message à la file d’attente nommée *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="a4c3b-150">Vous pouvez configurer le nombre maximal de tentatives.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="a4c3b-151">Le paramètre [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) est utilisé à la fois pour la gestion des objets blob incohérents et pour l’administration des messages de la file d’attente de messages incohérents.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="a4c3b-152">Le message en file d’attente associé aux objets blob incohérents correspond à un objet JSON, qui contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="a4c3b-153">FunctionId (au format *{nom_tâche_web}*.Functions.*{nom_fonction}*, par exemple : WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="a4c3b-154">BlobType (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a4c3b-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="a4c3b-155">ContainerName</span></span>
* <span data-ttu-id="a4c3b-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="a4c3b-156">BlobName</span></span>
* <span data-ttu-id="a4c3b-157">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a4c3b-158">Dans l’exemple de code suivant, la fonction `CopyBlob` comporte du code qui provoque l’échec de cette fonction chaque fois qu’elle est appelée.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="a4c3b-159">Une fois que le Kit de développement logiciel (SDK) a atteint le nombre de tentatives d’appel défini, un message est créé dans la file d’attente des objets blob incohérents. Ce message est traité par la fonction `LogPoisonBlob`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="a4c3b-160">Le Kit de développement logiciel (SDK) désérialise automatiquement le message JSON.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="a4c3b-161">Voici la classe `PoisonBlobMessage` :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="a4c3b-162"><a id="polling"></a> Algorithme d’interrogation des objets blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="a4c3b-163">Le Kit de développement logiciel (SDK) WebJobs analyse tous les conteneurs spécifiés par les attributs `BlobTrigger` au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="a4c3b-164">Dans un compte de stockage volumineux, cette analyse peut prendre du temps. Il se peut que les nouveaux objets blob ne soient pas tout de suite détectés et que les fonctions `BlobTrigger` ne soient pas exécutées avant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="a4c3b-165">Pour détecter des objets blob nouveaux ou modifiés après le démarrage de l’application, le Kit de développement logiciel (SDK) lit régulièrement les journaux de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="a4c3b-166">Les journaux des objets blob sont mis en mémoire tampon ; ils ne sont écrits physiquement que toutes les 10 minutes environ. Il peut donc y avoir un délai important après la création ou la mise à jour d’un objet blob avant l’exécution de la fonction `BlobTrigger` correspondante.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="a4c3b-167">Il existe une exception pour les objets blob que vous créez à l’aide de l’attribut `Blob` .</span><span class="sxs-lookup"><span data-stu-id="a4c3b-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="a4c3b-168">Lorsque le Kit de développement logiciel (SDK) WebJobs crée un objet blob, il le transmet immédiatement à toutes les fonctions `BlobTrigger` correspondantes.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="a4c3b-169">Par conséquent, si vous avez une chaîne d’entrées et de sorties d’objets blob, le Kit de développement logiciel (SDK) peut les traiter efficacement.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="a4c3b-170">Mais si vous voulez bénéficier d’une faible latence lors de l’exécution des fonctions de traitement des objets blob créés ou mis à jour par d’autres moyens, nous vous recommandons d’utiliser l’élément `QueueTrigger` plutôt que l’élément `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="a4c3b-171"><a id="receipts"></a> Reçus d’objets blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="a4c3b-172">Le Kit de développement logiciel (SDK) Webjobs s’assure qu’aucune fonction `BlobTrigger` n’est appelée plusieurs fois pour un seul et même objet blob, nouveau ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="a4c3b-173">Pour ce faire, il tient à jour les *reçus d’objets blob* afin de déterminer si la version d’un objet blob donné a été traitée.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="a4c3b-174">Les reçus d’objets blob sont stockés dans un conteneur appelé *azure-webjobs-hosts* associé au compte de stockage Microsoft Azure indiqué par la chaîne de connexion AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="a4c3b-175">Un reçu d’objet blob contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="a4c3b-176">Fonction appelée pour l’objet blob ("*{nom_tâche_web}*.Functions.*{nom_fonction}*", par exemple : « WebJob1.Functions.CopyBlob »)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="a4c3b-177">Nom du conteneur</span><span class="sxs-lookup"><span data-stu-id="a4c3b-177">The container name</span></span>
* <span data-ttu-id="a4c3b-178">Type d’objet blob (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a4c3b-179">Nom de l’objet blob</span><span class="sxs-lookup"><span data-stu-id="a4c3b-179">The blob name</span></span>
* <span data-ttu-id="a4c3b-180">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="a4c3b-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a4c3b-181">Si vous souhaitez forcer le retraitement d’un objet blob, vous pouvez supprimer manuellement le reçu de l’objet blob à partir du conteneur *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="a4c3b-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="a4c3b-182"><a id="queues"></a>Sujets connexes traités dans l’article relatif aux files d’attente</span><span class="sxs-lookup"><span data-stu-id="a4c3b-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="a4c3b-183">Pour en savoir plus sur la gestion du traitement d’objets blob déclenché par un message en file d’attente, ou pour consulter des scénarios relatifs au Kit de développement logiciel (SDK) WebJobs non spécifiques du traitement d’objets blob, consultez la rubrique [Utilisation du stockage de la file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a4c3b-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="a4c3b-184">Les sujets associés abordés dans cet article sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="a4c3b-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="a4c3b-185">Fonctions asynchrones</span><span class="sxs-lookup"><span data-stu-id="a4c3b-185">Async functions</span></span>
* <span data-ttu-id="a4c3b-186">Instances multiples</span><span class="sxs-lookup"><span data-stu-id="a4c3b-186">Multiple instances</span></span>
* <span data-ttu-id="a4c3b-187">Arrêt approprié</span><span class="sxs-lookup"><span data-stu-id="a4c3b-187">Graceful shutdown</span></span>
* <span data-ttu-id="a4c3b-188">Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction</span><span class="sxs-lookup"><span data-stu-id="a4c3b-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="a4c3b-189">Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="a4c3b-190">Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code</span><span class="sxs-lookup"><span data-stu-id="a4c3b-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="a4c3b-191">Configuration de l’élément `MaxDequeueCount` pour la gestion des objets blob incohérents.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="a4c3b-192">Déclenchement manuel d’une fonction</span><span class="sxs-lookup"><span data-stu-id="a4c3b-192">Trigger a function manually</span></span>
* <span data-ttu-id="a4c3b-193">Écriture de journaux</span><span class="sxs-lookup"><span data-stu-id="a4c3b-193">Write logs</span></span>

## <span data-ttu-id="a4c3b-194"><a id="nextsteps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4c3b-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="a4c3b-195">Ce guide fournit des exemples de code qui indiquent comment gérer des scénarios courants pour l’utilisation des objets blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c3b-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="a4c3b-196">Pour plus d’informations sur l’utilisation d’Azure Webjobs et du Kit de développement logiciel (SDK) WebJobs Azure, consultez la rubrique [Azure Webjobs - Ressources recommandées](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a4c3b-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

