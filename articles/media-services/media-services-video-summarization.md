---
title: "Utiliser Azure Media Video Thumbnails pour créer une synthèse d’une vidéo | Microsoft Docs"
description: "La synthèse d’une vidéo peut vous aider à créer des synthèses de longues vidéos en sélectionnant automatiquement des extraits intéressants à partir de la vidéo source. Elle est utile quand vous voulez offrir une présentation rapide de ce qui se trouve dans une vidéo longue."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="f10cb-104">Utiliser Azure Media Video Thumbnails pour créer une synthèse d’une vidéo</span><span class="sxs-lookup"><span data-stu-id="f10cb-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="f10cb-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f10cb-105">Overview</span></span>
<span data-ttu-id="f10cb-106">Le processeur multimédia **Azure Media Video Thumbnails** vous permet de créer une synthèse d’une vidéo pour les clients souhaitant juste voir un aperçu d’une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="f10cb-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="f10cb-107">Par exemple, les clients peuvent vouloir visionner une courte « synthèse d’une vidéo » quand ils passent le pointeur sur une miniature.</span><span class="sxs-lookup"><span data-stu-id="f10cb-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="f10cb-108">En ajustant les paramètres d’ **Azure Media Video Thumbnails** via une configuration prédéfinie, vous pouvez faire appel à la puissance de la technologie de détection et de concaténation d’images pour générer de façon algorithmique un sous-clip descriptif.</span><span class="sxs-lookup"><span data-stu-id="f10cb-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="f10cb-109">Le processeur multimédia **Azure Media Video Thumbnail** est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="f10cb-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="f10cb-110">Cette rubrique donne des informations détaillées sur **Azure Media Video Thumbnail** et montre comment l’utiliser avec le SDK Media Services pour .NET.</span><span class="sxs-lookup"><span data-stu-id="f10cb-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="f10cb-111">Limites</span><span class="sxs-lookup"><span data-stu-id="f10cb-111">Limitations</span></span>

<span data-ttu-id="f10cb-112">Dans certains cas, si votre vidéo n’est pas composée de scènes différentes, la sortie sera composée d’un seul plan.</span><span class="sxs-lookup"><span data-stu-id="f10cb-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="f10cb-113">Exemple de synthèse d’une vidéo</span><span class="sxs-lookup"><span data-stu-id="f10cb-113">Video summary example</span></span>
<span data-ttu-id="f10cb-114">Voici quelques exemples de ce que le processeur Azure Media Video Thumbnails peut faire :</span><span class="sxs-lookup"><span data-stu-id="f10cb-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="f10cb-115">Vidéo d’origine</span><span class="sxs-lookup"><span data-stu-id="f10cb-115">Original video</span></span>
[<span data-ttu-id="f10cb-116">Vidéo d’origine</span><span class="sxs-lookup"><span data-stu-id="f10cb-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="f10cb-117">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="f10cb-117">Video thumbnail result</span></span>
[<span data-ttu-id="f10cb-118">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="f10cb-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="f10cb-119">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="f10cb-119">Task configuration (preset)</span></span>
<span data-ttu-id="f10cb-120">Lors de la création d’une tâche de vidéo miniature avec **Azure Media Video Thumbnails**, vous devez spécifier une configuration prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="f10cb-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="f10cb-121">L’exemple de miniature ci-dessus a été créé avec la configuration JSON de base suivante :</span><span class="sxs-lookup"><span data-stu-id="f10cb-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="f10cb-122">Actuellement, vous pouvez modifier les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f10cb-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="f10cb-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f10cb-123">Param</span></span> | <span data-ttu-id="f10cb-124">Description</span><span class="sxs-lookup"><span data-stu-id="f10cb-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f10cb-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="f10cb-125">outputAudio</span></span> |<span data-ttu-id="f10cb-126">Spécifie si la vidéo obtenue contient, ou non, des données audio.</span><span class="sxs-lookup"><span data-stu-id="f10cb-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="f10cb-127">Les valeurs autorisées sont : True ou False.</span><span class="sxs-lookup"><span data-stu-id="f10cb-127">Allowed values are: True or False.</span></span> <span data-ttu-id="f10cb-128">La valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="f10cb-128">Default is True.</span></span> |
| <span data-ttu-id="f10cb-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="f10cb-129">fadeInFadeOut</span></span> |<span data-ttu-id="f10cb-130">Spécifie si des transitions en fondu sont, ou non, utilisées entre les différentes miniatures du film.</span><span class="sxs-lookup"><span data-stu-id="f10cb-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="f10cb-131">Les valeurs autorisées sont : True ou False.</span><span class="sxs-lookup"><span data-stu-id="f10cb-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="f10cb-132">La valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="f10cb-132">Default is True.</span></span> |
| <span data-ttu-id="f10cb-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="f10cb-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="f10cb-134">Entier qui spécifie la durée que doit avoir la vidéo obtenue.</span><span class="sxs-lookup"><span data-stu-id="f10cb-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="f10cb-135">La valeur par défaut dépend de la durée de la vidéo d’origine.</span><span class="sxs-lookup"><span data-stu-id="f10cb-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="f10cb-136">Le tableau suivant décrit la durée par défaut, quand **maxMotionThumbnailInSecs** n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="f10cb-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f10cb-137">Durée de la vidéo</span><span class="sxs-lookup"><span data-stu-id="f10cb-137">Video duration</span></span> |<span data-ttu-id="f10cb-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="f10cb-138">d < 3 min</span></span> |<span data-ttu-id="f10cb-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="f10cb-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="f10cb-140">Durée de la miniature</span><span class="sxs-lookup"><span data-stu-id="f10cb-140">Thumbnail duration</span></span> |<span data-ttu-id="f10cb-141">15 s (2-3 scènes)</span><span class="sxs-lookup"><span data-stu-id="f10cb-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="f10cb-142">30 s (3-5 scènes)</span><span class="sxs-lookup"><span data-stu-id="f10cb-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="f10cb-143">Le code JSON suivant définit les paramètres disponibles.</span><span class="sxs-lookup"><span data-stu-id="f10cb-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="f10cb-144">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="f10cb-144">.NET sample code</span></span>

<span data-ttu-id="f10cb-145">Le programme suivant montre comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="f10cb-145">The following program shows how to:</span></span>

1. <span data-ttu-id="f10cb-146">Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f10cb-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="f10cb-147">Créer un travail avec une tâche de vidéo miniature basée sur un fichier de configuration qui contient la présélection JSON suivante.</span><span class="sxs-lookup"><span data-stu-id="f10cb-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="f10cb-148">Télécharger les fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="f10cb-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f10cb-149">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f10cb-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="f10cb-150">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f10cb-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="f10cb-151">Exemple</span><span class="sxs-lookup"><span data-stu-id="f10cb-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="f10cb-152">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="f10cb-152">Video thumbnail output</span></span>
[<span data-ttu-id="f10cb-153">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="f10cb-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="f10cb-154">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f10cb-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f10cb-155">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f10cb-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f10cb-156">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="f10cb-156">Related links</span></span>
[<span data-ttu-id="f10cb-157">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="f10cb-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f10cb-158">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="f10cb-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

