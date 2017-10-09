---
title: "fichiers aaaUpload dans un compte Media Services à l’aide de .NET | Documents Microsoft"
description: "Découvrez comment tooget média du contenu dans Media Services création et téléchargement d’éléments multimédias."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Charger des fichiers dans un compte Media Services à l’aide de .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portail](media-services-portal-upload-files.md)
> 
> 

Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia. Hello **Asset** entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.

fichiers Hello dans asset de hello sont appelés **des fichiers**. Hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts. instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.

> [!NOTE]
> Hello suivant considérations s’appliquent :
> 
> * Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé. Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ». En outre, il ne peut exister un '.' pour l’extension de nom de fichier hello.
> * la longueur du nom de hello Hello ne doit pas dépasser 260 caractères.
> * Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services. Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.
> * Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .
> 

Lorsque vous créez des ressources, vous pouvez spécifier hello suivant les options de chiffrement. 

* **None** : aucun chiffrement. Il s’agit de valeur par défaut de hello. À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.
  Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option. 
* **CommonEncryption** : utilisez cette option quand vous téléchargez du contenu qui a déjà été chiffré et protégé par chiffrement commun ou gestion des droits numériques (DRM) PlayReady (par exemple, une diffusion en continu lisse, « Smooth Streaming », protégée par gestion des droits numériques (DRM) PlayReady).
* **EnvelopeEncrypted** : utilisez cette option quand vous téléchargez du contenu au format HLS chiffré avec AES. Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.
* **StorageEncrypted** - chiffre votre contenu en clair localement à l’aide du chiffrement AES-256 bits, puis le télécharge tooAzure Storage où il est stocké et chiffré au repos. Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie. Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque.
  
    Media Services fournit pour vos éléments multimédias un chiffrement de stockage sur disque, et non pas sur le réseau comme pour la gestion des droits numériques (DRM).
  
    Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources. Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).

Si vous spécifiez pour toobe de votre élément multimédia chiffré avec un **CommonEncrypted** option, ou un **EnvelopeEncypted** option, vous devez tooassociate votre élément multimédia avec un **ContentKey**. Pour plus d’informations, consultez [comment toocreate une ContentKey](media-services-dotnet-create-contentkey.md). 

Si vous spécifiez pour toobe de votre élément multimédia chiffré avec un **StorageEncrypted** option, hello Media Services SDK pour .NET créera un **StorateEncrypted** **ContentKey** pour votre élément multimédia.

Cette rubrique montre comment toouse Media Services .NET SDK ainsi que les fichiers de tooupload extensions Media Services .NET SDK dans un élément multimédia Media Services.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Téléchargement d’un fichier unique avec le Kit de développement logiciel (SDK) .NET de Media Services
Hello exemple de code ci-dessous utilise tooupload du Kit de développement .NET un seul fichier. Hello AccessPolicy et recherche sont créés et détruits par fonction de téléchargement hello. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Téléchargement de plusieurs fichiers avec le Kit de développement logiciel (SDK) .NET de Media Services
Hello suivant de code montre comment toocreate un élément multimédia et téléchargement de plusieurs fichiers.

code de Hello hello suivant :

* Crée un élément multimédia vide, à l’aide de la méthode de CreateEmptyAsset hello définie à l’étape précédente de hello.
* Crée un **AccessPolicy** instance qui définit les autorisations de hello et la durée de ressource de toohello d’accès.
* Crée un **recherche** instance qui fournit les actifs de toohello d’accès.
* Création d'une instance **BlobTransferClient**. Ce type représente un client qui fonctionne sur hello qu'objets BLOB Azure. Dans cet exemple nous utilisons la progression du téléchargement hello client toomonitor hello. 
* Énumère les fichiers dans le répertoire spécifié de hello et crée un **AssetFile** instance pour chaque fichier.
* Téléchargements hello des fichiers dans les Services de support à l’aide de hello **UploadAsync** (méthode). 

> [!NOTE]
> Utilisez hello UploadAsync méthode tooensure hello appels ne sont pas bloquées et les fichiers de hello sont téléchargés en parallèle.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Lors du téléchargement d’un grand nombre de ressources, tenez compte hello qui suit.

* Créez un objet **CloudMediaContext** par thread. Hello **CloudMediaContext** classe n’est pas thread-safe.
* Augmentez NumberOfConcurrentTransfers de valeur par défaut hello 2 tooa plus élevée, telle que 5. Cette propriété affecte toutes les instances de **CloudMediaContext**. 
* Conservez ParallelTransferThreadCount valeur hello par défaut 10.

