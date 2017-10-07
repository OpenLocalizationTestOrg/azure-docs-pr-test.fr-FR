---
title: "tooauto d’Azure Media Encoder Standard aaaUse-générer une échelle de la vitesse de transmission | Documents Microsoft"
description: "Cette rubrique montre comment toouse Media Encoder Standard (MES) tooauto-générer une échelle de la vitesse de transmission en fonction de la résolution d’entrée hello et la vitesse de transmission. vitesse de transmission et la résolution d’entrée hello ne seront jamais dépassées. Par exemple, si l’entrée de hello est 720p à 3 Mbits/s, sortie sera restent 720p au mieux et commence à un taux inférieurs à 3 Mbits/s."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="a6ce1-105">Utiliser Azure Media Encoder Standard tooauto-générer une échelle de la vitesse de transmission</span><span class="sxs-lookup"><span data-stu-id="a6ce1-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="a6ce1-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a6ce1-106">Overview</span></span>

<span data-ttu-id="a6ce1-107">Cette rubrique montre comment toouse Media Encoder Standard (MES) tooauto-générer une échelle de la vitesse de transmission (paires de résolution de la vitesse de transmission) en fonction de la résolution d’entrée hello et la vitesse de transmission.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="a6ce1-108">Hello générée automatiquement la présélection ne dépasse jamais vitesse de transmission et de résolution de hello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="a6ce1-109">Par exemple, si l’entrée de hello est 720p à 3 Mbits/s, sortie sera restent 720p au mieux et commence à un taux inférieurs à 3 Mbits/s.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="a6ce1-110">Encodage pour la diffusion en continu uniquement</span><span class="sxs-lookup"><span data-stu-id="a6ce1-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="a6ce1-111">Si votre objectif est de tooencode votre source vidéo uniquement pour la diffusion en continu, puis vous faut-il utiliser hello « Diffusion adaptative en continu » prédéfini lors de la création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="a6ce1-112">Lorsque vous utilisez hello **diffusion adaptative en continu** prédéfinis, encodeur MES hello sera intelligemment imposer une échelle de la vitesse de transmission.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="a6ce1-113">Toutefois, vous ne serez pas hello toocontrol en mesure de codage des coûts, car le service de hello détermine combien couches toouse et à quelle résolution.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="a6ce1-114">Vous pouvez voir des exemples de couches de sortie produits par MES suite à l’encodage avec hello **diffusion adaptative en continu** prédéfinie à la fin de hello de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="a6ce1-115">Hello de sortie actif contiennent des fichiers MP4 où audio et vidéo ne sont pas entrelacées.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="a6ce1-116">Encodage pour le téléchargement progressif et la diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="a6ce1-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="a6ce1-117">Si votre objectif est de tooencode votre vidéo source pour la diffusion en continu, ainsi que des fichiers MP4 à tooproduce pour le téléchargement progressif, puis vous faut-il utiliser hello « Contenu adaptative MP4 à plusieurs débits » prédéfini lors de la création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="a6ce1-118">Lorsque vous utilisez hello **contenu adaptative MP4 à plusieurs débits** prédéfinis, encodeur MES hello applique hello même encodage logique comme indiqué ci-dessus, mais la ressource en sortie hello contiendra alors MP4 de fichiers audio et vidéo sont entrelacées.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="a6ce1-119">Vous pouvez utiliser un de ces fichiers MP4 (par exemple, hello version la plus récente à débit binaire) en tant qu’un fichier de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="a6ce1-120"><a id="encoding_with_dotnet"></a>Encodage à l’aide du Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="a6ce1-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="a6ce1-121">Hello, exemple de code suivant utilise hello tooperform de Media Services .NET SDK tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6ce1-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="a6ce1-122">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-122">Create an encoding job.</span></span>
- <span data-ttu-id="a6ce1-123">Obtient un encodeur Media Encoder Standard toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="a6ce1-124">Ajouter une tâche de toohello tâche codage et spécifiez toouse hello **diffusion adaptative en continu** prédéfini.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="a6ce1-125">Créer un élément multimédia de sortie qui contiendra les actifs de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="a6ce1-126">Ajouter une événement Gestionnaire toocheck hello progression de la tâche.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="a6ce1-127">Envoi de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a6ce1-128">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6ce1-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a6ce1-129">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a6ce1-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a6ce1-130">Exemple</span><span class="sxs-lookup"><span data-stu-id="a6ce1-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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

