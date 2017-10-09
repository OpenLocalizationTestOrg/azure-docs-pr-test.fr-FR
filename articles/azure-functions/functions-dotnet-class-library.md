---
title: "aaaUsing .NET classe bibliothèques avec des fonctions de Azure | Documents Microsoft"
description: "Découvrez comment utilisent les bibliothèques de classes .NET tooauthor pour avec des fonctions d’Azure"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="4d04c-104">Utilisation de bibliothèques de classes .NET avec Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4d04c-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="4d04c-105">En outre tooscript fichiers, les fonctions Azure prend en charge la publication d’une bibliothèque de classes en tant qu’implémentation hello pour une ou plusieurs fonctions.</span><span class="sxs-lookup"><span data-stu-id="4d04c-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="4d04c-106">Nous vous recommandons d’utiliser hello [Azure fonctions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="4d04c-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d04c-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4d04c-107">Prerequisites</span></span> 

<span data-ttu-id="4d04c-108">Cet article a hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="4d04c-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="4d04c-109">[Visual Studio 2017 15.3 (préversion)](https://www.visualstudio.com/vs/preview/)</span><span class="sxs-lookup"><span data-stu-id="4d04c-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="4d04c-110">Installer les charges de travail hello **ASP.NET et le développement web** et **le développement Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d04c-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="4d04c-111">Outils d’Azure Functions pour Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4d04c-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="4d04c-112">Projet de bibliothèque de classes Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4d04c-112">Functions class library project</span></span>

