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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="d932e-104">Fichiers multimédia hyperlapse avec Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d932e-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="d932e-105">Azure Media Hyperlapse est un processeur multimédia (MP) qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action.</span><span class="sxs-lookup"><span data-stu-id="d932e-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="d932e-106">L'équivalent cloud du [bureau Microsoft Research Hyperlapse Pro et Hyperlapse Mobile pour les applications téléphoniques](http://aka.ms/hyperlapse), Microsoft Hyperlapse pour Azure Media Services, utilise la mise à l'échelle massive de traitement de supports multimédia Azure Media Services pour une évolutivité horizontale et une mise en parallèle du traitement en bloc d'Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="d932e-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d932e-107">Microsoft Hyperlapse est conçu pour fonctionner parfaitement dans du contenu « first-person » avec une caméra en mouvement.</span><span class="sxs-lookup"><span data-stu-id="d932e-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="d932e-108">Bien que les enregistrements effectués par des appareils photo soient toujours pris en charge, les performances et la qualité du processeur multimédia Azure Media Hyperlapse ne peuvent pas être garanties pour d'autres types de contenu.</span><span class="sxs-lookup"><span data-stu-id="d932e-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="d932e-109">Pour en savoir plus sur Microsoft Hyperlapse pour Azure Media Services et voir des exemples de vidéos, consultez la [billet de blog d'introduction](http://aka.ms/azurehyperlapseblog) depuis la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="d932e-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="d932e-110">Une tâche Azure Media Hyperlapse prend comme entrée un fichier de ressource MP4, MOV ou WMV, ainsi qu'un fichier de configuration qui spécifie les images sur lesquelles la technique image par image doit être appliquée et à quelle vitesse (par exemple, les 10 000 premières images à 2x).</span><span class="sxs-lookup"><span data-stu-id="d932e-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="d932e-111">La sortie est un rendu stabilisé et accéléré de l'entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="d932e-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="d932e-112">Pour connaître les dernières mises à jour d'Azure Media Hyperlapse, consultez les [blogs Media Services](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="d932e-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="d932e-113">Hyperlapse d'un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="d932e-113">Hyperlapse an asset</span></span>
<span data-ttu-id="d932e-114">Vous devez tout d'abord charger votre fichier d'entrée souhaité dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d932e-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="d932e-115">Pour en savoir plus sur les concepts relatifs au chargement et à la gestion de contenu, lisez l' [article sur la gestion de contenu](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d932e-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="d932e-116"><a id="configuration"></a>Configuration de la présélection pour Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d932e-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="d932e-117">Une fois votre contenu dans votre compte Media Services, vous devez construire la présélection de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d932e-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="d932e-118">Le tableau suivant décrit les champs spécifiés par l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d932e-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="d932e-119">Champ</span><span class="sxs-lookup"><span data-stu-id="d932e-119">Field</span></span> | <span data-ttu-id="d932e-120">Description</span><span class="sxs-lookup"><span data-stu-id="d932e-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d932e-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="d932e-121">StartFrame</span></span> |<span data-ttu-id="d932e-122">L'image à partir de laquelle le traitement avec Microsoft Hyperlapse doit commencer.</span><span class="sxs-lookup"><span data-stu-id="d932e-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="d932e-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="d932e-123">NumFrames</span></span> |<span data-ttu-id="d932e-124">Le nombre d'images à traiter</span><span class="sxs-lookup"><span data-stu-id="d932e-124">The number of frames to process</span></span> |
| <span data-ttu-id="d932e-125">Vitesse</span><span class="sxs-lookup"><span data-stu-id="d932e-125">Speed</span></span> |<span data-ttu-id="d932e-126">Le facteur de l'accélération de la vidéo d'entrée.</span><span class="sxs-lookup"><span data-stu-id="d932e-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="d932e-127">Voici un exemple de fichier de configuration conforme au format XML et JSON :</span><span class="sxs-lookup"><span data-stu-id="d932e-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="d932e-128">**Présélection XML :**</span><span class="sxs-lookup"><span data-stu-id="d932e-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="d932e-129">**Présélection JSON :**</span><span class="sxs-lookup"><span data-stu-id="d932e-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="d932e-130"><a id="sample_code"></a> Microsoft Hyperlapse avec le kit de développement logiciel .NET</span><span class="sxs-lookup"><span data-stu-id="d932e-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="d932e-131">La méthode suivante charge un fichier multimédia en tant qu'élément multimédia et crée une tâche avec le processeur multimédia Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="d932e-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="d932e-132">Pour que ce code fonctionne, vous devez déjà disposer d'un CloudMediaContext avec le nom « context ».</span><span class="sxs-lookup"><span data-stu-id="d932e-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="d932e-133">Pour en savoir plus à ce sujet, lisez l' [article sur la gestion de contenu](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d932e-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="d932e-134">L'argument de chaîne « hyperConfig » doit être une présélection de configuration conforme prédéfinie au format JSON ou XML, comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="d932e-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
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

### <span data-ttu-id="d932e-135"><a id="file_types"></a>Types de fichiers pris en charge</span><span class="sxs-lookup"><span data-stu-id="d932e-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="d932e-136">MP4 </span><span class="sxs-lookup"><span data-stu-id="d932e-136">MP4</span></span>
* <span data-ttu-id="d932e-137">MOV</span><span class="sxs-lookup"><span data-stu-id="d932e-137">MOV</span></span>
* <span data-ttu-id="d932e-138">WMV</span><span class="sxs-lookup"><span data-stu-id="d932e-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d932e-139">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d932e-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d932e-140">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d932e-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d932e-141">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="d932e-141">Related links</span></span>
[<span data-ttu-id="d932e-142">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="d932e-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d932e-143">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="d932e-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

