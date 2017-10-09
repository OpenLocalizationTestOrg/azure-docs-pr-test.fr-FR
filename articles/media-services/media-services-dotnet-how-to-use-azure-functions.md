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
#<a name="develop-azure-functions-with-media-services"></a>Développement de fonctions Azure Functions avec Media Services

Cette rubrique vous montre comment tooget démarrer avec la création de fonctions Azure qui utilisent les Services de support. Hello fonction Azure définis dans cette rubrique surveille un conteneur du compte de stockage nommé **d’entrée** de nouveaux fichiers MP4. Une fois qu’un fichier est déposé dans le conteneur de stockage hello, déclencheur d’objets blob hello exécutera la fonction hello.

Si vous souhaitez tooexplore et déployez des fonctions Azure existantes qui utilisent Azure Media Services, consultez [fonctions d’Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Ce référentiel contient des exemples qui utilisent les Services de support tooshow flux de travail connexe tooingesting contenu directement depuis le stockage blob, de l’encodage et écrire le contenu de sauvegarde tooblob stockage. Il contient également des exemples de comment toomonitor travail notifications via des WebHooks et des files d’attente Azure. Vous pouvez également développer vos fonctions basées sur des exemples hello Bonjour [fonctions d’Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) référentiel. les fonctions hello toodeploy, appuyez sur hello **déployer tooAzure** bouton.

## <a name="prerequisites"></a>Composants requis

- Avant de pouvoir créer votre première fonction, vous devez toohave un compte Azure actif. Si tel n’est pas le cas, des [comptes gratuits sont disponibles](https://azure.microsoft.com/free/).
- Si vous vous apprêtez à des fonctions de Azure toocreate qui effectuent des actions sur votre compte Azure Media Services (AMS) ou écouter tooevents envoyé par Media Services, vous devez créer un compte AMS, comme décrit [ici](media-services-portal-create-account.md).
- Présentation de [comment toouse Azure fonctions](../azure-functions/functions-overview.md). Consultez également :
    - [Liaisons HTTP et webhook Azure Functions](../azure-functions/functions-triggers-bindings.md)
    - [Comment tooconfigure paramètres de l’application Azure (fonction)](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Considérations

-  Fonctions Azure s’exécutant sous le plan de la consommation hello ont délai d’attente de 5 minutes à limiter.

## <a name="create-a-function-app"></a>Créer une Function App

1. Accédez toohello [portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.
2. Suivez [cette procédure](../azure-functions/functions-create-function-app-portal.md) pour créer une Function App.

>[!NOTE]
> Un compte de stockage que vous spécifiez dans hello **StorageConnection** variable d’environnement (voir l’étape suivante de hello) doit être Bonjour même région que votre application.

## <a name="configure-function-app-settings"></a>Configuration des paramètres Function App

Lorsque vous développez des fonctions de Media Services, il est pratique tooadd des variables d’environnement qui seront utilisés dans l’ensemble de vos fonctions. paramètres de l’application tooconfigure, cliquez sur lien de configurer les paramètres de l’application hello. Pour plus d’informations, consultez [comment tooconfigure paramètres de l’application Azure fonction](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Par exemple :

![Paramètres](./media/media-services-azure-functions/media-services-azure-functions001.png)

fonction Hello, définie dans cet article, suppose que vous avez hello suivant des variables d’environnement dans vos paramètres d’application :

**AMSAccount** : *nom de compte AMS* (ex. testams)

**AMSKey** : *clé de compte AMS* (ex. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)

**MediaServicesStorageAccountName** : *nom de compte de stockage* (ex. testamsstorage)

**MediaServicesStorageAccountKey** : *clé de compte de stockage* (ex. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)

**StorageConnection** : *connexion de stockage* (ex. DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)

## <a name="create-a-function"></a>Créer une fonction

Une fois votre Function App déployée, vous pouvez la retrouver parmi les fonctions Azure Functions **App Services**.

1. Sélectionnez votre Function App et cliquez sur **Nouvelle fonction**.
2. Choisissez hello **c#** language et **le traitement des données** scénario.
3. Choisissez le modèle **BlobTrigger**. Cette fonction sera déclenchée chaque fois qu’un objet blob est téléchargé en hello **d’entrée** conteneur. Hello **d’entrée** nom est spécifié dans hello **chemin d’accès**, à l’étape suivante de hello.

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Une fois que vous sélectionnez **BlobTrigger**, certains contrôles plus apparaîtra sur la page de hello.

    ![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Cliquez sur **Create**. 


## <a name="files"></a>Fichiers

Votre fonction Azure est associée à des fichiers de code et à d’autres fichiers décrits dans cette section. Par défaut, une fonction est associée à des fichiers **function.json** et **run.csx** (C#). Vous devez tooadd une **project.json** fichier. reste Hello de cette section affiche les définitions de hello pour ces fichiers.

![fichiers d'entrée](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

fichier de function.json Hello définit les liaisons de fonction hello et d’autres paramètres de configuration. Hello runtime utilise cette toomonitor d’événements fichier toodetermine hello et le fonctionnement de toopass retournées et données vers et à partir de l’exécution. Pour plus d’informations, consultez [Liaisons HTTP et webhook d’Azure Functions](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Ensemble hello **désactivé** propriété trop**true** fonction hello tooprevent en cours d’exécution. 


Voici un exemple de fichier **function.json**.

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

### <a name="projectjson"></a>project.json

fichier project.json de Hello contient des dépendances. Voici un exemple de **project.json** fichier incluant hello requis .NET Azure Media Services packages de Nuget. Notez que les numéros de version hello modifier avec les dernières mises à jour toohello packages, donc vous devez vérifier les versions les plus récentes hello. 

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
    
### <a name="runcsx"></a>run.csx

Il s’agit de code c# hello pour votre fonction.  fonction Hello défini ci-dessous moniteurs d’un conteneur du compte de stockage nommé **d’entrée** (c’est ce qui a été spécifié dans le chemin d’accès hello) pour les nouveaux fichiers MP4. Une fois qu’un fichier est déposé dans le conteneur de stockage hello, déclencheur d’objets blob hello exécutera la fonction hello.
    
exemple Hello définie dans cette section montre 

1. Comment tooingest un élément multimédia dans un service de média compte (en copiant un objet blob dans un élément multimédia AMS) et 
2. Comment toosubmit un travail d’encodage qui utilise « Diffusion adaptative en continu » Media Encoder Standard prédéfini.

Dans un scénario réel de hello, probablement vous souhaitez que la progression du travail tootrack et puis publiez votre élément multimédia encodé. Pour plus d’informations, consultez [notifications du travail Azure utiliser des WebHooks toomonitor Media Services](media-services-dotnet-check-job-progress-with-webhooks.md). Pour plus d’exemples, consultez [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Une fois que vous avez fini de définir votre fonction, cliquez sur **Enregistrer et exécuter**.

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
##<a name="test-your-function"></a>Tester votre fonction

tootest votre fonction, vous devez tooupload un fichier MP4 dans hello **d’entrée** conteneur hello du compte de stockage que vous avez spécifié dans la chaîne de connexion hello.  

## <a name="next-step"></a>Étape suivante

À ce stade, vous êtes prêt toostart développe une application de Media Services. 
 
Pour plus d’informations et des exemples et des solutions complètes de l’utilisation des fonctions d’Azure et les applications de la logique des flux de travail Azure Media Services toocreate la création de contenu personnalisé, consultez hello [exemple d’intégration fonctions Media Services .NET sur GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Consultez également [utiliser des WebHooks Azure toomonitor Media Services de notifications avec .NET la tâche](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