<span data-ttu-id="4d04c-113">À partir de Visual Studio, créez un projet Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4d04c-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="4d04c-114">nouveau modèle de projet Hello crée des fichiers de hello *host.json* et *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="4d04c-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="4d04c-115">Vous pouvez [personnaliser les paramètres d’exécution d’Azure Functions dans host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="4d04c-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="4d04c-116">fichier de Hello *local.settings.json* stocke les paramètres de l’application, les chaînes de connexion et les paramètres pour les outils de base de fonctions Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04c-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="4d04c-117">toolearn en savoir plus sur sa structure, consultez [Code et tester des fonctions Azure localement](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="4d04c-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="4d04c-118">Attribut FunctionName</span><span class="sxs-lookup"><span data-stu-id="4d04c-118">FunctionName attribute</span></span>

<span data-ttu-id="4d04c-119">attribut de Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marque une méthode comme un point d’entrée de fonction.</span><span class="sxs-lookup"><span data-stu-id="4d04c-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="4d04c-120">Il doit être utilisé avec un seul déclencheur et 0 ou plusieurs liaisons d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4d04c-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="4d04c-121">Conversion toofunction.json</span><span class="sxs-lookup"><span data-stu-id="4d04c-121">Conversion toofunction.json</span></span>

<span data-ttu-id="4d04c-122">Lors de la génération d’un projet de fonctions d’Azure, il génère un fichier `function.json` dans le répertoire de hello correspondant au nom de fonction hello défini par `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="4d04c-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="4d04c-123">Il spécifie le fichier d’assembly de projet toohello points et les liaisons et les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="4d04c-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="4d04c-124">Cette conversion est effectuée par le package NuGet de hello [Microsoft\.NET\.Sdk\.fonctions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="4d04c-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="4d04c-125">source de Hello n’est disponible dans le référentiel GitHub de hello [azure\-fonctions\-vs\-générer\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="4d04c-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="4d04c-126">Déclencheurs et liaisons</span><span class="sxs-lookup"><span data-stu-id="4d04c-126">Triggers and bindings</span></span>

<span data-ttu-id="4d04c-127">Hello tableau suivant répertorie les déclencheurs hello et des liaisons qui sont disponibles dans un projet de bibliothèque de classes de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04c-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="4d04c-128">Tous les attributs sont dans l’espace de noms hello `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="4d04c-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="4d04c-129">Liaison</span><span class="sxs-lookup"><span data-stu-id="4d04c-129">Binding</span></span> | <span data-ttu-id="4d04c-130">Attribut</span><span class="sxs-lookup"><span data-stu-id="4d04c-130">Attribute</span></span> | <span data-ttu-id="4d04c-131">Package NuGet</span><span class="sxs-lookup"><span data-stu-id="4d04c-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="4d04c-132">Déclencheur, entrée, sortie de Stockage Blob</span><span class="sxs-lookup"><span data-stu-id="4d04c-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="4d04c-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="4d04c-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="4d04c-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="4d04c-135">[Stockage d’objets blob]</span><span class="sxs-lookup"><span data-stu-id="4d04c-135">[Blob storage]</span></span> |
| [<span data-ttu-id="4d04c-136">Liaison d’entrée et de sortie de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4d04c-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="4d04c-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="4d04c-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="4d04c-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="4d04c-139">Déclencheur et sortie d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4d04c-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="4d04c-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="4d04c-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="4d04c-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="4d04c-142">Entrée et sortie de fichier externe</span><span class="sxs-lookup"><span data-stu-id="4d04c-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="4d04c-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="4d04c-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="4d04c-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="4d04c-145">Déclencheur HTTP et webhook</span><span class="sxs-lookup"><span data-stu-id="4d04c-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="4d04c-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="4d04c-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="4d04c-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="4d04c-148">Entrée et sortie de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="4d04c-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="4d04c-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="4d04c-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="4d04c-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="4d04c-151">Sortie de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4d04c-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="4d04c-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="4d04c-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="4d04c-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="4d04c-154">Déclencheur et sortie de Stockage File d’attente</span><span class="sxs-lookup"><span data-stu-id="4d04c-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="4d04c-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="4d04c-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="4d04c-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="4d04c-157">Sortie de SendGrid</span><span class="sxs-lookup"><span data-stu-id="4d04c-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="4d04c-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-158">[SendGridAttribute]</span></span> | <span data-ttu-id="4d04c-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="4d04c-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="4d04c-160">Déclencheur et sortie de Service Bus</span><span class="sxs-lookup"><span data-stu-id="4d04c-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="4d04c-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="4d04c-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="4d04c-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="4d04c-163">Entrée et sortie de Stockage Table</span><span class="sxs-lookup"><span data-stu-id="4d04c-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="4d04c-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="4d04c-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="4d04c-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="4d04c-166">Déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="4d04c-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="4d04c-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="4d04c-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="4d04c-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="4d04c-169">Sortie de Twilio</span><span class="sxs-lookup"><span data-stu-id="4d04c-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="4d04c-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="4d04c-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="4d04c-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="4d04c-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="4d04c-172">Liaisons de déclencheur, d’entrée, de sortie de Stockage Blob</span><span class="sxs-lookup"><span data-stu-id="4d04c-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="4d04c-173">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04c-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="4d04c-174">Pour plus d’informations sur les expressions et métadonnées de liaison, voir [Liaisons de Stockage Blob Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="4d04c-175">Un déclencheur d’objet blob est défini avec hello `[BlobTrigger]` attribut.</span><span class="sxs-lookup"><span data-stu-id="4d04c-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="4d04c-176">Vous pouvez utiliser les attributs hello `[StorageAccount]` compte de stockage hello toodefine qui est utilisé par une fonction entière ou une classe.</span><span class="sxs-lookup"><span data-stu-id="4d04c-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="4d04c-177">Objet BLOB d’entrée et sortie sont définies à l’aide de hello `[Blob]` d’attribut, ainsi que par un `FileAccess` paramètre indiquant de lecture ou d’écriture.</span><span class="sxs-lookup"><span data-stu-id="4d04c-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="4d04c-178">Hello suivant montre comment utiliser un déclencheur de l’objet blob et de liaison de sortie d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4d04c-178">hello following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="4d04c-179">Liaisons d’entrée et de sortie Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4d04c-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="4d04c-180">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4d04c-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="4d04c-181">toolearn savoir plus sur les fonctions hello de liaison de base de données Cosmos hello, consultez [les liaisons de base de données Azure fonctions Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="4d04c-182">toobind tooa Cosmos DB document, utilisez les attributs hello `[DocumentDB]` dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="4d04c-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="4d04c-183">Bonjour à l’exemple suivant présente un déclencheur de la file d’attente et une API DocumentDB liaison de sortie :</span><span class="sxs-lookup"><span data-stu-id="4d04c-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="4d04c-184">Déclencheur et sortie d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4d04c-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="4d04c-185">Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4d04c-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="4d04c-186">Pour plus d’informations, voir [Liaisons d’Event Hub Azure Functions](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="4d04c-187">types de Hello `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` et `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="4d04c-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="4d04c-188">Hello exemple suivant utilise un déclencheur de concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="4d04c-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="4d04c-189">Hello exemple suivant présente un concentrateur d’événements de sortie, à l’aide de la valeur de retour de méthode hello en tant que sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="4d04c-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="4d04c-190">Entrée et sortie de fichier externe</span><span class="sxs-lookup"><span data-stu-id="4d04c-190">External file input and output</span></span>

<span data-ttu-id="4d04c-191">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour des fichiers externes, tels que Google Drive, Dropbox et OneDrive.</span><span class="sxs-lookup"><span data-stu-id="4d04c-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="4d04c-192">toolearn, voir [liaisons du fichier externe de fonctions Azure](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="4d04c-193">attributs de Hello `[ExternalFileTrigger]` et `[ExternalFile]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="4d04c-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="4d04c-194">Hello exemple c# suivant illustre l’entrée et la sortie de liaison d’un fichier externe.</span><span class="sxs-lookup"><span data-stu-id="4d04c-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="4d04c-195">copies de code Hello hello le fichier de sortie de fichier d’entrée toohello.</span><span class="sxs-lookup"><span data-stu-id="4d04c-195">hello code copies hello input file toohello output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="4d04c-196">HTTP et webhooks</span><span class="sxs-lookup"><span data-stu-id="4d04c-196">HTTP and webhooks</span></span>

<span data-ttu-id="4d04c-197">Hello d’utilisation `HttpTrigger` déclencheur de toodefine HTTP attribut ou webhook.</span><span class="sxs-lookup"><span data-stu-id="4d04c-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="4d04c-198">Cet attribut est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="4d04c-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="4d04c-199">Vous pouvez personnaliser le niveau d’autorisation de hello, type de webhook, itinéraire et méthodes.</span><span class="sxs-lookup"><span data-stu-id="4d04c-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="4d04c-200">Hello exemple suivant définit un déclencheur HTTP avec l’authentification anonyme et _genericJson_ webhook type.</span><span class="sxs-lookup"><span data-stu-id="4d04c-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="4d04c-201">Entrée et sortie de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="4d04c-201">Mobile Apps input and output</span></span>

<span data-ttu-id="4d04c-202">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="4d04c-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="4d04c-203">toolearn, voir [liaisons des applications mobiles de fonctions Azure](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="4d04c-204">attribut de Hello `[MobileTable]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="4d04c-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="4d04c-205">exemple Hello illustre une applications mobiles liaison de sortie :</span><span class="sxs-lookup"><span data-stu-id="4d04c-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="4d04c-206">Sortie de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4d04c-206">Notification Hubs output</span></span>

<span data-ttu-id="4d04c-207">Azure Functions prend en charge une liaison de sortie pour Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4d04c-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="4d04c-208">toolearn, voir [liaison de sortie du Hub de Notification de fonctions Azure](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="4d04c-209">attribut de Hello `[NotificationHub]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="4d04c-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="4d04c-210">Déclencheur et sortie de Stockage File d’attente</span><span class="sxs-lookup"><span data-stu-id="4d04c-210">Queue storage trigger and output</span></span>

<span data-ttu-id="4d04c-211">Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04c-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="4d04c-212">Pour plus d’informations, voir [Liaisons de Stockage File d’attente Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="4d04c-213">Hello suivant montre la fonction de hello toouse type de retour avec une sortie de la file d’attente de liaison, à l’aide de hello `[Queue]` attribut.</span><span class="sxs-lookup"><span data-stu-id="4d04c-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="4d04c-214">toodefine un déclencheur de la file d’attente, utilisez hello `[QueueTrigger]` attribut.</span><span class="sxs-lookup"><span data-stu-id="4d04c-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="4d04c-215">Sortie de SendGrid</span><span class="sxs-lookup"><span data-stu-id="4d04c-215">SendGrid output</span></span>

<span data-ttu-id="4d04c-216">Azure Functions prend en charge une liaison de sortie SendGrid pour l’envoi de courrier par programmation.</span><span class="sxs-lookup"><span data-stu-id="4d04c-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="4d04c-217">toolearn, voir [SendGrid de fonctions Azure liaisons](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="4d04c-218">attribut de Hello `[SendGrid]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="4d04c-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="4d04c-219">Hello Voici un exemple d’utilisation d’un déclencheur de la file d’attente Service Bus et un à l’aide de la liaison pour la sortie SendGrid `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="4d04c-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="4d04c-220">Déclencheur et sortie de Service Bus</span><span class="sxs-lookup"><span data-stu-id="4d04c-220">Service Bus trigger and output</span></span>

<span data-ttu-id="4d04c-221">Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente et les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4d04c-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="4d04c-222">Pour plus d’informations sur la configuration des liaisons, voir [Liaisons Service Bus Azure Functions](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="4d04c-223">attributs de Hello `[ServiceBusTrigger]` et `[ServiceBus]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="4d04c-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="4d04c-224">Hello Voici un exemple d’un déclencheur de la file d’attente Service Bus :</span><span class="sxs-lookup"><span data-stu-id="4d04c-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="4d04c-225">Hello Voici un exemple d’une sortie de Bus de Service de liaison, à l’aide du type de retour de méthode hello en tant que sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="4d04c-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="4d04c-226">Entrée et sortie de Stockage Table</span><span class="sxs-lookup"><span data-stu-id="4d04c-226">Table storage input and output</span></span>

<span data-ttu-id="4d04c-227">Azure Functions prend en charge les liaisons d’entrée et de sortie pour Stockage de table Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04c-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="4d04c-228">toolearn, voir [liaisons de stockage de Table de fonctions Azure](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="4d04c-229">Hello exemple suivant est une classe avec deux fonctions, qui montre la sortie de stockage de table et des liaisons d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4d04c-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="4d04c-230">Déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="4d04c-230">Timer trigger</span></span>

<span data-ttu-id="4d04c-231">Azure Functions offre une liaison de déclencheur de minuteur qui vous permet d’exécuter votre code de fonction selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="4d04c-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="4d04c-232">toolearn savoir plus sur les fonctions hello de liaison de hello, consultez [planifier l’exécution de code avec les fonctions Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="4d04c-233">Sur le plan de la consommation de hello, vous pouvez définir des planifications avec un [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="4d04c-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="4d04c-234">Si vous utilisez un plan App Service, vous pouvez également utiliser une chaîne TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="4d04c-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="4d04c-235">Bonjour à l’exemple suivant définit un déclencheur du minuteur qui s’exécute toutes les 5 minutes :</span><span class="sxs-lookup"><span data-stu-id="4d04c-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="4d04c-236">Sortie de Twilio</span><span class="sxs-lookup"><span data-stu-id="4d04c-236">Twilio output</span></span>

<span data-ttu-id="4d04c-237">Prend en charge des fonctions Azure Twilio sortie liaisons tooenable vos fonctions toosend les messages SMS.</span><span class="sxs-lookup"><span data-stu-id="4d04c-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="4d04c-238">toolearn, voir [liaison de sortie d’envoi de SMS à partir des fonctions d’Azure à l’aide de hello Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="4d04c-239">attribut de Hello `[TwilioSms]` est défini dans le package de hello [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="4d04c-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="4d04c-240">Hello exemple c# suivant utilise une file d’attente déclencheur et un Twilio de liaison de sortie :</span><span class="sxs-lookup"><span data-stu-id="4d04c-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="4d04c-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d04c-241">Next steps</span></span>

<span data-ttu-id="4d04c-242">Pour plus d’informations sur l’utilisation d’Azure Functions dans un script C#, voir la référence du développeur de script [Azure Functions C\#](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="4d04c-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
