---
title: "Fichiers multimédias Hyperlapse avec Azure Media Hyperlapse | Microsoft Docs"
description: "Azure Media Hyperlapse crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action. Cette rubrique explique comment utiliser Media Indexer."
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
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Fichiers multimédia hyperlapse avec Azure Media Hyperlapse
Azure Media Hyperlapse est un processeur multimédia (MP) qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action.  L'équivalent cloud du [bureau Microsoft Research Hyperlapse Pro et Hyperlapse Mobile pour les applications téléphoniques](http://aka.ms/hyperlapse), Microsoft Hyperlapse pour Azure Media Services, utilise la mise à l'échelle massive de traitement de supports multimédia Azure Media Services pour une évolutivité horizontale et une mise en parallèle du traitement en bloc d'Hyperlapse.

> [!IMPORTANT]
> Microsoft Hyperlapse est conçu pour fonctionner parfaitement dans du contenu « first-person » avec une caméra en mouvement.  Bien que les enregistrements effectués par des appareils photo soient toujours pris en charge, les performances et la qualité du processeur multimédia Azure Media Hyperlapse ne peuvent pas être garanties pour d'autres types de contenu.  Pour en savoir plus sur Microsoft Hyperlapse pour Azure Media Services et voir des exemples de vidéos, consultez la [billet de blog d'introduction](http://aka.ms/azurehyperlapseblog) depuis la version préliminaire.
> 
> 

Une tâche Azure Media Hyperlapse prend comme entrée un fichier de ressource MP4, MOV ou WMV, ainsi qu'un fichier de configuration qui spécifie les images sur lesquelles la technique image par image doit être appliquée et à quelle vitesse (par exemple, les 10 000 premières images à 2x).  La sortie est un rendu stabilisé et accéléré de l'entrée vidéo.

Pour connaître les dernières mises à jour d'Azure Media Hyperlapse, consultez les [blogs Media Services](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Hyperlapse d'un élément multimédia
Vous devez tout d'abord charger votre fichier d'entrée souhaité dans Azure Media Services.  Pour en savoir plus sur les concepts relatifs au chargement et à la gestion de contenu, lisez l' [article sur la gestion de contenu](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Configuration de la présélection pour Hyperlapse
Une fois votre contenu dans votre compte Media Services, vous devez construire la présélection de votre configuration.  Le tableau suivant décrit les champs spécifiés par l'utilisateur :

| Champ | Description |
| --- | --- |
| StartFrame |L'image à partir de laquelle le traitement avec Microsoft Hyperlapse doit commencer. |
| NumFrames |Le nombre d'images à traiter |
| Vitesse |Le facteur de l'accélération de la vidéo d'entrée. |

Voici un exemple de fichier de configuration conforme au format XML et JSON :

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

### <a id="sample_code"></a> Microsoft Hyperlapse avec le kit de développement logiciel .NET
La méthode suivante charge un fichier multimédia en tant qu'élément multimédia et crée une tâche avec le processeur multimédia Azure Media Hyperlapse.

> [!NOTE]
> Pour que ce code fonctionne, vous devez déjà disposer d'un CloudMediaContext avec le nom « context ».  Pour en savoir plus à ce sujet, lisez l' [article sur la gestion de contenu](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> L'argument de chaîne « hyperConfig » doit être une présélection de configuration conforme prédéfinie au format JSON ou XML, comme décrit précédemment.
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

            // If job state is Error, the event handling
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

