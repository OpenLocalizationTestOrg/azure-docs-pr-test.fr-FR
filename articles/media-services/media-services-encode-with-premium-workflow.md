---
title: "aaaAdvanced encodage avec Workflow d’encodeur multimédia Premium | Documents Microsoft"
description: "Découvrez comment tooencode avec Workflow d’encodeur multimédia Premium. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="a4cc0-104">Encodage avancé avec Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="a4cc0-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="a4cc0-105">Le processeur multimédia Media Encoder Premium Workflow présenté dans cette rubrique n’est pas disponible en Chine.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="a4cc0-106">Pour les questions relatives à Encoder Premium, envoyez un e-mail à mepd sur Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="a4cc0-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a4cc0-107">Overview</span></span>
<span data-ttu-id="a4cc0-108">Microsoft Azure Media Services introduit hello **Workflow d’encodeur multimédia Premium** processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="a4cc0-109">Ce processeur offre des fonctionnalités d’encodage avancées pour vos flux de travail à la demande premium.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="a4cc0-110">Hello rubriques suivantes décrivent les détails associés trop**Workflow d’encodeur multimédia Premium**:</span><span class="sxs-lookup"><span data-stu-id="a4cc0-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="a4cc0-111">[Formats pris en charge par hello Workflow d’encodeur multimédia Premium](media-services-premium-workflow-encoder-formats.md) – traite des formats de fichier hello et codecs pris en charge par **Workflow d’encodeur multimédia Premium**.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="a4cc0-112">[Vue d’ensemble et la comparaison d’Azure sur les encodeurs de média à la demande](media-services-encode-asset.md) compare hello capacités de codage de **Workflow d’encodeur multimédia Premium** et **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="a4cc0-113">Cette rubrique montre comment tooencode avec **Workflow d’encodeur multimédia Premium** à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="a4cc0-114">Encodage des tâches pour hello **Workflow d’encodeur multimédia Premium** nécessitent un fichier de configuration distinct, appelé fichier de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="a4cc0-115">Ces fichiers ont une extension de lettres et sont créés à l’aide de hello [le Concepteur de flux de travail](media-services-workflow-designer.md) outil.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="a4cc0-116">Vous pouvez également obtenir par défaut de hello les fichiers de flux de travail [ici](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="a4cc0-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="a4cc0-117">dossier de Hello contient également la description hello de ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="a4cc0-118">fichiers de flux de travail de Hello doivent toobe téléchargé tooyour Media Services compte comme un élément multimédia, et cette ressource doit être passée toohello tâche de codage.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a4cc0-119">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a4cc0-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a4cc0-120">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a4cc0-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="a4cc0-121">Exemple d’encodage</span><span class="sxs-lookup"><span data-stu-id="a4cc0-121">Encoding example</span></span>

<span data-ttu-id="a4cc0-122">Hello exemple suivant montre comment tooencode avec **Workflow d’encodeur multimédia Premium**.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="a4cc0-123">Hello suivant les étapes est effectuée :</span><span class="sxs-lookup"><span data-stu-id="a4cc0-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="a4cc0-124">Créez une ressource et téléchargez un fichier de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="a4cc0-125">Créez une ressource et téléchargez un fichier multimédia source.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="a4cc0-126">Obtenir un processeur multimédia de « Workflow Premium d’encodeur multimédia » hello.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="a4cc0-127">Créez un travail et une tâche.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-127">Create a job and a task.</span></span>

    <span data-ttu-id="a4cc0-128">Dans la plupart des cas, la chaîne de configuration hello pour la tâche hello est vide (comme dans hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="a4cc0-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="a4cc0-129">Il existe certains scénarios avancés (nécessitant les propriétés d’exécution tootooset dynamiquement) auquel cas vous souhaitez fournir une tâche de codage toohello de chaîne XML.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="a4cc0-130">La création d'une superposition, l'assemblage parallèle ou séquentiel multimédia, le sous-titrage sont des exemples de ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="a4cc0-131">Ajoutez deux tâches de toohello d’éléments multimédias en entrée.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="a4cc0-132">1er – actif du flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="a4cc0-133">2 – élément multimédia vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a4cc0-134">tâche toohello avant multimédia hello doit être ajouté à actif du flux de travail Hello.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="a4cc0-135">chaîne de configuration Hello pour cette tâche doit être vide.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="a4cc0-136">Envoi de la tâche de codage hello.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-136">Submit hello encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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
                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

<span data-ttu-id="a4cc0-137">Pour les questions relatives à Encoder Premium, envoyez un e-mail à mepd sur Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="a4cc0-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4cc0-138">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a4cc0-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4cc0-139">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a4cc0-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