## <span data-ttu-id="a6ce1-131"><a id="output"></a>Sortie</span><span class="sxs-lookup"><span data-stu-id="a6ce1-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="a6ce1-132">Cette section présente trois exemples de couches de sortie produits par MES suite à l’encodage avec hello **diffusion adaptative en continu** prédéfini.</span><span class="sxs-lookup"><span data-stu-id="a6ce1-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="a6ce1-133">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="a6ce1-133">Example 1</span></span>
<span data-ttu-id="a6ce1-134">Une source avec une hauteur de « 1080 » et une fréquence d’images de « 29.970 » crée 6 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="a6ce1-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="a6ce1-135">Couche</span><span class="sxs-lookup"><span data-stu-id="a6ce1-135">Layer</span></span>|<span data-ttu-id="a6ce1-136">Hauteur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-136">Height</span></span>|<span data-ttu-id="a6ce1-137">Largeur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-137">Width</span></span>|<span data-ttu-id="a6ce1-138">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="a6ce1-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="a6ce1-139">1</span><span class="sxs-lookup"><span data-stu-id="a6ce1-139">1</span></span>|<span data-ttu-id="a6ce1-140">1080</span><span class="sxs-lookup"><span data-stu-id="a6ce1-140">1080</span></span>|<span data-ttu-id="a6ce1-141">1920</span><span class="sxs-lookup"><span data-stu-id="a6ce1-141">1920</span></span>|<span data-ttu-id="a6ce1-142">6780</span><span class="sxs-lookup"><span data-stu-id="a6ce1-142">6780</span></span>|
|<span data-ttu-id="a6ce1-143">2</span><span class="sxs-lookup"><span data-stu-id="a6ce1-143">2</span></span>|<span data-ttu-id="a6ce1-144">720</span><span class="sxs-lookup"><span data-stu-id="a6ce1-144">720</span></span>|<span data-ttu-id="a6ce1-145">1 280</span><span class="sxs-lookup"><span data-stu-id="a6ce1-145">1280</span></span>|<span data-ttu-id="a6ce1-146">3520</span><span class="sxs-lookup"><span data-stu-id="a6ce1-146">3520</span></span>|
|<span data-ttu-id="a6ce1-147">3</span><span class="sxs-lookup"><span data-stu-id="a6ce1-147">3</span></span>|<span data-ttu-id="a6ce1-148">540</span><span class="sxs-lookup"><span data-stu-id="a6ce1-148">540</span></span>|<span data-ttu-id="a6ce1-149">960</span><span class="sxs-lookup"><span data-stu-id="a6ce1-149">960</span></span>|<span data-ttu-id="a6ce1-150">2210</span><span class="sxs-lookup"><span data-stu-id="a6ce1-150">2210</span></span>|
|<span data-ttu-id="a6ce1-151">4</span><span class="sxs-lookup"><span data-stu-id="a6ce1-151">4</span></span>|<span data-ttu-id="a6ce1-152">360</span><span class="sxs-lookup"><span data-stu-id="a6ce1-152">360</span></span>|<span data-ttu-id="a6ce1-153">640</span><span class="sxs-lookup"><span data-stu-id="a6ce1-153">640</span></span>|<span data-ttu-id="a6ce1-154">1150</span><span class="sxs-lookup"><span data-stu-id="a6ce1-154">1150</span></span>|
|<span data-ttu-id="a6ce1-155">5</span><span class="sxs-lookup"><span data-stu-id="a6ce1-155">5</span></span>|<span data-ttu-id="a6ce1-156">270</span><span class="sxs-lookup"><span data-stu-id="a6ce1-156">270</span></span>|<span data-ttu-id="a6ce1-157">480</span><span class="sxs-lookup"><span data-stu-id="a6ce1-157">480</span></span>|<span data-ttu-id="a6ce1-158">720</span><span class="sxs-lookup"><span data-stu-id="a6ce1-158">720</span></span>|
|<span data-ttu-id="a6ce1-159">6</span><span class="sxs-lookup"><span data-stu-id="a6ce1-159">6</span></span>|<span data-ttu-id="a6ce1-160">180</span><span class="sxs-lookup"><span data-stu-id="a6ce1-160">180</span></span>|<span data-ttu-id="a6ce1-161">320</span><span class="sxs-lookup"><span data-stu-id="a6ce1-161">320</span></span>|<span data-ttu-id="a6ce1-162">380</span><span class="sxs-lookup"><span data-stu-id="a6ce1-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="a6ce1-163">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="a6ce1-163">Example 2</span></span>
<span data-ttu-id="a6ce1-164">Une source avec une hauteur de « 720 » et une fréquence d’images de « 23.970 » crée 5 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="a6ce1-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="a6ce1-165">Couche</span><span class="sxs-lookup"><span data-stu-id="a6ce1-165">Layer</span></span>|<span data-ttu-id="a6ce1-166">Hauteur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-166">Height</span></span>|<span data-ttu-id="a6ce1-167">Largeur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-167">Width</span></span>|<span data-ttu-id="a6ce1-168">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="a6ce1-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="a6ce1-169">1</span><span class="sxs-lookup"><span data-stu-id="a6ce1-169">1</span></span>|<span data-ttu-id="a6ce1-170">720</span><span class="sxs-lookup"><span data-stu-id="a6ce1-170">720</span></span>|<span data-ttu-id="a6ce1-171">1 280</span><span class="sxs-lookup"><span data-stu-id="a6ce1-171">1280</span></span>|<span data-ttu-id="a6ce1-172">2940</span><span class="sxs-lookup"><span data-stu-id="a6ce1-172">2940</span></span>|
|<span data-ttu-id="a6ce1-173">2</span><span class="sxs-lookup"><span data-stu-id="a6ce1-173">2</span></span>|<span data-ttu-id="a6ce1-174">540</span><span class="sxs-lookup"><span data-stu-id="a6ce1-174">540</span></span>|<span data-ttu-id="a6ce1-175">960</span><span class="sxs-lookup"><span data-stu-id="a6ce1-175">960</span></span>|<span data-ttu-id="a6ce1-176">1850</span><span class="sxs-lookup"><span data-stu-id="a6ce1-176">1850</span></span>|
|<span data-ttu-id="a6ce1-177">3</span><span class="sxs-lookup"><span data-stu-id="a6ce1-177">3</span></span>|<span data-ttu-id="a6ce1-178">360</span><span class="sxs-lookup"><span data-stu-id="a6ce1-178">360</span></span>|<span data-ttu-id="a6ce1-179">640</span><span class="sxs-lookup"><span data-stu-id="a6ce1-179">640</span></span>|<span data-ttu-id="a6ce1-180">960</span><span class="sxs-lookup"><span data-stu-id="a6ce1-180">960</span></span>|
|<span data-ttu-id="a6ce1-181">4</span><span class="sxs-lookup"><span data-stu-id="a6ce1-181">4</span></span>|<span data-ttu-id="a6ce1-182">270</span><span class="sxs-lookup"><span data-stu-id="a6ce1-182">270</span></span>|<span data-ttu-id="a6ce1-183">480</span><span class="sxs-lookup"><span data-stu-id="a6ce1-183">480</span></span>|<span data-ttu-id="a6ce1-184">600</span><span class="sxs-lookup"><span data-stu-id="a6ce1-184">600</span></span>|
|<span data-ttu-id="a6ce1-185">5</span><span class="sxs-lookup"><span data-stu-id="a6ce1-185">5</span></span>|<span data-ttu-id="a6ce1-186">180</span><span class="sxs-lookup"><span data-stu-id="a6ce1-186">180</span></span>|<span data-ttu-id="a6ce1-187">320</span><span class="sxs-lookup"><span data-stu-id="a6ce1-187">320</span></span>|<span data-ttu-id="a6ce1-188">320</span><span class="sxs-lookup"><span data-stu-id="a6ce1-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="a6ce1-189">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="a6ce1-189">Example 3</span></span>
<span data-ttu-id="a6ce1-190">Une source avec une hauteur de « 360 » et une fréquence d’images de « 29.970 » crée 3 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="a6ce1-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="a6ce1-191">Couche</span><span class="sxs-lookup"><span data-stu-id="a6ce1-191">Layer</span></span>|<span data-ttu-id="a6ce1-192">Hauteur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-192">Height</span></span>|<span data-ttu-id="a6ce1-193">Largeur</span><span class="sxs-lookup"><span data-stu-id="a6ce1-193">Width</span></span>|<span data-ttu-id="a6ce1-194">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="a6ce1-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="a6ce1-195">1</span><span class="sxs-lookup"><span data-stu-id="a6ce1-195">1</span></span>|<span data-ttu-id="a6ce1-196">360</span><span class="sxs-lookup"><span data-stu-id="a6ce1-196">360</span></span>|<span data-ttu-id="a6ce1-197">640</span><span class="sxs-lookup"><span data-stu-id="a6ce1-197">640</span></span>|<span data-ttu-id="a6ce1-198">700</span><span class="sxs-lookup"><span data-stu-id="a6ce1-198">700</span></span>|
|<span data-ttu-id="a6ce1-199">2</span><span class="sxs-lookup"><span data-stu-id="a6ce1-199">2</span></span>|<span data-ttu-id="a6ce1-200">270</span><span class="sxs-lookup"><span data-stu-id="a6ce1-200">270</span></span>|<span data-ttu-id="a6ce1-201">480</span><span class="sxs-lookup"><span data-stu-id="a6ce1-201">480</span></span>|<span data-ttu-id="a6ce1-202">440</span><span class="sxs-lookup"><span data-stu-id="a6ce1-202">440</span></span>|
|<span data-ttu-id="a6ce1-203">3</span><span class="sxs-lookup"><span data-stu-id="a6ce1-203">3</span></span>|<span data-ttu-id="a6ce1-204">180</span><span class="sxs-lookup"><span data-stu-id="a6ce1-204">180</span></span>|<span data-ttu-id="a6ce1-205">320</span><span class="sxs-lookup"><span data-stu-id="a6ce1-205">320</span></span>|<span data-ttu-id="a6ce1-206">230</span><span class="sxs-lookup"><span data-stu-id="a6ce1-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="a6ce1-207">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a6ce1-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a6ce1-208">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a6ce1-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a6ce1-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a6ce1-209">See Also</span></span>
[<span data-ttu-id="a6ce1-210">Vue d’ensemble de l’encodage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a6ce1-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

