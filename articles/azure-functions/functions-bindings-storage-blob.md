---
title: "Liaisons de Stockage Blob d’Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des déclencheurs et des liaisons Stockage Azure dans Azure Functions."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="1bded-104">Liaisons de stockage Blob Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1bded-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1bded-105">Cet article explique comment configurer et utiliser des liaisons Azure Stockage Blob dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1bded-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="1bded-106">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Azure Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="1bded-107">Pour les fonctionnalités qui sont disponibles dans toutes les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="1bded-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="1bded-108">Un [compte de stockage pour objet blob uniquement](../storage/common/storage-create-storage-account.md#blob-storage-accounts) n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1bded-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="1bded-109">Les déclencheurs et les liaisons de stockage blob nécessitent un compte de stockage à usage général.</span><span class="sxs-lookup"><span data-stu-id="1bded-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="1bded-110">Déclencheurs et liaisons de stockage blob</span><span class="sxs-lookup"><span data-stu-id="1bded-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="1bded-111">Avec le déclencheur Stockage Blob Azure, le code de votre fonction est appelé quand un objet blob nouveau ou mis à jour est détecté.</span><span class="sxs-lookup"><span data-stu-id="1bded-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="1bded-112">Le contenu de l’objet blob est fourni comme entrée de la fonction.</span><span class="sxs-lookup"><span data-stu-id="1bded-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="1bded-113">Définissez un déclencheur de stockage blob en utilisant l’onglet **Intégrer** dans le portail Functions.</span><span class="sxs-lookup"><span data-stu-id="1bded-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="1bded-114">Le portail crée la définition suivante dans la section **bindings** de *function.json* :</span><span class="sxs-lookup"><span data-stu-id="1bded-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="1bded-115">Les liaisons d’entrée et de sortie d’objet blob sont définies en utilisant `blob` comme type de liaison :</span><span class="sxs-lookup"><span data-stu-id="1bded-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="1bded-116">La propriété `path` prend en charge les expressions de liaison et les paramètres de filtre.</span><span class="sxs-lookup"><span data-stu-id="1bded-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="1bded-117">Consultez [Modèles de nom](#pattern).</span><span class="sxs-lookup"><span data-stu-id="1bded-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="1bded-118">La propriété `connection` doit contenir le nom d’un paramètre d’application comportant une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bded-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="1bded-119">Dans le portail Azure, l’éditeur standard de l’onglet **Intégrer** configure ce paramètre d’application pour vous quand vous sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bded-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1bded-120">Quand vous utilisez un déclencheur d’objet blob dans un plan Consommation, il peut y avoir jusqu’à 10 minutes de délai dans le traitement des nouveaux objets blob après qu’une application de fonction est devenue inactive.</span><span class="sxs-lookup"><span data-stu-id="1bded-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="1bded-121">Une fois l’application de fonction en cours d’exécution, les objets blob sont traités immédiatement.</span><span class="sxs-lookup"><span data-stu-id="1bded-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="1bded-122">Pour éviter ce délai initial, pensez à l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1bded-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="1bded-123">Utilisez un plan App Service avec le paramètre Toujours actif activé.</span><span class="sxs-lookup"><span data-stu-id="1bded-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="1bded-124">Utilisez un autre mécanisme pour déclencher le traitement de l’objet blob, comme un message de file d’attente qui contient le nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="1bded-125">Pour un exemple, consultez [Déclencheur de file d’attente avec liaison d’entrée d’objet blob](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="1bded-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="1bded-126">Modèles de nom</span><span class="sxs-lookup"><span data-stu-id="1bded-126">Name patterns</span></span>
<span data-ttu-id="1bded-127">Vous pouvez spécifier un modèle de nom d’objet blob dans la propriété `path`, qui peut être une expression de filtre ou de liaison.</span><span class="sxs-lookup"><span data-stu-id="1bded-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="1bded-128">Consultez [Expressions et modèles de liaison](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="1bded-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="1bded-129">Par exemple, pour filtrer des objets blob qui commencent par la chaîne « original », utilisez la définition suivante.</span><span class="sxs-lookup"><span data-stu-id="1bded-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="1bded-130">Ce chemin trouve un objet blob appelé *original-Blob1.txt* dans le conteneur *input*, et la valeur de la variable `name` dans le code de la fonction est `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="1bded-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="1bded-131">Pour se lier séparément au nom de fichier et à l’extension de l’objet blob, utilisez deux modèles.</span><span class="sxs-lookup"><span data-stu-id="1bded-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="1bded-132">Ce chemin trouve également un objet blob nommé *original-Blob1.txt*, et les variables `blobname` et `blobextension` du code de la fonction sont *original-Blob1* et *txt*.</span><span class="sxs-lookup"><span data-stu-id="1bded-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="1bded-133">Vous pouvez restreindre le type de fichier d’objets blob à l’aide d’une valeur fixe pour l’extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="1bded-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="1bded-134">Par exemple, pour déclencher uniquement sur des fichiers .png, utilisez le modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="1bded-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="1bded-135">Les accolades sont des caractères spéciaux dans les modèles de nom.</span><span class="sxs-lookup"><span data-stu-id="1bded-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="1bded-136">Pour spécifier des noms d’objet blob dont le nom contient des accolades, utilisez une séquence d’échappement sous la forme de deux accolades.</span><span class="sxs-lookup"><span data-stu-id="1bded-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="1bded-137">L’exemple suivante trouve un objet blob nommé *{20140101}-soundfile.mp3* dans le conteneur *images*, et la valeur de la variable `name` dans le code de la fonction est *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="1bded-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="1bded-138">Métadonnées d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="1bded-138">Trigger metadata</span></span>

<span data-ttu-id="1bded-139">Le déclencheur d’objet blob fournit plusieurs propriétés de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="1bded-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="1bded-140">Ces propriétés peuvent être utilisées dans des expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code.</span><span class="sxs-lookup"><span data-stu-id="1bded-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="1bded-141">Ces valeurs ont la même sémantique que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="1bded-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="1bded-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="1bded-142">**BlobTrigger**.</span></span> <span data-ttu-id="1bded-143">Saisissez `string`.</span><span class="sxs-lookup"><span data-stu-id="1bded-143">Type `string`.</span></span> <span data-ttu-id="1bded-144">Chemin de l’objet blob déclencheur</span><span class="sxs-lookup"><span data-stu-id="1bded-144">The triggering blob path</span></span>
- <span data-ttu-id="1bded-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="1bded-145">**Uri**.</span></span> <span data-ttu-id="1bded-146">Saisissez `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="1bded-146">Type `System.Uri`.</span></span> <span data-ttu-id="1bded-147">URI de l’objet blob pour l’emplacement principal.</span><span class="sxs-lookup"><span data-stu-id="1bded-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="1bded-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="1bded-148">**Properties**.</span></span> <span data-ttu-id="1bded-149">Saisissez `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="1bded-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="1bded-150">Propriétés système de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-150">The blob's system properties.</span></span>
- <span data-ttu-id="1bded-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="1bded-151">**Metadata**.</span></span> <span data-ttu-id="1bded-152">Saisissez `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="1bded-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="1bded-153">Métadonnées définies par l’utilisateur pour l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="1bded-154">Reçus d’objets blob</span><span class="sxs-lookup"><span data-stu-id="1bded-154">Blob receipts</span></span>
<span data-ttu-id="1bded-155">Le runtime Azure Functions vérifie qu’aucune fonction de déclencheur d’objet blob n’est appelée plusieurs fois pour un même objet blob, nouveau ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="1bded-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="1bded-156">Pour déterminer si la version d’un objet blob donné a été traitée, il gère des *reçus d’objet blob*.</span><span class="sxs-lookup"><span data-stu-id="1bded-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="1bded-157">Azure Functions stocke les reçus d’objet blob dans un conteneur appelé *azure-webjobs-hosts* dans le compte de stockage Azure de votre application de fonction (définie par le paramètre d’application `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="1bded-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="1bded-158">Un reçu d’objet blob contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1bded-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="1bded-159">Fonction déclenchée (« *&lt;nom de l’application de fonction>*.Functions.*&lt;nom de la fonction>* », par exemple : « MyFunctionApp.Functions.CopyBlob »)</span><span class="sxs-lookup"><span data-stu-id="1bded-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="1bded-160">Nom du conteneur</span><span class="sxs-lookup"><span data-stu-id="1bded-160">The container name</span></span>
* <span data-ttu-id="1bded-161">Type d’objet blob (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="1bded-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="1bded-162">Nom de l’objet blob</span><span class="sxs-lookup"><span data-stu-id="1bded-162">The blob name</span></span>
* <span data-ttu-id="1bded-163">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="1bded-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="1bded-164">Pour forcer le retraitement d’un objet blob, supprimez manuellement le reçu de l’objet blob du conteneur *azure-webjobs-hosts*.</span><span class="sxs-lookup"><span data-stu-id="1bded-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="1bded-165">Gestion des objets blob incohérents</span><span class="sxs-lookup"><span data-stu-id="1bded-165">Handling poison blobs</span></span>
<span data-ttu-id="1bded-166">En cas d’échec d’une fonction de déclencheur d’objet blob, Azure Functions réessaie cette fonction jusqu’à 5 fois par défaut.</span><span class="sxs-lookup"><span data-stu-id="1bded-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="1bded-167">Si les 5 tentatives échouent, Azure Functions ajoute un message à une file d’attente de stockage nommée *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="1bded-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="1bded-168">Le message en file d’attente associé aux objets blob incohérents correspond à un objet JSON, qui contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="1bded-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="1bded-169">FunctionId (au format *&lt;nom de l’application de fonction>*.Functions.*&lt;nom de la fonction>*)</span><span class="sxs-lookup"><span data-stu-id="1bded-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="1bded-170">BlobType (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="1bded-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="1bded-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="1bded-171">ContainerName</span></span>
* <span data-ttu-id="1bded-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="1bded-172">BlobName</span></span>
* <span data-ttu-id="1bded-173">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="1bded-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="1bded-174">Interrogation de blob pour les grands conteneurs</span><span class="sxs-lookup"><span data-stu-id="1bded-174">Blob polling for large containers</span></span>
<span data-ttu-id="1bded-175">Si le conteneur d’objets blob surveillé contient plus de 10 000 objets blob, le runtime Functions recherche les objets blob nouveaux ou modifiés dans les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="1bded-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="1bded-176">Ce processus ne se déroule pas en temps réel.</span><span class="sxs-lookup"><span data-stu-id="1bded-176">This process is not real time.</span></span> <span data-ttu-id="1bded-177">Il se peut qu’une fonction ne se déclenche que quelques minutes ou plus après la création de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="1bded-178">En outre, les [journaux de stockage sont créés selon le principe du meilleur effort](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="1bded-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="1bded-179">Il n’existe aucune garantie que tous les événements sont capturés.</span><span class="sxs-lookup"><span data-stu-id="1bded-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="1bded-180">Dans certaines conditions, des journaux peuvent être omis.</span><span class="sxs-lookup"><span data-stu-id="1bded-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="1bded-181">Si vous avez besoin de traitement d’objets blob plus rapide ou plus fiable, envisagez de créer un [message de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md) quand vous créez l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="1bded-182">Ensuite, utilisez un [déclencheur de file d’attente](functions-bindings-storage-queue.md) au lieu d’un déclencheur d’objet blob pour traiter l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="1bded-183">Utilisation d’un déclencheur d’objets blob et d’une liaison d’entrée</span><span class="sxs-lookup"><span data-stu-id="1bded-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="1bded-184">Dans les fonctions .NET, accédez aux données des objets blob en utilisant un paramètre de méthode comme `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="1bded-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="1bded-185">Ici, `paramName` est la valeur que vous avez spécifiée dans la [configuration du déclencheur](#trigger).</span><span class="sxs-lookup"><span data-stu-id="1bded-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="1bded-186">Dans les fonctions Node.js, accédez aux données de l’objet blob d’entrée en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="1bded-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1bded-187">Dans .NET, vous pouvez lier aux types de la liste ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1bded-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="1bded-188">S’ils sont utilisés comme liaison d’entrée, certains de ces types nécessitent une direction de liaison `inout` dans *function.json*.</span><span class="sxs-lookup"><span data-stu-id="1bded-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="1bded-189">Cette direction n’est pas prise en charge par l’éditeur standard : vous devez donc utiliser l’éditeur avancé.</span><span class="sxs-lookup"><span data-stu-id="1bded-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="1bded-190">`ICloudBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="1bded-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="1bded-191">`CloudBlockBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="1bded-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="1bded-192">`CloudPageBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="1bded-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="1bded-193">`CloudAppendBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="1bded-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="1bded-194">Si des objets blob de texte sont attendus, vous pouvez également lier à un type `string` .NET.</span><span class="sxs-lookup"><span data-stu-id="1bded-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="1bded-195">Ceci est recommandé uniquement si la taille de l’objet blob est petite, car tout le contenu de l’objet blob est chargé en mémoire.</span><span class="sxs-lookup"><span data-stu-id="1bded-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="1bded-196">En général, il est préférable d’utiliser un type `Stream` ou `CloudBlockBlob`.</span><span class="sxs-lookup"><span data-stu-id="1bded-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="1bded-197">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="1bded-197">Trigger sample</span></span>
<span data-ttu-id="1bded-198">Supposons le code function.json suivant, qui définit un déclencheur de stockage d’objet blob :</span><span class="sxs-lookup"><span data-stu-id="1bded-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="1bded-199">Consultez l’exemple dans le langage de votre choix pour voir comment enregistrer le contenu de chaque objet blob ajouté au conteneur surveillé.</span><span class="sxs-lookup"><span data-stu-id="1bded-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="1bded-200">C#</span><span class="sxs-lookup"><span data-stu-id="1bded-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="1bded-201">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1bded-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="1bded-202">Exemples de déclencheur d’objet blob en C#</span><span class="sxs-lookup"><span data-stu-id="1bded-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="1bded-203">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="1bded-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="1bded-204">Utilisation d’une liaison de sortie d’objet blob</span><span class="sxs-lookup"><span data-stu-id="1bded-204">Using a blob output binding</span></span>

<span data-ttu-id="1bded-205">Dans les fonctions .NET, vous devez utiliser un paramètre `out string` dans la signature de votre fonction ou un des types de la liste suivante.</span><span class="sxs-lookup"><span data-stu-id="1bded-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="1bded-206">Dans les fonctions Node.js, vous accédez à l’objet blob de sortie en utilisant `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="1bded-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1bded-207">Dans les fonctions .NET, vous pouvez définir une sortie vers les types suivants :</span><span class="sxs-lookup"><span data-stu-id="1bded-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="1bded-208">Exemple de déclencheur de file d’attente avec une entrée et une sortie d’objet blob</span><span class="sxs-lookup"><span data-stu-id="1bded-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="1bded-209">Supposons le code function.json suivant, qui définit un [déclencheur de stockage de file d’attente](functions-bindings-storage-queue.md), une entrée de stockage d’objet blob et une sortie de stockage d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1bded-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="1bded-210">Notez l’utilisation de la propriété de métadonnées `queueTrigger`.</span><span class="sxs-lookup"><span data-stu-id="1bded-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="1bded-211">dans les propriétés `path` de l’entrée et de la sortie d’objet blob :</span><span class="sxs-lookup"><span data-stu-id="1bded-211">in the blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="1bded-212">Consultez l’exemple dans le langage de votre choix pour voir comment copier l’objet blob d’entrée dans l’objet blob de sortie.</span><span class="sxs-lookup"><span data-stu-id="1bded-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="1bded-213">C#</span><span class="sxs-lookup"><span data-stu-id="1bded-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="1bded-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1bded-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="1bded-215">Exemple de liaison d’objet blob en C#</span><span class="sxs-lookup"><span data-stu-id="1bded-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="1bded-216">Exemple de liaison d’objet blob en Node.js</span><span class="sxs-lookup"><span data-stu-id="1bded-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="1bded-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bded-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