## <a id="ingest_in_bulk"></a>Réception d’éléments multimédias en bloc à l’aide du Kit de développement logiciel (SDK) .NET de Media Services
Le téléchargement de fichiers multimédias volumineux peut entraîner un goulot d’étranglement lors de la création de l'élément multimédia. Réception d’éléments multimédias en bloc ou « Réception en bloc », implique de découpler la création d’élément multimédia à partir du processus de téléchargement hello. toouse une approche de réception en bloc, créez un manifeste (IngestManifest) qui décrit l’élément multimédia de hello et ses fichiers associés. Utilisez ensuite méthode de téléchargement hello du conteneur d’objets blob de votre choix tooupload hello fichiers associés toohello du manifeste. Microsoft Azure Media Services surveille le conteneur d’objets blob hello associée hello manifeste. Une fois qu’un fichier est un conteneur d’objets blob toohello téléchargé, Microsoft Azure Media Services complète de création de ressource de hello en fonction de configuration hello d’actif hello dans le manifeste hello (IngestManifestAsset).

toocreate un nouvel IngestManifest appeler la méthode de création de hello exposée par hello collection les IngestManifests sur hello CloudMediaContext. Cette méthode crée un nouvel IngestManifest avec le nom de manifeste hello que vous fournissez.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Créer des composants de hello qui seront associés au bloc de hello IngestManifest. Configurer les options de chiffrement hello souhaité sur asset hello pour la réception en bloc.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Un IngestManifestAsset associe un élément multimédia à un IngestManifest en bloc pour la réception en bloc. Il associe également hello AssetFiles qui composent chaque élément multimédia. toocreate un IngestManifestAsset, utilisez la méthode de création de hello sur le contexte de serveur hello.

Hello exemple suivant montre Ajout deux IngestManifestAssets nouvelles qui associer des éléments de deux hello créé précédemment en bloc de toohello manifeste de réception. Chaque IngestManifestAsset associe également un ensemble de fichiers qui seront téléchargés pour chaque élément multimédia lors de la réception en bloc.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Vous pouvez utiliser n’importe quelle application de client haute vitesse capable de télécharger le conteneur de stockage blob pour les fichiers actifs hello toohello URI fourni par hello **IIngestManifest.BlobStorageUriForUpload** propriété Hello IngestManifest. [Aspera On Demand pour l'Application Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)est un service de téléchargement à grande vitesse intéressant. Vous pouvez également écrire du code les fichiers de ressources hello tooupload comme indiqué dans l’exemple de code suivant de hello.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

code Hello pour le téléchargement des fichiers d’éléments multimédias hello pour exemple hello utilisé dans cette rubrique est illustré hello, exemple de code suivant.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


Vous pouvez déterminer la progression hello de réception de hello en bloc pour tous les actifs associés à un **IngestManifest** en interrogeant la propriété de statistiques hello Hello **IngestManifest**. Dans les informations de progression tooupdate commande, vous devez utiliser un nouveau **CloudMediaContext** chaque fois que vous interrogez propriété Statistics de hello.

Hello exemple suivant montre comment interroger un IngestManifest par son **Id**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Téléchargement de fichiers à l’aide des extensions du Kit de développement logiciel (SDK) .NET
exemple Hello ci-dessous montre comment tooupload un seul fichier à l’aide des Extensions du Kit de développement logiciel .NET. Dans ce cas hello **CreateFromFile** méthode est utilisée, mais la version asynchrone de hello est également disponible (**CreateFromFileAsync**). Hello **CreateFromFile** méthode vous permet de spécifier le nom de fichier hello, option de chiffrement et un rappel Bonjour tooreport de commande la progression du fichier de hello du téléchargement.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Hello exemple suivant appelle la fonction de UploadFile et spécifie le chiffrement de stockage en tant que l’option de création hello actif.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez désormais encoder vos éléments multimédias téléchargés. Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).

Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré. Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Étape suivante
Maintenant que vous avez téléchargé un élément multimédia tooMedia Services, accédez à toohello [comment tooGet un processeur multimédia] [ How tooGet a Media Processor] rubrique.

[How tooGet a Media Processor]: media-services-get-media-processor.md

