---
title: "aaaHyperlapse des fichiers multimédias avec Azure Media Hyperlapse | Documents Microsoft"
description: "Azure Media Hyperlapse crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action. Cette rubrique montre comment toouse Media Indexer."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Fichiers multimédia hyperlapse avec Azure Media Hyperlapse
Azure Media Hyperlapse est un processeur multimédia (MP) qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action.  Hello frère de nuage trop[de Microsoft Research Pro de Hyperlapse bureau et mobiles de Hyperlapse téléphonique](http://aka.ms/hyperlapse), Hyperlapse Microsoft pour Azure Media Services utilise l’échelle massive de hello Hello Azure Media Services de support Plateforme toohorizontally de traitement de l’échelle et de paralléliser en bloc le traitement de Hyperlapse.

> [!IMPORTANT]
> Microsoft Hyperlapse est conçue toowork meilleures contenu subjective avec un appareil mobile.  Bien que les enregistrements de l’appareil photo pouvez continuer à utiliser, les performances de hello et la qualité de hello processeur de média Azure Media Hyperlapse ne peut pas être garanties pour d’autres types de contenu.  toolearn plus Hyperlapse Microsoft pour Azure Media Services et voir des vidéos d’exemple, l’extraction hello [billet de blog introduction](http://aka.ms/azurehyperlapseblog) à partir de la version préliminaire publique de hello.
> 
> 

Un Azure Media Hyperlapse travail prend comme entrée un fichier d’élément multimédia MP4, MOV ou WMV, ainsi que d’un fichier de configuration qui spécifie les images de la vidéo doivent être le temps écoulé et la vitesse de toowhat (par exemple, 10 000 premières images x 2).  sortie de Hello est un format de stabilisation et temps écoulé associé de la vidéo d’entrée de hello.

Bonjour Azure Media Hyperlapse mises à jour récentes, consultez [blogs de Media Services](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Hyperlapse d'un élément multimédia
Vous devez commencer tooupload votre tooAzure de fichier d’entrée souhaitée Media Services.  toolearn en savoir plus sur hello concepts impliqués dans le chargement et la gestion du contenu, lire hello [article de la gestion de contenu](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Configuration de la présélection pour Hyperlapse
Une fois votre contenu dans votre compte Media Services, vous devez tooconstruct votre configuration prédéfinie.  Hello tableau suivant décrit les champs de hello spécifié par l’utilisateur :

| Champ | Description |
| --- | --- |
| StartFrame |cadre Hello sur quel hello Microsoft Hyperlapse doit commencer le traitement. |
| NumFrames |nombre de Hello de frames tooprocess |
| Vitesse |facteur de Hello avec le toospeed vidéo d’entrée de hello. |

Hello Voici un exemple de fichier de configuration conformes au format XML et JSON :

**Présélection XML :**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Présélection JSON :**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Hyperlapse Microsoft avec hello AMS .NET SDK
Hello méthode ci-dessous télécharge un fichier multimédia comme un élément multimédia et crée un travail avec hello processeur de média Azure Media Hyperlapse.

> [!NOTE]
> Vous disposez déjà d’un CloudMediaContext dans la portée avec hello nom « contexte » de cette toowork de code.  toolearn plus d’informations sur cette option, lecture hello [article de la gestion de contenu](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> argument de chaîne Hello « hyperConfig » est attendu toobe une configuration conforme prédéfinie dans JSON ou XML comme décrit ci-dessus.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Types de fichiers pris en charge
* MP4 
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

