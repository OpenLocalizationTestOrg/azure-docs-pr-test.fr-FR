---
title: aaaDevelop fonctions Azure Media Services
description: "Cette rubrique montre comment toostart développement avec Media Services à l’aide des fonctions Azure hello portail Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="a10bf-103">Développement de fonctions Azure Functions avec Media Services</span><span class="sxs-lookup"><span data-stu-id="a10bf-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="a10bf-104">Cette rubrique vous montre comment tooget démarrer avec la création de fonctions Azure qui utilisent les Services de support.</span><span class="sxs-lookup"><span data-stu-id="a10bf-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="a10bf-105">Hello fonction Azure définis dans cette rubrique surveille un conteneur du compte de stockage nommé **d’entrée** de nouveaux fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="a10bf-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="a10bf-106">Une fois qu’un fichier est déposé dans le conteneur de stockage hello, déclencheur d’objets blob hello exécutera la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="a10bf-107">Si vous souhaitez tooexplore et déployez des fonctions Azure existantes qui utilisent Azure Media Services, consultez [fonctions d’Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="a10bf-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="a10bf-108">Ce référentiel contient des exemples qui utilisent les Services de support tooshow flux de travail connexe tooingesting contenu directement depuis le stockage blob, de l’encodage et écrire le contenu de sauvegarde tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="a10bf-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="a10bf-109">Il contient également des exemples de comment toomonitor travail notifications via des WebHooks et des files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="a10bf-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="a10bf-110">Vous pouvez également développer vos fonctions basées sur des exemples hello Bonjour [fonctions d’Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) référentiel.</span><span class="sxs-lookup"><span data-stu-id="a10bf-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="a10bf-111">les fonctions hello toodeploy, appuyez sur hello **déployer tooAzure** bouton.</span><span class="sxs-lookup"><span data-stu-id="a10bf-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a10bf-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a10bf-112">Prerequisites</span></span>

- <span data-ttu-id="a10bf-113">Avant de pouvoir créer votre première fonction, vous devez toohave un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a10bf-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="a10bf-114">Si tel n’est pas le cas, des [comptes gratuits sont disponibles](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a10bf-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="a10bf-115">Si vous vous apprêtez à des fonctions de Azure toocreate qui effectuent des actions sur votre compte Azure Media Services (AMS) ou écouter tooevents envoyé par Media Services, vous devez créer un compte AMS, comme décrit [ici](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a10bf-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="a10bf-116">Présentation de [comment toouse Azure fonctions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a10bf-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="a10bf-117">Consultez également :</span><span class="sxs-lookup"><span data-stu-id="a10bf-117">Also, review:</span></span>
    - [<span data-ttu-id="a10bf-118">Liaisons HTTP et webhook Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a10bf-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="a10bf-119">Comment tooconfigure paramètres de l’application Azure (fonction)</span><span class="sxs-lookup"><span data-stu-id="a10bf-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="a10bf-120">Considérations</span><span class="sxs-lookup"><span data-stu-id="a10bf-120">Considerations</span></span>

-  <span data-ttu-id="a10bf-121">Fonctions Azure s’exécutant sous le plan de la consommation hello ont délai d’attente de 5 minutes à limiter.</span><span class="sxs-lookup"><span data-stu-id="a10bf-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="a10bf-122">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="a10bf-122">Create a function app</span></span>

1. <span data-ttu-id="a10bf-123">Accédez toohello [portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a10bf-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="a10bf-124">Suivez [cette procédure](../azure-functions/functions-create-function-app-portal.md) pour créer une Function App.</span><span class="sxs-lookup"><span data-stu-id="a10bf-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="a10bf-125">Un compte de stockage que vous spécifiez dans hello **StorageConnection** variable d’environnement (voir l’étape suivante de hello) doit être Bonjour même région que votre application.</span><span class="sxs-lookup"><span data-stu-id="a10bf-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="a10bf-126">Configuration des paramètres Function App</span><span class="sxs-lookup"><span data-stu-id="a10bf-126">Configure function app settings</span></span>

<span data-ttu-id="a10bf-127">Lorsque vous développez des fonctions de Media Services, il est pratique tooadd des variables d’environnement qui seront utilisés dans l’ensemble de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="a10bf-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="a10bf-128">paramètres de l’application tooconfigure, cliquez sur lien de configurer les paramètres de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="a10bf-129">Pour plus d’informations, consultez [comment tooconfigure paramètres de l’application Azure fonction](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a10bf-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="a10bf-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a10bf-130">For example:</span></span>

![Paramètres](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="a10bf-132">fonction Hello, définie dans cet article, suppose que vous avez hello suivant des variables d’environnement dans vos paramètres d’application :</span><span class="sxs-lookup"><span data-stu-id="a10bf-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="a10bf-133">**AMSAccount** : *nom de compte AMS* (ex. testams)</span><span class="sxs-lookup"><span data-stu-id="a10bf-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="a10bf-134">**AMSKey** : *clé de compte AMS* (ex. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="a10bf-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="a10bf-135">**MediaServicesStorageAccountName** : *nom de compte de stockage* (ex. testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="a10bf-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="a10bf-136">**MediaServicesStorageAccountKey** : *clé de compte de stockage* (ex. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="a10bf-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="a10bf-137">**StorageConnection** : *connexion de stockage* (ex. DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="a10bf-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="a10bf-138">Créer une fonction</span><span class="sxs-lookup"><span data-stu-id="a10bf-138">Create a function</span></span>

<span data-ttu-id="a10bf-139">Une fois votre Function App déployée, vous pouvez la retrouver parmi les fonctions Azure Functions **App Services**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="a10bf-140">Sélectionnez votre Function App et cliquez sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="a10bf-141">Choisissez hello **c#** language et **le traitement des données** scénario.</span><span class="sxs-lookup"><span data-stu-id="a10bf-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="a10bf-142">Choisissez le modèle **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="a10bf-143">Cette fonction sera déclenchée chaque fois qu’un objet blob est téléchargé en hello **d’entrée** conteneur.</span><span class="sxs-lookup"><span data-stu-id="a10bf-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="a10bf-144">Hello **d’entrée** nom est spécifié dans hello **chemin d’accès**, à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="a10bf-146">Une fois que vous sélectionnez **BlobTrigger**, certains contrôles plus apparaîtra sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="a10bf-148">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="a10bf-149">Fichiers</span><span class="sxs-lookup"><span data-stu-id="a10bf-149">Files</span></span>

<span data-ttu-id="a10bf-150">Votre fonction Azure est associée à des fichiers de code et à d’autres fichiers décrits dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a10bf-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="a10bf-151">Par défaut, une fonction est associée à des fichiers **function.json** et **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="a10bf-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="a10bf-152">Vous devez tooadd une **project.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="a10bf-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="a10bf-153">reste Hello de cette section affiche les définitions de hello pour ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="a10bf-153">hello rest of this section shows hello definitions for these files.</span></span>

![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="a10bf-155">function.json</span><span class="sxs-lookup"><span data-stu-id="a10bf-155">function.json</span></span>

<span data-ttu-id="a10bf-156">fichier de function.json Hello définit les liaisons de fonction hello et d’autres paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="a10bf-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="a10bf-157">Hello runtime utilise cette toomonitor d’événements fichier toodetermine hello et le fonctionnement de toopass retournées et données vers et à partir de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="a10bf-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="a10bf-158">Pour plus d’informations, consultez [Liaisons HTTP et webhook d’Azure Functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="a10bf-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="a10bf-159">Ensemble hello **désactivé** propriété trop**true** fonction hello tooprevent en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a10bf-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="a10bf-160">Voici un exemple de fichier **function.json**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="a10bf-161">project.json</span><span class="sxs-lookup"><span data-stu-id="a10bf-161">project.json</span></span>

<span data-ttu-id="a10bf-162">fichier project.json de Hello contient des dépendances.</span><span class="sxs-lookup"><span data-stu-id="a10bf-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="a10bf-163">Voici un exemple de **project.json** fichier incluant hello requis .NET Azure Media Services packages de Nuget.</span><span class="sxs-lookup"><span data-stu-id="a10bf-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="a10bf-164">Notez que les numéros de version hello modifier avec les dernières mises à jour toohello packages, donc vous devez vérifier les versions les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="a10bf-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="a10bf-165">run.csx</span></span>

<span data-ttu-id="a10bf-166">Il s’agit de code c# hello pour votre fonction.</span><span class="sxs-lookup"><span data-stu-id="a10bf-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="a10bf-167">fonction Hello défini ci-dessous moniteurs d’un conteneur du compte de stockage nommé **d’entrée** (c’est ce qui a été spécifié dans le chemin d’accès hello) pour les nouveaux fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="a10bf-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="a10bf-168">Une fois qu’un fichier est déposé dans le conteneur de stockage hello, déclencheur d’objets blob hello exécutera la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="a10bf-169">exemple Hello définie dans cette section montre</span><span class="sxs-lookup"><span data-stu-id="a10bf-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="a10bf-170">Comment tooingest un élément multimédia dans un service de média compte (en copiant un objet blob dans un élément multimédia AMS) et</span><span class="sxs-lookup"><span data-stu-id="a10bf-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="a10bf-171">Comment toosubmit un travail d’encodage qui utilise « Diffusion adaptative en continu » Media Encoder Standard prédéfini.</span><span class="sxs-lookup"><span data-stu-id="a10bf-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="a10bf-172">Dans un scénario réel de hello, probablement vous souhaitez que la progression du travail tootrack et puis publiez votre élément multimédia encodé.</span><span class="sxs-lookup"><span data-stu-id="a10bf-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="a10bf-173">Pour plus d’informations, consultez [notifications du travail Azure utiliser des WebHooks toomonitor Media Services](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="a10bf-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="a10bf-174">Pour plus d’exemples, consultez [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="a10bf-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="a10bf-175">Une fois que vous avez fini de définir votre fonction, cliquez sur **Enregistrer et exécuter**.</span><span class="sxs-lookup"><span data-stu-id="a10bf-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="a10bf-176">Tester votre fonction</span><span class="sxs-lookup"><span data-stu-id="a10bf-176">Test your function</span></span>

<span data-ttu-id="a10bf-177">tootest votre fonction, vous devez tooupload un fichier MP4 dans hello **d’entrée** conteneur hello du compte de stockage que vous avez spécifié dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="a10bf-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="a10bf-178">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a10bf-178">Next step</span></span>

<span data-ttu-id="a10bf-179">À ce stade, vous êtes prêt toostart développe une application de Media Services.</span><span class="sxs-lookup"><span data-stu-id="a10bf-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="a10bf-180">Pour plus d’informations et des exemples et des solutions complètes de l’utilisation des fonctions d’Azure et les applications de la logique des flux de travail Azure Media Services toocreate la création de contenu personnalisé, consultez hello [exemple d’intégration fonctions Media Services .NET sur GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="a10bf-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="a10bf-181">Consultez également [utiliser des WebHooks Azure toomonitor Media Services de notifications avec .NET la tâche](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="a10bf-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="a10bf-182">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a10bf-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a10bf-183">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a10bf-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

