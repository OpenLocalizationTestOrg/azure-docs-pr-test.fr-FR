---
title: "Encoder un élément multimédia avec Media Encoder Standard à l’aide de .NET | Microsoft Docs"
description: "Cette rubrique montre comment utiliser .NET pour encoder vos éléments multimédias avec Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="de824-103">Encoder un élément multimédia avec Media Encoder Standard à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="de824-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="de824-104">Les tâches d’encodage sont une des opérations de traitement les plus courantes dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="de824-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="de824-105">Vous créez des tâches d’encodage pour convertir des fichiers multimédias d’un encodage à un autre.</span><span class="sxs-lookup"><span data-stu-id="de824-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="de824-106">Lorsque vous les encodez, vous pouvez utiliser l’encodeur multimédia intégré de Media Services.</span><span class="sxs-lookup"><span data-stu-id="de824-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="de824-107">Vous pouvez aussi utiliser un encodeur fourni par un partenaire Media Services. Ces encodeurs tiers sont disponibles sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="de824-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="de824-108">Cette rubrique montre comment utiliser .NET pour encoder vos éléments multimédias avec Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="de824-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="de824-109">Media Encoder Standard se configure à l’aide d’une des présélections d’encodeur décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="de824-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="de824-110">Nous vous recommandons de toujours encoder vos fichiers sources sous forme de jeu de fichiers MP4 à débit adaptatif, puis de convertir ce jeu au format souhaité au moyen de l’ [empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de824-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="de824-111">Si votre ressource de sortie est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="de824-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="de824-112">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="de824-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de824-113">MES génère un fichier de sortie avec un nom qui contient les 32 premiers caractères du nom du fichier d'entrée.</span><span class="sxs-lookup"><span data-stu-id="de824-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="de824-114">Le nom est basé sur ce qui est spécifié dans le fichier prédéfini.</span><span class="sxs-lookup"><span data-stu-id="de824-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="de824-115">Par exemple, "FileName": "{NomBase}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="de824-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="de824-116">{NomBase} est remplacé par les 32 premiers caractères du nom du fichier d'entrée.</span><span class="sxs-lookup"><span data-stu-id="de824-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="de824-117">Formats MES</span><span class="sxs-lookup"><span data-stu-id="de824-117">MES Formats</span></span>
[<span data-ttu-id="de824-118">Formats et codecs</span><span class="sxs-lookup"><span data-stu-id="de824-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="de824-119">Présélections MES</span><span class="sxs-lookup"><span data-stu-id="de824-119">MES Presets</span></span>
<span data-ttu-id="de824-120">Media Encoder Standard se configure à l’aide d’une des présélections d’encodeur décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="de824-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="de824-121">Métadonnées d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="de824-121">Input and output metadata</span></span>
<span data-ttu-id="de824-122">Quand vous encodez un ou plusieurs éléments multimédias d’entrée à l’aide de MES, vous obtenez un élément multimédia de sortie une fois cette tâche d’encodage terminée.</span><span class="sxs-lookup"><span data-stu-id="de824-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="de824-123">L’élément multimédia de sortie contient la vidéo, l’audio, les miniatures, le manifeste, et ainsi de suite, en fonction des paramètres d’encodage prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="de824-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="de824-124">Il contient également un fichier avec des métadonnées relatives à l’élément multimédia d’entrée.</span><span class="sxs-lookup"><span data-stu-id="de824-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="de824-125">Le nom du fichier XML de métadonnées a le format suivant : <asset_id>_metadata.xml (par exemple, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), où <asset_id> est la valeur AssetId de l’élément multimédia d’entrée.</span><span class="sxs-lookup"><span data-stu-id="de824-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="de824-126">Le schéma de ce XML de métadonnées d’entrée est décrit [ici](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="de824-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="de824-127">L’élément multimédia de sortie contient également un fichier avec des métadonnées relatives à l’élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="de824-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="de824-128">Le nom du fichier XML de métadonnées a le format suivant : <nom_fichier_source>_manifest.xml (par exemple, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="de824-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="de824-129">Le schéma de ce XML de métadonnées de sortie est décrit [ici](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="de824-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="de824-130">Si vous souhaitez examiner l’un des deux fichiers de métadonnées, vous pouvez créer un localisateur SAS et télécharger le fichier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="de824-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="de824-131">Vous trouverez un exemple illustrant comment créer un localisateur SAS et télécharger un fichier dans la rubrique Utilisation des extensions du SDK Media Services .NET.</span><span class="sxs-lookup"><span data-stu-id="de824-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="de824-132">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="de824-132">Download sample</span></span>
<span data-ttu-id="de824-133">Vous pouvez obtenir et exécuter un exemple qui montre comment encoder avec MES [ici](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="de824-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="de824-134">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="de824-134">.NET sample code</span></span>

<span data-ttu-id="de824-135">Le code suivant utilise le Kit de développement logiciel (SDK) .NET de Media Services pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="de824-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="de824-136">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="de824-136">Create an encoding job.</span></span>
* <span data-ttu-id="de824-137">Obtention d’une référence à l’encodeur Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="de824-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="de824-138">Spécifiez l’utilisation de la présélection [Diffusion en continu adaptative](media-services-autogen-bitrate-ladder-with-mes.md).</span><span class="sxs-lookup"><span data-stu-id="de824-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="de824-139">Ajout d’une tâche d’encodage unique.</span><span class="sxs-lookup"><span data-stu-id="de824-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="de824-140">Spécification de l’élément multimédia d’entrée à encoder.</span><span class="sxs-lookup"><span data-stu-id="de824-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="de824-141">Création d’un élément multimédia de sortie qui contiendra l’élément multimédia encodé.</span><span class="sxs-lookup"><span data-stu-id="de824-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="de824-142">Ajout d’un gestionnaire d’événements pour vérifier la progression de la tâche.</span><span class="sxs-lookup"><span data-stu-id="de824-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="de824-143">Envoyez le travail.</span><span class="sxs-lookup"><span data-stu-id="de824-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="de824-144">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de824-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="de824-145">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="de824-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="de824-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="de824-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="de824-147">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="de824-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="de824-148">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="de824-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="de824-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de824-149">Next steps</span></span>
<span data-ttu-id="de824-150">[Comment générer une miniature à l’aide de Media Encoder Standard avec .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Vue d’ensemble du codage Media Services](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="de824-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

