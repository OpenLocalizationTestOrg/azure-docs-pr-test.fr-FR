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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="21a69-104">Fichiers multimédia hyperlapse avec Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="21a69-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="21a69-105">Azure Media Hyperlapse est un processeur multimédia (MP) qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d'un contenu de caméra à la première personne (first-person camera) ou d'action.</span><span class="sxs-lookup"><span data-stu-id="21a69-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="21a69-106">Hello frère de nuage trop[de Microsoft Research Pro de Hyperlapse bureau et mobiles de Hyperlapse téléphonique](http://aka.ms/hyperlapse), Hyperlapse Microsoft pour Azure Media Services utilise l’échelle massive de hello Hello Azure Media Services de support Plateforme toohorizontally de traitement de l’échelle et de paralléliser en bloc le traitement de Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="21a69-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21a69-107">Microsoft Hyperlapse est conçue toowork meilleures contenu subjective avec un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="21a69-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="21a69-108">Bien que les enregistrements de l’appareil photo pouvez continuer à utiliser, les performances de hello et la qualité de hello processeur de média Azure Media Hyperlapse ne peut pas être garanties pour d’autres types de contenu.</span><span class="sxs-lookup"><span data-stu-id="21a69-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="21a69-109">toolearn plus Hyperlapse Microsoft pour Azure Media Services et voir des vidéos d’exemple, l’extraction hello [billet de blog introduction](http://aka.ms/azurehyperlapseblog) à partir de la version préliminaire publique de hello.</span><span class="sxs-lookup"><span data-stu-id="21a69-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="21a69-110">Un Azure Media Hyperlapse travail prend comme entrée un fichier d’élément multimédia MP4, MOV ou WMV, ainsi que d’un fichier de configuration qui spécifie les images de la vidéo doivent être le temps écoulé et la vitesse de toowhat (par exemple, 10 000 premières images x 2).</span><span class="sxs-lookup"><span data-stu-id="21a69-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="21a69-111">sortie de Hello est un format de stabilisation et temps écoulé associé de la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="21a69-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="21a69-112">Bonjour Azure Media Hyperlapse mises à jour récentes, consultez [blogs de Media Services](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="21a69-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="21a69-113">Hyperlapse d'un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="21a69-113">Hyperlapse an asset</span></span>
<span data-ttu-id="21a69-114">Vous devez commencer tooupload votre tooAzure de fichier d’entrée souhaitée Media Services.</span><span class="sxs-lookup"><span data-stu-id="21a69-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="21a69-115">toolearn en savoir plus sur hello concepts impliqués dans le chargement et la gestion du contenu, lire hello [article de la gestion de contenu](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="21a69-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="21a69-116"><a id="configuration"></a>Configuration de la présélection pour Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="21a69-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="21a69-117">Une fois votre contenu dans votre compte Media Services, vous devez tooconstruct votre configuration prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="21a69-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="21a69-118">Hello tableau suivant décrit les champs de hello spécifié par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="21a69-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="21a69-119">Champ</span><span class="sxs-lookup"><span data-stu-id="21a69-119">Field</span></span> | <span data-ttu-id="21a69-120">Description</span><span class="sxs-lookup"><span data-stu-id="21a69-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21a69-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="21a69-121">StartFrame</span></span> |<span data-ttu-id="21a69-122">cadre Hello sur quel hello Microsoft Hyperlapse doit commencer le traitement.</span><span class="sxs-lookup"><span data-stu-id="21a69-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="21a69-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="21a69-123">NumFrames</span></span> |<span data-ttu-id="21a69-124">nombre de Hello de frames tooprocess</span><span class="sxs-lookup"><span data-stu-id="21a69-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="21a69-125">Vitesse</span><span class="sxs-lookup"><span data-stu-id="21a69-125">Speed</span></span> |<span data-ttu-id="21a69-126">facteur de Hello avec le toospeed vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="21a69-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="21a69-127">Hello Voici un exemple de fichier de configuration conformes au format XML et JSON :</span><span class="sxs-lookup"><span data-stu-id="21a69-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="21a69-128">**Présélection XML :**</span><span class="sxs-lookup"><span data-stu-id="21a69-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="21a69-129">**Présélection JSON :**</span><span class="sxs-lookup"><span data-stu-id="21a69-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="21a69-130"><a id="sample_code"></a>Hyperlapse Microsoft avec hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="21a69-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="21a69-131">Hello méthode ci-dessous télécharge un fichier multimédia comme un élément multimédia et crée un travail avec hello processeur de média Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="21a69-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="21a69-132">Vous disposez déjà d’un CloudMediaContext dans la portée avec hello nom « contexte » de cette toowork de code.</span><span class="sxs-lookup"><span data-stu-id="21a69-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="21a69-133">toolearn plus d’informations sur cette option, lecture hello [article de la gestion de contenu](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="21a69-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="21a69-134">argument de chaîne Hello « hyperConfig » est attendu toobe une configuration conforme prédéfinie dans JSON ou XML comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="21a69-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

### <span data-ttu-id="21a69-135"><a id="file_types"></a>Types de fichiers pris en charge</span><span class="sxs-lookup"><span data-stu-id="21a69-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="21a69-136">MP4 </span><span class="sxs-lookup"><span data-stu-id="21a69-136">MP4</span></span>
* <span data-ttu-id="21a69-137">MOV</span><span class="sxs-lookup"><span data-stu-id="21a69-137">MOV</span></span>
* <span data-ttu-id="21a69-138">WMV</span><span class="sxs-lookup"><span data-stu-id="21a69-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="21a69-139">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="21a69-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21a69-140">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="21a69-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="21a69-141">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="21a69-141">Related links</span></span>
[<span data-ttu-id="21a69-142">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="21a69-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="21a69-143">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="21a69-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

