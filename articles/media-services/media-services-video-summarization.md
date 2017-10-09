---
title: "aaaUse Azure Media vidéo miniatures tooCreate une synthèse vidéo | Documents Microsoft"
description: "Synthèse vidéo peut vous aider à créer des résumés de vidéos long en sélectionnant automatiquement extraits intéressantes à partir de la vidéo source de hello. Cela est utile lorsque vous souhaitez tooprovide un aperçu rapide de quel tooexpect dans une vidéo longue."
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
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="52bc4-104">Utiliser Azure Media vidéo miniatures tooCreate une synthèse de la vidéo</span><span class="sxs-lookup"><span data-stu-id="52bc4-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="52bc4-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="52bc4-105">Overview</span></span>
<span data-ttu-id="52bc4-106">Hello **miniatures de vidéo Azure Media** le processeur multimédia (MP) vous permet de toocreate un résumé d’une vidéo qui est utile toocustomers souhaitant simplement toopreview un résumé d’une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="52bc4-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="52bc4-107">Par exemple, les clients souhaiteront toosee un bref « résumé vidéo » quand ils pointez sur une miniature.</span><span class="sxs-lookup"><span data-stu-id="52bc4-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="52bc4-108">En modifiant les paramètres de hello de **Azure Media vidéo miniatures** via une présélection de configuration, vous pouvez utiliser la détection de scènes puissant hello du point de gestion et de concaténation technologie tooalgorithmically générer un sous-élément descriptif.</span><span class="sxs-lookup"><span data-stu-id="52bc4-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="52bc4-109">Hello **miniature de vidéo Azure Media** Pack d’administration est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="52bc4-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="52bc4-110">Cette rubrique fournit des détails sur **miniature de vidéo Azure Media** et montre comment toouse avec Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="52bc4-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="52bc4-111">Limites</span><span class="sxs-lookup"><span data-stu-id="52bc4-111">Limitations</span></span>

<span data-ttu-id="52bc4-112">Dans certains cas, si votre vidéo n’est pas composé d’arrière-plan différente, hello sortie sera uniquement un seul plan.</span><span class="sxs-lookup"><span data-stu-id="52bc4-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="52bc4-113">Exemple de synthèse d’une vidéo</span><span class="sxs-lookup"><span data-stu-id="52bc4-113">Video summary example</span></span>
<span data-ttu-id="52bc4-114">Voici quelques exemples des processeurs multimédia Azure Media vidéo miniatures hello :</span><span class="sxs-lookup"><span data-stu-id="52bc4-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="52bc4-115">Vidéo d’origine</span><span class="sxs-lookup"><span data-stu-id="52bc4-115">Original video</span></span>
[<span data-ttu-id="52bc4-116">Vidéo d’origine</span><span class="sxs-lookup"><span data-stu-id="52bc4-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="52bc4-117">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="52bc4-117">Video thumbnail result</span></span>
[<span data-ttu-id="52bc4-118">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="52bc4-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="52bc4-119">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="52bc4-119">Task configuration (preset)</span></span>
<span data-ttu-id="52bc4-120">Lors de la création d’une tâche de vidéo miniature avec **Azure Media Video Thumbnails**, vous devez spécifier une configuration prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="52bc4-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="52bc4-121">Hello miniature exemple ci-dessus a été créé avec hello base JSON configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="52bc4-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="52bc4-122">Actuellement, vous pouvez modifier hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="52bc4-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="52bc4-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="52bc4-123">Param</span></span> | <span data-ttu-id="52bc4-124">Description</span><span class="sxs-lookup"><span data-stu-id="52bc4-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52bc4-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="52bc4-125">outputAudio</span></span> |<span data-ttu-id="52bc4-126">Spécifie ou non les vidéo résultants hello contient son audio.</span><span class="sxs-lookup"><span data-stu-id="52bc4-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="52bc4-127">Les valeurs autorisées sont : True ou False.</span><span class="sxs-lookup"><span data-stu-id="52bc4-127">Allowed values are: True or False.</span></span> <span data-ttu-id="52bc4-128">La valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="52bc4-128">Default is True.</span></span> |
| <span data-ttu-id="52bc4-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="52bc4-129">fadeInFadeOut</span></span> |<span data-ttu-id="52bc4-130">Spécifie ou non atténuation passe sont utilisés entre les miniatures de mouvement distinctes hello.</span><span class="sxs-lookup"><span data-stu-id="52bc4-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="52bc4-131">Les valeurs autorisées sont : True ou False.</span><span class="sxs-lookup"><span data-stu-id="52bc4-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="52bc4-132">La valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="52bc4-132">Default is True.</span></span> |
| <span data-ttu-id="52bc4-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="52bc4-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="52bc4-134">Entier qui spécifie la durée pendant laquelle hello ensemble résultant de la vidéo est.</span><span class="sxs-lookup"><span data-stu-id="52bc4-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="52bc4-135">La valeur par défaut dépend de la durée de la vidéo d’origine.</span><span class="sxs-lookup"><span data-stu-id="52bc4-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="52bc4-136">Hello tableau suivant décrit la durée par défaut de hello, lorsque **maxMotionThumbnailInSecs** n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="52bc4-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="52bc4-137">Durée de la vidéo</span><span class="sxs-lookup"><span data-stu-id="52bc4-137">Video duration</span></span> |<span data-ttu-id="52bc4-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="52bc4-138">d < 3 min</span></span> |<span data-ttu-id="52bc4-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="52bc4-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="52bc4-140">Durée de la miniature</span><span class="sxs-lookup"><span data-stu-id="52bc4-140">Thumbnail duration</span></span> |<span data-ttu-id="52bc4-141">15 s (2-3 scènes)</span><span class="sxs-lookup"><span data-stu-id="52bc4-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="52bc4-142">30 s (3-5 scènes)</span><span class="sxs-lookup"><span data-stu-id="52bc4-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="52bc4-143">Hello JSON suivant définit les paramètres disponibles.</span><span class="sxs-lookup"><span data-stu-id="52bc4-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="52bc4-144">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="52bc4-144">.NET sample code</span></span>

<span data-ttu-id="52bc4-145">suivant de Hello programme montre comment :</span><span class="sxs-lookup"><span data-stu-id="52bc4-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="52bc4-146">Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="52bc4-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="52bc4-147">Crée une tâche avec une tâche de miniature vidéo basée sur un fichier de configuration qui contient hello suivant présélection de json.</span><span class="sxs-lookup"><span data-stu-id="52bc4-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="52bc4-148">Télécharge les fichiers de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="52bc4-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="52bc4-149">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52bc4-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="52bc4-150">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="52bc4-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="52bc4-151">Exemple</span><span class="sxs-lookup"><span data-stu-id="52bc4-151">Example</span></span>

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
            // Read values from hello App.config file.
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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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

### <a name="video-thumbnail-output"></a><span data-ttu-id="52bc4-152">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="52bc4-152">Video thumbnail output</span></span>
[<span data-ttu-id="52bc4-153">Résultat de la vidéo miniature</span><span class="sxs-lookup"><span data-stu-id="52bc4-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="52bc4-154">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="52bc4-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="52bc4-155">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="52bc4-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="52bc4-156">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="52bc4-156">Related links</span></span>
[<span data-ttu-id="52bc4-157">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="52bc4-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="52bc4-158">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="52bc4-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

