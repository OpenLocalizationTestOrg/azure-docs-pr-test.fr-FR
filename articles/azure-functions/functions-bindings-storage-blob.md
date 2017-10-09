---
title: "liaisons de stockage d’objets Blob fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment toouse le stockage Azure déclenche et les liaisons dans les fonctions d’Azure."
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
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="5b371-104">Liaisons de stockage Blob Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b371-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5b371-105">Cet article explique comment tooconfigure et fonctionnent avec les liaisons de stockage d’objets Blob Azure dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5b371-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="5b371-106">Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5b371-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="5b371-107">Pour les fonctionnalités qui sont disponibles dans toutes les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="5b371-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="5b371-108">Un [compte de stockage pour objet blob uniquement](../storage/common/storage-create-storage-account.md#blob-storage-accounts) n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5b371-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="5b371-109">Les déclencheurs et les liaisons de stockage blob nécessitent un compte de stockage à usage général.</span><span class="sxs-lookup"><span data-stu-id="5b371-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="5b371-110">Déclencheurs et liaisons de stockage blob</span><span class="sxs-lookup"><span data-stu-id="5b371-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="5b371-111">À l’aide de déclencheur de stockage d’objets Blob Azure hello, votre code de fonction est appelée lorsqu’un objet blob nouveau ou mis à jour est détecté.</span><span class="sxs-lookup"><span data-stu-id="5b371-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="5b371-112">contenu d’objet blob Hello est fournies en tant que fonction de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="5b371-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="5b371-113">Définir un déclencheur de stockage d’objets blob à l’aide de hello **intégrer** portail de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="5b371-114">portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="5b371-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="5b371-115">Objet BLOB d’entrée et les liaisons de sortie sont définies à l’aide de `blob` en tant que type de liaison hello :</span><span class="sxs-lookup"><span data-stu-id="5b371-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="5b371-116">Hello `path` propriété prend en charge la liaison d’expressions et des paramètres de filtre.</span><span class="sxs-lookup"><span data-stu-id="5b371-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="5b371-117">Consultez [Modèles de nom](#pattern).</span><span class="sxs-lookup"><span data-stu-id="5b371-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="5b371-118">Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="5b371-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="5b371-119">Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5b371-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="5b371-120">Lorsque vous utilisez un déclencheur d’objets blob sur un plan de la consommation, il peut être délai de 10 minutes tooa dans le traitement de nouveaux objets BLOB après qu’une application de la fonction est devenu inactive.</span><span class="sxs-lookup"><span data-stu-id="5b371-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="5b371-121">Après que application de fonction hello est en cours d’exécution, les objets BLOB est traitées immédiatement.</span><span class="sxs-lookup"><span data-stu-id="5b371-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="5b371-122">tooavoid initiale de ce délai, envisagez l’une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="5b371-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="5b371-123">Utilisez un plan App Service avec le paramètre Toujours actif activé.</span><span class="sxs-lookup"><span data-stu-id="5b371-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="5b371-124">Utiliser un autre mécanisme tootrigger hello objet blob de traitement, par exemple un message de la file d’attente qui contient le nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="5b371-125">Pour un exemple, consultez [Déclencheur de file d’attente avec liaison d’entrée d’objet blob](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="5b371-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="5b371-126">Modèles de nom</span><span class="sxs-lookup"><span data-stu-id="5b371-126">Name patterns</span></span>
<span data-ttu-id="5b371-127">Vous pouvez spécifier un modèle de nom d’objet blob dans hello `path` propriété, qui peut être une expression de filtre ou de la liaison.</span><span class="sxs-lookup"><span data-stu-id="5b371-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="5b371-128">Consultez [Expressions et modèles de liaison](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="5b371-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="5b371-129">Par exemple, tooblobs toofilter qui commencent par la chaîne hello d’origine », » utiliser hello définition.</span><span class="sxs-lookup"><span data-stu-id="5b371-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="5b371-130">Ce chemin de recherche d’un objet blob nommé *d’origine-Blob1.txt* Bonjour *d’entrée* conteneur et la valeur de hello de hello `name` la variable dans le code de fonction est `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="5b371-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="5b371-131">extension et nom de fichier blob toobind toohello séparément, utilisent deux modèles.</span><span class="sxs-lookup"><span data-stu-id="5b371-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="5b371-132">Ce chemin de recherche également un objet blob nommé *d’origine-Blob1.txt*et la valeur hello Hello `blobname` et `blobextension` sont des variables dans le code de fonction *d’origine-Blob1* et *txt*.</span><span class="sxs-lookup"><span data-stu-id="5b371-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="5b371-133">Vous pouvez limiter le type de fichier hello d’objets BLOB à l’aide d’une valeur fixe pour l’extension de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="5b371-134">Par exemple, tootrigger uniquement sur les fichiers .png, hello utilisez modèle :</span><span class="sxs-lookup"><span data-stu-id="5b371-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="5b371-135">Les accolades sont des caractères spéciaux dans les modèles de nom.</span><span class="sxs-lookup"><span data-stu-id="5b371-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="5b371-136">toospecify les noms d’objet blob qui ont des accolades dans le nom de hello, d’échappement des accolades hello à l’aide de deux accolades.</span><span class="sxs-lookup"><span data-stu-id="5b371-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="5b371-137">exemple Hello recherche un objet blob nommé *{20140101}-soundfile.mp3* Bonjour *images* conteneur et hello `name` est de valeur de la variable dans le code de la fonction hello  *soundfile.MP3*.</span><span class="sxs-lookup"><span data-stu-id="5b371-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="5b371-138">Métadonnées d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="5b371-138">Trigger metadata</span></span>

<span data-ttu-id="5b371-139">déclencheur de blob Hello fournit plusieurs propriétés de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="5b371-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="5b371-140">Ces propriétés peuvent être utilisées dans des expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code.</span><span class="sxs-lookup"><span data-stu-id="5b371-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="5b371-141">Ces valeurs ont hello même sémantique que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="5b371-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="5b371-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="5b371-142">**BlobTrigger**.</span></span> <span data-ttu-id="5b371-143">Saisissez `string`.</span><span class="sxs-lookup"><span data-stu-id="5b371-143">Type `string`.</span></span> <span data-ttu-id="5b371-144">chemin d’accès de blob déclenchement Hello</span><span class="sxs-lookup"><span data-stu-id="5b371-144">hello triggering blob path</span></span>
- <span data-ttu-id="5b371-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="5b371-145">**Uri**.</span></span> <span data-ttu-id="5b371-146">Saisissez `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="5b371-146">Type `System.Uri`.</span></span> <span data-ttu-id="5b371-147">URI de l’objet blob de Hello pour l’emplacement principal de hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="5b371-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="5b371-148">**Properties**.</span></span> <span data-ttu-id="5b371-149">Saisissez `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="5b371-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="5b371-150">Bonjour les propriétés de système de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="5b371-150">hello blob's system properties.</span></span>
- <span data-ttu-id="5b371-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="5b371-151">**Metadata**.</span></span> <span data-ttu-id="5b371-152">Saisissez `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="5b371-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="5b371-153">métadonnées définies par l’utilisateur Hello pour l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="5b371-154">Reçus d’objets blob</span><span class="sxs-lookup"><span data-stu-id="5b371-154">Blob receipts</span></span>
<span data-ttu-id="5b371-155">Fonctions d’Azure Hello runtime garantit qu’aucune fonction de déclenchement d’objet blob n’est appelée plusieurs fois pour hello même objet blob de nouveau ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="5b371-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="5b371-156">toodetermine si une version de l’objet blob donné a été traitée, il gère *accusés de réception d’objets blob*.</span><span class="sxs-lookup"><span data-stu-id="5b371-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="5b371-157">Magasins de fonctions Azure blob accusés de réception dans un conteneur nommé *hôtes de tâches Web azure* Bonjour compte de stockage Azure pour votre application (fonction) (défini par le paramètre d’application hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="5b371-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="5b371-158">Un accusé de réception d’objet blob a hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b371-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="5b371-159">Hello déclenchée (fonction) («*&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*», par exemple : « MyFunctionApp.Functions.CopyBlob »)</span><span class="sxs-lookup"><span data-stu-id="5b371-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="5b371-160">nom du conteneur Hello</span><span class="sxs-lookup"><span data-stu-id="5b371-160">hello container name</span></span>
* <span data-ttu-id="5b371-161">type d’objet blob Hello (« BlockBlob » ou « Un PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="5b371-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="5b371-162">nom d’objet blob Hello</span><span class="sxs-lookup"><span data-stu-id="5b371-162">hello blob name</span></span>
* <span data-ttu-id="5b371-163">Hello ETag (un identificateur de version des objets blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="5b371-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="5b371-164">tooforce retraitement d’un objet blob, supprimez réception de blob hello pour cet objet blob hello *hôtes de tâches Web azure* conteneur manuellement.</span><span class="sxs-lookup"><span data-stu-id="5b371-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="5b371-165">Gestion des objets blob incohérents</span><span class="sxs-lookup"><span data-stu-id="5b371-165">Handling poison blobs</span></span>
<span data-ttu-id="5b371-166">En cas d’échec d’une fonction de déclencheur d’objet blob, Azure Functions réessaie cette fonction jusqu’à 5 fois par défaut.</span><span class="sxs-lookup"><span data-stu-id="5b371-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="5b371-167">Si toutes les 5 tentatives échouent, les fonctions Azure ajoute un message tooa stockage file d’attente nommée *webjobs-blobtrigger-incohérents*.</span><span class="sxs-lookup"><span data-stu-id="5b371-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="5b371-168">message de file d’attente Hello pour les objets BLOB incohérent est un objet JSON qui contient les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="5b371-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="5b371-169">ID de fonction (au format de hello  *&lt;nom de l’application fonction >*. Fonctions.  *&lt;nom de la fonction >*)</span><span class="sxs-lookup"><span data-stu-id="5b371-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="5b371-170">BlobType (« BlockBlob » ou « PageBlob »)</span><span class="sxs-lookup"><span data-stu-id="5b371-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="5b371-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="5b371-171">ContainerName</span></span>
* <span data-ttu-id="5b371-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="5b371-172">BlobName</span></span>
* <span data-ttu-id="5b371-173">ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)</span><span class="sxs-lookup"><span data-stu-id="5b371-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="5b371-174">Interrogation de blob pour les grands conteneurs</span><span class="sxs-lookup"><span data-stu-id="5b371-174">Blob polling for large containers</span></span>
<span data-ttu-id="5b371-175">Si le conteneur d’objets blob hello en cours d’analyse contient plus de 10 000 objets BLOB, les fonctions hello runtime analyse journal toowatch de fichiers pour les objets BLOB nouveau ou modifié.</span><span class="sxs-lookup"><span data-stu-id="5b371-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="5b371-176">Ce processus ne se déroule pas en temps réel.</span><span class="sxs-lookup"><span data-stu-id="5b371-176">This process is not real time.</span></span> <span data-ttu-id="5b371-177">Une fonction ne peut-être pas déclenchée jusqu'à ce que quelques minutes ou plus après que l’objet blob de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="5b371-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="5b371-178">En outre, les [journaux de stockage sont créés selon le principe du meilleur effort](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="5b371-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="5b371-179">Il n’existe aucune garantie que tous les événements sont capturés.</span><span class="sxs-lookup"><span data-stu-id="5b371-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="5b371-180">Dans certaines conditions, des journaux peuvent être omis.</span><span class="sxs-lookup"><span data-stu-id="5b371-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="5b371-181">Si vous avez besoin de traitement de l’objet blob plus rapide ou plus fiable, envisagez de créer un [message de la file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md) lorsque vous créez l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="5b371-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="5b371-182">Ensuite, utilisez un [déclencheur de la file d’attente](functions-bindings-storage-queue.md) au lieu d’un objet blob déclencheur tooprocess hello objet blob.</span><span class="sxs-lookup"><span data-stu-id="5b371-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="5b371-183">Utilisation d’un déclencheur d’objets blob et d’une liaison d’entrée</span><span class="sxs-lookup"><span data-stu-id="5b371-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="5b371-184">Dans des fonctions .NET, accéder aux données d’objet blob de hello à l’aide d’un paramètre de méthode comme `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="5b371-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="5b371-185">Ici, `paramName` est la valeur hello spécifiée Bonjour [configuration du déclencheur](#trigger).</span><span class="sxs-lookup"><span data-stu-id="5b371-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="5b371-186">Dans les fonctions de Node.js, hello d’accès d’entrée à l’aide des données blob `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="5b371-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="5b371-187">Dans .NET, vous pouvez lier tooany des types de hello dans la liste hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5b371-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="5b371-188">S’ils sont utilisés comme liaison d’entrée, certains de ces types nécessitent une direction de liaison `inout` dans *function.json*.</span><span class="sxs-lookup"><span data-stu-id="5b371-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="5b371-189">Cette direction n’est pas pris en charge par l’éditeur standard hello, vous devez donc utiliser hello éditeur avancé.</span><span class="sxs-lookup"><span data-stu-id="5b371-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="5b371-190">`ICloudBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="5b371-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="5b371-191">`CloudBlockBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="5b371-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="5b371-192">`CloudPageBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="5b371-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="5b371-193">`CloudAppendBlob` (nécessite la direction de liaison « inout »)</span><span class="sxs-lookup"><span data-stu-id="5b371-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="5b371-194">Si vous prévoyez des objets BLOB de texte, vous pouvez également lier tooa .NET `string` type.</span><span class="sxs-lookup"><span data-stu-id="5b371-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="5b371-195">Ceci est recommandé uniquement si la taille des objets blob hello est petite, comme le contenu d’objet blob entier hello est chargés en mémoire.</span><span class="sxs-lookup"><span data-stu-id="5b371-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="5b371-196">En règle générale, il est préférable de toouse un `Stream` ou `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="5b371-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="5b371-197">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="5b371-197">Trigger sample</span></span>
<span data-ttu-id="5b371-198">Supposons que vous avez hello suivant function.json qui définit un déclencheur de stockage d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="5b371-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="5b371-199">Voir exemple hello spécifiques au langage qui enregistre le contenu de hello de chaque objet blob qui est ajouté conteneur analysé de toohello.</span><span class="sxs-lookup"><span data-stu-id="5b371-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="5b371-200">C#</span><span class="sxs-lookup"><span data-stu-id="5b371-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="5b371-201">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5b371-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="5b371-202">Exemples de déclencheur d’objet blob en C#</span><span class="sxs-lookup"><span data-stu-id="5b371-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="5b371-203">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="5b371-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="5b371-204">Utilisation d’une liaison de sortie d’objet blob</span><span class="sxs-lookup"><span data-stu-id="5b371-204">Using a blob output binding</span></span>

<span data-ttu-id="5b371-205">Dans les fonctions de .NET, vous devez utiliser un `out string` paramètre dans votre signature de fonction ou l’un des types hello Bonjour suivant liste.</span><span class="sxs-lookup"><span data-stu-id="5b371-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="5b371-206">Dans les fonctions de Node.js, vous accédez à l’aide des objets blob de sortie hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="5b371-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="5b371-207">Dans les fonctions de .NET, vous pouvez produire tooany Hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="5b371-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="5b371-208">Exemple de déclencheur de file d’attente avec une entrée et une sortie d’objet blob</span><span class="sxs-lookup"><span data-stu-id="5b371-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="5b371-209">Supposons que vous avez hello suivant function.json, qui définit un [déclencheur de stockage de la file d’attente](functions-bindings-storage-queue.md), un stockage d’objets blob d’entrée et un stockage d’objets blob de sortie.</span><span class="sxs-lookup"><span data-stu-id="5b371-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="5b371-210">Utilisation de hello avis de hello `queueTrigger` propriété de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="5b371-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="5b371-211">dans l’objet blob de hello d’entrée et sortie `path` propriétés :</span><span class="sxs-lookup"><span data-stu-id="5b371-211">in hello blob input and output `path` properties:</span></span>

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

<span data-ttu-id="5b371-212">Voir exemple hello spécifiques au langage qui copie hello blob d’entrée toohello sortie blob.</span><span class="sxs-lookup"><span data-stu-id="5b371-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="5b371-213">C#</span><span class="sxs-lookup"><span data-stu-id="5b371-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="5b371-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5b371-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="5b371-215">Exemple de liaison d’objet blob en C#</span><span class="sxs-lookup"><span data-stu-id="5b371-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="5b371-216">Exemple de liaison d’objet blob en Node.js</span><span class="sxs-lookup"><span data-stu-id="5b371-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="5b371-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b371-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

