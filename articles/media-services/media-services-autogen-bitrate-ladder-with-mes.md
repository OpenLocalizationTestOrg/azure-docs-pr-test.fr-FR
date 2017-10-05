---
title: "Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission | Microsoft Docs"
description: "Cette rubrique explique comment utiliser Media Encoder Standard (MES) pour générer automatiquement une échelle des vitesses de transmission basée sur la résolution d’entrée et la vitesse de transmission. La résolution d’entrée et la vitesse de transmission ne seront jamais dépassées. Par exemple, si l’entrée est 720p à 3 Mbits/s, la sortie restera à 720p maximum démarrera à des vitesses inférieures à 3 Mbits/s."
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="4997f-105">Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission</span><span class="sxs-lookup"><span data-stu-id="4997f-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="4997f-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4997f-106">Overview</span></span>

<span data-ttu-id="4997f-107">Cette rubrique explique comment utiliser Media Encoder Standard (MES) pour générer automatiquement une échelle des vitesses de transmission (paires vitesse-résolution) basée sur la résolution d’entrée et la vitesse de transmission.</span><span class="sxs-lookup"><span data-stu-id="4997f-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="4997f-108">La présélection générée automatiquement ne dépassera jamais la résolution d’entrée et la vitesse de transmission.</span><span class="sxs-lookup"><span data-stu-id="4997f-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="4997f-109">Par exemple, si l’entrée est 720p à 3 Mbits/s, la sortie restera à 720p maximum démarrera à des vitesses inférieures à 3 Mbits/s.</span><span class="sxs-lookup"><span data-stu-id="4997f-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="4997f-110">Encodage pour la diffusion en continu uniquement</span><span class="sxs-lookup"><span data-stu-id="4997f-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="4997f-111">Si votre objectif est d’encoder votre vidéo source uniquement pour la diffusion en continu, il vous faut alors utiliser la présélection « Diffusion adaptative en continu » lors de la création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4997f-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="4997f-112">Lorsque vous utilisez la présélection **Diffusion adaptative**, l’encodeur MES limitera intelligemment l’échelle de vitesse de transmission.</span><span class="sxs-lookup"><span data-stu-id="4997f-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="4997f-113">Mais vous ne pourrez pas contrôler les frais d’encodage car le service détermine le nombre de couches à utiliser et à quelle résolution.</span><span class="sxs-lookup"><span data-stu-id="4997f-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="4997f-114">Vous pouvez consulter des exemples de couches de sortie produites par MES suite à un encodage avec la présélection **Diffusion adaptative** à la fin de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="4997f-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="4997f-115">L’élément multimédia de sortie contiendra des fichiers MP4 où les flux audio et vidéo ne sont pas entrelacés.</span><span class="sxs-lookup"><span data-stu-id="4997f-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="4997f-116">Encodage pour le téléchargement progressif et la diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="4997f-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="4997f-117">Si votre objectif est d’encoder votre vidéo source pour la diffusion en continu ainsi que pour produire des fichiers MP4 pour le téléchargement progressif, il vous faut utiliser la présélection « Contenu adaptatif MP4 à plusieurs débits » lors de la création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4997f-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="4997f-118">Lorsque vous utilisez la présélection **Contenu adaptative MP4 à plusieurs débits**, l’encodeur MES s’applique la même logique de codage que celle indiquée ci-dessus, mais maintenant la ressource en sortie contient des fichiers MP4 avec les flux audio et vidéo entrelacés.</span><span class="sxs-lookup"><span data-stu-id="4997f-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="4997f-119">Vous pouvez utiliser un de ces fichiers MP4 (par exemple, la version la plus élevée à débit binaire) en tant que fichier de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="4997f-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="4997f-120"><a id="encoding_with_dotnet"></a>Encodage à l’aide du Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="4997f-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="4997f-121">Le code suivant utilise le Kit de développement logiciel (SDK) .NET de Media Services pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4997f-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="4997f-122">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4997f-122">Create an encoding job.</span></span>
- <span data-ttu-id="4997f-123">Obtention d’une référence à l’encodeur Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="4997f-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="4997f-124">Ajout d’une tâche d’encodage au travail et spécification de l’option pour utiliser la présélection **Diffusion adaptative**.</span><span class="sxs-lookup"><span data-stu-id="4997f-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="4997f-125">Création d’un élément multimédia de sortie qui contiendra l’élément multimédia encodé.</span><span class="sxs-lookup"><span data-stu-id="4997f-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="4997f-126">Ajout d’un gestionnaire d’événements pour vérifier la progression de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4997f-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="4997f-127">Envoyez le travail.</span><span class="sxs-lookup"><span data-stu-id="4997f-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4997f-128">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4997f-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4997f-129">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4997f-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4997f-130">Exemple</span><span class="sxs-lookup"><span data-stu-id="4997f-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="4997f-131"><a id="output"></a>Sortie</span><span class="sxs-lookup"><span data-stu-id="4997f-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="4997f-132">Cette section présente trois exemples de couches de sortie produits par MES suite à un encodage avec la présélection **Diffusion adaptative**.</span><span class="sxs-lookup"><span data-stu-id="4997f-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="4997f-133">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="4997f-133">Example 1</span></span>
<span data-ttu-id="4997f-134">Une source avec une hauteur de « 1080 » et une fréquence d’images de « 29.970 » crée 6 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="4997f-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="4997f-135">Couche</span><span class="sxs-lookup"><span data-stu-id="4997f-135">Layer</span></span>|<span data-ttu-id="4997f-136">Hauteur</span><span class="sxs-lookup"><span data-stu-id="4997f-136">Height</span></span>|<span data-ttu-id="4997f-137">Largeur</span><span class="sxs-lookup"><span data-stu-id="4997f-137">Width</span></span>|<span data-ttu-id="4997f-138">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="4997f-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4997f-139">1</span><span class="sxs-lookup"><span data-stu-id="4997f-139">1</span></span>|<span data-ttu-id="4997f-140">1080</span><span class="sxs-lookup"><span data-stu-id="4997f-140">1080</span></span>|<span data-ttu-id="4997f-141">1920</span><span class="sxs-lookup"><span data-stu-id="4997f-141">1920</span></span>|<span data-ttu-id="4997f-142">6780</span><span class="sxs-lookup"><span data-stu-id="4997f-142">6780</span></span>|
|<span data-ttu-id="4997f-143">2</span><span class="sxs-lookup"><span data-stu-id="4997f-143">2</span></span>|<span data-ttu-id="4997f-144">720</span><span class="sxs-lookup"><span data-stu-id="4997f-144">720</span></span>|<span data-ttu-id="4997f-145">1 280</span><span class="sxs-lookup"><span data-stu-id="4997f-145">1280</span></span>|<span data-ttu-id="4997f-146">3520</span><span class="sxs-lookup"><span data-stu-id="4997f-146">3520</span></span>|
|<span data-ttu-id="4997f-147">3</span><span class="sxs-lookup"><span data-stu-id="4997f-147">3</span></span>|<span data-ttu-id="4997f-148">540</span><span class="sxs-lookup"><span data-stu-id="4997f-148">540</span></span>|<span data-ttu-id="4997f-149">960</span><span class="sxs-lookup"><span data-stu-id="4997f-149">960</span></span>|<span data-ttu-id="4997f-150">2210</span><span class="sxs-lookup"><span data-stu-id="4997f-150">2210</span></span>|
|<span data-ttu-id="4997f-151">4</span><span class="sxs-lookup"><span data-stu-id="4997f-151">4</span></span>|<span data-ttu-id="4997f-152">360</span><span class="sxs-lookup"><span data-stu-id="4997f-152">360</span></span>|<span data-ttu-id="4997f-153">640</span><span class="sxs-lookup"><span data-stu-id="4997f-153">640</span></span>|<span data-ttu-id="4997f-154">1150</span><span class="sxs-lookup"><span data-stu-id="4997f-154">1150</span></span>|
|<span data-ttu-id="4997f-155">5</span><span class="sxs-lookup"><span data-stu-id="4997f-155">5</span></span>|<span data-ttu-id="4997f-156">270</span><span class="sxs-lookup"><span data-stu-id="4997f-156">270</span></span>|<span data-ttu-id="4997f-157">480</span><span class="sxs-lookup"><span data-stu-id="4997f-157">480</span></span>|<span data-ttu-id="4997f-158">720</span><span class="sxs-lookup"><span data-stu-id="4997f-158">720</span></span>|
|<span data-ttu-id="4997f-159">6</span><span class="sxs-lookup"><span data-stu-id="4997f-159">6</span></span>|<span data-ttu-id="4997f-160">180</span><span class="sxs-lookup"><span data-stu-id="4997f-160">180</span></span>|<span data-ttu-id="4997f-161">320</span><span class="sxs-lookup"><span data-stu-id="4997f-161">320</span></span>|<span data-ttu-id="4997f-162">380</span><span class="sxs-lookup"><span data-stu-id="4997f-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="4997f-163">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="4997f-163">Example 2</span></span>
<span data-ttu-id="4997f-164">Une source avec une hauteur de « 720 » et une fréquence d’images de « 23.970 » crée 5 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="4997f-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="4997f-165">Couche</span><span class="sxs-lookup"><span data-stu-id="4997f-165">Layer</span></span>|<span data-ttu-id="4997f-166">Hauteur</span><span class="sxs-lookup"><span data-stu-id="4997f-166">Height</span></span>|<span data-ttu-id="4997f-167">Largeur</span><span class="sxs-lookup"><span data-stu-id="4997f-167">Width</span></span>|<span data-ttu-id="4997f-168">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="4997f-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4997f-169">1</span><span class="sxs-lookup"><span data-stu-id="4997f-169">1</span></span>|<span data-ttu-id="4997f-170">720</span><span class="sxs-lookup"><span data-stu-id="4997f-170">720</span></span>|<span data-ttu-id="4997f-171">1 280</span><span class="sxs-lookup"><span data-stu-id="4997f-171">1280</span></span>|<span data-ttu-id="4997f-172">2940</span><span class="sxs-lookup"><span data-stu-id="4997f-172">2940</span></span>|
|<span data-ttu-id="4997f-173">2</span><span class="sxs-lookup"><span data-stu-id="4997f-173">2</span></span>|<span data-ttu-id="4997f-174">540</span><span class="sxs-lookup"><span data-stu-id="4997f-174">540</span></span>|<span data-ttu-id="4997f-175">960</span><span class="sxs-lookup"><span data-stu-id="4997f-175">960</span></span>|<span data-ttu-id="4997f-176">1850</span><span class="sxs-lookup"><span data-stu-id="4997f-176">1850</span></span>|
|<span data-ttu-id="4997f-177">3</span><span class="sxs-lookup"><span data-stu-id="4997f-177">3</span></span>|<span data-ttu-id="4997f-178">360</span><span class="sxs-lookup"><span data-stu-id="4997f-178">360</span></span>|<span data-ttu-id="4997f-179">640</span><span class="sxs-lookup"><span data-stu-id="4997f-179">640</span></span>|<span data-ttu-id="4997f-180">960</span><span class="sxs-lookup"><span data-stu-id="4997f-180">960</span></span>|
|<span data-ttu-id="4997f-181">4</span><span class="sxs-lookup"><span data-stu-id="4997f-181">4</span></span>|<span data-ttu-id="4997f-182">270</span><span class="sxs-lookup"><span data-stu-id="4997f-182">270</span></span>|<span data-ttu-id="4997f-183">480</span><span class="sxs-lookup"><span data-stu-id="4997f-183">480</span></span>|<span data-ttu-id="4997f-184">600</span><span class="sxs-lookup"><span data-stu-id="4997f-184">600</span></span>|
|<span data-ttu-id="4997f-185">5</span><span class="sxs-lookup"><span data-stu-id="4997f-185">5</span></span>|<span data-ttu-id="4997f-186">180</span><span class="sxs-lookup"><span data-stu-id="4997f-186">180</span></span>|<span data-ttu-id="4997f-187">320</span><span class="sxs-lookup"><span data-stu-id="4997f-187">320</span></span>|<span data-ttu-id="4997f-188">320</span><span class="sxs-lookup"><span data-stu-id="4997f-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="4997f-189">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="4997f-189">Example 3</span></span>
<span data-ttu-id="4997f-190">Une source avec une hauteur de « 360 » et une fréquence d’images de « 29.970 » crée 3 couches vidéo :</span><span class="sxs-lookup"><span data-stu-id="4997f-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="4997f-191">Couche</span><span class="sxs-lookup"><span data-stu-id="4997f-191">Layer</span></span>|<span data-ttu-id="4997f-192">Hauteur</span><span class="sxs-lookup"><span data-stu-id="4997f-192">Height</span></span>|<span data-ttu-id="4997f-193">Largeur</span><span class="sxs-lookup"><span data-stu-id="4997f-193">Width</span></span>|<span data-ttu-id="4997f-194">Vitesse de transmission (Kbits/s)</span><span class="sxs-lookup"><span data-stu-id="4997f-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4997f-195">1</span><span class="sxs-lookup"><span data-stu-id="4997f-195">1</span></span>|<span data-ttu-id="4997f-196">360</span><span class="sxs-lookup"><span data-stu-id="4997f-196">360</span></span>|<span data-ttu-id="4997f-197">640</span><span class="sxs-lookup"><span data-stu-id="4997f-197">640</span></span>|<span data-ttu-id="4997f-198">700</span><span class="sxs-lookup"><span data-stu-id="4997f-198">700</span></span>|
|<span data-ttu-id="4997f-199">2</span><span class="sxs-lookup"><span data-stu-id="4997f-199">2</span></span>|<span data-ttu-id="4997f-200">270</span><span class="sxs-lookup"><span data-stu-id="4997f-200">270</span></span>|<span data-ttu-id="4997f-201">480</span><span class="sxs-lookup"><span data-stu-id="4997f-201">480</span></span>|<span data-ttu-id="4997f-202">440</span><span class="sxs-lookup"><span data-stu-id="4997f-202">440</span></span>|
|<span data-ttu-id="4997f-203">3</span><span class="sxs-lookup"><span data-stu-id="4997f-203">3</span></span>|<span data-ttu-id="4997f-204">180</span><span class="sxs-lookup"><span data-stu-id="4997f-204">180</span></span>|<span data-ttu-id="4997f-205">320</span><span class="sxs-lookup"><span data-stu-id="4997f-205">320</span></span>|<span data-ttu-id="4997f-206">230</span><span class="sxs-lookup"><span data-stu-id="4997f-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="4997f-207">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="4997f-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4997f-208">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4997f-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4997f-209">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4997f-209">See Also</span></span>
[<span data-ttu-id="4997f-210">Vue d’ensemble de l’encodage de Media Services</span><span class="sxs-lookup"><span data-stu-id="4997f-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

