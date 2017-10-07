---
title: "aaaEncode un élément multimédia avec Media Encoder Standard à l’aide de .NET | Documents Microsoft"
description: "Cette rubrique montre comment toouse .NET tooencode un élément multimédia à l’aide de Media Encoder standard."
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
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="cccb7-103">Encoder un élément multimédia avec Media Encoder Standard à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="cccb7-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="cccb7-104">Travaux d’encodage est une des opérations les plus courantes traitement hello dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="cccb7-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="cccb7-105">Vous créez des fichiers multimédias tooconvert travaux encodage à partir d’un tooanother de codage.</span><span class="sxs-lookup"><span data-stu-id="cccb7-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="cccb7-106">Lorsque vous codez, vous pouvez utiliser hello encodeur multimédia intégré de Media Services.</span><span class="sxs-lookup"><span data-stu-id="cccb7-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="cccb7-107">Vous pouvez également utiliser un encodeur fourni par un partenaire de Media Services ; encodeurs tiers sont disponibles via hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cccb7-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="cccb7-108">Cette rubrique montre comment toouse .NET tooencode vos éléments multimédias avec Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="cccb7-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="cccb7-109">Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cccb7-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="cccb7-110">Il est recommandé de tooalways Encoder vos fichiers sources dans un ensemble de fichiers MP4 de débit adaptatif, puis la convertir hello ensemble toohello format souhaité à l’aide de hello [empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cccb7-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="cccb7-111">Si votre ressource de sortie est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="cccb7-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="cccb7-112">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cccb7-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cccb7-113">Produit MES avec un nom qui contient un fichier de sortie hello les 32 premiers caractères de hello nom de fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cccb7-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="cccb7-114">nom de Hello est basé sur ce qui est spécifié dans le fichier de présélection hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="cccb7-115">Par exemple, "FileName": "{NomBase}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="cccb7-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="cccb7-116">{Basename} est remplacé par hello 32 premiers caractères du nom de fichier d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="cccb7-117">Formats MES</span><span class="sxs-lookup"><span data-stu-id="cccb7-117">MES Formats</span></span>
[<span data-ttu-id="cccb7-118">Formats et codecs</span><span class="sxs-lookup"><span data-stu-id="cccb7-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="cccb7-119">Présélections MES</span><span class="sxs-lookup"><span data-stu-id="cccb7-119">MES Presets</span></span>
<span data-ttu-id="cccb7-120">Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cccb7-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="cccb7-121">Métadonnées d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="cccb7-121">Input and output metadata</span></span>
<span data-ttu-id="cccb7-122">Lorsque vous encodez un élément multimédia d’entrée (ou plusieurs éléments multimédias à l’aide de MES), vous obtenez une ressource en sortie à hello achèvement réussi de qui encoder la tâche.</span><span class="sxs-lookup"><span data-stu-id="cccb7-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="cccb7-123">ressource en sortie Hello contient vidéo, audio, miniatures, manifeste, etc. selon hello valeur prédéfinie d’encodage que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="cccb7-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="cccb7-124">la ressource en sortie Hello contient également un fichier contenant des métadonnées sur l’élément multimédia d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="cccb7-125">nom du fichier XML de métadonnées hello Hello a hello suivant le format : < id_ressource > _metadata.xml (par exemple, 41114ad3-eb5e - 4c 57-8d92-5354e2b7d4a4_metadata), où < id_ressource > est la valeur AssetId de hello de ressource en entrée hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="cccb7-126">Hello schéma de ces métadonnées d’entrée XML décrit [ici](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cccb7-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="cccb7-127">la ressource en sortie Hello contient également un fichier contenant des métadonnées sur l’élément multimédia de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="cccb7-128">nom du fichier XML de métadonnées hello Hello a hello suivant le format : < nom_fichier_source > _manifest.xml (par exemple, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="cccb7-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="cccb7-129">schéma Hello de ces métadonnées de sortie XML est décrite [ici](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cccb7-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="cccb7-130">Si vous souhaitez un des fichiers de métadonnées hello deux tooexamine, vous pouvez créer un localisateur SAS et télécharger l’ordinateur local de hello fichier tooyour.</span><span class="sxs-lookup"><span data-stu-id="cccb7-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="cccb7-131">Vous trouverez un exemple montrant comment toocreate un localisateur SAS et télécharger un fichier à l’aide hello de Media Services .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="cccb7-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="cccb7-132">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="cccb7-132">Download sample</span></span>
<span data-ttu-id="cccb7-133">Vous pouvez obtenir et exécuter un exemple qui montre comment tooencode avec MES de [ici](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="cccb7-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="cccb7-134">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="cccb7-134">.NET sample code</span></span>

<span data-ttu-id="cccb7-135">Hello, exemple de code suivant utilise hello tooperform de Media Services .NET SDK tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="cccb7-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="cccb7-136">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="cccb7-136">Create an encoding job.</span></span>
* <span data-ttu-id="cccb7-137">Obtient un encodeur Media Encoder Standard toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="cccb7-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="cccb7-138">Spécifiez toouse hello [diffusion adaptative en continu](media-services-autogen-bitrate-ladder-with-mes.md) prédéfini.</span><span class="sxs-lookup"><span data-stu-id="cccb7-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="cccb7-139">Ajouter une tâche de toohello tâche encodage unique.</span><span class="sxs-lookup"><span data-stu-id="cccb7-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="cccb7-140">Spécifier une entrée de hello toobe asset encodé.</span><span class="sxs-lookup"><span data-stu-id="cccb7-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="cccb7-141">Créer un élément multimédia de sortie qui contiendra les actifs de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="cccb7-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="cccb7-142">Ajouter une événement Gestionnaire toocheck hello progression de la tâche.</span><span class="sxs-lookup"><span data-stu-id="cccb7-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="cccb7-143">Envoi de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="cccb7-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="cccb7-144">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cccb7-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="cccb7-145">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cccb7-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="cccb7-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="cccb7-146">Example</span></span> 

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="cccb7-147">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="cccb7-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cccb7-148">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="cccb7-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cccb7-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cccb7-149">Next steps</span></span>
<span data-ttu-id="cccb7-150">[La miniature toogenerate à l’aide de Media Encoder Standard avec .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[vue d’ensemble de Media Services d’encodage](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="cccb7-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

