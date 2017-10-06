---
title: "miniatures de toogenerate aaaHow à l’aide de Media Encoder Standard avec .NET"
description: "Cette rubrique montre comment toouse .NET tooencode un élément multimédia et générer des miniatures à hello simultanément à l’aide de Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="4fe04-103">Comment les miniatures toogenerate à l’aide de Media Encoder Standard avec .NET</span><span class="sxs-lookup"><span data-stu-id="4fe04-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="4fe04-104">Vous pouvez utiliser une ou plusieurs miniatures toogenerate Media Encoder Standard à partir de votre entrée vidéo dans [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), ou [BMP](https://en.wikipedia.org/wiki/BMP_file_format) formats de fichier d’image.</span><span class="sxs-lookup"><span data-stu-id="4fe04-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="4fe04-105">Vous pouvez soumettre des tâches produisant uniquement des images ou vous pouvez combiner la génération de miniatures avec l’encodage.</span><span class="sxs-lookup"><span data-stu-id="4fe04-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="4fe04-106">Cette rubrique fournit quelques exemples de présélections de miniatures XML et JSON pour de tels scénarios.</span><span class="sxs-lookup"><span data-stu-id="4fe04-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="4fe04-107">En fin de hello de rubrique de hello, vous trouverez une [exemple de code](#code_sample) qui montre comment toouse hello Media Services .NET SDK tooaccomplish hello tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4fe04-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="4fe04-108">Pour plus d’informations sur les éléments de hello sont utilisées dans les présélections d’exemple, vous devez passer en revue [schéma Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4fe04-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="4fe04-109">Assurez-vous que tooreview hello [considérations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span><span class="sxs-lookup"><span data-stu-id="4fe04-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="4fe04-110">Exemple – fichier PNG unique</span><span class="sxs-lookup"><span data-stu-id="4fe04-110">Example – single PNG file</span></span>

<span data-ttu-id="4fe04-111">Hello suivant JSON et XML prédéfini peut être utilisé tooproduce une seule sortie PNG fichier hors hello quelques secondes de la vidéo d’entrée hello, où les encodeur hello effectue une tentative de meilleur effort à la recherche d’un cadre « intéressant ».</span><span class="sxs-lookup"><span data-stu-id="4fe04-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="4fe04-112">Notez que les dimensions de l’image hello sortie ont été définies too100 %, ce qui signifie que ces correspondra à dimensions hello de vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="4fe04-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="4fe04-113">Notez également comment le paramètre de « Format » de hello dans « Sorties » est requis utiliser hello toomatch « PngLayers » dans la section « Codecs » de hello.</span><span class="sxs-lookup"><span data-stu-id="4fe04-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="4fe04-114">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="4fe04-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="4fe04-115">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="4fe04-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="4fe04-116">Exemple – une série d’images JPEG</span><span class="sxs-lookup"><span data-stu-id="4fe04-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="4fe04-117">Hello suivant JSON et XML prédéfini peut être utilisé tooproduce un ensemble de 10 images au niveau des horodateurs de 5 %, 15 %,..., 95 % de la chronologie d’entrée hello, où la taille d’image hello est toobe spécifié un quart qui Hello d’entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="4fe04-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="4fe04-118">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="4fe04-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="4fe04-119">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="4fe04-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="4fe04-120">Exemple – une image à un horodatage spécifique</span><span class="sxs-lookup"><span data-stu-id="4fe04-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="4fe04-121">Hello suivant présélection JSON et XML peut être utilisé tooproduce une image JPEG à hello marque des 30 secondes de la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="4fe04-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="4fe04-122">Cette présélection attend toobe d’entrée de hello plus de 30 secondes (autre hello travail échoue).</span><span class="sxs-lookup"><span data-stu-id="4fe04-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="4fe04-123">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="4fe04-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="4fe04-124">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="4fe04-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="4fe04-125"><a id="code_sample"></a>Exemple – encoder la vidéo et générer la miniature</span><span class="sxs-lookup"><span data-stu-id="4fe04-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="4fe04-126">Hello, exemple de code suivant utilise hello tooperform de Media Services .NET SDK tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fe04-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="4fe04-127">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4fe04-127">Create an encoding job.</span></span>
* <span data-ttu-id="4fe04-128">Obtient un encodeur Media Encoder Standard toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="4fe04-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="4fe04-129">Hello de charge prédéfini [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) qui contiennent hello encodage prédéfinis ainsi que les informations nécessaires toogenerate miniatures.</span><span class="sxs-lookup"><span data-stu-id="4fe04-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="4fe04-130">Vous pouvez l’enregistrer [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) ou [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) dans un hello et utiliser le fichier code tooload hello suivant.</span><span class="sxs-lookup"><span data-stu-id="4fe04-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="4fe04-131">Ajouter une tâche de toohello tâche encodage unique.</span><span class="sxs-lookup"><span data-stu-id="4fe04-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="4fe04-132">Spécifier une entrée de hello toobe asset encodé.</span><span class="sxs-lookup"><span data-stu-id="4fe04-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="4fe04-133">Créer un élément multimédia de sortie qui contiendra les actifs de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="4fe04-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="4fe04-134">Ajouter une événement Gestionnaire toocheck hello progression de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4fe04-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="4fe04-135">Envoi de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="4fe04-135">Submit hello job.</span></span>

<span data-ttu-id="4fe04-136">Consultez hello [développement Media Services avec .NET](media-services-dotnet-how-to-use.md) rubrique pour obtenir des instructions sur la façon de tooset de votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="4fe04-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="4fe04-137"><a id="json"></a>JSON de miniature prédéfini</span><span class="sxs-lookup"><span data-stu-id="4fe04-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="4fe04-138">Pour plus d’informations sur le schéma, consultez [cette](https://msdn.microsoft.com/library/mt269962.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4fe04-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="4fe04-139"><a id="xml"></a>XML de miniature prédéfini</span><span class="sxs-lookup"><span data-stu-id="4fe04-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="4fe04-140">Pour plus d’informations sur le schéma, consultez [cette](https://msdn.microsoft.com/library/mt269962.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4fe04-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="4fe04-141">Considérations</span><span class="sxs-lookup"><span data-stu-id="4fe04-141">Considerations</span></span>
<span data-ttu-id="4fe04-142">Hello suivant considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="4fe04-142">hello following considerations apply:</span></span>

* <span data-ttu-id="4fe04-143">Utilisez Hello des horodateurs explicite pour la plage de début/étape suppose que cette source d’entrée hello est 1 minute au moins.</span><span class="sxs-lookup"><span data-stu-id="4fe04-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="4fe04-144">Les éléments Jpg/Png/BmpImage possèdent les attributs de chaîne Start, Step et Range, qui peuvent être interprétés comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fe04-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="4fe04-145">Entiers non négatifs : nombre d’images, par exemple</span><span class="sxs-lookup"><span data-stu-id="4fe04-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="4fe04-146">"Start": "120"</span><span class="sxs-lookup"><span data-stu-id="4fe04-146">"Start": "120",</span></span>
  * <span data-ttu-id="4fe04-147">Durée de toosource relatif si exprimée sous la forme %-suivi du suffixe, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4fe04-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="4fe04-148">"Start": "15%"</span><span class="sxs-lookup"><span data-stu-id="4fe04-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="4fe04-149">Horodatage, s’il est exprimé au format</span><span class="sxs-lookup"><span data-stu-id="4fe04-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="4fe04-150">HH:MM:SS.</span><span class="sxs-lookup"><span data-stu-id="4fe04-150">format.</span></span> <span data-ttu-id="4fe04-151">par exemple</span><span class="sxs-lookup"><span data-stu-id="4fe04-151">Eg.</span></span> <span data-ttu-id="4fe04-152">"Start": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="4fe04-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="4fe04-153">Vous pouvez combiner et apparier les notations à votre guise.</span><span class="sxs-lookup"><span data-stu-id="4fe04-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="4fe04-154">En outre, début prend également en charge une Macro spéciale : {meilleures}, qui tente de toodetermine hello premier « intéressantes » frame de contenu de hello Remarque : (étape et la plage sont ignorés lorsque le démarrage est défini trop {meilleures})</span><span class="sxs-lookup"><span data-stu-id="4fe04-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="4fe04-155">La configuration par défaut est « Start:{Best} ».</span><span class="sxs-lookup"><span data-stu-id="4fe04-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="4fe04-156">Format de sortie doit toobe explicitement fourni pour chaque format d’Image : Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="4fe04-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="4fe04-157">Le cas échéant, MES correspondra à JpgVideo tooJpgFormat et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4fe04-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="4fe04-158">OutputFormat introduit une nouvelle Macro spécifique codec d’image : {Index}, laquelle doit toobe présent (une fois et une seule fois) pour les formats de sortie d’image.</span><span class="sxs-lookup"><span data-stu-id="4fe04-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fe04-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fe04-159">Next steps</span></span>

<span data-ttu-id="4fe04-160">Vous pouvez vérifier hello [progression de la tâche](media-services-check-job-progress.md) hello lors de la tâche de codage est en attente.</span><span class="sxs-lookup"><span data-stu-id="4fe04-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4fe04-161">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="4fe04-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fe04-162">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4fe04-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4fe04-163">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4fe04-163">See Also</span></span>
[<span data-ttu-id="4fe04-164">Vue d’ensemble de l’encodage de Media Services</span><span class="sxs-lookup"><span data-stu-id="4fe04-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

