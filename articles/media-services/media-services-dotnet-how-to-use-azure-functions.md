---
title: "Développement de fonctions Azure Functions avec Media Services"
description: "Cette rubrique montre comment développer des fonctions Azure Functions avec Media Services à l’aide du portail Azure."
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
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="84805-103">Développement de fonctions Azure Functions avec Media Services</span><span class="sxs-lookup"><span data-stu-id="84805-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="84805-104">Cette rubrique vous montre comment vous familiariser avec la création de fonctions Azure Functions qui utilisent Media Services.</span><span class="sxs-lookup"><span data-stu-id="84805-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="84805-105">La fonction Azure Function définie dans cette rubrique surveille un conteneur de compte de stockage nommé **input** pour les nouveaux fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="84805-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="84805-106">Une fois qu’un fichier est déplacé dans le conteneur de stockage, le déclencheur d’objet blob exécute la fonction.</span><span class="sxs-lookup"><span data-stu-id="84805-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="84805-107">Si vous souhaitez explorer et déployer des fonctions Azure existantes qui utilisent Azure Media Services, consultez [Fonctions Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="84805-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="84805-108">Ce référentiel contient des exemples qui utilisent Media Services pour afficher les flux de travail liés à l’ingestion de contenu directement à partir du Stockage Blob, à l’encodage et à l’écriture de contenu dans le Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="84805-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="84805-109">Il inclut également des exemples décrivant la manière de contrôler les notifications de travail via les WebHooks et les files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="84805-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="84805-110">Vous pouvez également développer vos fonctions en fonction des exemples dans le référentiel [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="84805-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="84805-111">Pour déployer les fonctions, appuyez sur le bouton **Déployer dans Azure**.</span><span class="sxs-lookup"><span data-stu-id="84805-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84805-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84805-112">Prerequisites</span></span>

- <span data-ttu-id="84805-113">Pour créer votre première fonction, vous devez avoir un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="84805-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="84805-114">Si tel n’est pas le cas, des [comptes gratuits sont disponibles](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="84805-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="84805-115">Si vous souhaitez créer des fonctions Azure Functions qui effectuent des actions sur votre compte Azure Media Services (AMS) ou qui écoutent des événements envoyés par Media Services, vous devez créer un compte AMS, comme décrit [ici](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="84805-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="84805-116">Comprendre [l’utilisation des fonctions Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84805-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="84805-117">Consultez également :</span><span class="sxs-lookup"><span data-stu-id="84805-117">Also, review:</span></span>
    - [<span data-ttu-id="84805-118">Liaisons HTTP et webhook Azure Functions</span><span class="sxs-lookup"><span data-stu-id="84805-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="84805-119">Guide pratique pour configurer les paramètres d’application Azure Functions</span><span class="sxs-lookup"><span data-stu-id="84805-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="84805-120">Considérations</span><span class="sxs-lookup"><span data-stu-id="84805-120">Considerations</span></span>

-  <span data-ttu-id="84805-121">Azure Functions s’exécutant sur le plan Consommation a une limite de délai d’expiration de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="84805-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="84805-122">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="84805-122">Create a function app</span></span>

1. <span data-ttu-id="84805-123">Accédez au [Portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="84805-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="84805-124">Suivez [cette procédure](../azure-functions/functions-create-function-app-portal.md) pour créer une Function App.</span><span class="sxs-lookup"><span data-stu-id="84805-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="84805-125">Un compte de stockage que vous spécifiez dans la variable d’environnement **StorageConnection** (voir l’étape suivante) doit être dans la même région que votre application.</span><span class="sxs-lookup"><span data-stu-id="84805-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="84805-126">Configuration des paramètres Function App</span><span class="sxs-lookup"><span data-stu-id="84805-126">Configure function app settings</span></span>

<span data-ttu-id="84805-127">Lorsque vous développez des fonctions Media Services, il est utile d’ajouter des variables d’environnement qui seront utilisées dans toutes vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="84805-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="84805-128">Pour configurer les paramètres d’application, cliquez sur le lien Configurer les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="84805-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="84805-129">Pour en savoir plus, consultez [Configuration des paramètres d’application Azure Function](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="84805-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="84805-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="84805-130">For example:</span></span>

![Paramètres](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="84805-132">La fonction, définie dans cet article, suppose que les variables d’environnement suivantes se trouvent dans vos paramètres d’application :</span><span class="sxs-lookup"><span data-stu-id="84805-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="84805-133">**AMSAccount** : *nom de compte AMS* (ex. testams)</span><span class="sxs-lookup"><span data-stu-id="84805-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="84805-134">**AMSKey** : *clé de compte AMS* (ex. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="84805-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="84805-135">**MediaServicesStorageAccountName** : *nom de compte de stockage* (ex. testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="84805-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="84805-136">**MediaServicesStorageAccountKey** : *clé de compte de stockage* (ex. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="84805-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="84805-137">**StorageConnection** : *connexion de stockage* (ex. DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="84805-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="84805-138">Créer une fonction</span><span class="sxs-lookup"><span data-stu-id="84805-138">Create a function</span></span>

<span data-ttu-id="84805-139">Une fois votre Function App déployée, vous pouvez la retrouver parmi les fonctions Azure Functions **App Services**.</span><span class="sxs-lookup"><span data-stu-id="84805-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="84805-140">Sélectionnez votre Function App et cliquez sur **Nouvelle fonction**.</span><span class="sxs-lookup"><span data-stu-id="84805-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="84805-141">Choisissez le langage **C#** et le scénario **Traitement des données**.</span><span class="sxs-lookup"><span data-stu-id="84805-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="84805-142">Choisissez le modèle **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="84805-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="84805-143">Cette fonction sera déclenchée à chaque fois qu’un objet blob est chargé dans le conteneur **input**.</span><span class="sxs-lookup"><span data-stu-id="84805-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="84805-144">Le nom **input** est spécifié dans le **chemin d’accès**, à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="84805-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="84805-146">Une fois que vous sélectionnez **BlobTrigger**, certaines commandes s’affichent sur la page.</span><span class="sxs-lookup"><span data-stu-id="84805-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="84805-148">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="84805-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="84805-149">Fichiers</span><span class="sxs-lookup"><span data-stu-id="84805-149">Files</span></span>

<span data-ttu-id="84805-150">Votre fonction Azure est associée à des fichiers de code et à d’autres fichiers décrits dans cette section.</span><span class="sxs-lookup"><span data-stu-id="84805-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="84805-151">Par défaut, une fonction est associée à des fichiers **function.json** et **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="84805-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="84805-152">Vous devez ajouter un fichier **project.json**.</span><span class="sxs-lookup"><span data-stu-id="84805-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="84805-153">Le reste de cette section présente les définitions de ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="84805-153">The rest of this section shows the definitions for these files.</span></span>

![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="84805-155">function.json</span><span class="sxs-lookup"><span data-stu-id="84805-155">function.json</span></span>

<span data-ttu-id="84805-156">Le fichier function.json définit les liaisons de fonction et d’autres paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="84805-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="84805-157">Le runtime utilise ce fichier pour déterminer les événements à surveiller et comment passer des données et renvoyer des données à partir de l’exécution de la fonction.</span><span class="sxs-lookup"><span data-stu-id="84805-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="84805-158">Pour plus d’informations, consultez [Liaisons HTTP et webhook d’Azure Functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="84805-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="84805-159">Définissez la propriété **disabled** sur **true** pour empêcher l’exécution de la fonction.</span><span class="sxs-lookup"><span data-stu-id="84805-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="84805-160">Voici un exemple de fichier **function.json**.</span><span class="sxs-lookup"><span data-stu-id="84805-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="84805-161">project.json</span><span class="sxs-lookup"><span data-stu-id="84805-161">project.json</span></span>

<span data-ttu-id="84805-162">Le fichier project.json contient des dépendances.</span><span class="sxs-lookup"><span data-stu-id="84805-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="84805-163">Voici un exemple de fichier **project.json** qui inclut les packages .NET Azure Media Services requis à partir de Nuget.</span><span class="sxs-lookup"><span data-stu-id="84805-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="84805-164">Notez que les numéros de version changeront avec les dernières mises à jour pour les packages, donc vous devez vérifier les versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="84805-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="84805-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="84805-165">run.csx</span></span>

<span data-ttu-id="84805-166">Il s’agit du code C# de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="84805-166">This is the C# code for your function.</span></span>  <span data-ttu-id="84805-167">La fonction définie ci-dessous surveille un conteneur de compte de stockage nommé **input** (c’est ce qui a été spécifié dans le chemin d’accès) pour les nouveaux fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="84805-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="84805-168">Une fois qu’un fichier est déplacé dans le conteneur de stockage, le déclencheur d’objet blob exécute la fonction.</span><span class="sxs-lookup"><span data-stu-id="84805-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="84805-169">L’exemple défini dans cette section montre</span><span class="sxs-lookup"><span data-stu-id="84805-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="84805-170">comment ingérer une ressource dans un compte Media Services (par copie d’un objet blob dans une ressource AMS) et</span><span class="sxs-lookup"><span data-stu-id="84805-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="84805-171">comment soumettre un travail d’encodage qui utilise la valeur prédéfinie « Diffusion adaptative en continu » de Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="84805-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="84805-172">Dans le scénario réel, vous voulez probablement effectuer le suivi de la progression du travail, puis publier votre ressource encodée.</span><span class="sxs-lookup"><span data-stu-id="84805-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="84805-173">Pour plus d’informations, consultez [Utiliser Azure WebHooks pour surveiller les notifications de travaux Media Services](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="84805-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="84805-174">Pour plus d’exemples, consultez [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="84805-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="84805-175">Une fois que vous avez fini de définir votre fonction, cliquez sur **Enregistrer et exécuter**.</span><span class="sxs-lookup"><span data-stu-id="84805-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
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

        // Get the destination asset container reference
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

        // Get hold of the destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="84805-176">Tester votre fonction</span><span class="sxs-lookup"><span data-stu-id="84805-176">Test your function</span></span>

<span data-ttu-id="84805-177">Pour tester votre fonction, vous devez charger un fichier MP4 dans le conteneur **input** du compte de stockage que vous avez spécifié dans la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="84805-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="84805-178">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="84805-178">Next step</span></span>

<span data-ttu-id="84805-179">À ce stade, vous êtes prêt à commencer le développement d’une application Media Services.</span><span class="sxs-lookup"><span data-stu-id="84805-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="84805-180">Pour plus d’informations, ainsi que des exemples et des solutions de l’utilisation d’Azure Functions et de Logic Apps avec Azure Media Services pour créer des flux de travail de création de contenu personnalisé, consultez [l’exemple Media Services .NET Functions Integration sur GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="84805-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="84805-181">Consultez également [Utiliser Azure WebHooks pour surveiller les notifications de travaux Media Services avec .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="84805-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="84805-182">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="84805-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="84805-183">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="84805-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

